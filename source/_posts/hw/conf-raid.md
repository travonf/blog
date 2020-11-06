---
title: 如何通过命令行配置RAID?
date: 2018-12-05 23:15:46
tags: "RAID"
---

# 概述
> LSI公司（LSI Corporation）（NASDAQ：LSI）是一家总部位于加利福尼亚州米尔皮塔斯 (Milpitas) 的半导体和软件领先供应商，其主要产品包括：RAID控制器、SSD控制器、ReadChannel、Preamp、Axxia网络处理器和定制ASIC等，为加速数据存储中心与移动网络性能提供了许多领先的解决方案。
在目前各大知名品牌服务器厂商：IBM、DELL、HP、华为、联想、宝德、浪潮、中科曙光等服务器都使用LSI品牌的阵列卡作为服务器存储控制器，而且其性能其他品牌RAID控制器无与伦比，可见LSI阵列卡的优越性。
LSI阵列卡默认采用基于图形化的BIOS界面来管理，服务器在开机自检界面提示按CTRL+C、CTRL+R、CTRL+H等组合键进入，可使用鼠标或键盘来完成RAID的配置等，这种比较适合少量机器手工配置的场景。如果大量的服务器RAID的配置任采用这种方法就显得力不从心了，不过实际上LSI官方推出了基于命令行的管理软件来实现对RAID控制卡的配置与管理，在操作系统内安装软件，可直接对RAID控制卡的管理，同时也可使用带驱动的Linux内核+脚本即可实现大量服务器批量化自动配置RAID来提高管理效率。
目前LSI官方发布的基于SAS/SATA控制器RAID控制卡产品型号（芯片）有：LSI1064、LSI1086、LSI1078、LSI2008、LSI2208、lSI2308、LSI3008、LSI3108等。
一般地，支持RAID 5的卡，我们称其为阵列卡，都可以使用LSI官方提供的MegaCli、SAS2IRCU等工具来管理，而不支持RAID 5的卡，我们称其为SAS卡，使用lsiutil工具来管理。HP的服务器则使用其特有的hpacucli工具来管理。

<!-- more -->

## Drive Group and Virtual Drive
With the increasing traffic volume of modern data centers, more data needs to run on a single server. When a single drive is insufficient to support system services in terms of capacity and security, multiple drives need to be combined to serve as a visible drive for external entities to meet service requirements. A drive group is a group of physical drives combined as a whole for external entities. Drive groups are the basis for virtual drives.

A virtual drive is a continuous data storage unit divided from a drive group. A virtual drive can be considered an independent drive. Thanks to certain configuration, a virtual drive can provide higher capacity, security, and data redundancy than a physical drive.

A virtual drive can be:
• A complete drive group.
• Multiple complete drive groups.
• Part of a drive group.
• Parts of multiple drive groups (a part is divided from every drive group, and these parts form a virtual drive).

Related conventions:
• A drive group is usually specified as **Drive Group** (DG for short).
• A virtual drive is usually specified as **Virtual Drive**, **Virtual Disk** (VD for short), **Volume**, **Array**, and **Logical Device** (LD for short).

关于DG和VD的区别可以看看上面的解释。

# 检测及修复
## 型号
``` bash
# 检查存储控制器型号
# lspci | grep "RAID bus controller: LSI Logic / Symbios Logic MegaRAID SAS 1078"
01:00.0 RAID bus controller: LSI Logic / Symbios Logic MegaRAID SAS 1078 (rev 04)

# lspci | grep "RAID bus controller: LSI Logic / Symbios Logic MegaRAID SAS 2108"
84:00.0 RAID bus controller: LSI Logic / Symbios Logic MegaRAID SAS 2108 [Liberator] (rev 05)

# lspci | grep "RAID bus controller: LSI Logic / Symbios Logic MegaRAID SAS 2208"
01:00.0 RAID bus controller: LSI Logic / Symbios Logic MegaRAID SAS 2208 [Thunderbolt] (rev 05)

# lspci | grep "Serial Attached SCSI controller: LSI Logic / Symbios Logic SAS2308"
01:00.0 Serial Attached SCSI controller: LSI Logic / Symbios Logic SAS2308 PCI-Express Fusion-MPT
 SAS-2 (rev 05)

# lspci | grep "RAID bus controller: LSI Logic / Symbios Logic MegaRAID SAS-3 3108"
03:00.0 RAID bus controller: LSI Logic / Symbios Logic MegaRAID SAS-3 3108 [Invader] (rev 02)

# lspci | grep "RAID bus controller: Hewlett-Packard Company"
06:00.0 RAID bus controller: Hewlett-Packard Company Smart Array Controller (rev 04)

03:00.0 RAID bus controller: Hewlett-Packard Company Smart Array Gen8 Controllers (rev 01)

# lspci | grep "RAID bus controller: Adaptec"
01:00.0 RAID bus controller: Adaptec AAC-RAID (rev 09)

# lspci | grep "RAID bus controller: 3ware Inc"
08:00.0 RAID bus controller: 3ware Inc 9690SA SAS/SATA-II RAID PCIe (rev 01)
```

