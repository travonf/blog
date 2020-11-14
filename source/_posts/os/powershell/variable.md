---
title: Powershell变量
date: 2010-01-01 08:00:00
updated: 2010-01-01 08:00:00
tags: "powershell"
categories: "OS"
---

# Powershell 定义变量

## 查看正在使用的变量

Powershell 将变量的相关信息的记录存放在名为`variable:`的驱动中。  
如果要查看所有定义的变量，可以直接遍历`variable:`

```powershell
> ls variable:
```

<!-- more -->

## 查找变量

```powershell
> ls variable:value*
```

## 验证变量是否存在

```powershell
> Test-Path variable:value1
```

## 删除变量

```powershell
> del variable:value1
```

## 使用专用的变量命令

`Clear-Variable`, `Get-Variable`, `New-Variable`, `Remove-Variable`, `Set-Variable`

# Powershell 自动化变量

Powershell 自动化变量 是那些一旦打开 Powershell 就会自动加载的变量。  
这些变量一般存放的内容包括:

1. 用户信息：例如用户的根目录`$home`
2. 配置信息：例如 `powershell` 控制台的大小，颜色，背景等。
3. 运行时信息：例如一个函数由谁调用，一个脚本运行的目录等。

`$NULL`  
包含 `NULL` 或空值。可以在命令和脚本中使用此变量表示 `NULL`，而不是使用字符串“`NULL`”。  
如果该字符串转换为非空字符串或非零整数，则可将该字符串解释为 `TRUE`。

`$PSScriptRoot`  
包含要从中执行脚本模块的目录。  
通过此变量，脚本可以使用模块路径来访问其他资源。

# Powershell 环境变量

## 查找环境变量

Powershell 把所有环境变量的记录保存在 `env:` 虚拟驱动中，因此可以列出所有环境变量  
一旦查出环境变量的名字就可以使用 `$env:name` 访问了

```powershell
> ls env:
```

# Powershell 变量的类型和强类型

可以通过 `$variable` 的 `GetType().Name` 查看和验证 Powershell 分配给变量的数据类型

```powershell
> (10).gettype().name
```

## 指定类型定义变量

定义变量时可以在变量前的中括号中加入数据类型

```powershell
> [byte]$b=101
```

Powershell 默认支持的 .NET 类型如下

```
- [array]
- [datetime]
- [guid]
- [hashtable]
- [int16]
- [int32]
- [int64]
- [nullable]
- [psobject]
- [regex]
- [scriptblock]
- [single]
- [switch]
- [timespan]
- [type]
- [uint16]
- [uint32]
- [uint64]
- [ XML ]
- [bool]
- [byte]
- [char]
- [decimal]
- [double]
- [enum]
- [float]
- [int]
- [long]
- [sbyte]
- [string]
```

## 定义数组 @()

```powershell
$a=1,2,3,'a','b','c'
$b=1..5
$c=5..1
```

## 定义哈希表 @{}

```powershell
$s = @{ Name="小明"; Age="12"; Sex="男"; }
$s["Name"]
$s.Count
$s.Keys
$s.Values
```
