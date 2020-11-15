---
title: 如何通过命令行配置BIOS?
date: 2018-06-01 08:00:00
updated: 2018-06-01 08:00:00
tags: "BIOS"
categories: "Hardware"
---

# 概述

目前全球只有四家独立 BIOS 供应商，  
曾经的 Award Software 与 General Software 均被 Phoenix Technologies 收购，  
Microid Research 被 Unicore Software 收购，  
SystemSoft 被 Insyde Software 收购。

| Company              | Remark                                                             |
| -------------------- | ------------------------------------------------------------------ |
| Phoenix Technologies | 美国凤凰科技。                                                     |
| American Megatrends  | 美国安迈科技，目前为全球最大的 BIOS 供应商。之前曾被凤凰科技超过。 |
| Insyde Software      | 台湾系微公司。                                                     |
| Byosoft              | 新兴厂商，中国大陆的百敖软件公司。                                 |

华为的服务器 BIOS vendor 为 Insyde，浪潮为 AMI，暂未发现使用其他厂商的 BIOS，另外两家 BIOS 暂未发现服务器使用。

<!-- more -->

# 检测及修复方法

不同的 BIOS 生厂商配置不同，检测与修复采用的方式不尽相同。

## 检查服务器生产商

通过以下命令检查 Manufacturer 字段值

```bash
dmidecode --type chassis
```

### 华为 / Huawei

```bash
# dmidecode 2.11
SMBIOS 2.8 present.
# SMBIOS implementations newer than version 2.7 are not
# fully supported by this version of dmidecode.

Handle 0x001F, DMI type 3, 25 bytes
Chassis Information
	Manufacturer: Huawei
	Type: Rack Mount Chassis
	Lock: Not Present
	Version: H31.2B
	Serial Number: To be filled by O.E.M.
	Asset Tag: TD070100368095
	Boot-up State: Safe
	Power Supply State: Safe
	Thermal State: Safe
	Security Status: None
	OEM Information: 0x00000000
	Height: 2 U
	Number Of Power Cords: 2
	Contained Elements: 0
	SKU Number: Not Specified
```

### 浪潮 / Inspur

```bash
# dmidecode 2.11
SMBIOS 2.8 present.
# SMBIOS implementations newer than version 2.7 are not
# fully supported by this version of dmidecode.

Handle 0x0003, DMI type 3, 25 bytes
Chassis Information
	Manufacturer: Inspur
	Type: Rack Mount Chassis
	Lock: Not Present
	Version: N32.2B
	Serial Number: 00
	Asset Tag: TD070100554754
	Boot-up State: Safe
	Power Supply State: Safe
	Thermal State: Safe
	Security Status: None
	OEM Information: 0x00000000
	Height: Unspecified
	Number Of Power Cords: 1
	Contained Elements: 1
		<OUT OF SPEC> (0)
	SKU Number: To be filled by O.E.M.
```

## 检查 BIOS 提供商及版本

通过以下命令检查 Vendor、Version 字段值

```bash
dmidecode --type bios
```

### Insyde Corp.

#### 1.69

```bash
# dmidecode 2.11
SMBIOS 2.8 present.
# SMBIOS implementations newer than version 2.7 are not
# fully supported by this version of dmidecode.

Handle 0x001D, DMI type 0, 24 bytes
BIOS Information
	Vendor: Insyde Corp.
	Version: 1.69
	Release Date: 10/31/2015
	Address: 0xE0000
	Runtime Size: 128 kB
	ROM Size: 16384 kB
	Characteristics:
		PCI is supported
		BIOS is upgradeable
		BIOS shadowing is allowed
		Boot from CD is supported
		Selectable boot is supported
		EDD is supported

		Japanese floppy for NEC 9800 1.2 MB is supported (int 13h)
		Japanese floppy for Toshiba 1.2 MB is supported (int 13h)
		5.25"/360 kB floppy services are supported (int 13h)
		5.25"/1.2 MB floppy services are supported (int 13h)
		3.5"/720 kB floppy services are supported (int 13h)
		3.5"/2.88 MB floppy services are supported (int 13h)
		8042 keyboard services are supported (int 9h)
		CGA/mono video services are supported (int 10h)
		ACPI is supported
		USB legacy is supported
		BIOS boot specification is supported
		Targeted content distribution is supported
		UEFI is supported
	BIOS Revision: 1.0

Handle 0x0026, DMI type 13, 22 bytes
BIOS Language Information
	Language Description Format: Long
	Installable Languages: 2
		en|US|iso8859-1
		zh|CN|unicode
	Currently Installed Language: en|US|iso8859-1
```

