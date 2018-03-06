### 使用FPGA

OpenHEC FPGA公有云目前接入了大量的[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012) FPGA节点\(芯片型号为：Xilinx ZYNQ 7030），让用户更加线上体验FPGA。![](/assets/openhec_fpga_cloud.png)

---

选择[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)为开发入口，点击**使用FPGA**, 无需任何等待，成功申请到FPGA节点。

如下图所示，FPGA操作页面主要提供了虚拟面板、终端界面、视频监控、运行记录、我的oDisk和操作说明主要功能。![](/assets/fpga_page.png)

#### 一、 **配置FPGA**

点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中相应的位流，同时选择FPGA需要的配置方式，点击配置即可以，如下图所示。![](/assets/fpga_config.png)配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。

OpenHEC 平台下FPGA位流的配置模式有三种，分别是纯FPGA模式、SoC模式和裸机模式。

* **纯FPGA模式**：使用纯FPGA模式下的**RELAX\_\*\*\***实验支撑包生成的位流
* **SoC模式**：使用SoC模式下的**RELAXSoC\_\*\*\***实验支撑包生成的位流
* **纯FPGA模式**：未使用RELAX实验支撑包生成的位流

---

#### 二、虚拟面板

虚拟面板仅在纯FPGA模式下，实时监控IO的输入输出状态变化及存储的读写；主要分为单步时钟、输入开关、输出信号灯、R8寄存器输入输出、R16寄存器输入输出、R32寄存器输入输出、读存储和写存储等功能；虚拟面板上的IO对应着纯FPGA模式下RELAX支撑包的top文件。![](/assets/fpga_panel.png)

---

#### 三、终端界面

终端界面是当前使用FPGA节点的Linux系统的ssh终端页面，终端系统的用户名和密码都是**root**, 用户根据页面的提示输入即可。

FPGA节点Linux系统中 **/home/linaro**目录自动同步**我的oDisk**的资料文件。![](/assets/gateone.png)

---

#### 四、视频监控

视频监控是当前正在使用的FPGA节点外设的实时监控，可以观察数码管、LED点阵、LCD显示等一些外设的直观效果。

![](/assets/fpga_moniter.png)

---

#### 五、我的oDisk

我的oDisk是OpenHEC平台用户的文件同步空间，方便本地、虚拟机和FPGA节点的文件同步；直接加载到FPGA节点开发目录下（**/home/linaro**）。![](/assets/my_odisk.png)

---

#### 六、 其他功能

OpenHEC FPGA云节点环境还提供了一些高级功能，如IO设置、运行记录、RAM基地址设置和SRAM存储访问设置。

1. **IO设置**  
   IO设置目的是为了用户调试方便，用户可将实验界面的IO所显示的名字与FPGA内部用户设计的逻辑命名设设置统一。

2. **运行记录**  
   运行记录主要提供了IO设置里面需要监控的信号的状态变化值，方便分析信号的中间状态。

3. **RAM基地址设置**

   RAM基地址设置主要是针对两片64MB的片外RAM基地址模式的设置，选择基地址相同即是独立编址；选择基地址不同即是统一编址。

4. **SRAM存储访问设置**  
   SRAM存储访问设置针对用到SRAM实验支撑包预留的操作接口；；在使用SRAM外设前，先选择打开SRAM存储；才能在WEB端对SRAM的读写进行控制；在不用SRAM外设时，选择关闭SRAM存储即可；默认模式下SRAM在WEB端的控制是关闭的。

#### 



