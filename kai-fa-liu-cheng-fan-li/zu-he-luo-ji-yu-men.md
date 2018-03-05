### [组合逻辑与门](http://www.iopenhec.com/#!/experiment/000020170401000000000006)

组合逻辑与门是以4输入的与门为例子，进行组合逻辑"Hello World"的入门单节点实验，是在纯FPGA模式下使用[RELAX\_FlyxSOM](http://www.iopenhec.com/#!/app/forum/topics/2332)实验支撑包来进行开发的。

#### 一、开发入口

组合逻辑与门的OpenHEC平台的开发入口是：[http://www.iopenhec.com/\#!/experiment/000020170401000000000006](http://www.iopenhec.com/#!/experiment/000020170401000000000006)

组合逻辑与门采用的硬件类型为[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)，具体芯片型号为**xc7z030fbg484-3**。

实验资料**oLib**目录中主要资料如下。

* 纯FPGA模式下的RELAX\_FlyxSOM实验支撑包

* 4输入与门IP核\(**OpenHEC\_user\_and4in\_logic\_1.0**\)

#### 二、使用虚拟机

1. ##### 新建用户逻辑工程

   启动vivado 2015.2后，选择**`Create New Project`**，点击**`Next`**，输入项目名为**`and4in_proj`**和项目位置新建在桌面下的**`proj_ip`**。

   点击**`Next`**，在**`Project Type`**选项里，将**`Do not specify source at this time`**勾选上。![](/assets/58d7bcffebbc015268da6e78760a6f62.png)

   点击**`Next`**，这里需要选择芯片的型号。在**`Parts`**选项选择**`xc7z030fbg484-3`**芯片即可。![](/assets/621a3218d853ad7928393746eb4708e3.png)点击**`Next`**，然后**`Finish`**完成项目的创建。

   ---

2. ##### 添加基础IP核

   在左侧菜单`Flow Navigator/Project Manager，`选项卡下点击`IP Catalog，`在窗口选择`IP Setting，`弹出`Project Setting`

   窗口，在`IP`选项卡，通过`+`添加`IP Repositories`，选择目下的`base_ip`目录，然后在`IP in Selected Repository`

   选择需要用到的IP\(即`OpenHEC_user_and4in_logic_1.0.zip`\) ，完成后点击下方`Apply`，然后点击`OK`。

   ---

3. ##### Vivado框图设计

   在`Flow Navigator/IP Integrator`选项卡下选择`Create Block Design`，在弹出的窗口中输入一个设计名，这里输入`and4in_bd`

   ，点击`OK`。

   在生成的Diagram界面中，选择`添加IP`按钮，在弹出的窗口中输入`and4in`选择IP，确认即可在Diagram界面出现这个IP \(见图5.6\)。

   点击实验模块端口（如 A ），右击选择`Make External`，引出所有端口（见图5.7 ）。

   在`Flow Navigator`选项卡选择`Generate Block Design`，在弹出的窗口中选择`Generate`，完成原理图设计。

   在`Source/Hierarchy`选项卡中，右击`Design Source`中的bd文件（如本实验中的and4in\_bd.bd），选择`Create HDL Wrapper`, 弹出`Create HDL Wrapper`对话框，选择`Copy generated wrapper to allow user_edits`（见图 5.8 ），点击`OK`。

   打开自动生成的`and4in_bd_wrapper.v`文件，重新定义module的名字由`and4in_bd_wrapper`修改为`user_wrapper_top`（见图 5.9）。

4. ##### 添加OpenHEC实验平台顶层文件
5. ##### 用户逻辑与实验支撑包的接口绑定
6. ##### 综合与实现
7. ##### 完成开发

#### 三、使用FPGA