## 命令
不同的RAID卡，厂商或型号不同，对应的命令也不同，以下是目前已知的检查命令：

| Corp | Model   | Cmd       |
| ---- | -----   | ---       |
| LSI  | SAS2208 | storcli64 |
| LSI  | SAS2308 | sas2ircu  |
| LSI  | SAS3008 | sas3ircu  |
| LSI  | SAS3108 | storcli64 |
| LSI  | SAS3316 | storcli64 |

## 示例
### storcli64
> storcli已经基本代替了megacli，官方推荐使用storcli管理RAID

#### 检查RAID
通过命令storcli64 /call show可以得到控制器信息
``` bash
# storcli64 /call show
Controller = 0
Status = Success
Description = None

Product Name = SAS2208
Serial Number = FW-AB2M2K4EXVAWC
SAS Address =  5101b5442bcc7000
Mfg. Date = 00/00/00
System Time = 08/22/2018 15:29:27
Controller Time = 08/22/2018 15:29:47
FW Package Build = 23.28.0-0023
BIOS Version = 5.46.02.2_4.16.08.00_0x06060A05
FW Version = 3.400.95-4061
Driver Name = megaraid_sas
Driver Version = 06.810.08.00
Controller Bus Type = N/A
PCI Slot = N/A
PCI Bus Number = 1
PCI Device Number = 0
PCI Function Number = 0
```
``` bash
Drive Groups = 5

# Drive Groups信息可以由以下命令单独列出
# storcli64 /call /dall show

TOPOLOGY :
========

--------------------------------------------------------------------------
DG Arr Row EID:Slot DID Type  State BT       Size PDC  PI SED DS3  FSpace
--------------------------------------------------------------------------
 0 -   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 0 0   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 0 0   0   0:0      1   DRIVE Onln  N  744.125 GB dflt N  N   none -
 1 -   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 1 0   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 1 0   0   0:1      4   DRIVE Onln  N  744.125 GB dflt N  N   none -
 2 -   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 2 0   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 2 0   0   0:2      3   DRIVE Onln  N  744.125 GB dflt N  N   none -
 3 -   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 3 0   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 3 0   0   0:3      8   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 -   -   -        -   RAID5 Optl  N    5.085 TB dflt N  N   none N
 4 0   -   -        -   RAID5 Optl  N    5.085 TB dflt N  N   none N
 4 0   0   0:4      2   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   1   0:5      7   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   2   0:6      9   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   3   0:7      11  DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   4   0:8      6   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   5   0:9      5   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   6   0:10     12  DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   7   0:11     10  DRIVE Onln  N  744.125 GB dflt N  N   none -
--------------------------------------------------------------------------

DG=Disk Group Index|Arr=Array Index|Row=Row Index|EID=Enclosure Device ID
DID=Device ID|Type=Drive Type|Onln=Online|Rbld=Rebuild|Dgrd=Degraded
Pdgd=Partially degraded|Offln=Offline|BT=Background Task Active
PDC=PD Cache|PI=Protection Info|SED=Self Encrypting Drive|Frgn=Foreign
DS3=Dimmer Switch 3|dflt=Default|Msng=Missing|FSpace=Free Space Present

# 这个地方的PDC就是disk cache, 可选On\Off\Default三种选项, 对应为enbl\dsbl\dflt
```
``` bash
Virtual Drives = 5

# Virtual Drives信息可以由以下命令单独列出
# storcli64 /call /vall show

VD LIST :
=======

---------------------------------------------------------------
DG/VD TYPE  State Access Consist Cache sCC       Size Name
---------------------------------------------------------------
0/0   RAID0 Optl  RW     Yes     NRWBD -   744.125 GB
1/1   RAID0 Optl  RW     Yes     NRWBD -   744.125 GB
2/2   RAID0 Optl  RW     Yes     NRWBD -   744.125 GB
3/3   RAID0 Optl  RW     Yes     NRWBD -   744.125 GB
4/4   RAID5 Optl  RW     Yes     RaWBD -     5.085 TB 6gRcrbya
---------------------------------------------------------------

Cac=CacheCade|Rec=Recovery|OfLn=OffLine|Pdgd=Partially Degraded|dgrd=Degraded
Optl=Optimal|RO=Read Only|RW=Read Write|B=Blocked|Consist=Consistent|
Ra=Read Ahead Adaptive|R=Read Ahead Always|NR=No Read Ahead|WB=WriteBack|
AWB=Always WriteBack|WT=WriteThrough|C=Cached IO|D=Direct IO|sCC=Scheduled
Check Consistency

# 可以看出有5个VD，VD 0-3为RAID0，State为Optimal，Access Policy为RW，
# Read Policy为NR，Write Policy为WB，Cache Policy为Direct IO
# VD4做了RAID5，Read Policy为Ra，Write Policy为WB，Cache Policy为Direct IO
```

