### RELAXSoC\_FlyxSOM入门手册

#### 一、功能简介

OpenHEC项目支撑包是OpenHEC平台上用于支持软硬协同加速器项目开发，目前主要支持Xilinx公司的Zynq系列器件。OpenHEC项目支撑包建立在Xilinx公司的Vivado系列开发工具基础上，以C、C++作为项目开发语言，支持基于高级语言的加速器功能调试和性能优化。为了方便软件开发人员快速高效地将算法移植到OpenHEC线上节点上，OpenHEC项目支撑包提供了基于GNU Make工具的项目自动编译机制，支持“一键”从高级语言代码直接生成加速器的FPGA位流文件和硬件接口驱动代码。

OpenHEC项目支撑包V1.0基本功能如下：

```
支持Xilinx公司的Zynq系列FPGA SoC和Vivado 2015.02开发环境
提供软硬协同的加速器项目工程框架
提供基于C、C++的加速器IP开发模板
提供标准的硬件接口定义，支持加速器IP通过32位的AXI4总线接口和32位AXI4 Lite总线接口与FPGA SoC的其它硬件资源进行互联
支持通过make命令的方式，“一键”直接从C、C++代码生成加速器的FPGA位流文件和接口驱动
```

#### 二、项目支撑包简介

基于OpenHEC项目支撑包，用户可以根据应用领域的特定算法快速建立自己的软硬协同的加速器开发项目。

##### 1 软硬协同的加速器结构组成

OpenHEC项目支撑包面向FPGA SoC，当前版本主要支持Xilinx公司的Zynq系列芯片。Zynq系列芯片内包含通用的ARM处理器核心（PS部分）和FPGA可重构逻辑资源（PL部分），构成了典型的异构计算架构。Zynq系列处理器详细信息请参考Xilinx官方手册《DS190: Zynq-7000 All Programmable SoC Overview》。

在上述架构的基础上，OpenHEC项目支撑包定义了一种通用的软硬件协同的加速器结构，如下图所示。![](/assets/37d3795ddcb39a1bc40b332c11c0b931.png)

软硬协同加速器包括软件功能部分、定制的硬件加速器和软硬件接口三个部分：

* **定制硬件加速器部分**
   对于一个算法，其最核心的部分是代码中花费时间最长的计算密集部分。将这一部分代码定制为硬件加速器，通过FPGA进行加速，可以显著提升算法性能。
  为了便于硬件加速器的实现，OpenHEC项目支撑包将FPGA分为系统区和用户区两个部分。其中，系统区逻辑由OpenHEC平台提供，预先定义了加速器软硬件之间的接口逻辑。系统区的硬件逻辑以DCP文件方式包含在支撑包中，由项目支撑包管理和使用。这种方式便于用户进行快速系统集成。用户区只需要关注加速器IP的设计和实现，即把算法核心代码段实现为定制硬件IP核。加速器IP是硬件加速区的核心功能部分。项目支撑包会自动地将系统区（接口逻辑）和用户区（加速器IP）集成在一起，构成整个硬件加速器。
* **软件功能部分**
  除了核心部分以外，算法还包括一些外围功能，如数据文件的加载、输入数据的预处理、计算结果的处理等。这些外围功能可以仍然以软件方式，在通用处理器上执行。软件部分和硬件加速器部分相结合，协同工作，共同完成整个应用算法的功能。
* **软硬件接口**
  软硬件之间需要通过接口进行控制和数据交换。项目支撑包预定义了两个接口：控制接口和数据接口。其中，控制接口基于AXI4 Lite协议，主要用于加速器IP的参数配置及启动、暂停等运行时控制。数据接口基于AXI4协议，可以支持访问软硬件共享的DDR内存，支持burst传输模式，用于软硬件之间大量数据的交换。

##### 2 项目支撑包目录结构

用户登录OpenHEC在线实验平台后，可以在具体硬件平台的实验支撑包区下载OpenHEC项目支撑包,这里即是`RELAXSoC_FlyxSOM`。

整个项目支撑包的目录结构如下：

| 一级目录 | 二级目录 | 说明 |
| :--- | :--- | :---: |
| hls |  | 存放项目编译过程中的代码高层综合相关的工程文件 |
| hw |  | 存放项目中FPGA硬件逻辑相关的工程文件 |
|  | hw/sys\_dcp | 存放FPGA上系统区的DCP文件，其中主要包含硬件接口部分的逻辑，由OpenHEC平台预先生成并提供用户使用 |
|  | hw/user\_dcp | 存放FPGA上用户区的DCP文件，其中包含由用户定义的加速器硬件逻辑 |
|  | hw/design\_dcp | 存放整个硬件设计（系统区+用户区）的DCP文件，编译过程中由系统自动生成 |
| imp |  | 存放最终编译生成的位流文件和驱动代码 |
|  | impl/bin\_file | 存放最终生成的位流文件 |
|  | impl/linux\_driver | 存放最终生成的用户自定义加速器的硬件接口驱动代码 |
| script |  | 存放项目支撑包中的配置和脚本文件 |
| src |  | 存放加速器IP的C、C++源代码 |
|  | src/tb | 存放加速器IP的测试代码，其中包含了软件功能仿真所需的main函数等 |
|  | src/data | 存放加速器IP在软件功能仿真时所需加载的数据文件 |
| makefile |  | 编译脚本 |

