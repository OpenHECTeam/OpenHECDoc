组合逻辑与门 

====

\#\# 1 简介

以4输入的与门为例子，进行组合逻辑"Hello World"的入门单节点实验。

\#\# 2 准备实验所需的文件

实验详情页面，点击“实验资料”tab页，根据自己的需要下载文件。

\#\# 3 申请实验开发工具（可选）

\*\*1、如果本机没有安装所需的开发工具（如Vivado等EDA软件），可参考下面的步骤:\*\*

```
在“实验资料”tab页中，下载实验支撑包等实验资料到本地

启动本地的Vivado开发工具
```

\*\*2、线上使用开发工具\*\*

```
在实验详情页面，在右侧点击“申请开发工具”，进入线上开发环境，实验相关资料等均在开发环境中的workpath目录中
```

\#\# 4 实验支撑包（\`RELAX\_FlyxSOM\`版本）

&gt; 友情提示： 本次实验是与门的组合逻辑的单节点入门实验，实验支撑包版本推荐使用\`RELAX\_FlyxSOM\`版本，请参考\`实验支撑包RELAX\_FlyxSOM入门手册\`

[http://www.iopenhec.com/\#!/app/forum/topics/2332](http://www.iopenhec.com/#!/app/forum/topics/2332)

\#\# 5 进入实验具体开发

本次实验以四输入与门为例，介绍如何在OpenHEC平台上以纯FPGA方式做实验开发。

\#\#\# 5.1 用户逻辑工程

\#\#\#\# 5.1.1 准备系统工程文件

1. OpenHEC实验支撑包预先存放在桌面下的pubpath/file\_path/RELAX\_FlyxSOM文件目录下，拷贝文件夹\`RELAX\_FlySOM\`到桌面文件夹\`workpath\`目录下进行工程开发。

1. 开发工程根目录为 \`/home/openhec/Desktop/workpath/RELAX\_FlyxSOM/\`。

\#\#\#\# 5.1.2 建立工程项目

1. 启动vivado 2015.2后，选择\`Create New Project\`，点击\`Next\`，输入项目名为\`and4in\_proj\`和项目位置为&lt;工程目录&gt;下的\`proj\_ip\`（见图5.1）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/2609ea22f7674378e7429aea9ea88128.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/2609ea22f7674378e7429aea9ea88128.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.1  创建实验名和实验目录&lt;/center&gt;

1. 点击\`Next\`，在\`Project Type\`选项里，将\`Do not specify source at this time\`勾选上（见图5.2）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/58d7bcffebbc015268da6e78760a6f62.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/58d7bcffebbc015268da6e78760a6f62.png\)\)

&lt;/center&gt;

&lt;center&gt;图5.2  项目类型选项&lt;/center&gt;

1. 点击\`Next\`，这里需要选择芯片的型号。在\`Parts\`选项选择\`xc7z030fbg484-3\`芯片即可（见图5.3）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/621a3218d853ad7928393746eb4708e3.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/621a3218d853ad7928393746eb4708e3.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.3  Flyx-SOM核心条选择 &lt;/center&gt;

1. 点击\`Next\`，然后\`Finish\`完成项目的创建。

\#\#\#\# 5.1.3 添加基础库IP核

在左侧菜单\`Flow Navigator/Project Manager\`选项卡下点击\`IP Catalog\`，在窗口选择\`IP Setting\`，弹出\`Project Setting\`窗口，在\`IP\`选项卡，通过\`+\`添加\`IP Repositories\`，选择&lt;工程目录&gt;下的\`base\_ip\`目录，然后在\`IP in Selected Repository\`选择需要用到的IP\(即\`OpenHEC\_user\_and4in\_logic\_1.0.zip\`\) ，完成后点击下方\`Apply\`，然后点击\`OK\`（见图5.4）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/478ff6676c1bcd54e317143cc6e62e42.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/478ff6676c1bcd54e317143cc6e62e42.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.4  IP核选择与添加 &lt;/center&gt;

\#\#\#\# 5.1.4 创建框图设计（调用基础库IP核）

1. 在\`Flow Navigator/IP Integrator\`选项卡下选择\`Create Block Design\`，在弹出的窗口中输入一个设计名，这里输入\`and4in\_bd\`，点击\`OK\`（见图5.5）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/1dfee6d6ba38992c10b159d0ee0cf8f8.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/1dfee6d6ba38992c10b159d0ee0cf8f8.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.5  创建工程BD文件 &lt;/center&gt;

1. 在生成的Diagram界面中，选择\`添加IP\`按钮，在弹出的窗口中输入\`and4in\`选择IP，确认即可在Diagram界面出现这个IP \(见图5.6\)。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/a47496d635eaf9220e5f17b5af18f8d9.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/a47496d635eaf9220e5f17b5af18f8d9.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.6  在BD中添加IP核 &lt;/center&gt;

1. 点击实验模块端口（如 A ），右击选择\`Make External\`，引出所有端口（见图5.7 ）。

&lt;center&gt; !\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/ba9665b76e123387eed2804878427436.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/ba9665b76e123387eed2804878427436.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.7  4输入与门模块 &lt;/center&gt;

1. 在\`Flow Navigator\`选项卡选择\`Generate Block Design\`，在弹出的窗口中选择\`Generate\`，完成原理图设计。

1. 在\`Source/Hierarchy\`选项卡中，右击\`Design Source\`中的bd文件（如本实验中的and4in\_bd.bd），选择\`Create HDL Wrapper\`, 弹出\`Create HDL Wrapper\`对话框，选择\`Copy generated wrapper to allow user\_edits\`（见图 5.8 ），点击\`OK\`。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/0d597b7274e841a0d3352313bf71e1fa.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/0d597b7274e841a0d3352313bf71e1fa.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.8  生成用户逻辑区TOP文件&lt;/center&gt;

1. 打开自动生成的\`and4in\_bd\_wrapper.v\`文件，重新定义module的名字由\`and4in\_bd\_wrapper\` 修改为\`user\_wrapper\_top\`（见图 5.9）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/3cbf66ba983096a569213bc6cd8e214c.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/3cbf66ba983096a569213bc6cd8e214c.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.9  重命名用户逻辑区TOP文件中的module模块名&lt;/center&gt;

\#\#\#\# 5.1.5 添加OpenHEC实验平台顶层文件

1. 设计完用户区逻辑后，接下来添加OpenHEC实验平台顶层文件，文件存放在&lt;工程目录&gt;下的\`relax\_top\`文件夹下，名为OpenHEC\_Exp\_Top.v。

1. 在\`Flow Navigator/Project Manager\`选项卡下选择\`Add Sources\`，在弹出的窗口中选择\`Add or create design sources\`，点击\`Next\`，点击\`+\`号标志，选择\`Add Files\`，添加&lt;工程目录&gt;下\`relax\_top\`文件夹下的\`OpenHEC\_Exp\_Top.v\`文件（见图5.10）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/599f8f2a617bb02bb7bc0b4d4f2cdf07.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/599f8f2a617bb02bb7bc0b4d4f2cdf07.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.10  添加OpenHEC实验平台顶层文件&lt;/center&gt;

1. 点击\`Finish\`完成OpenHEC实验平台顶层文件的加载。

\#\#\#\# 5.1.6 用户逻辑与实验支撑包的接口绑定

1. 打开\`and4in\_bd\_wrapper.v\`文件，拷贝\`and4in\_bd\`中的管脚绑定（见图5.11）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/152a2583b38c18b041d4366918386a54.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/152a2583b38c18b041d4366918386a54.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.11  拷贝用户逻辑区TOP文件中的管脚绑定&lt;/center&gt;

1. 打开\`OpenHEC\_Exp\_Top.v\`文件，找到 用户自定义顶层module实例化区域，粘贴\`and4in\_bd\`中拷贝的IO管脚绑定（见图5.12）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/e8fa69f5040403592cf9b9cff1541b56.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/e8fa69f5040403592cf9b9cff1541b56.png\)\)

&lt;/center&gt;

&lt;center&gt; 图5.12  粘贴用户逻辑区TOP中的管脚绑定到OpenHEC实验支撑包顶层中&lt;/center&gt;

1. 根据第4章节\`RELAX\_FlyxSOM\`实验支撑包解析说明，选择相应的IO管脚绑定。

1. 实验输入端口绑定，4个1-bit的输入信号（A, B, C, D），这里可以绑定到开关SW00, SW01, SW02, SW03上。

1. 实验输出端口绑定，1个1-bit的输出信号（F），绑定到LED00上。参考代码如下：

    \`\`\` verilog

    user\_wrapper\_top user\_wrapper\_top\_uut

    \(

        .A\(SW00\),

        .B\(SW01\),

        .C\(SW02\),

        .D\(SW03\),

        .F\(LED00\)

    \);

    \`\`\`

1. 在系统注释区域注释掉用户逻辑区绑定的IO输出端口。这里绑定了LED00管脚，因此需要加\*\*‘//’\*\*注释掉 LED00的初始赋值，参考代码如下：

    \`\`\` verilog

        //assign LED00 = SW00;

    \`\`\`

\#\#\# 5.2 综合与实现

OpenHEC实验支撑包中提供两个脚本文件，可以自动完成整个系统的综合，最终生成比特流文件。两个脚本文件存放在工程根目录的tcl目录下，其中\`relax\_syn\_flow.tcl\`用于对用户逻辑进行综合，\`relax\_imp\_flow.tcl\`用于将整个工程（包含用户逻辑和实验支撑包）实现为比特流文件。

tcl文件可以用文本编辑器打开编辑，WINDOWS下推荐用\`Nodepad++\`编辑器，Linux下推荐用\`gedit\`编辑器。

\#\#\#\# 5.2.1 生成用户逻辑区dcp文件

1. 打开\`relax\_syn\_flow.tcl\`，修改前两句\`set pco\_lab\_name\`、\`set project\_path\`后面的内容\(见下表\)。

\|  修改项  \|  修改前内容 \| 修改后内容  \|  说明  \|

\|  :--:   \|    :--:   \|   :--:    \| :--: \|

\| set pco\_lab\_name \|  xxxx.dcp    \|     flyx\_and4in.dcp  \|  综合后生成dcp文件的文件名  \|

\| set project\_path \|  xxx \| /home/openhec/Desktop/workpath/RELAX\_FlyxSOM         \|  OpenHEC实验支撑包解压后的根目录\|

1. 修改完成后保存退出。然后在Tcl  Console命令行中使用source命令来执行tcl脚本。

   \`\`\` tcl

source /home/openhec/Desktop/workpath/RELAX\_FlyxSOM/tcl/relax\_syn\_flow.tcl

    \`\`\`

1. 等待执行完成后，开始下一步生成比特流。

\#\#\#\# 5.2.2 生成bit文件

1.打开relax\_imp\_flow.tcl文件，修改下表指定的内容。

\|  修改项  \|  修改前内容 \| 修改后内容  \|  说明  \|

\|  :--:   \|    :--:   \|   :--:    \| :--: \|

\| set relax\_flyx\_lab\_imp\_name \|  xxxx.dcp \|     relax\_flyx\_and4in.dcp  \|  布局布线后后生成dcp文件的文件名  \|

\| set relax\_flyx\_lab\_bit\_name \|  xxx.bit \| relax\_flyx\_and4in.bit  \|  最终生成的BIT文件的文件名          \|

\| set pco\_lab\_name \|  xxxx.dcp    \|     flyx\_and4in.dcp  \|  综合后生成dcp文件的文件名  \|

\| set project\_path \|  xxx \| /home/openhec/Desktop/workpath/RELAX\_FlyxSOM         \|  OpenHEC实验支撑包解压后的根目录         \|

2.修改完成后保存退出。然后在Tcl  Console命令行中使用source命令来执行tcl脚本

\`\`\` tcl

    source /home/openhec/Desktop/workpath/RELAX\_FlyxSOM/tcl/relax\_imp\_flow.tcl

    \`\`\`

3.执行完之后，会生成（见图5.13 ）的界面，代表比特流生成成功, 生成的bit流文件默认存放在\*\*\`工程目录\`\*\*下的\*\*\`bit\`\*\*文件夹下。

```
&lt;center&gt;!\[图片\]\(http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/c17f5c72d2b93e07c0a8ba2cbfa2ea02.png\)
```

&lt;/center&gt;

```
&lt;center&gt;  图5.13  比特流生成成功示意图 &lt;/center&gt;
```

\#\#\# 5.3 完成开发，生成可执行文件

Vivado开发完成后会生成可下载到FPGA中的可执行文件（bit文件）。

```
本地开发：开发结束，可以进行线上节点使用