| **设置项**        | 可选值  |        |         |         |
|------------------|--------|--------|---------|---------|
| **accesspolicy** | RW     | RO     | Blocked | RmvBlkd |
| **rdcache**      | RA     | NoRA   |         |         |
| **wrcache**      | WT     | WB     | AWB     |         |
| **pdcache**      | On     | Off    | Default |         |
| **iopolicy**     | Cached | Direct |         |         |
``` bash
Physical Drives = 12

# Physical Drives信息可以由以下命令单独列出
# storcli64 /call /eall /sall show

PD LIST :
=======

----------------------------------------------------------------------------
EID:Slt DID State DG       Size Intf Med SED PI SeSz Model               Sp
----------------------------------------------------------------------------
0:0       1 Onln   0 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:1       4 Onln   1 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:2       3 Onln   2 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:3       8 Onln   3 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:4       2 Onln   4 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:5       7 Onln   4 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:6       9 Onln   4 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:7      11 Onln   4 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:8       6 Onln   4 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:9       5 Onln   4 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:10     12 Onln   4 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
0:11     10 Onln   4 744.125 GB SATA SSD N   N  512B INTEL SSDSC2BB800G6 U
----------------------------------------------------------------------------

EID-Enclosure Device ID|Slt-Slot No.|DID-Device ID|DG-DriveGroup
DHS-Dedicated Hot Spare|UGood-Unconfigured Good|GHS-Global Hotspare
UBad-Unconfigured Bad|Onln-Online|Offln-Offline|Intf-Interface
Med-Media Type|SED-Self Encryptive Drive|PI-Protection Info
SeSz-Sector Size|Sp-Spun|U-Up|D-Down|T-Transition|F-Foreign

```
``` bash

# BBU信息可以由以下命令单独列出
# storcli64 /call /bbu show

BBU_Info :
========

-----------------------------------------------------------------------
Model  State   RetentionTime Temp Mode MfgDate    Next Learn
-----------------------------------------------------------------------
CVPM02 Optimal 0 hour(s)     21C  0    2015/11/14 2018/08/23  10:48:12
-----------------------------------------------------------------------
```



#### 创建和删除RAID

**命令功能**
创建、删除RAID。

**命令格式**
``` bash
storcli64 /c`controller_id` add vd r`level` size=`capacity` drives=`enclosure_id`:`startid-endid`
```
``` bash
storcli64 /c`controller_id`/v`raid_id` del
```

**参数说明**

|参数          |参数说明                       |取值|
|--------------|-----------------------------|----|
|controller_id |RAID卡的ID                    |–   |
|level         |要配置的RAID级别               |–   |
|capacity      |要配置的RAID容量               |–   |
|enclosure_id  |硬盘所在Enclosure的ID          |–   |
|startid-endid |要加入RAID的硬盘的起始和结束ID   |–   |
|raid_id       |要删除的RAID的ID               |–   |
**使用指南**
无

