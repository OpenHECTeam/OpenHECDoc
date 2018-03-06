### RELAX\_FlyxSOM\_LED7SEG\_SRAM入门手册


#### 一、实验支撑包的目录结构
实验支撑包目录结构如下表所示。

| 一级目录 | 说明 |
| :--- | :---: |
| dcp/relax\_syn | OpenHEC平台预先生成好的实验支撑包dcp文件 |
| relax\_top | OpenHEC平台的顶层文件 |
| tcl | 工程项目进行综合与实现所需用到的tcl脚本文件 |


#### 二、实验支撑包lab_top接口说明

实验支撑包`RELAX_FlyxSOM`实验顶层模块lab_top中留出来的接口有FPGA自激励时钟、单步时钟、复位信号、通信IO输入输出信号、一片ROM接口和两片RAM读写接口。实验支撑包`RELAX_FlyxSOM_LED7SEG_SRAM`新增接口有码数码管、LED点阵和SRAM存储接口。具体的信号接口定义如下表所示。

	
|  信号名   |  IO方向  | 宽度  |  说明  |
|  :----   |  :--:   | :--:  |  :--:  |
| lab_clk  |  输入	 |  1    |  FPGA自激励时钟  |
| step_clk |  输入    |  1    |  用户单步时钟    |
| lab_reset|  输入    |  1    |  用户复位信号  |
| SW00     |  输入    |  1    |  通用IO输入开关   |
| SW01     |  输入    |  1    |  通用IO输入开关   |
| SW02     |  输入    |  1    |  通用IO输入开关   |
| SW03     |  输入    |  1    |  通用IO输入开关   |
| SW04     |  输入    |  1    |  通用IO输入开关   |
| SW05     |  输入    |  1    |  通用IO输入开关   |
| SW06     |  输入    |  1    |  通用IO输入开关   |
| SW07     |  输入    |  1    |  通用IO输入开关   |
| SW08     |  输入    |  1    |  通用IO输入开关   |
| SW09     |  输入    |  1    |  通用IO输入开关   |
| SW10     |  输入    |  1    |  通用IO输入开关   |
| SW11     |  输入    |  1    |  通用IO输入开关   |
| SW12     |  输入    |  1    |  通用IO输入开关   |
| SW13     |  输入    |  1    |  通用IO输入开关   |
| SW14     |  输入    |  1    |  通用IO输入开关   |
| SW15     |  输入    |  1    |  通用IO输入开关   |
| SW16     |  输入    |  1    |  通用IO输入开关   |
| SW17     |  输入    |  1    |  通用IO输入开关   |
| SW18     |  输入    |  1    |  通用IO输入开关   |
| SW19     |  输入    |  1    |  通用IO输入开关   |
| SW20     |  输入    |  1    |  通用IO输入开关   |
| SW21     |  输入    |  1    |  通用IO输入开关   |
| SW22     |  输入    |  1    |  通用IO输入开关   |
| SW23     |  输入    |  1    |  通用IO输入开关   |
| SW24     |  输入    |  1    |  通用IO输入开关   |
| SW25     |  输入    |  1    |  通用IO输入开关   |
| SW26     |  输入    |  1    |  通用IO输入开关   |
| SW27     |  输入    |  1    |  通用IO输入开关   |
| SW28     |  输入    |  1    |  通用IO输入开关   |
| SW29     |  输入    |  1    |  通用IO输入开关   |
| SW30     |  输入    |  1    |  通用IO输入开关   |
| SW31     |  输入    |  1    |  通用IO输入开关   |
| LED00    |  输出    |  1    |  通用IO输出灯    |
| LED01    |  输出    |  1    |  通用IO输出灯    |
| LED02    |  输出    |  1    |  通用IO输出灯    |
| LED03    |  输出    |  1    |  通用IO输出灯    |
| LED04    |  输出    |  1    |  通用IO输出灯    |
| LED05    |  输出    |  1    |  通用IO输出灯    |
| LED06    |  输出    |  1    |  通用IO输出灯    |
| LED07    |  输出    |  1    |  通用IO输出灯    |
| LED08    |  输出    |  1    |  通用IO输出灯    |
| LED09    |  输出    |  1    |  通用IO输出灯    |
| LED10    |  输出    |  1    |  通用IO输出灯    |
| LED11    |  输出    |  1    |  通用IO输出灯    |
| LED12    |  输出    |  1    |  通用IO输出灯    |
| LED13    |  输出    |  1    |  通用IO输出灯    |
| LED14    |  输出    |  1    |  通用IO输出灯    |
| LED15    |  输出    |  1    |  通用IO输出灯    |
| LED16    |  输出    |  1    |  通用IO输出灯    |
| LED17    |  输出    |  1    |  通用IO输出灯    |
| LED18    |  输出    |  1    |  通用IO输出灯    |
| LED19    |  输出    |  1    |  通用IO输出灯    |
| LED20    |  输出    |  1    |  通用IO输出灯    |
| LED21    |  输出    |  1    |  通用IO输出灯    |
| LED22    |  输出    |  1    |  通用IO输出灯    |
| LED23    |  输出    |  1    |  通用IO输出灯    |
| LED24    |  输出    |  1    |  通用IO输出灯    |
| LED25    |  输出    |  1    |  通用IO输出灯    |
| LED26    |  输出    |  1    |  通用IO输出灯    |
| LED27    |  输出    |  1    |  通用IO输出灯    |
| LED28    |  输出    |  1    |  通用IO输出灯    |
| LED29    |  输出    |  1    |  通用IO输出灯    |
| LED30    |  输出    |  1    |  通用IO输出灯    |
| LED31    |  输出    |  1    |  通用IO输出灯    |
| R8IN0    |  输入    |  8    |  通用8-bit IO输入 |
| R8IN1    |  输入    |  8    |  通用8-bit IO输入 |
| R8IN2    |  输入    |  8    |  通用8-bit IO输入 |
| R8IN3    |  输入    |  8    |  通用8-bit IO输入 |
| R8IN4    |  输入    |  8    |  通用8-bit IO输入 |
| R8IN5    |  输入    |  8    |  通用8-bit IO输入 |
| R8IN6    |  输入    |  8    |  通用8-bit IO输入 |
| R8IN7    |  输入    |  8    |  通用8-bit IO输入 |
| R8OUT0   |  输出    |  8    |  通用8-bit IO输出 |
| R8OUT1   |  输出    |  8    |  通用8-bit IO输出 |
| R8OUT2   |  输出    |  8    |  通用8-bit IO输出 |
| R8OUT3   |  输出    |  8    |  通用8-bit IO输出 |
| R8OUT4   |  输出    |  8    |  通用8-bit IO输出 |
| R8OUT5   |  输出    |  8    |  通用8-bit IO输出 |
| R8OUT6   |  输出    |  8    |  通用8-bit IO输出 |
| R8OUT7   |  输出    |  8    |  通用8-bit IO输出 |
| R16IN0   |  输入    |  16    |  通用16-bit IO输入 |
| R16IN1   |  输入    |  16    |  通用16-bit IO输入 |
| R16IN2   |  输入    |  16    |  通用16-bit IO输入 |
| R16IN3   |  输入    |  16    |  通用16-bit IO输入 |
| R16IN4   |  输入    |  16    |  通用16-bit IO输入 |
| R16IN5   |  输入    |  16    |  通用16-bit IO输入 |
| R16IN6   |  输入    |  16    |  通用16-bit IO输入 |
| R16IN7   |  输入    |  16    |  通用16-bit IO输入 |
| R16OUT0  |  输出    |  16    |  通用16-bit IO输出 |
| R16OUT1  |  输出    |  16    |  通用16-bit IO输出 |
| R16OUT2  |  输出    |  16    |  通用16-bit IO输出 |
| R16OUT3  |  输出    |  16    |  通用16-bit IO输出 |
| R16OUT4  |  输出    |  16    |  通用16-bit IO输出 |
| R16OUT5  |  输出    |  16    |  通用16-bit IO输出 |
| R16OUT6  |  输出    |  16    |  通用16-bit IO输出 |
| R16OUT7  |  输出    |  16    |  通用16-bit IO输出 |
| R32IN0    |  输入    |  32    |  通用32-bit IO输入 |
| R32IN1    |  输入    |  32    |  通用32-bit IO输入 |
| R32IN2    |  输入    |  32    |  通用32-bit IO输入 |
| R32IN3    |  输入    |  32    |  通用32-bit IO输入 |
| R32IN4    |  输入    |  32    |  通用32-bit IO输入 |
| R32IN5    |  输入    |  32    |  通用32-bit IO输入 |
| R32IN6    |  输入    |  32    |  通用32-bit IO输入 |
| R32IN7    |  输入    |  32    |  通用32-bit IO输入 |
| R32OUT0   |  输出    |  32    |  通用32-bit IO输出 |
| R32OUT1   |  输出    |  32    |  通用32-bit IO输出 |
| R32OUT2   |  输出    |  32    |  通用32-bit IO输出 |
| R32OUT3   |  输出    |  32    |  通用32-bit IO输出 |
| R32OUT4   |  输出    |  32    |  通用32-bit IO输出 |
| R32OUT5   |  输出    |  32    |  通用32-bit IO输出 |
| R32OUT6   |  输出    |  32    |  通用32-bit IO输出 |
| R32OUT7   |  输出    |  32    |  通用32-bit IO输出 |
| inst_addr |  输出    |  32    |  片上指令ROM的读地址接口 |
| inst_data |  输入    |  32    |  片上指令ROM的读数据接口 |
| ram_clk    |  输出    |  1    |  RAM的工作时钟 		  |
| ram_rst    |  输出    |  1    |  RAM的复位（高电平有效） |
| ram0_raddr |  输出    |  32    |  RAM0的读地址接口	   |
| ram0_rdata |  输入	   |  32    |  RAM0的读数据接口      |
| ram0_ren   |  输出    |  1    |  RAM0的读使能信号（高电平有效） |
| ram0_rvalid|  输入    |  1    |  RAM0的读有效信号（高电平有效） |
| ram0_waddr |  输出    |  32    | RAM0的写地址接口	  |
| ram0_wdata |  输出    |  32    | RAM0的写数据接口      |
| ram0_wen   |  输出    |  1    |  RAM0的写使能信号（高电平有效）|
| ram0_sel   |  输出    |  4    |  RAM0的写字节选通信号(高电平有效)|
| ram0_wready|  输入    |  1    |  RAM0的写准备信号（高电平有效） |
| ram1_raddr |  输出    |  32    |  RAM1的读地址接口	   |
| ram1_rdata |  输入	   |  32    |  RAM1的读数据接口      |
| ram1_ren   |  输出    |  1    |  RAM1的读使能信号（高电平有效） |
| ram1_rvalid|  输入    |  1    |  RAM1的读有效信号（高电平有效） |
| ram1_waddr |  输出    |  32    | RAM1的写地址接口	  |
| ram1_wdata |  输出    |  32    | RAM1的写数据接口      |
| ram1_wen   |  输出    |  1    |  RAM1的写使能信号（高电平有效）|
| ram1_sel   |  输出    |  4    |  RAM1的写字节选通信号(高电平有效)|
| ram1_wready|  输入    |  1    |  RAM1的写准备信号（高电平有效） |
| FlyxIO_seven_segment_a    |  输出    |  1    |  7段码管脚A     |
| FlyxIO_seven_segment_b    |  输出    |  1    |  7段码管脚B     |
| FlyxIO_seven_segment_c    |  输出    |  1    |  7段码管脚C      |
| FlyxIO_seven_segment_d    |  输出    |  1    |  7段码管脚D      |
| FlyxIO_seven_segment_e    |  输出    |  1    |  7段码管脚E      |
| FlyxIO_seven_segment_f    |  输出    |  1    |  7段码管脚F      |
| FlyxIO_seven_segment_g    |  输出    |  1    |  7段码管脚G      |
| FlyxIO_seven_segment_dp   |  输出    |  1    |  7段码管脚DP     |
| FlyxIO_seven_segment_dig1 |  输出    |  1    |  7段码管脚DIG1   |
| FlyxIO_seven_segment_dig2 |  输出    |  1    |  7段码管脚DIG2   |
| FlyxIO_led_array_row    |  输出    |  8    |  8x8LED点阵行   |
| FlyxIO_led_array_col    |  输出    |  8    |  8x8LED点阵列    |
| FlyxIO_sram_user_nce |  输出    |  1    |  SRAM芯片有效使能   |
| FlyxIO_sram_user_noe |  输出    |  1    |  SRAM芯片输出时能   |
| FlyxIO_sram_user_nwe |  输出    |  1    |  SRAM芯片写时能     |
| FlyxIO_sram_user_nlb |  输出    |  1    |  SRAM芯片低8位选通  |
| FlyxIO_sram_user_nub |  输出    |  1    |  SRAM芯片高8位选通  |
| FlyxIO_sram_user_addr|  输出    |  19    |  SRAM芯片地址线   |
| FlyxIO_sram_user_wrdata |  输出    |  16   |  SRAM写数据线   |
| FlyxIO_sram_user_rddata |  输入    |  16   |  SRAM读数据线   |