### American Megatrends Inc.

#### 4.10

```bash
# dmidecode 2.11
SMBIOS 2.8 present.
# SMBIOS implementations newer than version 2.7 are not
# fully supported by this version of dmidecode.

Handle 0x0000, DMI type 0, 24 bytes
BIOS Information
	Vendor: American Megatrends Inc.
	Version: 4.10
	Release Date: 09/22/2015
	Address: 0xF0000
	Runtime Size: 64 kB
	ROM Size: 8192 kB
	Characteristics:
		PCI is supported
		BIOS is upgradeable
		BIOS shadowing is allowed
		Boot from CD is supported
		Selectable boot is supported
		BIOS ROM is socketed
		EDD is supported
		5.25"/1.2 MB floppy services are supported (int 13h)
		3.5"/720 kB floppy services are supported (int 13h)
		3.5"/2.88 MB floppy services are supported (int 13h)
		Print screen service is supported (int 5h)
		Serial services are supported (int 14h)
		Printer services are supported (int 17h)


		ACPI is supported
		USB legacy is supported
		BIOS boot specification is supported
		Targeted content distribution is supported
		UEFI is supported
	BIOS Revision: 5.6

Handle 0x0097, DMI type 13, 22 bytes
BIOS Language Information
	Language Description Format: Long
	Installable Languages: 1
		en|US|iso8859-1

	Currently Installed Language: en|US|iso8859-1
```

#### 1.01.10

```bash
# dmidecode 2.12-dmifs
SMBIOS 2.8 present.

Handle 0x0000, DMI type 0, 24 bytes
BIOS Information
	Vendor: American Megatrends Inc.
	Version: 1.01.10
	Release Date: 07/08/2017
	Address: 0xF0000
	Runtime Size: 64 kB
	ROM Size: 8192 kB
	Characteristics:
		PCI is supported
		BIOS is upgradeable
		BIOS shadowing is allowed
		Boot from CD is supported
		Selectable boot is supported
		BIOS ROM is socketed
		EDD is supported
		5.25"/1.2 MB floppy services are supported (int 13h)
		3.5"/720 kB floppy services are supported (int 13h)
		3.5"/2.88 MB floppy services are supported (int 13h)
		Print screen service is supported (int 5h)
		8042 keyboard services are supported (int 9h)
		Serial services are supported (int 14h)
		Printer services are supported (int 17h)
		ACPI is supported
		USB legacy is supported
		BIOS boot specification is supported
		Targeted content distribution is supported
		UEFI is supported
	BIOS Revision: 5.11

Handle 0x0095, DMI type 13, 22 bytes
BIOS Language Information
	Language Description Format: Long
	Installable Languages: 2
		en|US|iso8859-1
		zh|CN|unicode
	Currently Installed Language: en|US|iso8859-1
```

### Others

| Manufacturer                   | BIOS Vendor              | BIOS Version     |
| ------------------------------ | ------------------------ | ---------------- |
| Dell Inc.                      | Dell Inc.                | 1.4.5            |
| Dell Inc.                      | Dell Inc.                | 1.4.5            |
| FOXCONN                        | American Megatrends Inc. | 6G104020         |
| FOXCONN                        | American Megatrends Inc. | 6G104020         |
| FOXCONN                        | American Megatrends Inc. | 6G104020         |
| FOXCONN                        | American Megatrends Inc. | 6G104020         |
| HPE                            | HPE                      | U30              |
| HPE                            | HPE                      | U30              |
| HPE                            | HPE                      | U30              |
| Huawei                         | INSYDE Corp.             | 0.55             |
| Inspur                         | Inspur                   | 3.0.25           |
| Inspur                         | Inspur                   | 3.0.25           |
| Lenovo                         | Lenovo                   | -[IVE116U-1.22]- |
| Lenovo                         | Lenovo                   | -[IVE116U-1.22]- |
| Lenovo                         | Lenovo                   | -[IVE116U-1.22]- |
| New H3C Technologies Co., Ltd. | American Megatrends Inc. | 1.00.26          |
| New H3C Technologies Co., Ltd. | American Megatrends Inc. | 1.00.26          |
| Sugon                          | American Megatrends Inc. | 0JGST025         |

# 命令帮助