**使用实例**
``` bash
# 创建RAID 0

domino:~# ./storcli64 /c0 add vd r0 size=100GB drives=252:0-3
Controller = 0
Status = Success
Description = Add VD Succeeded
```
``` bash
# 删除RAID

domino:~# ./storcli64 /c0/v0 del
Controller = 0
Status = Success
Description = Delete VD Succeeded
```


#### 设置RAID组的Cache读写属性

**命令功能**
设置RAID组的Cache读写属性。

**命令格式**
``` bash
storcli64 /c`controller_id`/v`raid_id` set wrcache=`mode`
```

**参数说明**

|参数               |参数说明          |取值|
|-------------------|-----------------|---|
|controller_id      |RAID卡的ID        |–  |
|raid_id            |待设置的RAID的ID   |–  |
|mode               |Cache读写模式      |wt：当磁盘子系统接收到所有传输数据后，控制器将给主机返回数据传输完成信号。 |
|                   |                  |wb：控制器Cache收到所有的传输数据后，将给主机返回数据传输完成信号。      |
|                   |                  |awb：在RAID卡无电容或电容损坏的情况下，强制使用“wb”模式。              |

**使用指南**
无

**使用实例**
``` bash
# 设置Cache读写模式为“wt”。

domino:~# ./storcli64 /c0/v0 set wrcache=wt
Controller = 0
Status = Success
Description = None
Details Status :
==============
---------------------------------------
VD Property Value Status  ErrCd ErrMsg
---------------------------------------
 0 wrCache  WT    Success     0 -
---------------------------------------
```



#### disk cache
``` bash
# 查看disk cache信息
# storcli64 /c0 /dall show
Controller = 0
Status = Success
Description = Show Diskgroup Succeeded


TOPOLOGY :
========

--------------------------------------------------------------------------
DG Arr Row EID:Slot DID Type  State BT       Size PDC  PI SED DS3  FSpace
--------------------------------------------------------------------------
 0 -   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 0 0   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 0 0   0   0:0      1   DRIVE Onln  N  744.125 GB dflt N  N   none -
 1 -   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 1 0   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 1 0   0   0:1      4   DRIVE Onln  N  744.125 GB dflt N  N   none -
 2 -   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 2 0   -   -        -   RAID0 Optl  N  744.125 GB dflt N  N   none N
 2 0   0   0:2      3   DRIVE Onln  N  744.125 GB dflt N  N   none -
 3 -   -   -        -   RAID0 Optl  N  744.125 GB dsbl N  N   none N
 3 0   -   -        -   RAID0 Optl  N  744.125 GB dsbl N  N   none N
 3 0   0   0:3      8   DRIVE Onln  N  744.125 GB dsbl N  N   none -
 4 -   -   -        -   RAID5 Optl  N    5.085 TB dflt N  N   none N
 4 0   -   -        -   RAID5 Optl  N    5.085 TB dflt N  N   none N
 4 0   0   0:4      2   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   1   0:5      7   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   2   0:6      9   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   3   0:7      11  DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   4   0:8      6   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   5   0:9      5   DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   6   0:10     12  DRIVE Onln  N  744.125 GB dflt N  N   none -
 4 0   7   0:11     10  DRIVE Onln  N  744.125 GB dflt N  N   none -
--------------------------------------------------------------------------

DG=Disk Group Index|Arr=Array Index|Row=Row Index|EID=Enclosure Device ID
DID=Device ID|Type=Drive Type|Onln=Online|Rbld=Rebuild|Dgrd=Degraded
Pdgd=Partially degraded|Offln=Offline|BT=Background Task Active
PDC=PD Cache|PI=Protection Info|SED=Self Encrypting Drive|Frgn=Foreign
DS3=Dimmer Switch 3|dflt=Default|Msng=Missing|FSpace=Free Space Present

# 上面的PDC就是disk cache, 可选On\Off\Default三种选项, 对应为enbl\dsbl\dflt

# 设定pdcache
storcli /c`x`/v`x` set pdcache=`On`|`Off`|`Default`
```



#### 自动rebuild
``` bash
# 使用如下命令检查auto rebuild的信息
# storcli64 /call show autorebuild
Controller = 0
Status = Success
Description = None


Controller Properties :
=====================

------------------
Ctrl_Prop   Value
------------------
AutoRebuild OFF
------------------

# 开启/关闭auto rebuild
storcli /c`x` set autorebuild=<`on`|`off`>
```



