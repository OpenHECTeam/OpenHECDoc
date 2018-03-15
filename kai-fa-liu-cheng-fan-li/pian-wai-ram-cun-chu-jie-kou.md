片外RAM存储接口

片外RAM存储接口是OpenHEC平台上纯FPGA模式下实验支撑包预留的访问片外RAM存储的接口，下面介绍在平台上如何使用片外RAM存储接口做访存相关的实验。

#### 一、开发入口

片外RAM存储接口的OpenHEC平台的开发入口是：[http://www.iopenhec.com/\#!/experiment/000020170413000000000005](http://www.iopenhec.com/#!/experiment/000020170401000000000006)

片外RAM存储接口采用的硬件类型为[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)，具体芯片型号为**xc7z030fbg484-3**。

实验资料**oLib**目录中主要资料如下。

* [纯FPGA模式下的RELAX\_FlyxSOM实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-ru-men-shou-ce.html)

实验支撑包中预留两片RAM存储接口，即为RAM0和RAM1，RAM存储的数据线为32位，地址线也为32位，其大小都为64MB,其详细接口定义如下表所示。

| 信号名 | IO方向 | 宽度 | 说明 | 功能 |
| :--- | :--- | :--- | :--- | :--- |
| ram\_clk | 输出 | 1 | RAM的工作时钟 | 可以接单步时钟或FPGA激励时钟 |
| ram\_rst | 输出 | 1 | RAM的复位 | 高电平复位逻辑 |
| ram0\_raddr | 输出 | 32 | RAM0的读地址接口 | 读操作时的偏移地址 |
| ram0\_rdata | 输入 | 32 | RAM0的读数据接口 | 单次读取4B数据。当rvalid为1时，rdata有效，直至下一次读数据返回 |
| ram0\_ren | 输出 | 1 | RAM0的读使能信号 | 当读地址就绪后，置ren为1，启动读操作 |
| ram0\_rvalid | 输入 | 1 | RAM0的读有效信号 | 当rvalid为1时，rdata上的数据更新为本次读操作的结果 |
| ram0\_waddr | 输出 | 32 | RAM0的写地址接口 | 写操作时的偏移地址 |
| ram0\_wdata | 输出 | 32 | RAM0的写数据接口 | 根据 ram0\_sel的信号值，如为4’b1111, 则单次写入4B数据 |
| ram0\_wen | 输出 | 1 | RAM0的写使能信号 | 当写地址和写数据就绪后，置wen为1，启动写操作 |
| ram0\_sel | 输出 | 4 | RAM0的写字节选通信号 | 写字节选通信号（高电平有效） |
| ram0\_wready | 输入 | 1 | RAM0的写准备信号 | wready为1时，表示RAM可执行写操作。为0时，写操作无效 |
| ram1\_raddr | 输出 | 32 | RAM1的读地址接口 | 读操作时的偏移地址 |
| ram1\_rdata | 输入 | 32 | RAM1的读数据接口 | 单次读取4B数据。当rvalid为1时，rdata有效，直至下一次读数据返回 |
| ram1\_ren | 输出 | 1 | RAM1的读使能信号 | 当读地址就绪后，置ren为1，启动读操作 |
| ram1\_rvalid | 输入 | 1 | RAM1的读有效信号 | 当rvalid为1时，rdata上的数据更新为本次读操作的结果 |
| ram1\_waddr | 输出 | 32 | RAM1的写地址接口 | 写操作时的偏移地址 |
| ram1\_wdata | 输出 | 32 | RAM1的写数据接口 | 根据 ram0\_sel的信号值，如为4’b1111, 则单次写入4B数据 |
| ram1\_wen | 输出 | 1 | RAM1的写使能信号 | 当写地址和写数据就绪后，置wen为1，启动写操作 |
| ram1\_sel | 输出 | 4 | RAM1的写字节选通信号 | 写字节选通信号（高电平有效） |
| ram1\_wready | 输入 | 1 | RAM1的写准备信号 | wready为1时，表示RAM可执行写操作。为0时，写操作无效 |

从线上实验环境中的虚拟面板下的写存储和读存储对RAM0和RAM1进行访存操作，其中RAM0的访存地址范围为0x0000000-0x03ffffff，RAM1的访存地址范围为0x04000000-0x07ffffff。从用户逻辑区对片外RAM0和RAM1进行访存操作，可以选择RAM0和RAM1统一编址，即RAM0和RAM1的基地址相同，此时RAM0和RAM1的访存地址范围为0x00000000-0x07ffffff；也可以选择RAM0和RAM1独立编址，即RAM0和RAM1的基地址不相同，此时RAM0的访存地址范围为0x00000000-0x03ffffff，RAM1的访存地址范围为0x04000000-0x07ffffff。请用户设计时选择采用合适的编址方式：统一编址和独立编址，并且登录WEB实验页面后需要对选择RAM基地址设置成相同或不相同。![](/assets/b8b3e1f02e83183f66262d84488910b1.png)

---

#### 二、使用虚拟机

1. ##### 新建用户逻辑工程

   启动vivado 2015.2后，选择**Create New Project**，点击**Next**，输入项目名为**ram\_proj**和项目位置新建在桌面下的**proj\_ip**文件夹。

   点击**Next**，在**Project Type**选项里，将**Do not specify source at this time**勾选上。

   点击**Next**，这里需要选择芯片的型号。在**Parts**选项选择**xc7z030fbg484-3**芯片即可。

   点击**Next**，然后**Finish**完成项目的创建。

2. ##### 添加OpenHEC实验平台顶层文件

   设计完用户区逻辑后，接下来添加OpenHEC实验平台顶层文件，文件存放在**oLib/RELAX\_FlyxSOM/relax\_top **文件夹下，名为**OpenHEC\_Exp\_Top.v**。

   在**Flow Navigator/Project Manager**选项卡下选择**Add Sources**，在弹出的窗口中选择**Add or create design sources**，点击**Next**，点击**+**号标志，选择**Add Files**，添加** oLib/RELAX\_FlyxSOM/relax\_top** 文件夹下的**OpenHEC\_Exp\_Top.v**文件。

   选择 **Copy sources into project**`,`点击**Finish**`,`完成OpenHEC实验平台顶层文件的加载。

3. ##### 用户逻辑与[实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-ru-men-shou-ce.html)的接口绑定

   RAM时钟ram\_clk和复位信号ram\_rst的接口绑定，参考代码如下：

   ```verilog
    //RAM CLK AND RESET
    assign ram_clk = step_clk;
    assign ram_rst = lab_reset;
   ```

   片外RAM0存储接口绑定，参考代码如下：

   ```verilog
    //RAM0 Read Channel
    assign ram0_raddr = R32IN1;
    assign R32OUT1 = ram0_rdata;
    assign ram0_ren = SW00;
    assign LED00 = ram0_rvalid;
    //RAM0 Write Channl
    assign ram0_waddr = R32IN2;
    assign ram0_wdata = R32IN3;
    assign ram0_wen = SW01;
    assign ram0_sel = R8IN0[3:0];
    assign LED01 = ram0_wready;
   ```

   片外RAM1存储接口绑定，参考代码如下：

   ```verilog
    //RAM1 Read Channel
    assign ram1_raddr = R32IN4;
    assign R32OUT2 = ram1_rdata;
    assign ram1_ren = SW02;
    assign LED02 = ram1_rvalid;
    //RAM1 Write Channl
    assign ram1_waddr = R32IN5;
    assign ram1_wdata = R32IN6;
    assign ram1_wen = SW03;
    assign ram1_sel = R8IN1[3:0];
    assign LED03 = ram1_wready;
   ```

   在系统注释区域注释掉用户逻辑区绑定的IO输出端口及系统预留用户调用模块。参考代码如下：

   ```verilog
   //RAM0 Read Interface
    //assign    ram0_ren = 1'b0;
    //assign    ram0_raddr 、、
    //assign    ram0_waddr = 32'b0;
    //assign    ram0_wen = 1'b0;
    //assign    ram0_sel = 4'b0000;
    //assign    ram0_wdata = 32'b0;
    //RAM1 Read Interface
    //assign    ram1_ren = 1'b0;
    //assign    ram1_raddr = 32'b0;
    //RAM1 Write Interface
    //assign    ram1_waddr = 32'b0;
    //assign    ram1_wen = 1'b0;
    //assign    ram1_sel = 4'b0000;
    //assign    ram1_wdata = 32'b0;
    //RAM CLK AND RESET
    //assign ram_clk = step_clk;
    //assign ram_rst = 1'b1;
    //assign    LED00 = SW00;
    //assign    LED01 = SW01;
    //assign    LED02 = SW02;
    //assign    LED03 = SW03;
    //assign R32OUT0 = R32IN0;
    //assign R32OUT1 = R32IN1;
    //assign R32OUT2 = R32IN2;
    /*user_wrapper_top user_wrapper_top_uut
    (
    );*/
   ```

4. ##### 综合与实现

   OpenHEC实验支撑包中提供综合实现的tcl脚本，可以自动完成整个系统的综合，最终生成比特流文件。点击 **Tools/Run Tcl Script**，选择文件夹**oLib/RELAX\_FlyxSOM/tcl **下的**relax\_syn\_imp\_flow.tcl**文件，点击OK，自动运行综合与实现，等待生成位流。比特流文件存放在桌面文件夹**proj\_ip/ram\_proj**下。![](/assets/synram.png)

5. ##### 完成开发

   拷贝桌面文件夹**proj\_ip/ram\_proj**下的位流文件**ram\_proj.bit** 到oDisk目录，完成开发。

---

#### 三、使用FPGA

完成了FPGA的开发后，用户既可以在OpenHEC部署在云端的FPGA硬件上验证与门的bit文件了。

1. ##### 配置比特流到FPGA

   点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中刚刚拷贝的**ram\_proj.bit**位流，同时选择纯FPGA模式的配置方式，点击配置即可以。配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。

2. **RAM存储基地址设置**

   配置完位流文件后，需要对片外RAM存储RAM0和RAM1的基地址进行设置，基地址相同即是统一编址，基地址不相同即是独立编址。这里选择RAM0和RAM1独立编址的方式，即基地址不相同。

3. ##### 写存储

   位流配置成功后，点击展开写存储，展开写存储操作页面。

   第一步：选择片外RAM0的基地址0x0000000，WEB下访问存储的地址范围如下表所示。

   | 存储类型 | 数据位宽 | WEB访问基地址 | WEB访问终地址 | 用户逻辑区基地址 | 用户逻辑区终地址 | 大小 | 说明 |
   | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
   | ROM | 32-bit | 0x40000000 | 0x400007ff | 0x00000000 | 0x000007ff | 2KB |  |
   | RAM0 | 32-bit | 0x00000000 | 0x03ffffff | 0x00000000 | 0x03ffffff | 64MB | 独立编址 |
   | RAM1 | 32-bit | 0x04000000 | 0x07ffffff | 0x00000000 | 0x03ffffff | 64MB | 独立编址 |
   | RAM0 | 32-bit | 0x00000000 | 0x03ffffff | 0x00000000 | 0x07ffffff | 128MB | 统一编址 |
   | RAM1 | 32-bit | 0x04000000 | 0x07ffffff | 0x00000000 | 0x07ffffff | 128MB | 统一编址 |
   | SRAM | 16-bit | 0x50000000 | 0x50ffffff | 0x00000000 | 0x00ffffff | 16MB |  |

   第二步：增加值或者导入写入的文件，导入文件的格式为二进制文件编码；从ROM基地址依次写入1, 2, … , f的值。![](/assets/writeram0002.png)

   第三步： 点击发送数据，此时才会开始把准备好的数据，写入片外RAM0存储中。

4. ##### 读存储

   点击展开读存储，展开读存储操作页面。

   第一步：选择片外RAM0的基地址0x0000000。

   第二步：输入展示地址个数为60。

   第三步：点击**查看结果**，在下方表中可以查看片外RAM0的数据，也可以生成文件导出。![](/assets/rdram0002.png)

5. ##### IO实时监控片外RAM接口信号

   从OpenHEC平台FPGA实验环境下的虚拟面板对片外RAM进行写操作和读操作完成后，接下来对用户逻辑区的片外RAM进行IO实时监控。

   RAM0复位操作。设置复位1, 点击单步时钟激励，对RAM0进行复位。

   RAM0读操作。设置RAM0的读使能信号ram0\_ren为高, 输入读地址信号到ram0\_raddr，等待读有效ram0\_rvalid信号为高的时候，点击单步时钟观察读读回来的数据 ram0\_rdata的值。![](/assets/ram_show0008.png)![](/assets/ram_show_0009.png)![](/assets/ram_show_0010.png)

   RAM0写操作。设置RAM0的写时能信号ram0\_wen为高，字节选通信号ram0\_sel全为高，输入写地址信号到ram0\_waddr，写地址数据ram0\_wdata，点击单步时钟多次后，拉低写使能信号ram0\_wen， 当ram0\_wready信号由低变成高电平时，表示写入成功。这里往RAM0的0x00000000里面写入数据0x12345678。返回到读存储页面，点击确认，检查RAM0的地址位为0x00000000是否变成数据0x12345678。![](/assets/ram_show_0011.png)![](/assets/ram_show_0012.png)



