### [教学板SRAM存储接口](http://www.iopenhec.com/#!/experiment/000020170413000000000006)

教学板SRAM存储接口是在纯FPGA模式下使用[**RELAX\_FlyxSOM\_LED7SEG\_SRAM**](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-sram-ru-men-shou-ce.html)实验支撑包来进行开发的，提供了用户如何在线上使用SRAM存储的接口。

#### 一、开发入口

教学板SRAM存储接口的OpenHEC平台的开发入口是：[http://www.iopenhec.com/\#!/experiment/000020170413000000000006](http://www.iopenhec.com/#!/experiment/000020170401000000000006)

教学板SRAM存储接口的硬件类型为[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)，具体芯片型号为**xc7z030fbg484-3**。

实验资料**oLib**目录中主要资料如下。

* 纯FPGA模式下的[**RELAX\_FlyxSOM\_LED7SEG\_SRAM**](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-sram-ru-men-shou-ce.html)实验支撑包

SRAM接口说明如下表所示。WEB实验页面中的写存储和读存储对SRAM进行访存操作的地址范围为0x5000000-0x50ffffff。用户逻辑取对SRAM进行访存操作的地址范围为0x00000000 - 0x00ffffff。

| 信号名 | IO方向 | 宽度 | 说明 | 功能 |
| :--- | :--- | :--- | :--- | :--- |
| FlyxIO\_sram\_user\_nce | 输出 | 1 | SRAM芯片有效使能 | 低电平有效 |
| FlyxIO\_sram\_user\_noe | 输出 | 1 | SRAM芯片输出时能 | 读时为低电平，写时为高电平 |
| FlyxIO\_sram\_user\_nwe | 输出 | 1 | SRAM芯片写时能 | 读时为高电平，写时位低电平 |
| FlyxIO\_sram\_user\_nlb | 输出 | 1 | SRAM芯片低8位选通 | 选通时为低电平，不选通置为高电平 |
| FlyxIO\_sram\_user\_nub | 输出 | 1 | SRAM芯片高8位选通 | 选通时为低电平，不选通置为高电平 |
| FlyxIO\_sram\_user\_addr | 输出 | 19 | SRAM芯片地址线 |  |
| FlyxIO\_sram\_user\_wrdata | 输出 | 16 | SRAM写数据线 |  |
| FlyxIO\_sram\_user\_rd\_data | 输入 | 16 | SRAM读数据线 |  |

#### 二、使用虚拟机

1. ##### **新建用户逻辑工程**

   启动vivado 2015.2后，选择**Create New Project**，点击**Next**，输入项目名为**sram\_proj**和项目位置新建在桌面下的**proj\_ip**。

   点击**Next**，在**Project Type**选项里，将**Do not specify source at this time**勾选上。

   点击**Next**，这里需要选择芯片的型号，在**Parts**选项选择**xc7z030fbg484-3**芯片即可。

   点击**Next**，然后**Finish**完成项目的创建。

2. **添加OpenHEC实验平台顶层文件**

   接下来添加OpenHEC实验平台顶层文件，文件存放在**oLib/RELAX\_FlyxSOM\_LED7SEG\_SRAM/relax\_top **文件夹下，名为**OpenHEC\_Exp\_Top.v**。

   在**Flow Navigator/Project Manager**选项卡下选择**Add Sources**，在弹出的窗口中选择**Add or create design sources**，点击**Next**，点击**+**号标志，选择**Add Files**，添加** oLib/RELAX\_FlyxSOM\_LED7SEG\_SRAM/relax\_top** 文件夹下的**OpenHEC\_Exp\_Top.v**文件。

   选择 **Copy sources into project**`,`点击**Finish**`,`完成OpenHEC实验平台顶层文件的加载。

3. **用户逻辑与实验支撑包的接口绑定**

   支撑包[**RELAX\_FlyxSOM\_LED7SEG\_SRAM实验支撑包**](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-sram-ru-men-shou-ce.html) 已经预先完成了用户逻辑与实验支撑包的绑定，参考代码如下，

4. **综合与实现**

   OpenHEC实验支撑包中提供综合实现的tcl脚本，可以自动完成整个系统的综合，最终生成比特流文件。点击 **Tools/Run Tcl Script**，选择文件夹**oLib/RELAX\_FlyxSOM\_LED7SEG\_SRAM/tcl **下的**relax\_syn\_imp\_flow.tcl**文件，点击OK，自动运行综合与实现，等待生成位流。比特流文件存放在桌面文件夹**proj\_ip/led\_proj**下。

5. **完成开发**

   拷贝桌面文件夹**proj\_ip/led\_proj**下的位流文件**led\_proj.bit** 到oDisk目录，完成开发。![](/assets/finish_led.png)

#### 三、使用FPGA

完成了FPGA的开发后，用户既可以在OpenHEC部署在云端的FPGA硬件上验证数码管的bit文件了。

1. ##### 配置比特流到FPGA

   点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中刚刚拷贝的**led\_proj.bit**位流，同时选择纯FPGA模式的配置方式，点击配置即可以。配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。

2. ##### IO实时监控

   根据[**RELAX\_FlyxSOM\_LED7SEG**实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)中数码管的编码规则，在虚拟面板点击单步时钟，同时切换到监控视频页面会看到点阵LED呈现对角线顺序显示，每点击一次单步时钟按钮，LED点动一步。

   ![](/assets/led0003.png)![](/assets/led0004.png)![](/assets/led0005.png)![](/assets/led0006.png)![](/assets/led0007.png)![](/assets/led0008.png)