#### 设置启动项

**命令功能**
设置虚拟磁盘或物理硬盘为启动项。

**命令格式**
``` bash
storcli64 /c`controller_id`/v`vd_id` set bootdrive=on
storcli64 /c`controller_id`/e`enclosure_id`/s`slot_id` set bootdrive=on
```

**参数说明**

|参数          |参数说明              |取值|
|--------------|--------------------|----|
|controller_id |RAID卡的ID           |–   |
|vd_id         |待设置的虚拟磁盘的ID   |–   |
|enclosure_id  |硬盘所在Enclosure的ID |–   |
|slot_id       |硬盘槽位号            |–   |

**使用指南**
无

**使用实例**

``` bash
# 设置VD0为启动项

domino:~# ./storcli64 /c0/v0 set bootdrive=on
Controller = 0
Status = Success
Description = Noe
Detailed Status :
===============
----------------------------------------
VD Property   Value Staus  ErrCd ErrMsg
----------------------------------------
 0 Boot Drive On    Success    0 -
----------------------------------------
```
``` bash
# 设置slot 7硬盘为启动项

domino:~# ./storcli64 /c0/e252/s7 set bootdrive=on
Controller = 0
Status = Success
Description = Noe
Controller Properties :
=====================
-------------------
Ctrl_Prop Value
-------------------
BootDrive PD:252_7
-------------------
```

``` bash
# 列出bootdrive信息
storcli /cx show bootdrive

# 指定某组为bootdrive
storcli /cx/vx set bootdrive=<on|off>

# 指定某盘为bootdrive
storcli /cx[/ex]/sx set bootdrive=<on|off>
```
``` bash
# 检查启动盘
# storcli64 /c0 show bootdrive
Controller = 0
Status = Success
Description = None


Controller Properties :
=====================

----------------
Ctrl_Prop Value
----------------
BootDrive VD:0
----------------
```



### sas2ircu
#### 设置指定RAID组作为第一启动项

**命令功能**
设置指定RAID组作为第一启动项。

**命令格式**
``` bash
sas2ircu `controller_id` bootir `volume_id`
```

**参数说明**

|参数            |参数说明                    |取值|
|---------------|---------------------------|---|
|controller_id  |RAID卡的ID                  |–  |
|volume_id      |待设置为第一启动项的RAID组ID   |–  |

**使用指南**
无

**使用实例**
``` bash
# 设置指定RAID组作为第一启动项。
domino:~# ./sas2ircu 0 bootir 322
Avago Technologies SAS2 IR Configuration Utility.
Version 13.00.00.00 (2016.03.08)
Copyright (c) 2009-2016 Avago Technologies. All rights reserved.

SAS2IRCU: Command bootir Completed Successfully.
SAS2IRCU: Utility Completed Successfully.
```


#### 设置指定单盘作为第一启动项

**命令功能**
设置指定单盘作为第一启动项。

**命令格式**
``` bash
sas2ircu `controller_id` bootencl `enclosure_id`:`slot_id`
```

**参数说明**

|参数            |参数说明              |取值|
|---------------|---------------------|----|
|controller_id  |RAID卡的ID            |–  |
|enclosure_id   |硬盘所在Enclosure的ID  |–  |
|slot_id        |硬盘槽位号             |–  |

**使用指南**
	无

**使用实例**
``` bash
# 设置指定单盘作为第一启动项
domino:~# ./sas2ircu 0 bootencl 1:4
Avago Technologies SAS2 IR Configuration Utility.
Version 13.00.00.00 (2016.03.08)
Copyright (c) 2009-2016 Avago Technologies. All rights reserved.

SAS2IRCU: Command BOOTENCL Completed Successfully.
SAS2IRCU: Utility Completed Successfully.
```


### sas3ircu
用法同sas2ircu

# 问题
辨别RAID厂商、型号是个大问题，当前采用严格匹配方式，未适配的型号统统忽略了，比如说下面这些：
58:00.0 RAID bus controller: LSI Logic / Symbios Logic Device 0014 (rev 01)

# 参考
StorCLI Reference Manual - Broadcom
Disk Controller parameters -- Best practice
未完待续...
