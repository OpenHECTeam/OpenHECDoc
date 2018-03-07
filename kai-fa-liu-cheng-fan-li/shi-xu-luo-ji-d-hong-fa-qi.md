### [时序逻辑D触发器](http://www.iopenhec.com/#!/experiment/000020170413000000000002)

时序逻辑D触发器是基于虚拟面板做时序逻辑的入门实验：带同步清0、同步置1的D触发器，是在纯FPGA模式下使用[RELAX\_FlyxSOM](http://www.iopenhec.com/#!/app/forum/topics/2332)实验支撑包来进行开发的。

#### 一、开发入口

时序逻辑D触发器的OpenHEC平台的开发入口是：[http://www.iopenhec.com/\#!/experiment/000020170413000000000002](http://www.iopenhec.com/#!/experiment/000020170401000000000006)

时序逻辑D触发器采用的硬件类型为[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)，具体芯片型号为**xc7z030fbg484-3**。

实验资料**oLib**目录中主要资料如下。

* [纯FPGA模式下的RELAX\_FlyxSOM实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-ru-men-shou-ce.html)

* D触发器IP核\(**OpenHEC\_user\_d\_flipflop\_logic\_1.0**\)

实验中的D触发器IP核的verilog代码如下：



#### 二、使用虚拟机

1. ##### 新建用户逻辑工程

   启动vivado 2015.2后，选择**Create New Project**，点击**Next**，输入项目名为**flipflop\_proj**和项目位置新建在桌面下的**proj\_ip**。

   点击**Next**，在**Project Type**选项里，将**Do not specify source at this time**勾选上。

   点击**Next**，这里需要选择芯片的型号。在**Parts**选项选择**xc7z030fbg484-3**芯片即可。

   点击**Next**，然后**Finish**完成项目的创建。

   ---

2. ##### 添加基础IP核

   从**oLib**中拷贝与门的IP核 **OpenHEC\_user\_d\_flipflop\_logic\_1.0.zip**到桌面文件夹**proj\_ip **`里面。`

   在左侧菜单**Flow Navigator/Project Manager**`，`选项卡下点击**IP Catalog**`，`在窗口选择**IP Setting**`，`弹出**Project Setting**窗口，在`IP`选项卡，通过**+**添加**IP Repositories**，选择桌面文件夹**proj\_ip**目录，然后在**IP in Selected Repository**，选择需要用到的IP\(即**OpenHEC\_user\_d\_flipflop\_logic\_1.0.zip**\) ，完成后点击下方**Apply**，然后点击**OK**。

   ---

3. ##### Vivado框图设计

   在**Flow Navigator/IP Integrator**选项卡下选择**Create Block Design**，在弹出的窗口中输入一个设计名，这里输入**and4in\_bd**

   ，点击**OK**。![](/assets/cbd001.png)

   在生成的Diagram界面中，选择**添加IP**按钮，在弹出的窗口中输入**and4in**选择IP，确认即可在Diagram界面出现这个IP 。![](/assets/a47496d635eaf9220e5f17b5af18f8d9.png)

   点击实验模块端口（如 A ），右击选择**Make External**，引出所有端口。![](/assets/ba9665b76e123387eed2804878427436.png)

   在**Flow Navigator**选项卡选择**Generate Block Design**，在弹出的窗口中选择**Generate**，完成原理图设计。

   在**Source/Hierarchy**选项卡中，右击**Design Source**中的bd文件（如本实验中的and4in\_bd.bd），选择**Create HDL Wrapper**, 弹出**Create HDL Wrapper**对话框，选择**Copy generated wrapper to allow user\_edits**，点击**OK**。![](/assets/0d597b7274e841a0d3352313bf71e1fa.png)

   ---

4. ##### 添加OpenHEC实验平台顶层文件

   设计完用户区逻辑后，接下来添加OpenHEC实验平台顶层文件，文件存放在**oLib/RELAX\_FlyxSOM/relax\_top **文件夹下，名为**OpenHEC\_Exp\_Top.v**。在**Flow Navigator/Project Manager**选项卡下选择**Add Sources**，在弹出的窗口中选择**Add or create design sources**，点击**Next**，点击**+**号标志，选择**Add Files**，添加** oLib/RELAX\_FlyxSOM/relax\_top** 文件夹下的**OpenHEC\_Exp\_Top.v**文件。选择 **Copy sources into project**`,`点击**Finish**`,`完成OpenHEC实验平台顶层文件的加载。![](/assets/addtop001.png)

   ---

5. ##### 用户逻辑与实验支撑包的接口绑定

   打开**and4in\_bd\_wrapper.v**文件，拷贝and4in\_bd中的管脚绑定。

   ![](/assets/and4bd001.png)

   打开**OpenHEC\_Exp\_Top.v**文件，找到用户自定义顶层module实例化区域，粘贴and4in\_bd中拷贝的IO管脚绑定, 并重新命名模块的名字为 and4in\_bd\_wrapper。![](/assets/top001.png)

   根据[`RELAX_FlyxSOM`实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-ru-men-shou-ce.html)解析说明，选择相应的IO管脚绑定。实验输入端口绑定，4个1-bit的输入信号（A, B, C, D），这里可以绑定到开关SW00, SW01, SW02, SW03上。实验输出端口绑定，1个1-bit的输出信号（F），绑定到LED00上。在系统注释区域注释掉用户逻辑区绑定的IO输出端口。这里绑定了LED00管脚，因此需要加‘//’注释掉 LED00的初始赋值。参考代码如下：

   1. ```
      //assign LED00 = SW00; 

      and4in_bd_wrapper user_wrapper_top_uut
       (
           .A(SW00),
           .B(SW01),
           .C(SW02),
           .D(SW03),
           .F(LED00)
       );
      ```

6. ---

   ##### 综合与实现

   OpenHEC实验支撑包中提供综合实现的tcl脚本，可以自动完成整个系统的综合，最终生成比特流文件。点击 **Tools/Run Tcl Script**，选择文件夹**oLib/RELAX\_FlyxSOM/tcl **下的**relax\_syn\_imp\_flow.tcl**文件，点击OK，自动运行综合与实现，等待生成位流。比特流文件存放在桌面文件夹**proj\_ip/and4in\_proj**下。![](/assets/gbit001.png)

   ---

7. ##### 完成开发

   拷贝桌面文件夹**proj\_ip/and4in\_proj**下的位流文件**and4in\_proj.bit** 到oDisk目录，完成开发。![](/assets/cpodsik001.png)

   ---

#### 三、使用FPGA

完成了FPGA的开发后，用户既可以在OpenHEC部署在云端的FPGA硬件上验证与门的bit文件了。

1. ##### 配置比特流到FPGA

   点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中刚刚拷贝的and4in\_proj.bit位流，同时选择纯FPGA模式的配置方式，点击配置即可以，如下图所示。配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。![](/assets/genbit004.png)

2. ##### IO实时监控

   当输入开关A、B、 C、 D都置1时，输出信号灯F 才会点亮。![](/assets/and4in_001.png)

   当输入开关A、B、 C、 D其中有一个置0时，输出信号灯F 都不亮。![](/assets/adn4in002.png)



