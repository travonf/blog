---
title: EXCEL函数
date: 2011-01-01 08:00:00
updated: 2011-01-01 08:00:00
tags: "excel"
categories: ["Office", "Excel"]
---

## `INDEX`函数

返回指定的行与列交叉处的单元格引用。 如果引用由不连续的选定区域组成，可以选择某一选定区域。

```excel
INDEX(reference, row_num, [column_num], [area_num])
```

当函数 INDEX 的第一个参数为数组常量时，使用数组形式。

```excel
INDEX(array, row_num, [column_num])
```

## `MATCH`函数

返回指定的项目在区域中的位置，行或者列

```excel
MATCH(lookup_value, lookup_array, [match_type])
```
