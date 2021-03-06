title: 0a-esp8266ex_datasheet_cn
---

# 1.	概述 
#### ESP8266EX 由乐鑫公司开发，提供了一套高度集成的 Wi-Fi SoC 解决方案，其低功耗、紧凑设计和高稳定性可以满足用户的需求。

#### ESP8266EX 拥有完整的且自成体系的 Wi-Fi 网络功能，既能够独立应用，也可以作为从机搭载于其他主机 MCU 运行。当 ESP8266EX 独立应用时，能够直接从外接 Flash 中启动。内置的高速缓冲存储器有利于提高系统性能，并且优化存储系统。此外 ESP8266EX 只需通过 SPI/SDIO 接口或 I2C/UART 口即可作为 Wi-Fi 适配器，应用到基于任何微控制器的设计中。

#### ESP8266EX 集成了天线开关、射频 balun、功耗放大器、低噪放大器和过滤器。这样紧凑的设计仅需极少的外部电路并且将 PCB 的尺寸降到最低。ESP8266EX 还集成了增强版的 Tensilica’s L106 钻一系列 32-bit 内核处理器，带片上SRAM。 ESP8266EX 可以通过 GPIO 外接传感器和其他设备。

## 1.1WiFi协议

##### • 支持 802.11 b/g/n/e/i。

##### • 支持 Wi-Fi Direct (P2P)。

##### • 基础结构型网络 (Infrastructure BSS) 工作站 (Station) 模式/P2P 模式/SoftAP 模式。

##### • 支持 CCMP（CBC-MAC、计数器模式）、 TKIP (MIC、 RC4)、 WAPI (SMS4)、 WEP(RC4)、 CRC 的硬件加速器。

##### • WPA/PA2 PSK 和 WPS。

##### • 802.11 i 安全特征：预认证和 TSN。

##### • 支持 802.11n (2.4 GHz)。

##### • 支持 MIMO 1×1 和 2×1、 STBC、 A- MPDU 和 A-MSDU 帧聚合技术、 0.4μs 的保护间隔。

##### • WMM 低功耗 U-APSD。

##### • 多队列管理，充分利用802.11e 标准的 QoS 传输优先。

##### • UMA 认证标准。

##### • 802.1h/RFC1042 帧封装。

##### • 分散 DMA，实现数据传输操作时 Zero Copy，优化 CPU 负载。

##### • 自适应速率回退算法基于实际信噪比(SNR) 和丢包信息来控制最佳传输速率和发射功耗。

##### • MAC 层上的自动动重传和回复以防止在慢速主机环境中的数据包丢弃。

## 1.2.	技术参数 

###### 表 1-1 主要技术参数 

![表 1-1. 主要技术参数 ](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/1.png)

## 1.3.	应用

##### • 家庭自动化

##### • 智能插座、智能灯

##### • Mesh 网络

##### • 工业无线控制

##### • 婴儿监控器

##### • IP 摄像机

##### • 传感器网络

# 2.管脚定义

#### 管脚布局如图 2-1 所示。

![图 2-1. 管脚布局](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/2.png)

###### 图 2-1. 管脚布局

#### 管脚定义如表 2-1 所示。

###### 表 2-1. 管脚定义

![表 2-1. 管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/4.png)
 
# 3.功能描述

#### ESP8266EX 的功能原理如图 3-1 所示。

![图 3-1. 功能原理图](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/5.png)

###### 图 3-1. 功能原理图

## 3.1. CPU、存储和 Flash

### 3.1.1. CPU

#### ESP8266EX 内置 Tensilica L106， 32-bit 微处理器 (MCU)，具有超低功耗的 16-bit RSIC。CPU 时钟速度为 80 MHz，最高可达 160 MHz。支持实时操作系统 (RTOS)。目前 Wi-Fi 协议栈只用了 20% 的 MIPS，其他的都可以用来做应用编程和开发。 CPU 包括以下接口。

