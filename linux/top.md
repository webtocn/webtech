top命令是Linux下常用的性能分析工具,能够实时显示系统中各个进程的资源占用状况,类似于Windows的任务管理器.

　　下面详细介绍它的使用方法:

　　　　　　　　　　　　　　（实时监控系统资源使用情况图）

![http://pic002.cnblogs.com/images/2012/442643/2012110223525032.jpg](http://pic002.cnblogs.com/images/2012/442643/2012110223525032.jpg)

 

统计信息区前五行是系统整体的统计信息：

　　第一行是任务队列信息,同 uptime  命令的执行结果.其内容如下：

|01:06:48|当前时间|
|:--:|:--:|
|up 1:22|系统运行时间，格式为时:分|
|1 user|当前登录用户数|
|load average: 0.06, 0.60, 0.48|系统负载，即任务队列的平均长度.            三个数值分别为  1分钟、5分钟、15分钟前到现在的平均值.|

　　第二、三行为进程和CPU的信息,当有多个CPU时，这些内容可能会超过两行.内容如下：

|Tasks: 29 total|进程总数|
|:--:|:--:|
|1 running|正在运行的进程数|
|28 sleeping|睡眠的进程数|
|0 stopped|停止的进程数|
|0 zombie|僵尸进程数|
|Cpu(s): 0.3% us|用户空间占用CPU百分比|
|1.0% sy|内核空间占用CPU百分比|
|0.0% ni|用户进程空间内改变过优先级的进程占用CPU百分比|
|98.7% id|空闲CPU百分比|
|0.0% wa|等待输入输出的CPU时间百分比|
|0.0% hi| CPU服务于硬中断所耗费的时间总额|
|0.0% si、0.0%st| CPU服务于软中断所耗费的时间总额、Steal Time|

　　最后两行为内存信息.内容如下：

|Mem: 191272k total|物理内存总量|
|:--:|:--:|
|173656k used|使用的物理内存总量|
|17616k free|空闲内存总量|
|22052k buffers|用作内核缓存的内存量|
|Swap: 192772k total|交换区总量|
|0k used|使用的交换区总量|
|192772k free|空闲交换区总量|
|123988k cached|缓冲的交换区总量.            内存中的内容被换出到交换区,而后又被换入到内存,但使用过的交换区尚未被覆盖,            该数值即为这些内容已存在于内存中的交换区的大小.            相应的内存再次被换出时可不必再对交换区写入.|

进程信息区统计信息区域的下方显示了各个进程的详细信息.

　　首先来认识一下各列的含义：

|序号|列名|含义|
|:--:|:--:|:--:|
|1|PID|进程id|
|2|PPID|父进程id|
|3|RUSER|Real user name|
|4|UID|进程所有者的用户id|
|5|USER|进程所有者的用户名|
|6|GROUP|进程所有者的组名|
|7|TTY|启动进程的终端名.不是从终端启动的进程则显示为 ?|
|8|PR|优先级|
|9|NI|nice值.负值表示高优先级，正值表示低优先级|
|10|P|最后使用的CPU,仅在多CPU环境下有意义|
|11|%CPU|上次更新到现在的CPU时间占用百分比|
|12|TIME|进程使用的CPU时间总计,单位秒|
|13|TIME+|进程使用的CPU时间总计,单位1/100秒|
|14|%MEM|进程使用的物理内存百分比|
|15|VIRT|进程使用的虚拟内存总量,单位kb,VIRT=SWAP+RES|
|16|SWAP|进程使用的虚拟内存中,被换出的大小,单位kb.|
|17|RES|进程使用的、未被换出的物理内存大小,单位kb,RES=CODE+DATA|
|18|CODE|可执行代码占用的物理内存大小,单位kb|
|19|DATA|可执行代码以外的部分(数据段+栈)占用的物理内存大小,单位kb|
|20|SHR|共享内存大小,单位kb|
|21|nFLT|页面错误次数|
|22|nDRT|最后一次写入到现在,被修改过的页面数.|
|23|S|进程状态:            D=不可中断的睡眠状态            R=运行            S=睡眠            T=跟踪/停止            Z=僵尸进程|
|24|COMMAND|命令名/命令行|
|25|WCHAN|若该进程在睡眠,则显示睡眠中的系统函数名|
|26|Flags|任务标志,参考 sched.h|

　　默认情况下仅显示比较重要的  PID、USER、PR、NI、VIRT、RES、SHR、S、%CPU、%MEM、TIME+、COMMAND  几个列！

　　可以通过下面的快捷键来更改显示内容：
　　更改显示内容通过 f 键可以选择显示的内容（按 f 键之后会显示列的列表，按 a-z  即可显示或隐藏对应的列，最后按回车键确定）
　　按 o 键可以改变列的显示顺序（按小写的 a-z 可以将相应的列向右移动，而大写的 A-Z  可以将相应的列向左移动，最后按回车键确定）
　　按大写的 F 或 O 键，然后按 a-z 可以将进程按照相应的列进行排序，而大写的  R 键可以将当前的排序倒转.

 

文章参考：

linux top命令详解
 