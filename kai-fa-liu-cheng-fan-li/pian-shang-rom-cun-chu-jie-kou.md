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

#### 二、使用虚拟机

1. ##### 新建用户逻辑工程

   启动vivado 2015.2后，选择**Create New Project**，点击**Next**，输入项目名为**rom\_proj**和项目位置新建在桌面下的**proj\_ip**文件夹。

   点击**Next**，在**Project Type**选项里，将**Do not specify source at this time**勾选上。

   点击**Next**，这里需要选择芯片的型号。在**Parts**选项选择**xc7z030fbg484-3**芯片即可。

   点击**Next**，然后**Finish**完成项目的创建。

   ---

2. ##### 添加OpenHEC实验平台顶层文件

   设计完用户区逻辑后，接下来添加OpenHEC实验平台顶层文件，文件存放在**oLib/RELAX\_FlyxSOM/relax\_top **文件夹下，名为**OpenHEC\_Exp\_Top.v**。

   在**Flow Navigator/Project Manager**选项卡下选择**Add Sources**，在弹出的窗口中选择**Add or create design sources**，点击**Next**，点击**+**号标志，选择**Add Files**，添加** oLib/RELAX\_FlyxSOM/relax\_top** 文件夹下的**OpenHEC\_Exp\_Top.v**文件。

   选择 **Copy sources into project**`,`点击**Finish**`,`完成OpenHEC实验平台顶层文件的加载。

   ---

3. ##### 用户逻辑与实验支撑包的接口绑定

   打开**OpenHEC\_Exp\_Top.v**文件，找到用户自定义顶层module实例化区域，粘贴and4in\_bd中拷贝的IO管脚绑定, 并重新命名模块的名字为 **flipflop\_bd\_wrapper** 。

   根据[`RELAX_FlyxSOM`实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-ru-men-shou-ce.html)解析说明，选择相应的IO管脚绑定。IO输入端口绑定，时钟**clk**和复位**reset**分别绑定到单步时钟**step\_clk**和复位信号**lab\_reset**上; 2个1-bit的输入信号（**set**,  **d**），这里可以绑定到开关**SW30**, **SW31**上。  
   IO输出端口绑定，2个1-bit的输出信号（**q**, **qn**），绑定到**LED30**, **LED31**上。  
   在系统注释区域注释掉用户逻辑区绑定的IO输出端口。这里绑定了**LED30**和**LED31**管脚，因此需要加‘//’注释掉LED30和LED31的初始赋值。  参考代码如下：

   ```verilog
       //assign LED30 = SW30;
       //assign LED31 = SW31;
       flipflop_bd_wrapper user_wrapper_top_uut
       (
           .clk(step_clk),
           .reset(lab_reset),
           .set(SW30),
           .d(SW31),
           .q(LED30),
           .qn(LED31)
       );
   ```

4. ##### 综合与实现

   OpenHEC实验支撑包中提供综合实现的tcl脚本，可以自动完成整个系统的综合，最终生成比特流文件。点击 **Tools/Run Tcl Script**，选择文件夹**oLib/RELAX\_FlyxSOM/tcl **下的**relax\_syn\_imp\_flow.tcl**文件，点击OK，自动运行综合与实现，等待生成位流。比特流文件存放在桌面文件夹**proj\_ip/flipflop\_proj**下。![](/assets/genbit002.png)

5. ##### 完成开发

   拷贝桌面文件夹**proj\_ip/flipflop\_proj**下的位流文件**flipflop\_proj.bit** 到oDisk目录，完成开发。![](/assets/finishdev002.png)

#### 三、使用FPGA

完成了FPGA的开发后，用户既可以在OpenHEC部署在云端的FPGA硬件上验证与门的bit文件了。

1. ##### 配置比特流到FPGA

   点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中刚刚拷贝的**flipflop\_proj.bit**位流，同时选择纯FPGA模式的配置方式，点击配置即可以。配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。

2. ##### IO实时监控

   当复位信号置为1，其他输入信号set和d，不管置0或者置1；点击单步时钟，输出信号q始终为不亮，qn始终为亮，实现了同步清0的逻辑功能。![](/assets/flip001.png)

   当复位信号置为0，输入信号set置1时，d不管是置0或者置1；点击单步时钟，输出信号q始终亮，qn始终不亮，实现了同步置1的逻辑功能。![](/assets/flip002.png)

   当复位信号置为0，输入信号set置0时；点击单步时钟，输出信号q和qn始终是输入信号d的取反值，实现了D触发器的逻辑功能。![](/assets/flip003.png)



