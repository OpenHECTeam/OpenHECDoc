### [硬件协同之sobel算法加速](http://www.iopenhec.com/#!/experiment/000020170417000000000004)

Sobel边缘检测算法是图像视频处理中的一个经典算法，在计算机视觉等领域应用广泛。

![](/assets/sobel_0001.png)

如上图所示，sobel算法加速是在项目支撑包**RELAXSoC\_FlyxSOM**的基础上，将Sobel加速器IP添加到FPGA的用户区，与接口逻辑一起构成完整的Sobel加速器。Sobel的软件功能部分运行在ARM处理器上，负责将图像数据加载到共享内存、对Sobel加速器进行初始化，以及将计算结果处理后写回图像文件。

##### **一、开发入口**

软硬件协同之sobel算法加速的开发入口是：

[http://www.iopenhec.com/\#!/experiment/000020170417000000000004](http://www.iopenhec.com/#!/experiment/000020170417000000000004)

采用的硬件类型为[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)，具体芯片型号为**xc7z030fbg484-3**。

实验资料**oLib**目录中主要资料如下。

* RELAXSoC\_FlyxSOM为项目支撑包文件
* sobel\_hls\_src目录下包含sobel算法的hls代码
* sobel\_sw\_prog目录下包含了运行sobel加速核ARM上的软件代码。

##### 二、使用虚拟机

1. 建立项目工程
   从oLib中拷贝项目支撑包到桌面工作目录下
   ，将Sobel算法的HLS代码添加到项目支撑包中，即将sobel\_hls\_src目录下的所有文件和目录一起上传到RELAXSoC\_FlyxSOM的src目录下。
2. Sobel代码修改  
   OpenHEC项目支撑包环境下，需要对Sobel加速器的HLS顶层函数接口进行修改，接口函数名和约束必须符合项目支撑包的要求。

   修改后的代码如下：

   ```c
   void user_accel(volatile hls_int32 *inout_pix, unsigned int byte_rdoffset, unsigned int byte_wroffset, int rows, int cols, int stride, int addr_reserved)  
   {
       //#pragma HLS RESOURCE variable=inout_pix core=AXI4M
       //Data Flow Bus(Read and Write)
       #pragma HLS INTERFACE m_axi depth=2048 port=inout_pix offset=off bundle=user_axi
       //Control Bus
       #pragma HLS INTERFACE s_axilite register port=return offset=0x00 bundle=user_axi4lite
       #pragma HLS INTERFACE s_axilite register port=byte_rdoffset offset=0x14 bundle=user_axi4lite
       #pragma HLS INTERFACE s_axilite register port=byte_wroffset offset=0x1c bundle=user_axi4lite
       #pragma HLS INTERFACE s_axilite register port=rows offset=0x24 bundle=user_axi4lite
       #pragma HLS INTERFACE s_axilite register port=cols offset=0x2c bundle=user_axi4lite
       #pragma HLS INTERFACE s_axilite register port=stride offset=0x34 bundle=user_axi4lite
       //Ensure Address Range
       #pragma HLS INTERFACE s_axilite register port=addr_reserved offset=0xFFF0 bundle=user_axi4lite
       ......
   }
   ```

   修改内容包括：

   函数名由sobel\_filter改为user\_accel

   增加int addr\_reserved，offset=0xFFF0，用于约束地址总线位宽为32位

   将inout\_pix参数绑定到user\_axi接口，使加速器IP可以直接访问内存；同时，将其它参数也绑定到user\_axi4lite，用于配置加速器IP。

3. 编译并生成加速器位流文件

   完成代码修改后，在RELAXSoC\_FlyxSOM目录下执行make命令，编译整个项目。编译后，在impl/bin\_file目录下可以看到已生成好的Sobel加速器位流文件user\_design.bit。

   自此，Sobel硬件加速器部分已经全部完成，下面是节点上的软件部分的实现。

4. 软件功能部分主要包括加载图像文件、配置并启动Sobel硬件加速器，以及最后将结果写入图像文件。这部分代码在sobel\_test目录下，包含多个.h和.c文件，其中，sobel软件部分的主函数在sobel\_test.c中实现。

   ```c
   int main()
   {
       void *user_base_addr;
       int ncols = 1920;
       int nrows = 1080;
       //将控制接口映射到进程的地址空间
       set_mapbase(&user_base_addr, BASE_ADDR);
       unsigned char *R, *G, *B;
       R = (unsigned char*)malloc(ncols*nrows*sizeof(unsigned char));
       G = (unsigned char*)malloc(ncols*nrows*sizeof(unsigned char));
       B = (unsigned char*)malloc(ncols*nrows*sizeof(unsigned char));
       //读取输入图像文件
       BMP_Read("test_1080p.bmp", nrows, ncols, R, G, B);
       int size = ncols*nrows*4;
       clearMemory(0x34000000, size);
       //将输入图像文件写入物理地址为0x34000000起始的内存区域中
       Write_AXI4_RGB_DATA(R, G, B, ncols, nrows, 0x34000000);
       //配置Sobel加速器IP的各项参数
       write_uint32(user_base_addr, RDOFFSET, 0x34000000);
       write_uint32(user_base_addr, WROFFSET, 0x36000000);
       write_uint32(user_base_addr, ROWS, nrows);
       write_uint32(user_base_addr, COLS, ncols);
       write_uint32(user_base_addr, STRIDE, ncols);
       //启动加速器IP
       write_uint32(user_base_addr, AP_CTRL, 1);    
       //以轮询方式检测加速器是否执行完毕
       while(1){
           if(read_uint32(user_base_addr, AP_CTRL)&0x2==0x2) break;
       }
       //执行完毕后，将结果数据从0x36000000起始的内存区域中读取计算结果
       Read_AXI4_RGB_DATA(R, G, B, ncols, nrows, 0x36000000);
       //将计算结果写入结果文件中
       BMP_Write("result.bmp", nrows, ncols, R, G, B);
       free(R);
       free(G);
       free(B);
       return 0;
   }
   ```

5. 拷贝oLib中** sobel\_sw\_prog**文件夹到桌面下，在终端下进入到拷贝后的文件夹路径，输入**make**，即可以看到生成节点ARM端的可执行程序**a.out**。

6. 拷贝**sobel\_sw\_prog**到**oDisk**中_，_同时把生成的位流文件**user\_design.bit**放到**oDisk**中的**sobel\_sw\_prog**文件夹中_。_

##### 三、使用FPGA

1. Sobel加速器需要运行在OpenHEC在线平台的硬件节点上，sobel\_test中提供了一个执行脚本fpga\_run.sh，内容如下

   ```bash
   #!/bin/bash
   #### EXECUTE ON FPGA
   ./devmem2 0xf8008000 w 1
   ./devmem2 0xf8008014 w 1
   cat user_design.bit > /dev/xdevcfg
   ./a.out
   ```

2. **./devmem2 0xf8008000 w 1**和**./devmem2 0xf8008014 w 1**用于将Zynq芯片内的AXI HP0接口总线带宽设置为32位。这两个命令的执行需要一个外部工具devmem2，该工具由OpenHEC提供。cat user\_design.bit &gt; /dev/xdevcfg命令负责将位流文件user\_design.bit配置到FPGA上。最后也可以使用配置FPGA按钮，选择SoC模式来配置FPGA。./a.out执行Sobel加速器测试。

3. 在节点上实现软件功能

   点击终端登录，在/home/linaro下找到sobel\_sw\_prog目录下，通过执行./fpga\_run.sh脚本，配置FPGA并开始执行。Sobel加速器执行时采用的输入图像如下：![](/assets/sobel_input.png)

   执行完成后，得到输出图像文件result.bmp，打开后如下。![](/assets/sobel_output.png)