##### 3 基于项目支撑包的加速器项目开发流程

以下是基于OpenHEC项目支撑包的用户项目开发流程图。![](/assets/a82280fd8aca941f036b1e9441232a02.png)

用户基于OpenHEC的项目开发过程中，可以遵循以下步骤：

1. 对待开发或移植的算法进行软硬功能划分。其中，计算密集的核心函数部分设计成硬件加速器，运行于FPGA上。核心函数以外的功能仍然以软件代码方式运行于通用处理器核心上。
2. 基于C、C++语言，在纯软件环境下进行加速器功能设计、开发和正确性验证。
3. 针对加速器设计的性能目标，在加速器代码中添加针对高层综合的编译指示和约束，对加速器代码进行优化。
4. 在项目工程目录下编译整个工程，项目支撑包会自动生成加速器的位流文件和Linux驱动代码。
5. 登录OpenHEC线上平台，申请节点资源。在节点上实现加速器以外的软件功能，并通过生成的接口驱动调用FPGA上加速器。完成代码后，在节点上通过本地GCC工具链编译生成可执行文件。
6. 在节点上，将位流文件配置到FPGA，然后执行可执行文件，进行算法功能验证和性能测试。

#### 4 编译命令

OpenHEC项目支撑包提供以下编译命令：

| 命令 | 功能 |
| :--- | :--- |
| make | “一键”完成整个编译过程，从C、C++代码生成最终的位流文件和驱动代码 |
| make clean | 清除编译生成的所有中间文件和目标文件 |
| make user\_ip | 自动建立Vivado HLS工程并打开IDE模式 |
| make csim | Shell模式下执行加速器功能仿真 |
| make csynth | Shell模式下执行高层综合，生成加速器IP |
| make user\_dcp | 单独生成加速器IP（用户区）DCP文件 |
| make design\_dcp | 单独生成整个硬件加速器的DCP文件 |
| make bin\_file | 单独生成硬件加速器的FPGA位流文件 |
| make driver | 单独生成FPGA SoC环境下的加速器软硬件接口驱动代码 |

表中前三项为最基本的编译命令，是OpenHEC项目支撑包中最常用的三个命令。从第四项开始属于针对特定中间目标的编译命令，是OpenHEC项目支撑包为中高级用户提供的更加方便、灵活的开发工具。

与纯软件项目一样，GNU Make工具会自动管理项目中的代码更新。根据目标文件之间的依赖关系，仅在代码发生更新时，对工程进行编译。

#### 三、加速器项目开发指南

##### 1 建立用户自己的加速器开发项目

从线上平台下载的项目支撑包提供了一个空的项目工程框架，用户需要在此基础上建立属于自己的项目工程。用户可以通过以下两种方式建立自己的项目。

1. 从零开始，手动创建并添加代码文件到src和tb目录下并创建工程。
2. 将已有的算法软件代码复制到src和tb目录下，以此为基础建立工程。

无论采取哪种方式，作为一个完整的工程，src和tb目录下至少需要各建立一个C、C++的代码文件。如果加速器功能仿真需要从外部数据文件读取测试激励，可以将测试激励文件放在data目录下，项目支撑包会自动将其添加到工程中。

OpenHEC项目支撑包支持两种加速器开发模式：IDE模式和shell模式。

* **IDE模式**  
  建好代码文件后，在dev\_proj目录下，执行make user\_ip命令。该命令将基于src和tb目录下代码文件建立用户加速器IP设计的子工程，并打开Vivado HLS IDE环境，进入图形化开发界面。![](/assets/8ba669f1620e610ad45bfa8bd6b9b4c0.png)

  Vivado HLS IDE使用方法请参考Xilinx官方用户手册《UG871: Vivado Design Suite Tutorial High-Level Synthesis》

* **Shell模式**  
  用户直接可以直接通过vim、gedit等第三方的文本编辑器进行代码开发。项目支撑包的makefile支持以命令行方式执行功能仿真、综合和IP生成，对应的命令如下：

  | 命令 | 功能 |
  | :--- | :--- |
  | make csim | 执行功能仿真，进行代码功能调试 |
  | make csynth | 执行高层综合，将C、C++代码转换成硬件逻辑，并打包生成加速器IP。 |

  ```
  在Shell模式下，项目支撑包会自动对整个项目进行管理。
  ```

