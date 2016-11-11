<properties
	pageTitle="虚拟机配置静态 IP 以后无法连接的解决办法"
	description="介绍如何解决虚拟机配置静态 IP 以后无法连接的问题"
	services="virtual-machines"
	documentationCenter=""
	authors=""
	manager=""
	editor=""
	tags=""/>

<tags
	ms.service="virtual-machine-aog"
	ms.date="10/27/2016"
	wacn.date="11/10/2016"/>


#虚拟机配置静态 IP 以后无法连接的解决办法

### 问题描述

将虚拟机内部 IP 地址从动态获取改成静态 IP 以后,远程连接失败。

### 问题分析

Azure 虚拟机的内部 IP 默认为动态分配, 由 DHCP 服务自动分配, 在虚拟机的生命周期内, 该 DHCP 租赁是永久存在的, 无论您是否对这个虚拟网络指定了自定义的地址段与否.
另外, 虚拟 IP(VIP) 是您访问虚拟机的一个外部 IP 地址, 用来指定您部署虚拟机的云服务. 在云服务的生命周期内, 该地址同样会保持不变。

### 解决方案

**方案一:**

通过 azure 门户管理,重启虚拟机或者调整虚拟机的尺寸, (比如从中型调整到大型)。

**方案二:**

如果方案一, 依然无法解决连接的问题, 建议您选择删除虚拟机保留磁盘, 然后基于该磁盘新建虚拟机. **特别注意:** 如果您希望保留云服务的虚拟 IP(VIP) , 在删除虚拟机之前, 在该云服务下, 新建一台临时虚拟机. 在云服务下, 只有有至少一台虚拟机存在, 则该云服务的虚拟 IP 就可以得到保留。

**方案三:**

如果上述两方案, 还是无法解决连接的问题, 建议您删除虚拟机保留磁盘, 下载该磁盘到本地, 从本地的 Hyper-V server 上启动, 通过串口的方式进入虚拟机, 将静态 IP 改成动态获取.保存配置以后, 将该磁盘上传, 然后基于该磁盘新建虚拟机。