---

#### 三、实验支撑包lab_top.v源码解析
	
1. module lab_top区域： 这一块定义IO管脚的信号，用户不能随意修改。

	``` verilog
	module lab_top
	(
		// 		Clock   20MHz	
		input	wire			lab_clk,

		// Step Clock Signals 
		input	wire			step_clk,
	
		/* 	 	Reset  Signals	 
		 *		HIGH_     ACTIVE OR LOW_ACTIVE
		 *	  	Deterimined by WEB Optition
		 */
		input	wire			lab_reset,
			
		/*
		 *  SW 
		 * input Signals  
		 */
		input	wire			SW00,
		input	wire			SW01,
		input	wire			SW02,
		input	wire			SW03,
		input	wire			SW04,
		input	wire			SW05,
		input	wire			SW06,
		input	wire			SW07,
		input	wire			SW08,
		input	wire			SW09,
		input	wire			SW10,
		input	wire			SW11,
		input	wire			SW12,
		input	wire			SW13,
		input	wire			SW14,
		input	wire			SW15,
		input	wire			SW16,
		input	wire			SW17,
		input	wire			SW18,
		input	wire			SW19,
		input	wire			SW20,
		input	wire			SW21,
		input	wire			SW22,
		input	wire			SW23,
		input	wire			SW24,
		input	wire			SW25,
		input	wire			SW26,
		input	wire			SW27,
		input	wire			SW28,
		input	wire			SW29,
		input	wire			SW30,
		input	wire			SW31,
		
		/*
		 *   LED 
		 * output Signals  
		 */
		output	wire			LED00,
		output	wire			LED01,
		output	wire			LED02,
		output	wire			LED03,
		output	wire			LED04,
		output	wire			LED05,
		output	wire			LED06,
		output	wire			LED07,
		output	wire			LED08,
		output	wire			LED09,
		output	wire			LED10,
		output	wire			LED11,
		output	wire			LED12,
		output	wire			LED13,
		output	wire			LED14,
		output	wire			LED15,
		output	wire			LED16,
		output	wire			LED17,
		output	wire			LED18,
		output	wire			LED19,
		output	wire			LED20,
		output	wire			LED21,
		output	wire			LED22,
		output	wire			LED23,
		output	wire			LED24,
		output	wire			LED25,
		output	wire			LED26,
		output	wire			LED27,
		output	wire			LED28,
		output	wire			LED29,
		output	wire			LED30,
		output	wire			LED31,
			
		/*
		 *   Register 8-bit 
		 * 	 Input	Signals
		 */
		input	wire	[ 7: 0]	R8IN0,
		input	wire	[ 7: 0]	R8IN1,
		input	wire	[ 7: 0]	R8IN2,
		input	wire	[ 7: 0]	R8IN3,
		input	wire	[ 7: 0]	R8IN4,
		input	wire	[ 7: 0]	R8IN5,
		input	wire	[ 7: 0]	R8IN6,
		input	wire	[ 7: 0]	R8IN7,
		
		/*
		 *   Register 8-bit 
		 * 	 Output	Signals
		 */	
		output	wire	[ 7: 0]	R8OUT0,
		output	wire	[ 7: 0]	R8OUT1,
		output	wire	[ 7: 0]	R8OUT2,
		output	wire	[ 7: 0]	R8OUT3,
		output	wire	[ 7: 0]	R8OUT4,
		output	wire	[ 7: 0]	R8OUT5,
		output	wire	[ 7: 0]	R8OUT6,
		output	wire	[ 7: 0]	R8OUT7,
			
		/*
		 *   Register 16-bit 
		 * 	 Input	Signals
		 */
		input	wire	[15: 0]	R16IN0,
		input	wire	[15: 0]	R16IN1,
		input	wire	[15: 0]	R16IN2,
		input	wire	[15: 0]	R16IN3,
		input	wire	[15: 0]	R16IN4,
		input	wire	[15: 0]	R16IN5,
		input	wire	[15: 0]	R16IN6,
		input	wire	[15: 0]	R16IN7,
		
		/*
		 *   Register 16-bit 
		 * 	 Output	Signals
		 */	
		output	wire	[15: 0]	R16OUT0,
		output	wire	[15: 0]	R16OUT1,
		output	wire	[15: 0]	R16OUT2,
		output	wire	[15: 0]	R16OUT3,
		output	wire	[15: 0]	R16OUT4,
		output	wire	[15: 0]	R16OUT5,
		output	wire	[15: 0]	R16OUT6,
		output	wire	[15: 0]	R16OUT7,
			
		/*
		*   Register 32-bit 
		* 	 Input	Signals
		*/
		input	wire	[31: 0]	R32IN0,
		input	wire	[31: 0]	R32IN1,
		input	wire	[31: 0]	R32IN2,
		input	wire	[31: 0]	R32IN3,
		input	wire	[31: 0]	R32IN4,
		input	wire	[31: 0]	R32IN5,
		input	wire	[31: 0]	R32IN6,
		input	wire	[31: 0]	R32IN7,
		
		/*
		 *   Register 32-bit 
		 * 	 Output	Signals
		 */	
		output	wire	[31: 0]	R32OUT0,
		output	wire	[31: 0]	R32OUT1,
		output	wire	[31: 0]	R32OUT2,
		output	wire	[31: 0]	R32OUT3,
		output	wire	[31: 0]	R32OUT4,
		output	wire	[31: 0]	R32OUT5,
		output	wire	[31: 0]	R32OUT6,
		output	wire	[31: 0]	R32OUT7,	
			
		/*
		 *   Instruction ROM Interface 
		 *
		 *   32-bit Address	 
		 * 	 BaseAddr = 0x40000000
		 *	 HighAddr = 0x40000800
		 *   Size	 =  2K
		 */
		output	wire	[31: 0]    inst_addr,
		input	wire    [31: 0]    inst_data,

		/*
		 *  Mapped RAM0  Interface  
		 *
		 *  32-bit Address
	     *  BaseAddr = 0x00000000
		 *	HighAddr = 0x03ffffff
		 *	Range = 64M
		 */
		 output wire                ram_clk,
		 output wire                ram_rst,
		 output wire    [31: 0]     ram0_raddr,
		 input  wire    [31: 0]     ram0_rdata,
		 output wire	        	ram0_ren,
		 input  wire            	ram0_rvalid,
		 output wire    [31: 0] 	ram0_waddr,
		 output wire    [31: 0] 	ram0_wdata,
		 output wire            	ram0_wen,
		 output wire    [3 : 0]     ram0_sel,
		 input  wire            	ram0_wready,
			
		/*
		 *  Mapped RAM1  Interface  
		 *
		 *  32-bit Address
		 *  BaseAddr = 0x04000000
	     *	HighAddr = 0x07ffffff
		 *	Range = 64M
		 */ 
		 output wire	[31: 0]		ram1_raddr,
		 input  wire    [31: 0]		ram1_rdata,
		 output wire	        	ram1_ren,
		 input  wire            	ram1_rvalid,
		 output wire    [31: 0] 	ram1_waddr,
		 output wire    [31: 0] 	ram1_wdata,
		 output wire            	ram1_wen,
		 output wire	[3 : 0]		ram1_sel,
		 input  wire            	ram1_wready,
		 
		/*
		 *  Flyx-IO Board
		 *
		 *  Seven Segement
		 *  Mointered By Camera	
		 *
	     */
		output  wire				FlyxIO_seven_segment_a,
		output  wire				FlyxIO_seven_segment_b,
		output	wire				FlyxIO_seven_segment_c,
		output	wire				FlyxIO_seven_segment_d,
		output	wire				FlyxIO_seven_segment_e,
		output	wire				FlyxIO_seven_segment_f,
		output	wire				FlyxIO_seven_segment_g,
		output	wire				FlyxIO_seven_segment_dp,
		output	wire				FlyxIO_seven_segment_dig1,
		output	wire				FlyxIO_seven_segment_dig2,
	
		/*
	     *  Flyx-IO Board
		 *
		 *  8x8 LED Array
		 *  Mointered By Camera	
		 *
		 */
		output	wire	[ 7: 0]		FlyxIO_led_array_row,
		output	wire	[ 7: 0]		FlyxIO_led_array_col，
		
		/*
         *  Flyx-IO Board
	     *
	     *  SRAM 512 x 16 bit	
	     *	
	     *  SRAM for User Defined Signals
        */
        output	wire				FlyxIO_sram_user_nce,
        output	wire				FlyxIO_sram_user_noe,
		output	wire				FlyxIO_sram_user_nwe,
		output	wire				FlyxIO_sram_user_nlb,
		output	wire				FlyxIO_sram_user_nub,
		output	wire	[18:0]		FlyxIO_sram_user_addr,
		output	wire	[15:0]		FlyxIO_sram_user_wrdata,
		input	wire	[15:0]		FlyxIO_sram_user_rddata
	);
	```
	