##### 2 加速器顶层函数模板定义

在IDE模式或Shell下，用户可以采用C、C++语言完成加速器设计、实现和功能仿真（或称为C仿真）。然后通过在代码中添加各种约束和编译指示。Vivado HLS高层综合工具会基于约束和编译指示，自动将C、C++代码转换成加速器硬件IP。

OpenHEC项目支撑包预定义了加速器顶层函数模板。该模板以C、C++用户可以基于该模板进行加速器接口和功能设计。user\_accel定义如下：

```HLS
void user_accel(TYPE1 param1, TYPE2 param2, …. , TYPE3 paramN){
//加速器接口约束

//加速器功能实现

}
```

user\_accel包含以下四个主要部分：

1. 函数名：一方面，作为C仿真的入口，主函数或其它外围函数通过调用user\_accel函数来对加速器功能进行功能仿真。另一方面，函数名user\_accel直接对应加速器IP的硬件模块名，在硬件模块集成时被项目支撑包使用。注意：项目支撑包默认user\_accel为加速器名。因此，开发过程中请勿更改函数名，否则项目支撑包中的自动化工具将无法识别加速器IP。
2. 参数列表：参数类型TYPE、参数名param和参数个数可以根据加速器设计的需要由用户自己定义，但需要遵循HLS的代码规范，使HLS工具能正确地将函数参数转换为硬件IP接口。
3. 加速器接口约束：对参数列表中的各个参数添加约束，使HLS工具能将其转换成指定协议的硬件接口。
4. 加速器功能实现：该部分包含加速器功能所有实现，代码中支持函数的嵌套调用。![](/assets/f16772ac91cb2a8e538730dd098d6fdc.png)

##### 3 加速器IP的设计、开发和功能仿真

在user\_accel函数模板的基础上，用户可以开始加速器IP的开发。下面以伪代码形式给出一个简单的示例。

```HLS
void user_accel(TYPE1 param1, TYPE2 param2, …. , TYPE3 paramN){
//加速器接口约束

//加速器功能代码
Func_A();
    Func_B();
    for( … ){
        Processing C;
    }
}
```

加速器功能代码部分由子函数Func\_A和Func\_B，以及执行Processing C的for循环体共同组成。子函数可以在当前文件或其它代码文件中定义和实现。相关文件同样放在src目录下，就可以在执行make命令时自动添加到工程中。

完成C或C++代码的功能描述后，需要进行功能仿真。功能仿真的目的是在高级语言代码层面进行加速器功能正确性验证。功能仿真需要建立testbench。所有user\_accel函数以外的功能都可以纳入到testbench中，其中包括C、C++中的main函数。最简单的testbench如下：

```HLS
void main(){
    数据加载、预处理等；
    user_accel();
结果对比或打印输出;
}
```

testbench文件也是普通的C、C++代码文件，但必须放在src/tb目录下。Testbench中调用了user\_accel，并在调用之前和之后做一些相应的处理，比如user\_accel执行完后，对计算结果的正确性进行验证。

准备好testbench后，可以通过IDE上的C仿真按钮，或Shell模式下的make csim进行功能仿真。功能仿真时，首先会对所有代码进行编译。与传统的软件代码编译过程一样，编译过程会进行基本的语法检查，出错后会给出错误提示。编译完成后，自动开始执行功能仿真。用户在testbench中加入的结果比对或打印输出可以帮助判断加速器IP设计是否正确，并依此进行功能调试。

##### 4 面向加速器硬件IP实现的代码优化和编译指示

完成功能仿真后，下一步目标是将user\_accel代码生成硬件IP。HLS工具会自动完成C、C++代码到硬件逻辑的转换。用户需要做的是让代码符合高层综合的编码规范，并且在代码中添加必要的编译指示和接口约束，使HLS工具能按照用户的要求生成硬件IP接口和逻辑。此外，为了达到更高的性能，需要对访存、循环迭代等核心代码进行优化设计。

