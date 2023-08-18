---
title: 2023年hvv中篇了-WPS 相关攻击事件的分析
date: 2023-08-18 22:46:00
categories:
  - [信息安全,2023年hvv行动]
tags:
  - WPS漏洞
  - 恶意代码
description: 微步在线终端 EDR OneSEC 捕获到利用 WPS 进行攻击的事件，该事件会导致：攻击者可以通过 WPS 的相关服务创建恶意文件并执行恶意代码。该事件从 8 月 14 号开始陆续影响了多家企业和单位的少量员工终端电脑，攻击者通过运行阿里云云助手或伪装成阿里云云助手的木马程序，对该终端电脑进行控制。
cover: https://github.com/zizhuspot/www.dagangya.top/assets/134364698/ef634ad6-fe4b-4cc4-a997-0b839ca383aa

---
蜜罐捕获....蜜罐捕获...蜜罐捕获....蜜罐捕获....蜜罐捕获....

据说蜜罐立功了....

抓了很多红队

![image](https://github.com/zizhuspot/www.dagangya.top/assets/134364698/d1122572-4a4b-4278-b0fc-f99fb71208af)

## 不管怎样...HVV算了接近尾声了

一年一度的行动  要等一年  大伙们高兴不

先来说说一个大事记吧....

## 研究称近5成或患精神障碍疾病

近期一个来自昆士兰大学和哈佛医学院的联合小组，在对29个国家超15万名成年受试者的数据进行分析后提出：有50%的人，在他们75岁的时候会至少患上一种精神障碍疾病。其中男性最常见的心理障碍分别是酗酒、抑郁症、特定恐惧症；女性最常见的心理障碍则是抑郁症、特定恐惧症、创伤后应激障碍三种。

近期一个来自昆士兰大学和哈佛医学院的联合小组，在对29个国家超15万名成年受试者的数据进行分析后提出：有50%的人，在他们75岁的时候会至少患上一种精神障碍疾病。其中男性最常见的心理障碍分别是酗酒、抑郁症、特定恐惧症；女性最常见的心理障碍则是抑郁症、特定恐惧症、创伤后应激障碍三种。

反正，生活压力.........大家块自查吧，做好预防..............

这项研究的目标是通过使用世界精神卫生调查的数据，提供有关心理障碍在整个生命周期内发病频率和时间的更新和改进的估计。这些调查在2001年至2022年间进行，包括来自29个国家的18岁或以上的受访者。分析采用了世界卫生组织的复合国际诊断访谈，以评估13种DSM-IV心理障碍的发病年龄、终身患病率和病态风险。

该研究的主要发现包括：

任何心理障碍的终身患病率在男性和女性受访者中均约为29%。

到75岁时，女性受访者的任何心理障碍的病态风险（53.1%）高于男性受访者（46.4%）。

心理障碍首次发作的最常见年龄约为15岁，男性的发病年龄中位数为19岁，女性为20岁。

对于男性来说，滥用酒精障碍和重性抑郁障碍是最常见的障碍，而对于女性来说，重性抑郁障碍和特定恐惧症是最常见的。

![image](https://github.com/zizhuspot/www.dagangya.top/assets/134364698/503537ff-0d35-4059-8155-44bec0a61f68)


## 参加hvv的战友们-心理可还好？？

可别到时候去看意思哈

反正小编我是怕了....

hvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvvhvv

熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜熬夜

![image](https://github.com/zizhuspot/www.dagangya.top/assets/134364698/7a9a40ef-7e9a-43aa-b3e7-7b064892c8d1)

算了那也是75岁以后的事

还是说重点....

## Wps rce之后的供应链投毒

哎 天天的漏洞 忙不过来了

关于 WPS 相关攻击事件的分析说明

事件背景

2023 年 8 月 15 日，微步在线终端 EDR OneSEC 捕获到利用 WPS 进行攻击的事件，该事件会导致：攻击者可以通过 WPS 的相关服务创建恶意文件并执行恶意代码。该事件从 8 月 14 号开始陆续影响了多家企业和单位的少量员工终端电脑，攻击者通过运行阿里云云助手或伪装成阿里云云助手的木马程序，对该终端电脑进行控制。
攻击过程

目前部分攻击环节尚不明确，微步情报局根据 OneSEC EDR 检测到的行为日志、OneDNS 拦截的域名解析日志、TDP 捕获的攻击流量及相关情报，推断攻击过程大致如下：

1、攻击者通过某种手法劫持 WPS 的相关服务。

2、攻击者利用 WPS 相关服务进程将恶意程序或官方阿里云云助手投递至符合条件的受害者主机。

3、WPS 运行的部分进程被恶意程序通过 dll 劫持的手法执行阿里云云助手进行上线权限维持及后续远控行为。

4、攻击者进一步在终端执行后续的恶意代码。

## 影响范围：

经分析确认，该事件只影响 WPS Office for Windows（个人版）且仅限定于特定企业的小部分目标用户。

企业版、XC 环境等其它版本用户均不受影响。另外，私网用户在网络物理隔离状态下，也不受影响。

## 处置建议：

1、根据【关联 IoC】反查企业内曾连接过的终端，确认被控终端；

2、建议员工按照【个人自查】方式进行自查，确认是否被控；

3、确认被控后，对应终端可采取如下措施进行处置：

a) 进入 wps.exe 所在目录，再进入 office6 目录查找删除如下文件 mpr.dll、aliyun_agent_latest_setup.exe、 aliyun_assist_service.exe、iertutil.dll 、mpr.dll 文件；

b) 卸载阿里云盾，默认安装位置为 C:\ProgramData\aliyun\assist\；

c) 通过 WPS 官网下载并安装最新个人版；

 4、在网络边界封禁对应的 IOC，或者应用微步的 OneDNS 云网关和 OneSIG 本地化安全情报网关进行自动化拦截；

 5、更新微步的 TDP、TIP、OneEDR、OneSandbox 确保最新的 IOC 可应用在检测与响应中；

 6、终端侧安装微步的终端 EDR 平台 OneSEC，确保对后续攻击行为的持续检测与响应。