2. 存储器接口系统默认赋值区域： 系统默认存储器初值，用户如若用到相应的接口信号，需要注释对应的赋值语句。

	``` verilog

		//RAM0 Read Interface
		assign	ram0_ren  = 1'b0;
		assign	ram0_raddr = 32'b0;	
		
		//RAM0 Write Interface
		assign	ram0_waddr = 32'b0;
		assign	ram0_wen = 1'b0;
		assign	ram0_sel = 4'b0000;
		assign	ram0_wdata = 32'b0;
		
		//RAM1 Read Interface
		assign	ram1_ren = 1'b0;
		assign	ram1_raddr = 32'b0;
		
		//RAM1 Write Interface
		assign	ram1_waddr = 32'b0;
		assign	ram1_wen = 1'b0;
		assign	ram1_sel = 4'b0000;
		assign	ram1_wdata = 32'b0;
		
		//RAM CLK AND RESET
		assign ram_clk = step_clk;
		assign ram_rst = 1'b1;
		
	``` 
	
3. IO接口系统默认绑定区域： 系统默认管脚绑定区域，若用到相应的接口输出信号，需要注释对应的赋值语句。	

	``` verilog

		/*
		**	SW LED
		**
		*/
		assign	LED00 = SW00;
		assign	LED01 = SW01;
		assign	LED02 = SW02;
		assign	LED03 = SW03;
		assign	LED04 = SW04;
		assign	LED05 = SW05;
		assign	LED06 = SW06;
		assign	LED07 = SW07;
		assign	LED08 = SW08;
		assign	LED09 = SW09;
		assign	LED10 = SW10;
		assign	LED11 = SW11;
		assign	LED12 = SW12;
		assign	LED13 = SW13;
		assign	LED14 = SW14;
		assign	LED15 = SW15;
		assign	LED16 = SW16;
		assign	LED17 = SW17;
		assign	LED18 = SW18;
		assign	LED19 = SW19;
		assign	LED20 = SW20;
		assign	LED21 = SW21;
		assign	LED22 = SW22;
		assign	LED23 = SW23;
		assign	LED24 = SW24;
		assign	LED25 = SW25;
		assign	LED26 = SW26;
		assign	LED27 = SW27;
		assign	LED28 = SW28;
		assign	LED29 = SW29;
		assign  LED30 = SW30;
		assign  LED31 = SW31;
		/*
		**	8-bit Register 
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
		**	16-bit Register
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
		**	32-bit Register
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

4. 数码管接口系统默认赋值区域： 系统默认码初值，用户如若用到相应的接口信号，需要注释对应的赋值语句。

	``` verilog
	assign FlyxIO_seven_segment_a = SW00;
	assign FlyxIO_seven_segment_b = SW01;
	assign FlyxIO_seven_segment_c = SW02;
	assign FlyxIO_seven_segment_d = SW03;
	assign FlyxIO_seven_segment_e = SW04;
	assign FlyxIO_seven_segment_f = SW05;
	assign FlyxIO_seven_segment_g = SW06;
	assign FlyxIO_seven_segment_dp = SW07;
	assign FlyxIO_seven_segment_dig1 = SW08;
	assign FlyxIO_seven_segment_dig2 = SW09;
	```

5. 点阵LED接口系统默认赋值区域： 系统默认LED点阵初值，用户如若用到相应的接口信号，需要注释对应的赋值语句。

	``` verilog
	assign FlyxIO_led_array_row = R8IN0;
	assign FlyxIO_led_array_col = R8IN1;
	```

6. SRAM存储接口默认区域：系统默认SRAM初始化，用户如若用到SRAM存储接口，需要根据自己的逻辑重构代码。
	``` verilog
	reg					reg_sram_user_nce;
	reg					reg_sram_user_noe;
	reg					reg_sram_user_nwe;
	reg					reg_sram_user_nlb;
	reg					reg_sram_user_nub;
	reg		[18:0]		reg_sram_user_addr;
	reg		[15:0]		reg_sram_user_wrdata;
	reg		[15:0]		reg_R16OUT0;
	
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

	```


7. 用户自定义顶层module实例化区域

	``` verilog
	
		user_wrapper_top user_wrapper_top_uut
		(
		
		);
	
	```
	
---

#### 四、数码管

一个数码管有八段：A、B、C、D、E、F 、G、H、DP，即由八个发光二极管组成。
![](/assets/c116e3cddc3985166d8aa20ae8a0da85.png)

发光二极管导通的方向是一定的，这八个发光二极管的公共端有两种：可分共阳极（公共端接高电平或+5V电压）和共阴极（共低电平或接地）两种数码管。教学板卡中采用的是共阳极数码管的接法，其原理图下图所示。
![](/assets/12d8d018ab27e26ca8e491af506b0be4.png)

共阳极数码位选信号（`DIG1`和`DIG2`）选为高电平时（即1）选中数码管，各段（`A`、`B`、`C`、`D`、`E`、`F` 、`G`、`H`和`DP`）选为低电平时（即0）选中各数码管。

共阳极二极管的编码如下表所示，其中`1`表示接高电平，`0`表示接低电平，编码值的规则是DP在高位，A在低位。

|  显示数字  |  DP | G | F | E | D | C| B | A | 编码|
|  :--:   |  :--:   | :--:  |  :--:  |   :--:   | :--:  |  :--:  |:--:  |  :--:  |
| 0x0   |   1    |  1    |   0  |  0  |  0  |  0  |  0  |  0 |    0xC0 |
| 0x1   |   1    |  1    |   1  |  1  |  1  |  0  |  0  |  1 |    0xF9 |
| 0x2   |   1    |  0    |   1  |  0  |  0  |  1  |  0  |  0 |    0xA4 |
| 0x3   |   1    |  0    |   1  |  1  |  0  |  0  |  0  |  0 |    0xB0 |
| 0x4   |   1    |  0    |   0  |  1  |  1  |  0  |  0  |  1 |    0x99 |
| 0x5   |   1    |  0    |   0  |  1  |  0  |  0  |  1  |  0 |    0x92 |
| 0x6   |   1    |  0    |   0  |  0  |  0  |  0  |  1  |  0 |    0x82 |
| 0x7   |   1    |  1    |   1  |  1  |  1  |  0  |  0  |  0 |    0xF8 |
| 0x8   |   1    |  0    |   0  |  0  |  0  |  0  |  0  |  0 |    0x80 |
| 0x9   |   1    |  0    |   0  |  1  |  0  |  0  |  0  |  0 |    0x90 |
| 0xA   |   1    |  0    |   0  |  0  |  1  |  0  |  0  |  0 |    0x88 |
| 0xB   |   1    |  0    |   0  |  0  |  0  |  0  |  1  |  1 |    0x83 |
| 0xC   |   1    |  1    |   0  |  0  |  0  |  1  |  1  |  0 |    0xC6 |
| 0xD   |   1    |  0    |   1  |  0  |  0  |  0  |  0  |  1 |    0xA1 |
| 0xE   |   1    |   0   |   0  |  0  |  0  |  1  |  1  |  0 |    0x86  |
| 0xF   |   1    |  0    |   0  |  0  |  1  |  1  |  1  |  0 |    0x8E  |

#### 五、点阵LED

8x8点阵LED其主要分为共阳和共阴两种，一般是根据点阵第一个引脚的极性所定义的，第一个引脚为阳极则为共阳，反之则为共阴。
![](/assets/d1ac68349ebff59899268fe48ef73487.png)

8x8点阵LED的行列定义如下图所示。
![](/assets/0c08845b67c1c610589ec1ecceb8d8f0.png)

实验中教学板卡采用的是共阳极的连接（即行共阳），其原理图如下图所示。
![](/assets/7ac55a3fced98b196ced79fe057400df.png)

当列中的PIN脚为低电平时（即PIN13、PIN3、PIN4、PIN10、PIN6、PIN11、PIN15和PIN16），选中PIN脚所在的列；当行中的PIN脚为高电平时（即PIN9、PIN14、PIN8、PIN12、PIN1、PIN7、PIN2和PIN5），选中PIN脚所在的行；只有当行中和列中的PIN脚同时被选中十才能点亮相应LED点。

#### 六、SRAM存储

教学版中采用的SRAM芯片型号为`IS61WV51216BLL`,其地址线是512K，数据线是16bit。用户可以参考其芯片手册及相关资料，这里不作详细说明。资料参考连接： http://pdf1.alldatasheet.com/datasheet-pdf/view/311087/ISSI/IS61WV51216BLL-10TLI.html




