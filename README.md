# ESP32 Paperang Emulator

### 用ESP32 DIY 热敏打印机，模拟Paperang/喵喵机通信协议，可以通过蓝牙连接手机，接收、打印Paperang APP/喵喵机APP/作业帮APP发送的打印数据

![封面](https://github.com/1452206376/ESP32-Paperang-Emulator/blob/master/images/main.png )

[Bilibili视频链接](https://www.bilibili.com/video/BV1v54y127xZ )

-----

**3D模型可能不适合你的打印头,如果打印头尺寸与3D模型相差太大建议重新设计3D模型**

## 注意事项/调试过程

**注意：以下内容必须认真阅读，否则可能会出现各种问题，甚至烧坏打印头**

### 焊接

焊接时按照元器件从小到大顺序焊接，焊接完成后先检查是否有短路、虚焊、漏焊元件等情况（可以不焊接CP2104和自动复位电路，PCB后面预留有烧录程序用的测试点）

PCB焊接完成后不要立刻焊接打印头测试，先连接电池和开关，将电位器指针调至中间，闭合开关，用万用表直流50V或20V档位测量 VH+ 与 GND 之间的电压，并**缓慢调节**电位器，逆时针旋转升压，顺时针旋转降压。直到输出电压略小于打印头加热元件额定电压，然后焊接打印头。VH+ 可调节的范围：VBAT - 28V，最好不要将电位器调到两端。

我使用的打印头的额定电压为7.2V，型号为三星SMP640, 可作参考

------

将libraries文件夹与esp32开发板安装目录下的libraries文件夹合并，这个文件夹的位置：

Windows，一般在

`C:\Users\Admin\AppData\Local\Arduino15\packages\esp32\hardware\esp32\1.0.4\libraries`

Linux，一般在

`~/.arduino15/packages/esp32/hardware/esp32/1.0.4/libraries`

修改了官方库的缓冲区大小
-----

### 编译/连接/上传

开发板选择ESP32_Wrover_Module，认真核对Printer.ino开头部分的的配置是否符合打印头，然后上传。

上传完成后，如果听到蜂鸣器响1短声，说明启动正常，且 ESP32 的 PSRAM 工作正常。

### 打印测试

在APP中连接打印机，打印**一行**文字，如果打印过程中打印机中途**停止转动**、打印**速度过慢**、文字**颜色过深**或像素点形状**不规则**，请立刻（2秒内）断开开关检查**程序**配置、**电路**连接、打印纸上的**图案**和**串口**输出信息中是否有“ERROR”字样（有就说明有丢包现象），这些信息有助于排错。因为ESP32复位后需要一段时间自检，然后配置IO口。如果开关断开不及时很容易烧坏打印头

默认打印头步进电机转**4**步，打印机走纸**一像素**的距离，如果发现打印的文字长度**过长**或**过扁**，请修改startPrint函数中的goFront1()函数出现位置和次数，这个函数的作用是使打印头步进电机走1步

如果打印正常，就可以把它固定进3D打印的盒子里了

最后，祝大家一次成功（上面说的错误很容易修复，基本都是丢包或配置不当造成的），没有信心可以准备两个型号相同的打印头，用其中一个测试好后换另外一个打印头装盒，这样可以保证打印机做好后打印效果最好。

有什么解决不了的问题或 代码/PCB 的bug请发Issue或PR。建议直接私信作者Bilibili @小李电子实验室  UID:213123506，开学后每三周检查一次私信和评论

-----
## 文件列表：
|文件夹名|描述|
|--|--|
|3D-Model|3D模型|
|images|一些图片|
|libraries|库文件|
|PCB|PCB工程文件和GERBER文件|
|Program|Arduino 程序文件|
|Python|（仅作备份）Python程序|
-----

如果觉的好别忘了Star :)

## 参考资料链接

[喵喵机折腾记-ihcblog](https://www.ihcblog.com/miaomiaoji/ )

[hansel163-paperang_printer](https://github.com/hansel163/paperang_printer )