## 威胁情报 IOC

wps-bj-config.oss-cn-beijing.aliyuncs.com

k3b0615l9cmeyvsxz8ohmsm22.oss-cn-shenzhen.aliyuncs.com

k3b0615l9cmeyvsxz8ohmsm22.oss-cn-shenzhen.aliyuncs.com

ceshi1231.s3-us-east-1-accelerate.ossfiles.com

ceshi1231.s3-us-east-1.ossfiles.com

wsgidav.cc645c33006424e22b2806d688cbbee15.cn-beijing.alicontainer.com

crnmfmihtq3lsdg4a9ovpf6m9cjh.oss-cn-shenzhen.aliyuncs.com

s5zcvaulmz8cfa5a12.oss-cn-shenzhen.aliyuncs.com

2rc9t3d47h9lbnacknl.oss-cn-shenzhen.aliyuncs.com

xl6uc35ctrj1dg1t77yqaqu026ht.oss-cn-shenzhen.aliyuncs.com

n5vj9t91l9hex6wlw2y7085coy.oss-cn-shenzhen.aliyuncs.com

182.92.210.30

39.98.177.61

## 个人自查

1、 进入 wps.exe 所在目录，再进入 office6 目录，查找是否存在 mpr.dll、aliyun_agent_latest_setup.exe（或命名为 aliyun_assist_service.exe）文件；

通常目录格式为：

C:\Users\【用户名】\AppData\Local\Kingsoft\WPS Office\【版本号】\office6\aliyun_agent_latest_setup.exe

C:\Users\【用户名】\AppData\Local\Kingsoft\WPS Office\【版本号】\office6\mpr.dll

2、 进入 office6 目录下 addons\everythingsearch\everythingbinary 目录， 查找是否存在 iertutil.dll 文件；

 通常目录格式为：

C:\Users\【用户名】\AppData\Local\Kingsoft\WPS Office\【版本号】\office6\addons\everythingsearch\everythingbinary\iertutil.dll

3、 以上路径都存在对应文件，则说明该机器已失陷。

不管怎样 好好干活

## 我在内网很想你

![image](https://github.com/zizhuspot/www.dagangya.top/assets/134364698/288e0def-e7ae-45ba-aa59-c63471c442f3)




