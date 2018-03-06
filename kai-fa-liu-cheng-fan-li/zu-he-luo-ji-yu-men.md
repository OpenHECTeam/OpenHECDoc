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

   启动vivado 2015.2后，选择`Create New Project`，点击`Next`，输入项目名为`and4in_proj`和项目位置新建在桌面下的`proj_ip`。![](/assets/new_project.png)

   点击`Next`，在`Project Type`选项里，将`Do not specify source at this time`勾选上。![](/assets/58d7bcffebbc015268da6e78760a6f62.png)

   点击`Next`，这里需要选择芯片的型号。在`Parts`选项选择`xc7z030fbg484-3`芯片即可。![](/assets/621a3218d853ad7928393746eb4708e3.png)点击`Next`，然后`Finish`完成项目的创建。

   ---

2. ##### 添加基础IP核

   从oLib中拷贝与门的IP核 `OpenHEC_user_and4in_logic_1.0.zip`到桌面文件夹`proj_ip 里面。`

   在左侧菜单`Flow Navigator/Project Manager，`选项卡下点击`IP Catalog，`在窗口选择`IP Setting，`弹出`Project Setting`

   窗口，在`IP`选项卡，通过`+`添加`IP Repositories`，选择桌面文件夹`proj_ip`目录，然后在`IP in Selected Repository`

   选择需要用到的IP\(即`OpenHEC_user_and4in_logic_1.0.zip`\) ，完成后点击下方`Apply`，然后点击`OK`。![](/assets/addand4in_ip.png)

   ---

3. ##### Vivado框图设计

   在`Flow Navigator/IP Integrator`选项卡下选择`Create Block Design`，在弹出的窗口中输入一个设计名，这里输入`and4in_bd`

   ，点击`OK`。![](/assets/cbd001.png)

   在生成的Diagram界面中，选择`添加IP`按钮，在弹出的窗口中输入`and4in`选择IP，确认即可在Diagram界面出现这个IP 。![](/assets/a47496d635eaf9220e5f17b5af18f8d9.png)

   点击实验模块端口（如 A ），右击选择`Make External`，引出所有端口。![](/assets/ba9665b76e123387eed2804878427436.png)

   在`Flow Navigator`选项卡选择`Generate Block Design`，在弹出的窗口中选择`Generate`，完成原理图设计。

   在`Source/Hierarchy`选项卡中，右击`Design Source`中的bd文件（如本实验中的and4in\_bd.bd），选择`Create HDL Wrapper`, 弹出`Create HDL Wrapper`对话框，选择`Copy generated wrapper to allow user_edits`，点击`OK`。![](/assets/0d597b7274e841a0d3352313bf71e1fa.png)

   ---

4. ##### 添加OpenHEC实验平台顶层文件

   设计完用户区逻辑后，接下来添加OpenHEC实验平台顶层文件，文件存放在oLib/RELAX\_FlyxSOM/relax\_top 文件夹下，名为OpenHEC\_Exp\_Top.v。在`Flow Navigator/Project Manager`选项卡下选择`Add Sources`，在弹出的窗口中选择`Add or create design sources`，点击`Next`，点击`+`号标志，选择`Add Files`，添加 oLib/RELAX\_FlyxSOM/relax\_top 文件夹下的`OpenHEC_Exp_Top.v`文件。选择 `Copy sources into project,`点击`Finish,`完成OpenHEC实验平台顶层文件的加载。![](/assets/addtop001.png)

   ---

5. ##### 用户逻辑与实验支撑包的接口绑定

   打开and4in\_bd\_wrapper.v文件，拷贝and4in\_bd中的管脚绑定。

   ![](/assets/and4bd001.png)

   打开OpenHEC\_Exp\_Top.v文件，找到用户自定义顶层module实例化区域，粘贴and4in\_bd中拷贝的IO管脚绑定, 并重新命名模块的名字为 and4in\_bd\_wrapper。![](/assets/top001.png)

   根据`RELAX_FlyxSOM`实验支撑包解析说明，选择相应的IO管脚绑定。实验输入端口绑定，4个1-bit的输入信号（A, B, C, D），这里可以绑定到开关SW00, SW01, SW02, SW03上。实验输出端口绑定，1个1-bit的输出信号（F），绑定到LED00上。在系统注释区域注释掉用户逻辑区绑定的IO输出端口。这里绑定了LED00管脚，因此需要加‘//’注释掉 LED00的初始赋值。参考代码如下：

   1. ```
      //assign LED00 = SW00; 

      user_wrapper_top user_wrapper_top_uut
       (
           .A(SW00),
           .B(SW01),
           .C(SW02),
           .D(SW03),
           .F(LED00)
       );
      ```

6. ##### 综合与实现


7. ##### 完成开发

#### 三、使用FPGA



