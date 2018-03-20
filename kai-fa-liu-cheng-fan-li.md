### 开发流程范例

下面通过若干开发流程范例展示在OpenHEC平台上进行FPGA开发。

OpenHEC平台上FPGA开发主要支持纯FPGA模式、SoC模式和裸机模式，这里重点介绍纯FPGA模式和SoC模式下的经典开发流程范例。

#### 一、纯FPGA模式

1. **OpenHEC平台IO虚拟面板**
   [组合逻辑与门](http://www.iopenhec.com/#!/experiment/000020170401000000000006)
   [时序逻辑D触发器](http://www.iopenhec.com/#!/experiment/000020170413000000000002)
2. **OpenHEC平台存储虚拟面板**
   [片上ROM存储接口](http://www.iopenhec.com/#!/experiment/000020170413000000000004)
   [片外RAM存储接口](http://www.iopenhec.com/#!/experiment/000020170413000000000005)
3. **OpenHEC平台教学板（物理外设）+虚拟面板**
   [组合逻辑数码管](http://www.iopenhec.com/#!/experiment/000020170405000000000089)
   [时序逻辑LED点阵](http://www.iopenhec.com/#!/experiment/000020170413000000000003)
   [教学板SRAM存储接口](http://www.iopenhec.com/#!/experiment/000020170413000000000006)

### 二、SoC模式

1. **基于RELAXSoC支撑包的加速核SoC模式开发**
   [软硬件协同sobel算法加速](http://www.iopenhec.com/#!/experiment/000020170417000000000004)

### 



