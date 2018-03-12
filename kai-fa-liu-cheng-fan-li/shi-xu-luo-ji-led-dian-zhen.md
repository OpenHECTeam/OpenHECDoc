### [时序逻辑LED点阵](http://www.iopenhec.com/#!/experiment/000020170413000000000003)

时序逻辑LED点阵是基于虚拟面板+教学板卡的线上实验方式，实现8x8点阵LED的对角线顺序点亮，是在纯FPGA模式下使用[**RELAX\_FlyxSOM\_LED7SEG**](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)实验支撑包来进行开发的。

#### 一、开发入口

时序逻辑LED点阵的OpenHEC平台的开发入口是：[http://www.iopenhec.com/\#!/experiment/000020170413000000000003](http://www.iopenhec.com/#!/experiment/000020170401000000000006)

时序逻辑LED点阵采用的硬件类型为[Flyx-SOM](http://www.iopenhec.com/#!/hardware/000020161019000000000012)，具体芯片型号为**xc7z030fbg484-3**。

实验资料**oLib**目录中主要资料如下。

* [纯FPGA模式下的**RELAX\_FlyxSOM\_LED7SEG**实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)
* LED点阵对角线顺序点亮的参考代码（led\_array.v ）

本次实验基于教学板卡+虚拟面板的线上实验方式，实现8x8点阵LED的对角线顺序显示。其参考代码如下：

```verilog
module led_arrary
(
    input   wire            clk,
    input   wire            rst,
    output  wire    [7:0]   FlyxIO_led_array_row,
    output  wire    [7:0]   FlyxIO_led_array_col
);

    reg     [ 7: 0] reg_led_row;
    reg     [ 7: 0] reg_led_col;

    assign FlyxIO_led_array_row = reg_led_row;
    assign FlyxIO_led_array_col = reg_led_col;

    always @ (posedge clk) 
    begin
        if(rst) 
            begin
                reg_led_row <= 8'b00000001;
                reg_led_col <= 8'b11111110;
            end 
        else 
            begin
                reg_led_row <= {reg_led_row[6:0], reg_led_row[7]};
                reg_led_col <= {reg_led_col[6:0], reg_led_col[7]};  
            end
    end

endmodule
```

#### 二、使用虚拟机

1. ##### **新建用户逻辑工程**

   启动vivado 2015.2后，选择**Create New Project**，点击**Next**，输入项目名为**led\_proj**和项目位置新建在桌面下的**proj\_ip**。

   点击**Next**，在**Project Type**选项里，将**Do not specify source at this time**勾选上。

   点击**Next**，这里需要选择芯片的型号。在**Parts**选项选择**xc7z030fbg484-3**芯片即可。

   点击**Next**，然后**Finish**完成项目的创建。

2. ##### 添加led点阵显示的用户逻辑

   添加LED点阵对角线顺序点亮的逻辑源文件，文件存放在**oLib/led\_array.v**下。

   在**Flow Navigator/Project Manager**选项卡下选择**Add Sources**，在弹出的窗口中选择**Add or create design sources**，点击**Next**，点击**+**号标志，选择**Add Files**，添加** oLib**文件夹下的**led\_array.v**文件。

   选择 **Copy sources into project**`,`点击**Finish**`,`完成LED点阵显示用户文件的加载。

3. **添加OpenHEC实验平台顶层文件**

   接下来添加OpenHEC实验平台顶层文件，文件存放在**oLib/RELAX\_FlyxSOM\_LED7SEG/relax\_top **文件夹下，名为**OpenHEC\_Exp\_Top.v**。

   在**Flow Navigator/Project Manager**选项卡下选择**Add Sources**，在弹出的窗口中选择**Add or create design sources**，点击**Next**，点击**+**号标志，选择**Add Files**，添加** oLib/RELAX\_FlyxSOM/relax\_top** 文件夹下的**OpenHEC\_Exp\_Top.v**文件。

   选择 **Copy sources into project**`,`点击**Finish**`,`完成OpenHEC实验平台顶层文件的加载。

4. **用户逻辑与实验支撑包的接口绑定**

   根据[**RELAX\_FlyxSOM\_LED7SEG**实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)解析说明，用户逻辑的工作时钟clk和复位信号rst分别绑定到**step\_clk**和复位信号**lab\_reset上**，输出管脚 **FlyxIO\_led\_array\_col **和**FlyxIO\_led\_array\_row**直接一一绑定到点阵LED的列和行管脚上，同时注释掉点阵LED中的赋值语句。

   ```verilog
   //assign FlyxIO_led_array_row = R8IN0;
   //assign FlyxIO_led_array_col = R8IN1;
   led_arrary user_wrapper_top_uut
   (
           .clk(step_clk),
           .rst(lab_reset),
           .FlyxIO_led_array_col(FlyxIO_led_array_col),
           .FlyxIO_led_array_row(FlyxIO_led_array_row)
   );
   ```

5. **综合与实现**

   OpenHEC实验支撑包中提供综合实现的tcl脚本，可以自动完成整个系统的综合，最终生成比特流文件。点击 **Tools/Run Tcl Script**，选择文件夹**oLib/RELAX\_FlyxSOM\_LED7SEG/tcl **下的**relax\_syn\_imp\_flow.tcl**文件，点击OK，自动运行综合与实现，等待生成位流。比特流文件存放在桌面文件夹**proj\_ip/led\_proj**下。![](/assets/led_genbit.png)

6. **完成开发**

   拷贝桌面文件夹**proj\_ip/led\_proj**下的位流文件**led\_proj.bit** 到oDisk目录，完成开发。![](/assets/finish_led.png)

#### 三、使用FPGA

完成了FPGA的开发后，用户既可以在OpenHEC部署在云端的FPGA硬件上验证数码管的bit文件了。

1. ##### 配置比特流到FPGA

   点击**配置FPGA**，弹出配置FPGA页面，默认加载**我的oDisk**中bit后缀的FPGA位流；先选中刚刚拷贝的**led\_proj.bit**位流，同时选择纯FPGA模式的配置方式，点击配置即可以。配置FPGA成功后，在虚拟面板有FPGA位流配置成功的提示信息。

2. ##### IO实时监控

   根据[**RELAX\_FlyxSOM\_LED7SEG**实验支撑包](http://doc.iopenhec.com/ying-jian/flyx-somji-chu-pei-zhi/ying-jian-zhi-cheng-bao/shi-yan-zhi-cheng-bao-relax-flyxsom-led7seg-ru-men-shou-ce.html)中数码管的编码规则，在虚拟面板点击单步时钟，同时切换到监控视频页面会看到点阵LED呈现对角线顺序显示，每点击一次单步时钟按钮，LED点动一步。

   ![](/assets/led0003.png)![](/assets/led0004.png)![](/assets/led0005.png)![](/assets/led0006.png)![](/assets/led0007.png)![](/assets/led0008.png)