##### • 可连接片内存储控制器和外部 Flash 的可配置 RAM/ROM 接口 (iBus)

##### • 连接存储控制器的数据 RAM 接口 (dBus)

##### • 访问寄存器的 AHB 接口

### 3.1.2. 内置存储

#### ESP8266EX 芯片内置了存储控制器，包含 ROM 和 SRAM。 MCU 可以通过 iBus、 dBus和 AHB 接口访问存储控制器。在发起请求后，所有存储单元都可以被访问。存储仲裁器会根据处理器接受这些请求的时间，决定访问顺序。

#### 芯片内无可编程存储器，用户程序必须由外部 Flash 存储。

### 3.1.3. 外置 Flash

#### ESP8266EX 使用外置 SPI Flash 存储用户程序。理论上最大可支持 16 MB 的存储。建议按照如下所示来分配 SPI Flash 容量。

##### • 不支持 OTA：最少支持 512 kB

##### • 可支持 OTA：最少支持 1 MB

⚠ 注意：支持的 SPI 模式： Standard SPI、 Dual SPI 和 Quad SPI。因此在烧录程序到 Flash 时要选择正确的 SPI 模式，否则下载的固件／程序可能无法正常正作。

## 3.2. AHB 和 AHB 模块
#### AHB 模块充当仲裁器，通过 MAC、主机的 SDIO 和 CPU 控制 AHB 接口由于发送地址不同， AHB 数据请求可能到达以下两个从机中的一个。

##### • APB 模块

##### • 闪存控制器（通常在无主机的情况下）

#### 高速请求一般是用来访问 Flash 控制器，而访问寄存器通过的是 APB 模块。

#### APB 模块充当解码器。但只可以访问 ESP8266EX 主模块内可编程的寄存器。由于发送地址不同， APB 请求可能到达射频接收器、 SI/SPI、主机 SDIO、 GPIO、 UART、实时时钟(RTC)、 MAC 或数字基带。

## 3.3. 时钟

### 3.3.1. 高频时钟

#### 基于外部晶振， ESP8266EX内部晶体振荡器可以生成射频时钟。该时钟可用于驱动 Tx 和Rx 混频器。晶振频率在 24 MHz 到 52 MHz 之间。

#### 尽管晶体振荡器的内部校准功能使得一系列的晶体满足时钟生成条件，但是晶体的质量仍然是影响获得合适的相位噪声和 Wi-Fi 灵敏度的因素。请参照表 3-1 来测量频率偏移。

###### 表 3-1. 高频时钟参数

![表 3-1. 高频时钟参数](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/6.png)

### 3.3.2. 外部时钟参考要求
#### 外部时钟的频率在 24 MHz 到 52 MHz 之间。为了使射频性能良好，时钟需满足要求如表3-2 所示

###### 表 3-2. 外部时钟参考要求

![表 3-2. 外部时钟参考要求](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/7.png)

## 3.4. 射频

#### ESP8266EX 射频主要包含以下模块。

##### • 2.4 GHz 接收器

##### • 2.4 GHz 发射器

##### • 高速时钟生成器和晶体振荡器

##### • 实时时钟

##### • 偏置电路与稳压器

### 3.4.1. 信道频率

#### 根据 IEEE802.11b/g/n标准，射频收发器支持以下信道。

###### 表 3-3. 频率信道

![表 3-3. 频率信道](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/8.png)

### 3.4.2. 2.4 GHz 接收器

#### 2.4 GHz 接收器把射频信号降频，变成正交基带信号，用 2 个高分辨率的高速 ADC 将后者转为数字信号。为了适应不同的信号频道， ESP8266EX 集成了射频滤波器、自动增益控制 (AGC)、 DC 偏移补偿电路和基带滤波器。

### 3.4.3. 2.4 GHz 发射器