> 查找各种资料发现，  
> Huawei 服务器使用 Insyde BIOS，可以使用`uniCfg`命令在线读取相关 BIOS item 及写入配置，  
> Inspur 服务器使用 AMI BIOS，官方提供`AMISCE`工具在线配置 BIOS，  
> 这个工具具体命令在不同操作系统及架构下名称不同，如 Linux x64 叫`SCELNX_64`，Windows x64 叫`scewin_64`，  
> 目前服务器大部分使用的都是 Linux OS，我们当前关注 LNX 即可。

## uniCfg

```bash
#/bin/uniCfg -h

Usage: uniCfg [OPTION]
 -v
 -V
      Display version of this tool


 -i
 -I
      Display generic information


 -c
 -C
      Clear BIOS Setup Configuration
      Notice: It must be reboot or power off after clear.
              1. Read/Write Configuration value after clear without reboot/poweroff,it will report error
              2. Clear BIOS Setup Configuration again without reboot/poweroff, it will report error

 -r <Configuration>...
 -R <Configuration>...
      Read Configuration value from BIOS Setup, the Configuration is case sensitive.
      For example:
      ./uniCfg -r PowerSaving
      ./uniCfg -r BootOrder
      It supports read more Configuration items at once, for example:
      ./uniCfg -r BootOrder PowerSaving CustomPowerPolicy


 -w <Configuration:value>...
 -W <Configuration:value>...
      Write Configuration value to BIOS Setup, the Configuration is case sensitive.
      Notice:
      1. Value must be numeric, can not be the value description (like as Enable/Disable).
         If the number bigger than ten, use 0x (hex) to start.
      2. BootOrder is special, the value use four number, like 1203, 2301, 0123, 3120 and so on.
         0:PXE/1:HDD/2:CD DVD/3:OTHER.
      For example:
      ./uniCfg -w PowerSaving:1
      ./uniCfg -w BootOrder:2301
      It supports write more Configuration items at once, for example:
      ./uniCfg -w BootOrder:2301 PowerSaving:1 CustomPowerPolicy:1

 -rf [FileName]
 -RF [FileName]
      Read Configuration from file, then use the Configuration to read value from BIOS Setup.
      The Configuration is case sensitive.
      Notice:
      1. If omit the file argument, it will use the Reference to read the Configuration.
      2. If use the file argument, the file content should follow below two format,
         and only have one Configuration in one line.
           Format 1 example:
           PowerSaving
           BootOrder
           CustomPowerPolicy
           Format 2 example:
           PowerSaving:1
           BootOrder:2301
           CustomPowerPolicy:1
      3. The result of the Configuration value will be saved as uniCfg.ini file,
         it will replace the old uniCfg.ini if it exist.

 -wf [FileName]
 -WF [FileName]
      Read Configuration and value from file, then write the Configuration and value to BIOS Setup.
      The Configuration is case sensitive.
      Notice:
      1. If omit the file argument, it will use the uniCfg.ini file as the file argument.
         At this case, if the uniCfg.ini file is not exist, it will report error.
      2. If use the file argument, the file content should follow below format,
         only have one Configuration in one line.
           Format example:
           PowerSaving:1
           BootOrder:2301
           CustomPowerPolicy:1

 -O Setup/SetupDefault/CustomDefault
      Get each item config value form Setup/SetupDefault/CustomDefault, the result will store in ../custom.
 SetCustomDefault
      Store current configuration to CustomDefault.
 LoadCustomDefault
      Retore Customdefault configuration to Setup.

 -hh
 -HH
      Print the Reference, include Configuration Reference, and Dependence Reference.
      The Configuration Reference format show as below:
      "Configuration":"value1:Description1/value2:Description2"  -- "BIOS Setup Name"

 other option:

 customset.ini      Configure BIOS Setup by customset.ini file, mostly, it use for production line.

 -rb <FileName>
 -RB <FileName>
      Read Setup Data to Bin file

 -wb <FileName>
 -WB <FileName>
      Write Bin file to setup data

Warning:
          1. Some Menu has subMenu, when set subMenu, Menu must be enabled;
             When Menu is disabled, subMenu should be disabled too.
             run option -hh or -HH to see which Menu has subMenu.(Dependence Reference)
          2. To make sure the setting function is OK, it must be reboot after setting.
          3. It may cause power on unnormally if the setting is not correctly.

 time 260.00 (ms).
```

根据以上命令帮助可以得出脚本开发的大致思路，

