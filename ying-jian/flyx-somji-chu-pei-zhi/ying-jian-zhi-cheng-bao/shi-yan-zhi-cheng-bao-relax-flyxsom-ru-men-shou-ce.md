### RELAX\_FlyxSOM入门手册

#### 一、实验支撑包的目录结构

实验支撑包目录结构如下表所示。

| 一级目录 | 说明 |
| :--- | :---: |
| dcp/relax\_syn | OpenHEC平台预先生成好的实验支撑包dcp文件 |
| relax\_top | OpenHEC平台的顶层文件 |
| tcl | 工程项目进行综合与实现所需用到的tcl脚本文件 |

#### 二、实验支撑包**lab\_top**接口说明

实验顶层模块lab\_top中留出来的接口有FPGA自激励时钟、单步时钟、复位信号、通信IO输入输出信号、一片ROM接口和两片RAM读写接口。具体的信号接口定义如下表所示。

| 信号名 | IO方向 | 宽度 | 说明 |
| :--- | :---: | :---: | :---: |
| lab\_clk | 输入 | 1 | FPGA自激励时钟 |
| step\_clk | 输入 | 1 | 用户单步时钟 |
| lab\_reset | 输入 | 1 | 用户复位信号 |
| SW00 | 输入 | 1 | 通用IO输入开关 |
| SW01 | 输入 | 1 | 通用IO输入开关 |
| SW02 | 输入 | 1 | 通用IO输入开关 |
| SW03 | 输入 | 1 | 通用IO输入开关 |
| SW04 | 输入 | 1 | 通用IO输入开关 |
| SW05 | 输入 | 1 | 通用IO输入开关 |
| SW06 | 输入 | 1 | 通用IO输入开关 |
| SW07 | 输入 | 1 | 通用IO输入开关 |
| SW08 | 输入 | 1 | 通用IO输入开关 |
| SW09 | 输入 | 1 | 通用IO输入开关 |
| SW10 | 输入 | 1 | 通用IO输入开关 |
| SW11 | 输入 | 1 | 通用IO输入开关 |
| SW12 | 输入 | 1 | 通用IO输入开关 |
| SW13 | 输入 | 1 | 通用IO输入开关 |
| SW14 | 输入 | 1 | 通用IO输入开关 |
| SW15 | 输入 | 1 | 通用IO输入开关 |
| SW16 | 输入 | 1 | 通用IO输入开关 |
| SW17 | 输入 | 1 | 通用IO输入开关 |
| SW18 | 输入 | 1 | 通用IO输入开关 |
| SW19 | 输入 | 1 | 通用IO输入开关 |
| SW20 | 输入 | 1 | 通用IO输入开关 |
| SW21 | 输入 | 1 | 通用IO输入开关 |
| SW22 | 输入 | 1 | 通用IO输入开关 |
| SW23 | 输入 | 1 | 通用IO输入开关 |
| SW24 | 输入 | 1 | 通用IO输入开关 |
| SW25 | 输入 | 1 | 通用IO输入开关 |
| SW26 | 输入 | 1 | 通用IO输入开关 |
| SW27 | 输入 | 1 | 通用IO输入开关 |
| SW28 | 输入 | 1 | 通用IO输入开关 |
| SW29 | 输入 | 1 | 通用IO输入开关 |
| SW30 | 输入 | 1 | 通用IO输入开关 |
| SW31 | 输入 | 1 | 通用IO输入开关 |
| LED00 | 输出 | 1 | 通用IO输出灯 |
| LED01 | 输出 | 1 | 通用IO输出灯 |
| LED02 | 输出 | 1 | 通用IO输出灯 |
| LED03 | 输出 | 1 | 通用IO输出灯 |
| LED04 | 输出 | 1 | 通用IO输出灯 |
| LED05 | 输出 | 1 | 通用IO输出灯 |
| LED06 | 输出 | 1 | 通用IO输出灯 |
| LED07 | 输出 | 1 | 通用IO输出灯 |
| LED08 | 输出 | 1 | 通用IO输出灯 |
| LED09 | 输出 | 1 | 通用IO输出灯 |
| LED10 | 输出 | 1 | 通用IO输出灯 |
| LED11 | 输出 | 1 | 通用IO输出灯 |
| LED12 | 输出 | 1 | 通用IO输出灯 |
| LED13 | 输出 | 1 | 通用IO输出灯 |
| LED14 | 输出 | 1 | 通用IO输出灯 |
| LED15 | 输出 | 1 | 通用IO输出灯 |
| LED16 | 输出 | 1 | 通用IO输出灯 |
| LED17 | 输出 | 1 | 通用IO输出灯 |
| LED18 | 输出 | 1 | 通用IO输出灯 |
| LED19 | 输出 | 1 | 通用IO输出灯 |
| LED20 | 输出 | 1 | 通用IO输出灯 |
| LED21 | 输出 | 1 | 通用IO输出灯 |
| LED22 | 输出 | 1 | 通用IO输出灯 |
| LED23 | 输出 | 1 | 通用IO输出灯 |
| LED24 | 输出 | 1 | 通用IO输出灯 |
| LED25 | 输出 | 1 | 通用IO输出灯 |
| LED26 | 输出 | 1 | 通用IO输出灯 |
| LED27 | 输出 | 1 | 通用IO输出灯 |
| LED28 | 输出 | 1 | 通用IO输出灯 |
| LED29 | 输出 | 1 | 通用IO输出灯 |
| LED30 | 输出 | 1 | 通用IO输出灯 |
| LED31 | 输出 | 1 | 通用IO输出灯 |
| R8IN0 | 输入 | 8 | 通用8-bit IO输入 |
| R8IN1 | 输入 | 8 | 通用8-bit IO输入 |
| R8IN2 | 输入 | 8 | 通用8-bit IO输入 |
| R8IN3 | 输入 | 8 | 通用8-bit IO输入 |
| R8IN4 | 输入 | 8 | 通用8-bit IO输入 |
| R8IN5 | 输入 | 8 | 通用8-bit IO输入 |
| R8IN6 | 输入 | 8 | 通用8-bit IO输入 |
| R8IN7 | 输入 | 8 | 通用8-bit IO输入 |
| R8OUT0 | 输出 | 8 | 通用8-bit IO输出 |
| R8OUT1 | 输出 | 8 | 通用8-bit IO输出 |
| R8OUT2 | 输出 | 8 | 通用8-bit IO输出 |
| R8OUT3 | 输出 | 8 | 通用8-bit IO输出 |
| R8OUT4 | 输出 | 8 | 通用8-bit IO输出 |
| R8OUT5 | 输出 | 8 | 通用8-bit IO输出 |
| R8OUT6 | 输出 | 8 | 通用8-bit IO输出 |
| R8OUT7 | 输出 | 8 | 通用8-bit IO输出 |
| R16IN0 | 输入 | 16 | 通用16-bit IO输入 |
| R16IN1 | 输入 | 16 | 通用16-bit IO输入 |
| R16IN2 | 输入 | 16 | 通用16-bit IO输入 |
| R16IN3 | 输入 | 16 | 通用16-bit IO输入 |
| R16IN4 | 输入 | 16 | 通用16-bit IO输入 |
| R16IN5 | 输入 | 16 | 通用16-bit IO输入 |
| R16IN6 | 输入 | 16 | 通用16-bit IO输入 |
| R16IN7 | 输入 | 16 | 通用16-bit IO输入 |
| R16OUT0 | 输出 | 16 | 通用16-bit IO输出 |
| R16OUT1 | 输出 | 16 | 通用16-bit IO输出 |
| R16OUT2 | 输出 | 16 | 通用16-bit IO输出 |
| R16OUT3 | 输出 | 16 | 通用16-bit IO输出 |
| R16OUT4 | 输出 | 16 | 通用16-bit IO输出 |
| R16OUT5 | 输出 | 16 | 通用16-bit IO输出 |
| R16OUT6 | 输出 | 16 | 通用16-bit IO输出 |
| R16OUT7 | 输出 | 16 | 通用16-bit IO输出 |
| R32IN0 | 输入 | 32 | 通用32-bit IO输入 |
| R32IN1 | 输入 | 32 | 通用32-bit IO输入 |
| R32IN2 | 输入 | 32 | 通用32-bit IO输入 |
| R32IN3 | 输入 | 32 | 通用32-bit IO输入 |
| R32IN4 | 输入 | 32 | 通用32-bit IO输入 |
| R32IN5 | 输入 | 32 | 通用32-bit IO输入 |
| R32IN6 | 输入 | 32 | 通用32-bit IO输入 |
| R32IN7 | 输入 | 32 | 通用32-bit IO输入 |
| R32OUT0 | 输出 | 32 | 通用32-bit IO输出 |
| R32OUT1 | 输出 | 32 | 通用32-bit IO输出 |
| R32OUT2 | 输出 | 32 | 通用32-bit IO输出 |
| R32OUT3 | 输出 | 32 | 通用32-bit IO输出 |
| R32OUT4 | 输出 | 32 | 通用32-bit IO输出 |
| R32OUT5 | 输出 | 32 | 通用32-bit IO输出 |
| R32OUT6 | 输出 | 32 | 通用32-bit IO输出 |
| R32OUT7 | 输出 | 32 | 通用32-bit IO输出 |
| inst\_addr | 输出 | 32 | 片上指令ROM的读地址接口 |
| inst\_data | 输入 | 32 | 片上指令ROM的读数据接口 |
| ram\_clk | 输出 | 1 | RAM的工作时钟 |
| ram\_rst | 输出 | 1 | RAM的复位（高电平有效） |
| ram0\_raddr | 输出 | 32 | RAM0的读地址接口 |
| ram0\_rdata | 输入 | 32 | RAM0的读数据接口 |
| ram0\_ren | 输出 | 1 | RAM0的读使能信号（高电平有效） |
| ram0\_rvalid | 输入 | 1 | RAM0的读有效信号（高电平有效） |
| ram0\_waddr | 输出 | 32 | RAM0的写地址接口 |
| ram0\_wdata | 输出 | 32 | RAM0的写数据接口 |
| ram0\_wen | 输出 | 1 | RAM0的写使能信号（高电平有效） |
| ram0\_sel | 输出 | 4 | RAM0的写字节选通信号\(高电平有效\) |
| ram0\_wready | 输入 | 1 | RAM0的写准备信号（高电平有效） |
| ram1\_raddr | 输出 | 32 | RAM1的读地址接口 |
| ram1\_rdata | 输入 | 32 | RAM1的读数据接口 |
| ram1\_ren | 输出 | 1 | RAM1的读使能信号（高电平有效） |
| ram1\_rvalid | 输入 | 1 | RAM1的读有效信号（高电平有效） |
| ram1\_waddr | 输出 | 32 | RAM1的写地址接口 |
| ram1\_wdata | 输出 | 32 | RAM1的写数据接口 |
| ram1\_wen | 输出 | 1 | RAM1的写使能信号（高电平有效） |
| ram1\_sel | 输出 | 4 | RAM1的写字节选通信号\(高电平有效\) |
| ram1\_wready | 输入 | 1 | RAM1的写准备信号（高电平有效） |

