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

   支撑包[**RELAX\_FlyxSOM\_LED7SEG\_SRAM实验支撑包**](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-sram-ru-men-shou-ce.html) 已经预先完成了用户逻辑与实验支撑包的绑定，在系统注释区域注释掉用户逻辑区绑定的IO输出端口及系统预留用户调用模块，参考代码如下。

   ```verilog
    reg                      reg_sram_user_nce;
    reg                      reg_sram_user_noe;
    reg                      reg_sram_user_nwe;
    reg                      reg_sram_user_nlb;
    reg                      reg_sram_user_nub;
    reg        [18:0]        reg_sram_user_addr;
    reg        [15:0]        reg_sram_user_wrdata;
    reg        [15:0]        reg_R16OUT0;
    assign FlyxIO_sram_user_nce = reg_sram_user_nce;
    assign FlyxIO_sram_user_noe = reg_sram_user_noe;
    assign FlyxIO_sram_user_nwe = reg_sram_user_nwe;
    assign FlyxIO_sram_user_nlb = reg_sram_user_nlb;
    assign FlyxIO_sram_user_nub = reg_sram_user_nub;
    assign FlyxIO_sram_user_addr = reg_sram_user_addr;
    assign FlyxIO_sram_user_wrdata = reg_sram_user_wrdata;
    assign R16OUT0 = reg_R16OUT0;
    always @ (posedge step_clk)
    begin
        if(lab_reset)
            begin
                reg_sram_user_nce <= 1'b1;
                reg_sram_user_noe <= 1'b1;
                reg_sram_user_nwe <= 1'b1;
                reg_sram_user_nlb <= 1'b1;
                reg_sram_user_nub <= 1'b1;
                reg_sram_user_addr <= 19'b0;
                reg_sram_user_wrdata <= 16'h0000;
                reg_R16OUT0 <= 16'h0000;
            end
        else
            begin
                reg_sram_user_nce <= SW10;
                reg_sram_user_noe <= SW11;
                reg_sram_user_nwe <= SW12;
                reg_sram_user_nlb <= SW13;
                reg_sram_user_nub <= SW14;
                reg_sram_user_addr <= R32IN0[18:0];
                reg_sram_user_wrdata <= R16IN0;
                reg_R16OUT0 <= FlyxIO_sram_user_rddata;
            end    
    end

     //assign R16OUT0 = R16IN0;
    /*user_wrapper_top user_wrapper_top_uut
    (
    );*/
   ```

4. **综合与实现**

   OpenHEC实验支撑包中提供综合实现的tcl脚本，可以自动完成整个系统的综合，最终生成比特流文件。点击 **Tools/Run Tcl Script**，选择文件夹**oLib/RELAX\_FlyxSOM\_LED7SEG\_SRAM/tcl **下的**relax\_syn\_imp\_flow.tcl**文件，点击OK，自动运行综合与实现，等待生成位流。比特流文件存放在桌面文件夹**proj\_ip/sram\_proj**下。![](/assets/sram_genbit.png)

5. **完成开发**

   拷贝桌面文件夹**proj\_ip/sram\_proj**下的位流文件**sram\_proj.bit** 到oDisk目录，完成开发。![](/assets/sram_finish.png)

#### 三、使用FPGA

完成了FPGA的开发后，用户既可以在OpenHEC部署在云端的FPGA硬件上验证数码管的bit文件了。

1. ##### 配置比特流到FPGA

   点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中刚刚拷贝的**sram\_proj.bit**位流，同时选择纯FPGA模式的配置方式，点击配置即可以。配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。

2. ##### 写存储

   位流配置成功后，点击**高级设置**中的**SRAM访问设置**，选择**打开WEB模式访问SRAM存储**，返回成功信息后；然后点击写存储，展开写存储操作页面。

   第一步：选择SRAM的基地址0x5000000，WEB下访问存储的地址范围如下表所示。

   | 存储类型 | 数据位宽 | WEB访问基地址 | WEB访问终地址 | 用户逻辑区基地址 | 用户逻辑区终地址 | 大小 | 说明 |
   | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
   | ROM | 32-bit | 0x40000000 | 0x400007ff | 0x00000000 | 0x000007ff | 2KB |  |
   | RAM0 | 32-bit | 0x00000000 | 0x03ffffff | 0x00000000 | 0x03ffffff | 64MB | 独立编址 |
   | RAM1 | 32-bit | 0x04000000 | 0x07ffffff | 0x00000000 | 0x03ffffff | 64MB | 独立编址 |
   | RAM0 | 32-bit | 0x00000000 | 0x03ffffff | 0x00000000 | 0x07ffffff | 128MB | 统一编址 |
   | RAM1 | 32-bit | 0x04000000 | 0x07ffffff | 0x00000000 | 0x07ffffff | 128MB | 统一编址 |
   | SRAM | 16-bit | 0x50000000 | 0x50ffffff | 0x00000000 | 0x00ffffff | 16MB |  |

   第二步：增加值或者导入写入的文件，导入文件的格式为二进制文件编码；从ROM基地址依次写入1, 2, … , f的值。![](/assets/writeram0002.png)

   第三步： 点击发送数据，此时才会开始把准备好的数据，写入到教学板的SRAM中。

3. ##### 读存储

   ##### 点击展开读存储，展开读存储操作页面。

   ##### 第一步：选择SRAM的基地址0x50000000。

   ##### 第二步：输入展示地址个数为30。

   ##### 第三步：点击**查看结果**，在下方表中可以SRAM中的数据，也可以生成文件导出。
4. ##### IO实时监控

   ##### 

##### 



