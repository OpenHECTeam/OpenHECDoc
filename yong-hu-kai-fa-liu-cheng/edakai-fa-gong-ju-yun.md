### 使用虚拟机

选择硬件平台下的[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)为开发入口，点击使用虚拟机，请耐心等待三分种左右，等待虚拟机页面。

虚拟机主要提供了FPGA开发必备的EDA工具Xilinx **Vivado**、用户文件同步空间**oDisk**、支撑包库及相应资料**oLib**等，如下图所示。![](/assets/vivado.png)

---

#### 一、实验说明

实验说明是当前资源入口的相关说明文档，点击**查看实验说明**即可查看。

#### 二、**oLib**

**oLib**是当前资源入口的相关实验资料及所用到的平台支撑包，在开发时直接引用即可以。

目前OpenHEC平台上的[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)支撑包主要有4类，其支撑包名如下，主要用在纯FPGA开发模式和SoC开发模式。

* **RELAX\_FlyxSOM  ----  纯FPGA开发模式**  
  1. 480个虚拟输入  
  2. 480个虚拟输出  
  3. 2KB片上ROM  
  4. 两个64MB片外RAM

* **REAX\_FlyxSOM\_LED7SEG  ---纯FPGA开发模式**  
  1. 480个虚拟输入  
  2. 480个虚拟输出  
  3. 2KB片上ROM  
  4. 两个64MB片外RAM  
  5. 数码管物理外设  
  6. LED点阵物理外设

* **RELAX\_FlyxSOM\_LED7SEG\_SRAM  --- 纯FPGA开发模式**  
  1. 480个虚拟输入  
  2. 480个虚拟输出  
  3. 2KB片上ROM  
  4. 两个64MB片外RAM  
  5. 数码管物理外设  
  6. LED点阵物理外设  
  7. SRAM物理外设

* **RELAXSoC\_FlyxSOM   --- SoC开发模式**  
  1. 1组32-bit AXI4Lite Master  
  2. 1组32-bit AXI4 Slave  
  3. ZYNQ PS端软件驱动库

[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)支撑包的详细文档请参考 。

#### 三、**oDisk**

**oDisk**是OpenHEC平台用户的文件同步空间，方便本地、虚拟机和FPGA节点的文件同步。在浏览器端点击**上传本地文件**或**下载云端文件**进行文件同步。

#### 四、EDA开发工具

虚拟机EDA开发工具主要有Vivado、Vivado HLS和Vivado SDK。

* **Vivado**  
  Vivado设计套件，是FPGA厂商赛灵思公司2012年发布的集成设计环境。Vivado的设计流程主要分为工程设计、综合、实现和生成FPGA位流，其主要流程如下图。

  ```
             ![](/assets/07f7b2541ba1bc7e2b022c3fc062e74f.png)
  ```

* **Vivado HLS**

  Vivado 高层综合技术（HLS）实现直接使用 C，C++ 以及 System C 语言规范对赛灵思全可编程器件进行编程，无需手动创建 RTL，从而可加速 IP（功能模块） 创建。

  ```
              ![](/assets/hls.png)
  ```

* **Vivado SDK**