---

#### 三、实验支撑包**lab\_top.v**源码解析

1. module lab\_top区域： 这一块定义IO管脚的信号，用户不能随意修改。

   ```verilog
    module lab_top
    (
        //         Clock   20MHz    
        input    wire            lab_clk,

        // Step Clock Signals 
        input    wire            step_clk,

        /*          Reset  Signals     
         *        HIGH_     ACTIVE OR LOW_ACTIVE
         *          Deterimined by WEB Optition
         */
        input    wire            lab_reset,

        /*
         *  SW 
         * input Signals  
         */
        input    wire            SW00,
        input    wire            SW01,
        input    wire            SW02,
        input    wire            SW03,
        input    wire            SW04,
        input    wire            SW05,
        input    wire            SW06,
        input    wire            SW07,
        input    wire            SW08,
        input    wire            SW09,
        input    wire            SW10,
        input    wire            SW11,
        input    wire            SW12,
        input    wire            SW13,
        input    wire            SW14,
        input    wire            SW15,
        input    wire            SW16,
        input    wire            SW17,
        input    wire            SW18,
        input    wire            SW19,
        input    wire            SW20,
        input    wire            SW21,
        input    wire            SW22,
        input    wire            SW23,
        input    wire            SW24,
        input    wire            SW25,
        input    wire            SW26,
        input    wire            SW27,
        input    wire            SW28,
        input    wire            SW29,
        input    wire            SW30,
        input    wire            SW31,

        /*
         *   LED 
         * output Signals  
         */
        output    wire            LED00,
        output    wire            LED01,
        output    wire            LED02,
        output    wire            LED03,
        output    wire            LED04,
        output    wire            LED05,
        output    wire            LED06,
        output    wire            LED07,
        output    wire            LED08,
        output    wire            LED09,
        output    wire            LED10,
        output    wire            LED11,
        output    wire            LED12,
        output    wire            LED13,
        output    wire            LED14,
        output    wire            LED15,
        output    wire            LED16,
        output    wire            LED17,
        output    wire            LED18,
        output    wire            LED19,
        output    wire            LED20,
        output    wire            LED21,
        output    wire            LED22,
        output    wire            LED23,
        output    wire            LED24,
        output    wire            LED25,
        output    wire            LED26,
        output    wire            LED27,
        output    wire            LED28,
        output    wire            LED29,
        output    wire            LED30,
        output    wire            LED31,

        /*
         *   Register 8-bit 
         *      Input    Signals
         */
        input    wire    [ 7: 0]    R8IN0,
        input    wire    [ 7: 0]    R8IN1,
        input    wire    [ 7: 0]    R8IN2,
        input    wire    [ 7: 0]    R8IN3,
        input    wire    [ 7: 0]    R8IN4,
        input    wire    [ 7: 0]    R8IN5,
        input    wire    [ 7: 0]    R8IN6,
        input    wire    [ 7: 0]    R8IN7,

        /*
         *   Register 8-bit 
         *      Output    Signals
         */    
        output    wire    [ 7: 0]    R8OUT0,
        output    wire    [ 7: 0]    R8OUT1,
        output    wire    [ 7: 0]    R8OUT2,
        output    wire    [ 7: 0]    R8OUT3,
        output    wire    [ 7: 0]    R8OUT4,
        output    wire    [ 7: 0]    R8OUT5,
        output    wire    [ 7: 0]    R8OUT6,
        output    wire    [ 7: 0]    R8OUT7,

        /*
         *   Register 16-bit 
         *      Input    Signals
         */
        input    wire    [15: 0]    R16IN0,
        input    wire    [15: 0]    R16IN1,
        input    wire    [15: 0]    R16IN2,
        input    wire    [15: 0]    R16IN3,
        input    wire    [15: 0]    R16IN4,
        input    wire    [15: 0]    R16IN5,
        input    wire    [15: 0]    R16IN6,
        input    wire    [15: 0]    R16IN7,

        /*
         *   Register 16-bit 
         *      Output    Signals
         */    
        output    wire    [15: 0]    R16OUT0,
        output    wire    [15: 0]    R16OUT1,
        output    wire    [15: 0]    R16OUT2,
        output    wire    [15: 0]    R16OUT3,
        output    wire    [15: 0]    R16OUT4,
        output    wire    [15: 0]    R16OUT5,
        output    wire    [15: 0]    R16OUT6,
        output    wire    [15: 0]    R16OUT7,

        /*
        *   Register 32-bit 
        *      Input    Signals
        */
        input    wire    [31: 0]    R32IN0,
        input    wire    [31: 0]    R32IN1,
        input    wire    [31: 0]    R32IN2,
        input    wire    [31: 0]    R32IN3,
        input    wire    [31: 0]    R32IN4,
        input    wire    [31: 0]    R32IN5,
        input    wire    [31: 0]    R32IN6,
        input    wire    [31: 0]    R32IN7,

        /*
         *   Register 32-bit 
         *      Output    Signals
         */    
        output    wire    [31: 0]    R32OUT0,
        output    wire    [31: 0]    R32OUT1,
        output    wire    [31: 0]    R32OUT2,
        output    wire    [31: 0]    R32OUT3,
        output    wire    [31: 0]    R32OUT4,
        output    wire    [31: 0]    R32OUT5,
        output    wire    [31: 0]    R32OUT6,
        output    wire    [31: 0]    R32OUT7,    

        /*
         *   Instruction ROM Interface 
         *
         *   32-bit Address     
         *      BaseAddr = 0x40000000
         *     HighAddr = 0x40000800
         *   Size     =  2K
         */
        output    wire    [31: 0]    inst_addr,
        input    wire    [31: 0]    inst_data,

        /*
         *  Mapped RAM0  Interface  
         *
         *  32-bit Address
         *  BaseAddr = 0x00000000
         *    HighAddr = 0x03ffffff
         *    Range = 64M
         */
         output wire                ram_clk,
         output wire                ram_rst,         
         output    wire    [31: 0]        ram0_raddr,
         input    wire    [31: 0]        ram0_rdata,
         output    wire                ram0_ren,
         input    wire                ram0_rvalid,
         output    wire    [31: 0]     ram0_waddr,
         output    wire    [31: 0]     ram0_wdata,
         output    wire                ram0_wen,
         output    wire    [3 : 0]        ram0_sel,
         input    wire                ram0_wready,

        /*
         *  Mapped RAM1  Interface  
         *
         *  32-bit Address
         *  BaseAddr = 0x04000000
         *    HighAddr = 0x07ffffff
         *    Range = 64M
         */ 
         output    wire    [31: 0]        ram1_raddr,
         input    wire    [31: 0]        ram1_rdata,
         output    wire                ram1_ren,
         input    wire                ram1_rvalid,
         output    wire    [31: 0]     ram1_waddr,
         output    wire    [31: 0]     ram1_wdata,
         output    wire                ram1_wen,
         output    wire    [3 : 0]        ram1_sel,
         input    wire                ram1_wready    
    );
   ```

