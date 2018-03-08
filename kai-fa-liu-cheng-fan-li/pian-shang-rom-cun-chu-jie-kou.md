### [片上ROM存储接口](http://www.iopenhec.com/#!/experiment/000020170413000000000004)

片上ROM存储接口是OpenHEC平台上纯FPGA模式下实验支撑包预留的片上ROM资源，下面介绍在平台上如何使用ROM存储接口做访存相关的实验。

#### 一、开发入口

片上ROM存储接口的OpenHEC平台的开发入口是：[http://www.iopenhec.com/\#!/experiment/000020170413000000000004](http://www.iopenhec.com/#!/experiment/000020170401000000000006)

片上ROM存储接口采用的硬件类型为[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)，具体芯片型号为**xc7z030fbg484-3**。

实验资料**oLib**目录中主要资料如下。

* [纯FPGA模式下的RELAX\_FlyxSOM实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-ru-men-shou-ce.html)

实验支撑包中预留片上ROM接口，ROM的数据线为32位，地址线为32位，其大小为2KB。OpenHEC平台上FPGA实验环境的写存储和读存储页面可以进行片上ROM读写验证，其访存的地址范围为0x40000000-0x400007ff。用户实验逻辑访问读取片内ROM接口的地址范围为0x00000000 - 0x000007ff，实验支撑包顶层verilog接口定义如下：

```verilog
    /*
     *   Instruction ROM Interface 
     *
     *   32-bit Address     
     *      BaseAddr = 0x40000000
     *     HighAddr = 0x400007ff
     *   Size     =  2K
     */
    output   wire    [31: 0]    inst_addr,
    input    wire    [31: 0]    inst_data,
```

---

#### 二、使用虚拟机

1. ##### 新建用户逻辑工程

   启动vivado 2015.2后，选择**Create New Project**，点击**Next**，输入项目名为**rom\_proj**和项目位置新建在桌面下的**proj\_ip**文件夹。

   点击**Next**，在**Project Type**选项里，将**Do not specify source at this time**勾选上。

   点击**Next**，这里需要选择芯片的型号。在**Parts**选项选择**xc7z030fbg484-3**芯片即可。

   点击**Next**，然后**Finish**完成项目的创建。

2. ##### 添加OpenHEC实验平台顶层文件

   设计完用户区逻辑后，接下来添加OpenHEC实验平台顶层文件，文件存放在**oLib/RELAX\_FlyxSOM/relax\_top **文件夹下，名为**OpenHEC\_Exp\_Top.v**。

   在**Flow Navigator/Project Manager**选项卡下选择**Add Sources**，在弹出的窗口中选择**Add or create design sources**，点击**Next**，点击**+**号标志，选择**Add Files**，添加** oLib/RELAX\_FlyxSOM/relax\_top** 文件夹下的**OpenHEC\_Exp\_Top.v**文件。

   选择 **Copy sources into project**`,`点击**Finish**`,`完成OpenHEC实验平台顶层文件的加载。

3. ##### 用户逻辑与实验支撑包的接口绑定

   根据[`RELAX_FlyxSOM`实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-ru-men-shou-ce.html)解析说明，在用户逻辑区，片上ROM接口预留了地址线和数据线，仅提供了读功能，采用组合逻辑的读取方式，地址线inst\_addr一旦更新值，数据线inst\_data便会更新当前的数据值。因此只需要在实验顶层文件中，与支撑包绑定相应的接口即可。

   片上ROM接口地址线端口绑定，32位地址线\`inst\_addr\`直接绑定到32-bit输入寄存器上\`R32IN0\`。  
   片上ROM接口数据线端口绑定，32位数据线\`inst\_data\`直接绑定到32-bit输出寄存器上\`R32OUT0\`。  
   在系统注释区域注释掉用户逻辑区绑定的IO输出端口及系统预留用户调用模块。这里绑定了LED00管脚，因此需要加‘//’注释掉 LED00的初始赋值。

   参考代码如下：

   ```verilog
   assign inst_addr = R32IN0;
   assign R32OUT0 = inst_data;
   //assign R32OUT0 = R32IN0;
   /*user_wrapper_top user_wrapper_top_uut
   (
   );*/
   ```

4. ##### 综合与实现

   OpenHEC实验支撑包中提供综合实现的tcl脚本，可以自动完成整个系统的综合，最终生成比特流文件。点击 **Tools/Run Tcl Script**，选择文件夹**oLib/RELAX\_FlyxSOM/tcl **下的**relax\_syn\_imp\_flow.tcl**文件，点击OK，自动运行综合与实现，等待生成位流。比特流文件存放在桌面文件夹**proj\_ip/rom\_proj**下。![](/assets/syn003.png)

5. ##### 完成开发

   拷贝桌面文件夹**proj\_ip/rom\_proj**下的位流文件**rom\_proj.bit** 到oDisk目录，完成开发。

---

#### 三、使用FPGA

完成了FPGA的开发后，用户既可以在OpenHEC部署在云端的FPGA硬件上验证与门的bit文件了。

1. ##### 配置比特流到FPGA

   点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中刚刚拷贝的**rom\_proj.bit**位流，同时选择纯FPGA模式的配置方式，点击配置即可以。配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。

2. ##### 写存储

   位流配置成功后，点击展开写存储，展开写存储操作页面。![](/assets/writeram001.png)

   第一步：选择片内ROM的基地址0x4000000，WEB下访问存储的地址范围如下表所示。

   | 存储类型 | 数据位宽 | WEB访问基地址 | WEB访问终地址 | 用户逻辑区基地址 | 用户逻辑区终地址 | 大小 | 说明 |
   | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
   | ROM | 32-bit | 0x40000000 | 0x400007ff | 0x00000000 | 0x000007ff | 2KB |  |
   | RAM0 | 32-bit | 0x00000000 | 0x03ffffff | 0x00000000 | 0x03ffffff | 64MB | 独立编址 |
   | RAM1 | 32-bit | 0x04000000 | 0x07ffffff | 0x00000000 | 0x03ffffff | 64MB | 独立编址 |
   | RAM0 | 32-bit | 0x00000000 | 0x03ffffff | 0x00000000 | 0x07ffffff | 128MB | 统一编址 |
   | RAM1 | 32-bit | 0x04000000 | 0x07ffffff | 0x00000000 | 0x07ffffff | 128MB | 统一编址 |
   | SRAM | 16-bit | 0x50000000 | 0x50ffffff | 0x00000000 | 0x00ffffff | 16MB |  |

   第二步：增加值或者导入写入的文件，导入文件的格式为二进制文件编码；从ROM基地址依次写入1, 2, … , f的值。![](/assets/writeram0002.png)

   第三步： 点击发送数据，此时才会开始把准备好的数据，写入片上ROM中。

3. ##### 读存储

   点击展开读存储，展开读存储操作页面。![](/assets/rdram0001.png)

   第一步：选择片上ROM的基地址40000000。

   第二步：输入展示地址个数为60。

   第三步：点击**查看结果**，在下方表中可以查看片上ROM的数据，也可以生成文件导出。![](/assets/rdram0002.png)

4. ##### IO实时监控片上ROM接口信号

   从OpenHEC平台FPGA实验环境下的虚拟面板对片上ROM进行写操作和读操作完成后，下一步试试监控用户逻辑区的ROM逻辑进行IO实时监控。

   片内ROM存储接口是组合逻辑的访问模式。在R32寄存器输入输出，给片上ROM接口的地址线inst\_addr中输入地址信息,观察数据线inst\_data的实时变化状态。![](/assets/iorom0001.png)![](/assets/iorom0002.png)

   ![](/assets/iorom0003.png)