* **添加接口约束**

  当前版本的OpenHEC项目支撑包提供两个32位AXI总线接口，一个是32位的AXI4接口，支持burst类型数据传输；另一个是32位的AXI4 Lite接口，仅支持单个总线事务传输，主要用于性能要求不高的场景，如IP的运行时参数配置。下面是接口约束的一个简单示例。

  ```HLS
  void user_accel(TYPE1 param1, TYPE2 param2, …. , TYPE3 paramN){
      //加速器接口约束
      //HP inteface(axi4 master)
      #pragma HLS INTERFACE m_axi port = param1 offset = slave bundle = user_axi register
      #pragma HLS INTERFACE s_axilite port = param1 bundle = user_axi4lite register
      //GP interface(axi4lite slave)
      #pragma HLS INTERFACE s_axilite port = param2bundle = user_axi4lite register
      #pragma HLS INTERFACE s_axilite port =param3 bundle = user_axi4lite register
      #pragma HLS INTERFACE s_axilite port = param4 bundle = user_axi4lite register`
      ……
      #pragma HLS INTERFACE s_axilite port =paramN bundle = user_axi4lite register
      #pragma HLS INTERFACE s_axilite port = addr_reserved offset = 0xFFF0 bundle = user_axi4lite register
      #pragma HLS INTERFACE s_axilite port = return bundle = user_axi4lite register
      //加速器功能代码
  }
  ```

  每一条接口约束均以\#pragma关键词开头。OpenHEC项目支撑包预定义了两个AXI类的总线接口，分别为user\_axi和user\_axi4lite。前者是32位的AXI4类型接口，后者是32位的AXI4 Lite类型接口。

  第一部分是user\_axi接口约束，包含两条语句。语句\#pragma HLS INTERFACE m\_axi port = param1 offset = slave bundle = user\_axi register表示，参数param1被指定为m\_axi类型接口，接口名为user\_axi，用于加速器与内存之间的批量数据访问。访问内存的时候需要制定访存起始地址，语句\#pragma HLS INTERFACE s\_axilite port = param1 bundle = user\_axi4lite register表示，将param1基地址配置接口寄存器添加到user\_axi4lite接口中，运行时可以通过user\_axi4lite接口动态地对访存基地址进行配置。

  第二部分是user\_axi4lite接口约束。通过N-1条语句，将param2至paramN参数作为接口寄存器添加到user\_axi4lite接口，因此接口名均为user\_axi4lite。语句\#pragma HLS INTERFACE s\_axilite port = addr\_reserved offset = 0xFFF0 bundle = user\_axi4lite register的作用是指定地址边界，帮助HLS工具生成32位地址信号的总线接口。对于param2到paramN，用户可以在接口约束中手工指定各个接口寄存器的偏移地址，也可以交由工具自动分配。

  根据上面的接口约束示例，用户需要只根据自己的函数参数列表，修改param1到paramN的接口约束语句，定义满足自己加速器设计要求的IP接口。

  完成接口约束后，user\_accel函数的各个参数将被映射到对应的硬件接口。图中左侧为user\_accel函数，高层综合后生成右侧的user\_accel硬件IP模块。其中，蓝色文字为接口信号，包括时钟、复位等控制信号，以及两个AXI总线接口。user\_accel函数参数对应到user\_axi和user\_axi4lite两个AXI总线接口。红色文字部分为user\_axi4lite接口的接口寄存器列表。软件在运行时通过访问user\_axi4lite接口的寄存器来配置加速器IP。user\_axi接口由加速器内部使用，用于读写共享内存中的数据。

  关于接口约束的更详细说明请参考Xilinx官方手册《UG902: Vivado Design Suite User Guide High-Level Synthesis》

* **代码优化和编译指示**

  为了达到更好的性能，需要对访存、循环迭代等核心代码进行优化设计，并针对不同的硬件结构实现目标对代码设置编译指示。代码优化和编译指示设置的详细方法请参考Xilinx官方用户手册《UG902: Vivado Design Suite User Guide High-Level Synthesis》

##### 5 高层综合与IP生成

完成加速器设计后，在IDE模式下点击综合按钮，或在Shell模式下执行make csynth，执行高层综合。综合完成后，自动生成加速器硬件逻辑并打包成IP的形式。同时，HLS工具会自动生成report文件。report中给出了加速器IP的性能（吞吐率和延迟）、资源开销、接口定义等信息。用户可以根据report，调整代码优化策略和修改编译指示，生成符合用户需求的加速器IP。![](/assets/e4b161633923b4a088816fbe8f75e1fd.png)

在Shell环境下，用户通过可以在`RELAXSoC_FlyxSOM/solution1/impl/report`目录下找到report文件。

##### 6 硬件加速器的自动集成和实现

完成加速器IP的设计和实现后，如果在IDE模式下，请首先退出Vivado HLS工具界面，回到Shell模式。在`RELAXSoC_FlyxSOM`目录下，执行make命令，项目支撑包会自动负责将加速器IP和系统区接口逻辑进行系统集成，最后完成整个硬件加速器的实现。

完成加速器实现后，生成用于加速器的位流文件和接口驱动代码，分别保存在`RELAXSoC_FlyxSOM/impl/bin_file`和`RELAXSoC_FlyxSOM/impl/linux_driver`目录下。