#### 2.4 GHz 发射器将正交基带信号升频到 2.4 GHz，使用大功耗互补金属氧化物半导(CMOS) 功耗放大器驱动天线。数字校准的使用进一步地改善了功耗放大器的线性，从而在 802.11b 传输中达到 +19.5 dBm 的平均功耗，在 802.11n 传输中达到 +16 dBm 的平均功耗，功能超强。为了抵消无线电接收器的瑕疵， ESP8266EX 还另增了以下校准措施。

##### • 载波泄露

##### • I/Q 相位匹配

##### • 基带非线性

#### 这些内置的校准措施减少了生产测试所需的时间和设备。

### 3.4.4. 时钟生成器

#### 时钟生成器为接收器和发射器生成 2.4 GHz 正交基带时钟信号，其所有部件均集成于芯⽚上，包括：电感器、变容二极管、闭环滤波器、监管者和分频器。

#### 时钟生成器含有内置校准电路和自测电路。正交时钟相位和相位噪声通过拥有专利的校准算法在芯片上进行最优处理，以确保接收器和发射器达到最佳性能。

## 3.5. Wi-Fi

#### ESP8266EX 支持 TCP/IP 协议，完全遵循 802.11 b/g/n/e/i WLAN MAC 协议和 Wi-Fi Direct 标准。它支持分布式控制功能 (DCF) 下的基本服务集 (BSS) 操作，也支持符合最新的 Wi-Fi P2P 协议的 P2P 团体操作。 ESP8266EX 自动采用低层协议功能。

##### • RTS/CTS

##### • 确认字符

##### • 分片和重组

##### • 聚合

##### • 帧封装 (802.11h/RFC 1042)

##### • 自动信标监测/扫描

##### • P2P Wi-Fi direct

#### 跟 P2P 发现程序一样，被动或主动扫描一旦在适当的指令下起动，就会自主完成。执行电源管理时，与主机互动最少，如此一来，工作时间达到最短。

# 4. 外设接口

## 4.1. 通用输入/输出接口 (GPIO)

#### ESP8266EX 共有 17 个 GPIO 管脚，通过配置适当的寄存器可以给它们分配不同的功能。

#### 每个 GPIO 都可以配置为内部上拉/下拉，或者被设置为高阻。当被配置为输入时，可通过读取寄存器获取输入值；输日也可以被设置为边缘触发或电平触发来产生 CPU 中断。简言之， IO 管脚是双向、非反相和三态的，带有三态控制的输入和输出缓冲器。

#### 这些管脚可以与其他功能复用，例如 I2C、 I2S、 UART、 PWM、 IR 遥控、 LED Light 和Button 接口等。

#### 选择性的保持功能可以应需植入 IO 中。当 IO 不由内外部电路驱动时，保持功能可以被用于保持上次的状态。保持功能给管脚引入一些正反馈。因此，管脚的外部驱动必须强于正反馈。脱离保持状态所需的驱动力很小，在 5μA 之内。

## 4.2. SDIO

#### ESP8266EX 拥有 1 个从机 SDIO 接口，接口管脚定义如下表 4-1 所示。支持 4-bit 25MHz SDIO v1.1 和 4-bit 50 MHz SDIO v2.0。

###### 表 4-1. SDIO 管脚定义

![表 4-1. SDIO 管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/10.png)

## 4.3. 串行外设接口 (SPI/HSPI)

#### ESP8266EX 拥有 1 个通用从机/主机 SPI， 1 个从机 SDIO/SPI，和 1 个通用从机/主机HSPI。所有接口的功能均由硬件实现。接口定义如下所示。

### 4.3.1. 通用 SPI（主机/从机）

###### 表 4-2. SPI 接口定义

![表 4-2. SPI 接口定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/11.png)

说明：SPI 模式可由软件编程实现。时钟频率最⼤为 80 MHz。

### 4.3.2. HSPI（从机）

###### 表 4-3. HSPI（从机）管脚定义

![表 4-3. HSPI（从机）管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/12.png)

## 4.4. I2C 接口

