---
layout: post
title: MAVLINK速览
category: 技术
tags: MAVLINK apm
keywords:
description:
---

Micro Air Vehicle Link由ETH的Lorenz Meier提出，字面意思是小型飞行器链路协议，主要用于控制无人机设备，后来也被用在机器人系统中。起初是伴随着PX4的开源工程提出，期间得到了PX4，PIXHAWK，APM和Parrot等平台的测试，逐渐成为了无人设备通信的主流标准，在机器人操作系统ROS上也有它应用的实例。

感兴趣的同学可以点[Lorenz的简历][1]看看，09年硕士期间开展了Pixhawk开源硬件工程，现在博士在读，研究移动平台视觉，很厉害的哥们。

##通俗定义

Mavlink用于地面站和无人设备之间的通信，是个非常轻量级的协议，由包头和载荷组成。

可以类比TCP/IP协议，只不过它只有一级罢了。是的，它只有物理层，简洁明快。这个物理层设备是UART，可以是有线的RS232/USB，也可以是无线Radio。这个单层的包头规定了消息的源，组件编号，类型等，指明消息是发送给谁的。

以太网协议中，数据报文装帧，然后通过网卡驱动把它编码成比特流发送出去。接收端网卡将比特流解码成帧，再由用户程序拿出数据。

![此处输入图片的描述][2]

在Mavlink中，发送接收过程类似。不同的是硬件接口由网卡换成了串口。

![此处输入图片的描述][3]

##消息结构

消息17字节 = 6字节头部 + 9字节载荷 + 2字节校验和

6字节头部包括：

1. 消息头，永远0xFE
2. 消息长度，9
3. 序列号，0~255之间轮转，0x4e表示之前的序号是0x4d
4. 系统ID，哪个系统发的消息，一般指地面站或无人设备
5. 组件ID，系统的那个组件发的消息，主要为以后扩展，目前还没被用起来
6. 消息ID，消息类型

消息处理模块需要检查消息校验和。需要注意的是，错误率与波特率反相关，这也是为何3DR的数传波特率都设为57600的原因，我猜是工程试验得到的一个折中。

载荷中的数据是raw data，消息处理软件需要将raw data按照约定好的协议转换成数据结构。

##消息类型

1. MAVLINK_MSG_ID_HEARTBEAT 0：心跳消息，确保地面站和无人设备处于连接状态，断开则触发failsafe处理
2. MAVLINK_MSG_ID_REQUEST_DATA_STREAM 66:Sensors, RC channels, GPS position, status, Extra 1/2/3
3. MAVLINK_MSG_ID_COMMAND_LONG 76:Loiter unlimited, RTL, Land, Mission start, Arm/Disarm, Reboot

. . .
不再赘述，具体参见参考资料中的pdf

##代码组成

在APM代码中，gcs相关的程序是几个loop任务。ardupilot/ArduCopter/Arducopter.pde中：

{% highlight c %}
static const AP_Scheduler::Task scheduler_tasks[] PROGMEM = {
. . .
. . .
{ update_notify, 2, 100 },
{ one_hz_loop, 100, 420 },
{ gcs_check_input, 2, 550 },
{ gcs_send_heartbeat, 100, 150 },
{ gcs_send_deferred, 2, 720 },
{ gcs_data_stream_send, 2, 950 },
. . .
. . .
. . .
{% endhighlight %}

1. gcs_check_input：消息处理循环
2. gcs_send_heartbeat：发送心跳消息
3. gcs_send_deferred：Mavlink中有个超时重发队列，每次发送消息都会把重发队列再排空一遍，这类消息是MSG_RETRY_DEFERRED，真实情况是不会发送这条消息，只会借助这条消息将队列重发一遍
4. gcs_data_stream_send：发送Mavlink消息

####参考资料

1. [MavLink Tutorial for Absolute Dummies][4]


  [1]: http://www.inf.ethz.ch/personal/lomeier/
  [2]: http://images.cnitblog.com/blog/549839/201310/13181705-d195bfedccba41ad9c66df4df38eba76.png
  [3]: http://qgroundcontrol.org/_media/dev/qgroundcontrol-architecture.png
  [4]: http://api.ning.com/files/i*tFWQTF2R*7Mmw7hksAU-u9IABKNDO9apguOiSOCfvi2znk1tXhur0Bt00jTOldFvob-Sczg3*lDcgChG26QaHZpzEcISM5/MAVLINK_FOR_DUMMIESPart1_v.1.1.pdf