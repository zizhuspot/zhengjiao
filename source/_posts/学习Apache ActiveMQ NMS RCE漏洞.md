---
title: 关于Apache ActiveMQ NMS RCE漏洞学习分析
date: 2023-09-15 10:50:00
categories:
  - 信息安全
tags:
  - Apache ActiveMQ NMS-RCE漏洞
description: 描述
---
# Apache ActiveMQ NMS-RCE漏洞信息

##  1、漏洞描述
 
This vulnerability allows remote attackers to execute arbitrary code on affected installations of Apache ActiveMQ NMS. Interaction with this library is required to exploit this vulnerability but attack vectors may vary depending on the implementation.

The specific flaw exists within the Body accessor method. The issue results from the lack of proper validation of user-supplied data, which can result in deserialization of untrusted data. An attacker can leverage this vulnerability to execute code in the context of the current process.

该漏洞允许远程攻击者在受影响的 Apache ActiveMQ NMS 安装上执行任意代码。要利用此漏洞，需要与此库进行交互，但攻击向量可能会根据实现的不同而有所不同。

Body 访问器方法中存在特定缺陷。该问题是由于缺乏对用户提供的数据进行适当验证而导致的，这可能会导致不受信任的数据被反序列化。攻击者可以利用此漏洞在当前进程的上下文中执行代码。

## 2、漏洞影响组件及版本：

activemq-nms-openwire< 2.1.0-rc1

Apache.NMS.AMQP.dll （AMQP协议）< 2.1.0

Apache.NMS.ActiveMQ.dll （OpenWire协议）< 2.1.0


## 3、搭建模拟环境

demo

## 4、漏洞分析

（1） NMS的消息格式

Apache.NMS.ActiveMQ.Commands.ActiveMQBlobMessage

Apache.NMS.ActiveMQ.Commands.ActiveMQBytesMessage

Apache.NMS.ActiveMQ.Commands.ActiveMQMapMessage

Apache.NMS.ActiveMQ.Commands.ActiveMQObjectMessage : ActiveMQMessage, IObjectMessage, IMessage

Apache.NMS.ActiveMQ.Commands.ActiveMQStreamMessage

Apache.NMS.ActiveMQ.Commands.ActiveMQTextMessage

其中在处理ActiveMQObjectMessage的消息body时，会对其进行序列化和反序列化，并且未对其做任何限制，导致RCE。

## 通过发送ActiveMQObjectMessage消息时对其进行序列化的过程

调用producer.Send(IObjectMessage)之后会调用ActiveMQMessageMarshaller#LooseMarshal方法处理消息

public override void LooseMarshal(OpenWireFormat wireFormat, object o, BinaryWriter dataOut)

    {
    
      ActiveMQMessage activeMqMessage = (ActiveMQMessage) o;
      
      activeMqMessage.BeforeMarshall(wireFormat);
      
      base.LooseMarshal(wireFormat, o, dataOut);
      
      activeMqMessage.AfterMarshall(wireFormat);
      
    }
    
此时activeMqMessage的type是ActiveMQObjectMessage，

进而调用ActiveMQObjectMessage#BeforeMarshall()方法对消息体序列化，

![image](https://github.com/zizhuspot/www.dagangya.top/assets/134364698/2dd1d6a4-6782-4ba2-9429-61dff90f51a6)


此时序列化的formatter为BinaryFormatter，消息体this.body是构造恶意的对象，最后将序列化的对象存放到content中。

## 如何触发反序列化？

当客户端消费消息时会拿到ActiveMQObjectMessage的类IObjectMessage message = consumer.Receive() as IObjectMessage;

对消息体进行处理时，即调用message.body方法，用getbody方法实现如下：

![image](https://github.com/zizhuspot/www.dagangya.top/assets/134364698/0eb2b1f0-d49a-429d-a2c0-3ae4172f8354)

直接将之前存放序列化对象的content反序列化。

复现如下：使用的链子是TextFormattingRunProperties。

![image](https://github.com/zizhuspot/www.dagangya.top/assets/134364698/be64f96b-3bc5-4921-a5bc-19c912209f4e)


## 补丁分析

使用SerializationBinder限制反序列化类型，支持自定义的白名单列表

![image](https://github.com/zizhuspot/www.dagangya.top/assets/134364698/a464fad2-b870-4c1c-b0fc-1f0bb0c8e005)


## 参考
commit