#### ESP8266EX 拥有 1 个 I2C 接口，用于连接微控制器以及外围设备，如传感器等。 I2C 接口定义如表 4-4 所示。

###### 表 4-4. I2C 管脚定义

![表 4-4. I2C 管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/13.png)

#### ESP8266EX 既支持 I2C 主机也支持 I2C 从机功能。 I2C 接口功能可由软件编程实现，时钟频率最高约为 100 kHz，需高于从设备最慢速的时钟频率。

## 4.5. I2S 接口

#### ESP8266EX 拥有 1 个 I2S 输入接口和 1 个 I2S 输出接口。 I2S 主要用于音频数据采集、处理和传输，也可用于串口数据输入输出，如支持 LED 彩灯（WS2812 系列）。 I2S 管脚定义如表 4-5 所示。 I2C 接口能可以使用复用 GPIO 通过软件编程实现，支持链表DMA。

###### 表 4-5. I2S 管脚定义

![表 4-5. I2S 管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/14.png)

## 4.6. 通用异步收发器 (UART)

#### ESP8266EX 拥有两个 UART 接口，分别为 UART0 和 UART，接口定义如表 4-6 所示。

###### 表 4-6. UART 管脚定义

![表 4-6. UART 管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/15.png)

#### 2 个 UART 接口的数据传输均由硬件实现。数据传输速度可达 115200*40 (4.5 Mbps)。

#### UART0 可以用做通信接口，支持流控。由于 UART1 目前只有数据传输功能，所以一般用作打印 log。

说明：

UART0 默认会在上电启动期间输出一些打印，此期间打印内容的波特率与所用的外部晶振频率有关。使用 40 MHz 晶振时，该段打印波特率为 115200；使用 26 MHz 晶振时，该段打印波特率为 74880。如果打印信息影响设备功能，建议在上电期间将 U0TXD、 U0RXD 分别与 U0RTS (MTDO)， U0CTS (MTCK) 交换，以屏蔽打印。

## 4.7. 脉冲宽度调制 (PWM)

#### ESP8266EX 拥有 4 个 PWM 输出接口，如表 4-7 所示。用户可自行扩展。

###### 表 4-7. PWM 管脚定义

![表 4-7. PWM 管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/16.png)

#### PWM 接口功能由软件实现。例如，在 LED 智能照明的示例中， PWM 通过定时器的中断实现，最小分辨率可达 44 ns。 PWM 频率的可调节范围为 1000μs 到 10000μs，即 100Hz 到 1 kHz 之间。当 PWM 频率为 1 kHz，占空⽐为 1/22727， 1 kHz 的刷新率下可达超过 14-bit 的分辨率。

## 4.8. IR 遥控接口

#### ESP8266EX 芯片目前定义了 1 个 IR 红外遥控接口，该接口定义如表 4-8 所示。

###### 表 4-8. IR 红外遥控管脚定义

![表 4-8. IR 红外遥控管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/24.png)

#### IR 红外遥控接口由软件实现，接口使用 NEC 编码及调制解调，采用 38 kHz 的调制载波，占空比为 1/3 的方波。传输范围在 1m 左右，传输范围由 2 个因素决定，一个是 GPIO 口的最大额定电流，另一个是红外接收管内部的限流电阻的大小。电阻越大，电流越小，功耗也越小，反之亦然。传输半⻆度为 15° 到 30°，取决于红外接收管的辐射⽅向。

## 4.9. ADC（模/数转换器）

#### ESP8266EX 内置了一个 10-bit 精度的 SAR ADC。 TOUT（管脚 6）定义如表 4-9 所示。

###### 表 4-9. ADC 管脚定义

![表 4-9. ADC 管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/17.png)

#### ADC 端口（管脚 6 TOUT）可提供以下两种应用，但不可同时使用。

##### • 测量 VDD3P3（管脚 3 和 4）上的电源电压。

![测量 VDD3P3（管脚 3 和 4）上的电源电压](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/18.png)