1. 通过`uniCfg -rf [FileName]`方式读取关注的全部配置，
2. 然后解析到 dict 中，
3. 与预设值逐一比对，
4. 结果一致则通过，
5. 不一致尝试通过`uniCfg -w <Configuration>`方式更新，
6. 更新失败则交由人工负责，或者找出解决办法，更新脚本。

那么问题来了，`[FileName]`文件内容中各个检查项名称是什么？
目前已知情况，不同的硬件架构检查项名称不同

## SCELNX_64

> SCE(Setup Control Environment)工具是一种命令行工具，提供一种简单的方法在 EFI, DOS, Linux 或者 Windows 环境下去更新 BIOS NVRAM 变量。用户可以通过 AMISCE 工具从 BIOS 中直 接提取几乎所有的 Setup 变量，对提取出变量的脚本文件，通过文本编译器等工具修改后再更 新到 BIOS。

```bash
Default Usage:
	SCELNX_64 /o /s <NVRAM Script File> [/h <HII dump file>] [/sd <Duplicate Script File>] [/b] [/v] [/q] [/lang [Lang Code]] [/sp] [/g] [/a] [/d] [/ndef] [/ce] [/hb]
	SCELNX_64 /i /s <NVRAM Script File> [/ds] [/dm] [/b] [/r] [/lang [Lang Code]] [/d] [/cpwd | /cpwds | /cpwde <Current Admin Password>] [/hb]

To Export PLDM Tables:
	SCELNX_64 /o /p <PLDM File Name> [/sp] [/g] [/b] [/ndef] [/hb]

To Import PLDM Tables:
	SCELNX_64 /i /p <PLDM File Name> [/b] [/hb]

Single Question Update Usage:
	SCELNX_64 /i [/cpwd | /cpwds | /cpwde <Current Admin Password>] [/lang <Lang Code>] /ms <question map string> /qv <question value> [/bt <device type>] [/q] [/d] [/dm] [/ds] [/hb]

	Note: Values of type numeric will be taken as hex always (0x prefix optional).

Single Question Export Usage:
	SCELNX_64 /o [/lang <Lang Code>] /ms <question map string> [/q] [/d] [/hb]

To set new user and new admin password for Setup:
	SCELNX_64 /cpwd <current admin password> /apwd <new admin Password> [/hb]
	SCELNX_64 /cpwd <current admin password> /upwd <new user Password> [/hb]
	SCELNX_64 /cpwd <current admin password> /apwd <new admin Password> /upwd <new user password> [/hb]

To set new user and new admin password of type Scan Code for Setup:
	SCELNX_64 /cpwds <current admin password> /apwds <new admin Password> [/hb]
	SCELNX_64 /cpwds <current admin password> /upwds <new user Password> [/hb]
	SCELNX_64 /cpwds <current admin password> /apwds <new admin Password> /upwds <new user password> [/hb]

To set new user and new admin password of type EFI Key for Setup:
	SCELNX_64 /cpwde <current admin password> /apwde <new admin Password> [/hb]
	SCELNX_64 /cpwde <current admin password> /upwde <new user Password> [/hb]
	SCELNX_64 /cpwde <current admin password> /apwde <new admin Password> /upwde <new user password> [/hb]

Raw Mode Usage:
	SCELNX_64 /o [/c] /l <listing file> /n <NVRAM Raw File> /h <HII dump file> [/d] [/hb]
	SCELNX_64 /i /l <listing file> /n <NVRAM Raw File> [/f] [/d] [/cpwd | /cpwds | /cpwde <Current Admin Password>] [/hb]
	where,
	   /o - Indicates Dump NVRAM data for Variables found in Listing File
	   /i - Indicates Import modified Variable data found in Listing File
	   to the NVRAM
	   /c - Optional, Creates Variable Listing File containing information
	   about all the variables found in NVRAM
	   /l - Indicates Variable Listing File
	   /n - Indicates NVRAM Script File
	   /h - Indicates HII data file
	   /s - Indicates advanced script file
	   /f - Imports the NVRAM script file even when the CRC checksum of
	   the target BIOS & the script file differs
	   /v - Indicates verbose mode
	   /q - Indicates Quiet mode
	   /ds - Indicates Current Question Value can be set as BIOS Standard Default Value
	   /dm - Indicates Current Question Value can be set as BIOS Manufacturing Default Value
	   /b  - Enables export/import of boot order controls
	   /r  - Indicates restriction of migration mode
	   /lang - Enables mapping language mode
	   /sp - Enables Expression Evaluation for Suppressif Opcode
	   /g - Enables Expression Evaluation for Grayoutif Opcode
	   /a - Enables Setup Question having Empty or Blank names to be exported
	   /cpwd - To validate the admin password and unlock the protected variables update
	   /apwd - To set new admin password
	   /upwd - To set new user Password
	   /cpwds - To validate the admin password of type Scan Code and unlock the protected variables update
	   /apwds - To set new admin password of type Scan Code
	   /upwds - To set new user Password of type Scan Code
	   /cpwde - To validate the admin password of type EFI Key and unlock the protected variables update
	   /apwde - To set new admin password of type EFI Key
	   /upwde - To set new user Password of type EFI Key
	   /sd - Export duplicate questions in new file
	   /ms - Indicates Map String of the Setup Question
	   /qv - Indicates Question Value to be set for the Setup Question
	   /bt - Indicates the device type for legacy boot device
	   /p - Indicates PLDM File
	   /ce - Comment out suppress and gray out controls in script file
	   /hb - Hides tool information banner
	   /d - Skip checking for AptioV BIOS and behave normally
	   /ndef - Export only those Questions whose Value is different from the Default

Driver Options:
	SCELNX_64 /MAKEDRV
	/MAKEDRV - Make AFULNX driver with user defined environment
	 	Example: /MAKEDRV KERNEL=/lib/modules/$(uname -r)/build

	SCELNX_64 /GENDRV OUTPUT=./driver
	/GENDRV - Generate AFULNX driver source files to specific directory.
		[Option 1]: Specific kernel source 'KERNEL=XXXX'
		same as the /MAKEDRV
		[Option 2]: Specific output directory 'OUTPUT=XXXX'
		Example: /GENDRV KERNEL=/usr/src OUTPUT=./driver
```