2. 存储器接口系统默认赋值区域： 系统默认存储器初值，用户如若用到相应的接口信号，需要注释对应的赋值语句。

   ```verilog
        //RAM0 Read Interface
        assign    ram0_ren  = 1'b0;
        assign    ram0_raddr = 32'b0;    

        //RAM0 Write Interface
        assign    ram0_waddr = 32'b0;
        assign    ram0_wen = 1'b0;
        assign    ram0_sel = 4'b0000;
        assign    ram0_wdata = 32'b0;

        //RAM1 Read Interface
        assign    ram1_ren = 1'b0;
        assign    ram1_raddr = 32'b0;

        //RAM1 Write Interface
        assign    ram1_waddr = 32'b0;
        assign    ram1_wen = 1'b0;
        assign    ram1_sel = 4'b0000;
        assign    ram1_wdata = 32'b0;

        //RAM CLK AND RESET
        assign ram_clk = step_clk;
        assign ram_rst = 1'b1;
   ```

3. IO接口系统默认绑定区域： 系统默认管脚绑定区域，若用到相应的接口输出信号，需要注释对应的赋值语句。

   ```verilog
        /*
        **    SW LED
        **
        */
        assign    LED00 = SW00;
        assign    LED01 = SW01;
        assign    LED02 = SW02;
        assign    LED03 = SW03;
        assign    LED04 = SW04;
        assign    LED05 = SW05;
        assign    LED06 = SW06;
        assign    LED07 = SW07;
        assign    LED08 = SW08;
        assign    LED09 = SW09;
        assign    LED10 = SW10;
        assign    LED11 = SW11;
        assign    LED12 = SW12;
        assign    LED13 = SW13;
        assign    LED14 = SW14;
        assign    LED15 = SW15;
        assign    LED16 = SW16;
        assign    LED17 = SW17;
        assign    LED18 = SW18;
        assign    LED19 = SW19;
        assign    LED20 = SW20;
        assign    LED21 = SW21;
        assign    LED22 = SW22;
        assign    LED23 = SW23;
        assign    LED24 = SW24;
        assign    LED25 = SW25;
        assign    LED26 = SW26;
        assign    LED27 = SW27;
        assign    LED28 = SW28;
        assign    LED29 = SW29;
        assign    LED30 = SW30;
        assign    LED31 = SW31;
        /*
        **    8-bit Register 
        **
        */    
        assign R8OUT0 = R8IN0;
        assign R8OUT1 = R8IN1;
        assign R8OUT2 = R8IN2;
        assign R8OUT3 = R8IN3;
        assign R8OUT4 = R8IN4;
        assign R8OUT5 = R8IN5;
        assign R8OUT6 = R8IN6;
        assign R8OUT7 = R8IN7;
        /*
        **    16-bit Register 
        **
        */
        assign R16OUT0 = R16IN0;
        assign R16OUT1 = R16IN1;
        assign R16OUT2 = R16IN2;
        assign R16OUT3 = R16IN3;
        assign R16OUT4 = R16IN4;
        assign R16OUT5 = R16IN5;
        assign R16OUT6 = R16IN6;
        assign R16OUT7 = R16IN7;
        /*
        **    32-bit Register 
        **
        */
        assign R32OUT0 = R32IN0;
        assign R32OUT1 = R32IN1;
        assign R32OUT2 = R32IN2;
        assign R32OUT3 = R32IN3;
        assign R32OUT4 = R32IN4;
        assign R32OUT5 = R32IN5;
        assign R32OUT6 = R32IN6;
        assign R32OUT7 = R32IN7;
   ```

4. 用户自定义顶层module实例化区域

   ```verilog
        user_wrapper_top user_wrapper_top_uut
        (

        );
   ```