线上开发：开发结束，文件被同步到该实验下的FPGA节点工作目录（如图5.14），在申请实验界面
```

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/3d9a754aa0140ae33031d27b74482a14.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/3d9a754aa0140ae33031d27b74482a14.jpg\)\)

&lt;/center&gt;

&lt;center&gt;图5.14 节点工作空间&lt;/center&gt;

\#\# 6 在FPGA上验证结果

到这一步，用户就可以在OpenHEC部署在云端的FPGA硬件上验证所生成的bit文件了。

\#\#\# 6.1 申请OpenHEC云上的FPGA节点

申请OpenHEC云上的FPGA节点的主要步骤如下。

1. 在实验详情页面点击\*\*申请实验设备\*\*。

2. 进入申请节点页面后，点击\*\*点击申请\*\*按钮。

3. 成功申请到节点后，便可以进入实验操作主界面，如图6.1所示。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/79973f1176d52eb81195e7d51f93e1c3.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/79973f1176d52eb81195e7d51f93e1c3.jpg\)\)

&lt;/center&gt;

&lt;center&gt;图6.1  实验操作界面&lt;/center&gt;

\#\#\# 6.2 上传比特流或其他测试文件（可选）

1. \*\*最终生成的bit文件在本机上\*\*： 在配置到云端的FPGA中之前, 首先要上传到\*\*节点工作空间\*\*（图6.1）。点击\`节点工作空间\`下面的\`上传文件\`按钮，可以上传FPGA bit文件、ARM可执行程序以及测试文件等。

1. \*\*最终bit文件在OpenHEC开发工具云服务器生成的，文件已被同步到\`FPGA节点工作空间\`\*\*：直接进入下一步。

\#\#\# 6.3 配置比特流到FPGA

1. 点击\`配置FPGA\`，弹出个人空间目录跟当前工作节点的工作目录下的比特流可配置文件（图6.2）

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/16cfe1f9ecff96f7a921d1191d631925.png\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/16cfe1f9ecff96f7a921d1191d631925.png\)\)

&lt;/center&gt;

&lt;center&gt;图6.2  配置比特流&lt;/center&gt;

1. 点击上传的.bin文件，此时前面的小圆圈被填充，选择\`纯FPGA模式\`，点击“配置”按钮进行配置比特流，如果配置成功，页面会出现一个窗口，显示配置比特流成功，点击确认即可。

\#\#\# 6.4 IO设置

IO设置的目的是为了用户调试方便，允许用户将实验界面的IO所显示的名字与FPGA内部用户设计的逻辑命名设为一样的。

1. \*\*逻辑IO管脚与OpenHEC平台实验支撑包提供的IO管脚的绑定关系对应\*\*：本实验中的用户逻辑引脚与OpenHEC平台实验支撑包提供的IO管脚的绑定详见章节4.6.6，参考代码如下。

   \`\`\` verilog

   user\_wrapper\_top user\_wrapper\_top\_uut

   \(

   ```
    .A\(SW00\),

    .B\(SW01\),

    .C\(SW02\),

    .D\(SW03\),

    .F\(LED00\)
   ```

   \);

   \`\`\`

1. \*\*WEB页面IO管脚设置\*\*：点击实验主界面的上方功能区\`IO设置\`按钮，弹出\`设置输入输出\`对话框，重命名SW00 、SW01 、SW03、SW04和LED00，分别设置为A、B、C、D和F；并且选中相应的监控信号，方便实时记录这些IO管脚的变化状态（见图6.3）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/58947d0a7437b9673fcdbc129f8869f0.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/58947d0a7437b9673fcdbc129f8869f0.jpg\)\)

&lt;/center&gt;

&lt;center&gt; 图6.3  重命名WEB页面IO管脚&lt;/center&gt;

1. \*\*IO管脚配置可收藏\*\*：在上方选中\`是否收藏此方案\`，设置实验的WEB页面IO管脚方案为\` and4in\_config\` （见图6.3），方便用户加载常用的一些自定义的方案配置。

\#\#\# 6.5 IO实时监控

1. 用户可以根据自己的实验逻辑选择IO管脚的触发方式：组合逻辑和时序逻辑，如图6.4所示。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/407252187962e84dd72fc89b35d29cac.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/407252187962e84dd72fc89b35d29cac.jpg\)\)

&lt;/center&gt;

&lt;center&gt;图6.4  选择IO触发模式&lt;/center&gt;

1. 本实验是四输入的与门逻辑，采用的是\*\*组合逻辑\*\*的IO触发方式 ，其IO实时监控界面如图6.5所示。

&lt;center&gt; !\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/2911b54b717d4d1147c1217902fb68a6.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/2911b54b717d4d1147c1217902fb68a6.jpg\)\)

&lt;/center&gt;

&lt;center&gt;图6.5  四输入与门实时监控主要信号&lt;/center&gt;

1. 当输入开关A、B、 C、 D都置1时，输出信号灯F 才会点亮 （见图6.6）。 

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/e3456d054cf4014ca49b59a9788598b0.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/e3456d054cf4014ca49b59a9788598b0.jpg\)\)

&lt;/center&gt;

&lt;center&gt;图6.6  四输入与门IO实时监控运行图 &lt;/center&gt;

1. 当输入开关A、B、 C、 D其中有一个置0时，输出信号灯F 都不亮（见图6.7）。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/a589f389384c76a53c69d35127ad6acf.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/a589f389384c76a53c69d35127ad6acf.jpg\)\)

&lt;/center&gt;

&lt;center&gt;图6.7  四输入与门IO实时监控运行图 &lt;/center&gt;

\#\#\# 6.6 IO运行记录

IO运行记录主要提供了IO设置里面需要监控的信号。图6.8所示是四输入与门运行时IO监控结果。

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/704b54a6087ab27d3abeb9cad4c6a9a3.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/704b54a6087ab27d3abeb9cad4c6a9a3.jpg\)\)

&lt;/center&gt;

&lt;center&gt;!\[图片\]\([http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/699dfd9bbee4dd77ec81872127884ba2.jpg\](http://61.177.139.248:18080/OpenHEC//api/ExperimentService/MDimages/699dfd9bbee4dd77ec81872127884ba2.jpg\)\)

&lt;/center&gt;

&lt;center&gt;图6.8 四输入与门运行结果展示&lt;/center&gt;