根据上述命令帮助可以得知，

- 使用`SCELNX_64 /o /s <NVRAM Script File>`方式可以得出全部配置，
- 使用`SCELNX_64 /i /s <NVRAM Script File>`方式可以刷新全部配置，
- 使用`SCELNX_64 /o [/lang <Lang Code>] /ms <question map string>`方式可以单独得出某项配置，
- 使用`SCELNX_64 /i [/lang <Lang Code>] /ms <question map string> /qv <question value>`方式可以单独刷新某项配置，  
  那么问题又来了，`<question map string>`和`<question value>`如何确定？

## 范例

### 导出所有配置

```bash
/bin/SCELNX_64 /o /s /tmp/nvram_script.txt
# ----------------------------------------------------------------------------
# |                Copyright (c)2017 American Megatrends, Inc.               |
# |                      AMISCE Utility. Ver 5.03.1106                       |
# ----------------------------------------------------------------------------
# WARNING: Duplicate questions found. Only one question will be enabled in the script.
# Script file exported successfully.
```

### 导入所有配置

```bash
/bin/SCELNX_64 /i /s /tmp/nvram_script.txt
/bin/SCELNX_64 /i /s /tmp/nvram_script.txt /lang en-US
/bin/SCELNX_64 /i /s /tmp/nvram_script.txt /lang x-AMI
```

### 查询和设置 Numa

```bash
# 查询Numa
/bin/SCELNX_64 /o /lang en-US /q /d /hb /ms "NUMA"
Options =*[00]Disabled
         [01]Enabled
```

```bash
# 启用Numa
/bin/SCELNX_64 /i /lang en-US /q /d /hb /ms "NUMA" /qv 0x01
```

### 查询和设置 Hyper-Threading

```bash
# 查询HT
/bin/SCELNX_64 /o /lang en-US /q /d /hb /ms "Hyper-Threading"
Options =*[01]Disabled
         [00]Enabled
```

```bash
# 关闭HT
/bin/SCELNX_64 /i /lang en-US /q /d /hb /ms "Hyper-Threading" /qv 0x00
```

# 问题

1. Insyde BIOS Configuration 的名称或存在与否与架构有关?
2. AMI BIOS 的某些项重复，无法修改如何解决?
3. `SCELNX_64 /i /s <NVRAM Script File>`方式存在错误如何解决?

# 参考

[通过 Linux 命令行修改服务器 BIOS 配置](https://huataihuang.gitbooks.io/cloud-atlas/content/server/firmware/modify_bios_through_linux_command.html)  
[修改华为服务器 BIOS 配置项](http://support.huawei.com/enterprise/zh/doc/EDOC1000061912?section=j019)