##### • 测量 TOUT（管脚 6）的输入电压。

![测量 VDD3P3（管脚 3 和 4）上的电源电压](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/19.png)

说明：

SDK 包提供 esp_init_data_default.bin，并且包含射频初始化参数 (0 ~ 127 Bytes)。

esp_init_data_default.bin 中的第 107 byte，命名为 ”vdd33_const”， 此参数的定义如下：

##### • 当 vdd33_const = 0xff，ESP8266EX 芯片会进内内部自测 VDD3P3 管脚 3 和 管脚 4 上的电源电压，根据测量结果优化射频电路工作状态。

##### • 当 18 =< vdd33_const =< 36，ESP8266EX 使用（vdd33_const/10）来校准和优化射频电路工作状态。

##### • 当 vdd33_const < 18 或 36 < vdd33_const < 255 时，ESP8266EX 使用默认值 2.5V 来校准和优化射频电路工作状态。

## 4.10. LED Light 和 Button 接口

#### ESP8266EX拥有多达 17 个 GPIO 接口，均可定义作为 LED 与 Button 的控制接口。基于目前 ESP8266EX 一些示例设计的应用，我们对 LED 与 Button 的 GPIO 接口定义如表 4-10 所示。

###### 表 4-10. LED 和 Button 管脚定义

![表 4-10. LED 和 Button 管脚定义](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/20.png)

#### 上述共定义了一个 Button 和 2 个 LED 的接口。通用情况下，MTCK 作为复位按键的控制；GPIO0 用作 Wi-Fi 用作状态指示灯；MTDI 用作与服务器通信的指示灯。

# 5. 电气参数

## 5.1. 电气特性

###### 表 5-1. 电气特性

![表 5-1. 电气特性](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/21.png)

## 5.2. 功耗

###### 表 5-2. 功耗

![表 5-2. 功耗](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/22.png)

## 5.3. Wi-Fi 射频特征

#### 表 5-3 中数据是在室内温度下，电压为 3.3V 和 1.1V 时分别测得。

###### 表 5-3. Wi-Fi 射频特征

![表 5-3. Wi-Fi 射频特征](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/23.png)

# 6. 封装信息

![图 6-1. ESP8266EX 封装](http://docs.gizwits.com/assets/zh-cn/module_source/esp8266/25.png)

###### 图 6-1. ESP8266EX 封装

说明：

##### • INST_NAME 指的是在 eagle_soc.h 定义下的 IO_MUX REGISTER，例如 MTDI_U 指的是PERIPHS_IO_MUX_MTDI_U。

##### • Net Name 指的是原理图中的管脚名称。

##### • 功能指的是每个管脚的多功能。

##### • 功能 1 ~ 5 对应 SDK 中的功能 0 ~ 4。例如，将 MTDI 设置为 GPIO12，如下所示：

###### - #define	FUNC_GPIO12		3	//defined	in	eagle_soc.h

###### - PIN_FUNC_SELECT（PERIPHS_IO_MUX_MTDI_U,FUNC_GPIO12）

# I. 附录 - 资源

##### • [ESP8266串口烧写说明](http://docs.gizwits.com/zh-cn/deviceDev/ESP8266%E4%B8%B2%E5%8F%A3%E7%83%A7%E5%86%99%E8%AF%B4%E6%98%8E.html)

##### • [获取乐鑫ESP 8266 Gagent日志（教程中“1.获取乐鑫ESP 8266 Gagent日志”）](http://docs.gizwits.com/zh-cn/deviceDev/%E9%80%9A%E8%AE%AF%E6%A8%A1%E7%BB%84%E8%B0%83%E8%AF%95%E6%97%A5%E5%BF%97%E6%8A%93%E5%8F%96%E6%95%99%E7%A8%8B.html)

##### • [GAgent for ESP8266 04020024下载](http://gizwits.oss.aliyuncs.com/hardware_resource/GAgent_00ESP826_04020024_17062808.zip)
