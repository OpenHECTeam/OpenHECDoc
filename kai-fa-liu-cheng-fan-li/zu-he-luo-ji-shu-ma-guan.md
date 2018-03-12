### [组合逻辑数码管](http://www.iopenhec.com/#!/experiment/000020170405000000000089)

组合逻辑数码管是基于虚拟面板+教学板卡的线上实验方式，实现从0到F的数码管显示，是在纯FPGA模式下使用[**RELAX\_FlyxSOM\_LED7SEG**](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)实验支撑包来进行开发的。。

#### 一、开发入口

组合逻辑数码管的OpenHEC平台的开发入口是：[http://www.iopenhec.com/\#!/experiment/000020170405000000000089](http://www.iopenhec.com/#!/experiment/000020170401000000000006)

组合逻辑数码管采用的硬件类型为[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)，具体芯片型号为**xc7z030fbg484-3**。

实验资料**oLib**目录中主要资料如下。

* [纯FPGA模式下的**RELAX\_FlyxSOM\_LED7SEG**实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)

#### 二、使用虚拟机

1. ##### **新建用户逻辑工程**

   启动vivado 2015.2后，选择**Create New Project**，点击**Next**，输入项目名为**seg\_proj**和项目位置新建在桌面下的**proj\_ip**。

   点击**Next**，在**Project Type**选项里，将**Do not specify source at this time**勾选上。

   点击**Next**，这里需要选择芯片的型号。在**Parts**选项选择**xc7z030fbg484-3**芯片即可。

   点击**Next**，然后**Finish**完成项目的创建。

2. **添加OpenHEC实验平台顶层文件**

   接下来添加OpenHEC实验平台顶层文件，文件存放在**oLib/RELAX\_FlyxSOM\_LED7SEG/relax\_top **文件夹下，名为**OpenHEC\_Exp\_Top.v**。

   在**Flow Navigator/Project Manager**选项卡下选择**Add Sources**，在弹出的窗口中选择**Add or create design sources**，点击**Next**，点击**+**号标志，选择**Add Files**，添加** oLib/RELAX\_FlyxSOM/relax\_top** 文件夹下的**OpenHEC\_Exp\_Top.v**文件。

   选择 **Copy sources into project**`,`点击**Finish**`,`完成OpenHEC实验平台顶层文件的加载。

3. **用户逻辑与实验支撑包的接口绑定**

   根据[**RELAX\_FlyxSOM\_LED7SEG**实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)解析说明，数码管的管脚可以跟开关管脚一一绑定。这里面没有调用用户IP核，因此需要注释掉实列化IP核模块的区域。

   ```verilog
   assign FlyxIO_seven_segment_a = SW00;
   assign FlyxIO_seven_segment_b = SW01;
   assign FlyxIO_seven_segment_c = SW02;
   assign FlyxIO_seven_segment_d = SW03;
   assign FlyxIO_seven_segment_e = SW04;
   assign FlyxIO_seven_segment_f = SW05;
   assign FlyxIO_seven_segment_g = SW06;
   assign FlyxIO_seven_segment_dp = SW07;
   assign FlyxIO_seven_segment_dig1 = SW08;
   assign FlyxIO_seven_segment_dig2 = SW09;

   /*user_wrapper_top user_wrapper_top_uut
    (
    );*/
   ```

4. **综合与实现**

   OpenHEC实验支撑包中提供综合实现的tcl脚本，可以自动完成整个系统的综合，最终生成比特流文件。点击 **Tools/Run Tcl Script**，选择文件夹**oLib/RELAX\_FlyxSOM\_LED7SEG/tcl **下的**relax\_syn\_imp\_flow.tcl**文件，点击OK，自动运行综合与实现，等待生成位流。比特流文件存放在桌面文件夹**proj\_ip/seg\_proj**下。![](/assets/seg_gen_bit.png)

5. **完成开发**

   拷贝桌面文件夹**proj\_ip/seg\_proj**下的位流文件**seg\_proj.bit** 到oDisk目录，完成开发。![](/assets/finish_seg.png)

#### 三、使用FPGA

完成了FPGA的开发后，用户既可以在OpenHEC部署在云端的FPGA硬件上验证数码管的bit文件了。

1. ##### 配置比特流到FPGA

   点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中刚刚拷贝的**seg\_proj.bit**位流，同时选择纯FPGA模式的配置方式，点击配置即可以。配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。

2. ##### IO实时监控

   根据[**RELAX\_FlyxSOM\_LED7SEG**实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)中数码管的编码规则，当输入开关DIG1、DIG2都置1时，从监控视频中可以观察到，数码管会显示字符。![](/assets/seg_panel0001.png)![](/assets/seg_led0002.png)

3. ##### **数码管显示 0.0.**

   ![](blob:file:///34ebe832-4ac7-4c3f-8cd5-7d70251bda67)![](blob:file:///f22ac639-a20c-4cd3-91de-81728ad20223)

4. ##### **数码管显示 1.1.**

   ![](blob:file:///0e5afef0-9f2d-405b-87e0-157b6a95d4e1)![](/assets/segshow0004.png)

5. ##### **数码管显示 6.6.**

   ![](/assets/segshow0005.png)![](/assets/segshow0007.png)



