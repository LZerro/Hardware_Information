coresight

文档指引

《debug_interface_v6_0_architecture_specification_IHI0074A.pdf》
B4.2 SWD protocol operation 协议操作
B4.2.1 Successful write operation (OK response)

DP区寄存器列表 Table B2-3 shows the DPv3 register map.

4.4 写DP区寄存器以开启AP区寄存器使能。 向CTRL/STAT寄存器写入0x50000000
B2.2.3 CTRL/STAT, Control/Status register
```
CSYSPWRUPREQ, bit[30] 
CDBGPWRUPREQ, bit[28] 
```
-----------------------------------------------------------------------------

各个名称缩写 https://blog.csdn.net/weixin_45264425/article/details/134048809
JTAG
SWD Serial Wire Debug。
SWO Serial Wire Output。
SWV Serial Wire Viewer。
ETF 嵌入式跟踪FIFO
ETM Embedded Trace Macrocell
ETB Embedded Trace Buffer。CoreSight ETB 是一个跟踪接收器，它可使用可配置大小的 RAM 为跟踪数据提供芯片上存储
MTB Micro Trace Buffer。
ITM Instrumentation Trace Macrocell。 ITM块是一个嵌入式跟踪宏单元（ETM）架构规范中的一部分
DWT Data Watchpoint and Trace Unit。
SWIT 是一种跟踪数据格式，它记录了应用程序执行时的指令序列和相关数据
STM，系统跟踪宏单元

H743有trace功能

https://pyocd.io/docs/swo_swv.html

SWD时序分析 dpacc access
https://blog.csdn.net/chengdong1314/article/details/79875456/
https://blog.csdn.net/baiyibin0530/article/details/51682179

A23的解释，这个文章非常实用。 【SWD 协议入门指引及实际寄存器读写波形示例】
https://blog.csdn.net/smartpower/article/details/112431969

DAP主要是由DP和AP组件。
DP负责接收外部的JTAG或SW数据，然后转化为对AP的访问，
而对AP的访问，是可以发起memory-mapped的访问。
因此就可以对内部的资源进行访问。

coresight（一）coresight简介
https://zhuanlan.zhihu.com/p/149519501

DAP包括了三个AP

- APB-AP：对挂接到debug APB总线上的内部调试设备的访问
- AHB-AP：对挂载在AHB系统总线上的设备的访问
- JTAG-AP：对JTAG设备的访问。这个是兼容以前较早的ARM处理器，如ARM9。这些较早的处理器内部是用JTAG来调试的。但是现在的ARM处理器，已经不用这种方式，统一用memory-mapped方式进行调试。

目前的ARM soc中，一般至少会包括一个DAP。
而一个DAP可以包括1-256个AP（access port），AP受DP的控制。
只有对AP的访问，才可以转化成memory-mapped总线，对soc的内部资源进行访问。

coresight（二）coresight寄存器
https://zhuanlan.zhihu.com/p/149853267
http://www.lujun.org.cn/?p=2189

使用 jlink 对STM32H7进行指令追踪配置 https://blog.csdn.net/LIAOYUANGANG/article/details/119942755
J-Trace入门系列：2）ART-PI 也能玩转Stream Trace https://club.rt-thread.org/ask/article/3832021de38d0785.html


SWO只能用来做打印吗？程序主动做输出也可以的。

能否自动输出数据？比较PC这些？壁虎板的ISR是怎么实现的？


SWO Trace
https://software-dl.ti.com/ccs/esd/documents/xdsdebugprobes/emu_swo_trace.html

https://developer.arm.com/documentation/101407/0539/Debugging/Code-and-Data-Trace--Cortex-M-/Trace-Features
Trace Interfaces

One or more of the following optional trace interfaces can be implemented on a Cortex-M device:

- The Serial Wire Trace Output (SWO), 
which forwards the trace data either in a "Manchester" encoding 
or a "UART/NRZ" encoding. 
This interface does not support ETM trace data. 
Streaming Trace is supported without ETM instructions.
- The 1-to-4-Pin Synchronous Trace Output (TPIU), 
which supports ETM trace data and has a greater bandwidth than the SWO when using the 4 pin setup. Streaming Trace is supported.

- The Embedded Trace Buffer (ETB), 
which provides on-chip storage of trace data using 32-bit RAM. 
Data is accessed through registers. // 数据通过寄存器访问。类FIFO？
No additional output-pins are needed. // 不用额外的引脚
Streaming Trace is not supported.


	