---
title: Powershell运算符
date: 2010-01-01 08:00:00
updated: 2010-01-01 08:00:00
tags: "powershell"
categories: ["OS", "Windows", "Powershell"]
---

当我正准备记下学习 Powershell 函数的心得时，突然因为别的事情需要使用计算器。于是我就将就已经打开的 Powershell 控制台完成了计算。这个时间，我突然想起，忘了把 Powersehll 的运算符记录下来。

## Powersehll 有哪些运算符

Powershell 有哪些运行符？当然 Google 有答案，也许 Baidu 也有答案。不过我决定还是先问 Powershell 试试。所以我尝试了这么一条命令：

```
PS F:\> help about_operator 
```

嘿，蒙对了，这里果然有 Powershell 运算符的详细介绍。
Powershell 支持运算符主要有这么几种类型：

- 算术运算符：用于进行数值计算
- 赋值运算符：给变量赋值，或者计算后赋值
- 比较运算符：条件运算符的其中一类，用于比较值或对象的大小
- 逻辑运算符：条件运算符的另一类，用于连接多个条件表达式
- 重定向运算符：用于重定向的运算符，详情参考`about_redirection`
- 拆分/联接运算符：字符串运算符的一类，用于对字符串进行拆分和联接
- 类型运算符：判断或更改对象的类型
- 一元运算符：就是`++`和`--`啦
- 特殊运算符：其它比较特殊的运算符

虽然 Powershell 的帮助文档里已经对运算符进行了很详细的分类，但是为便于理解不同类型的运算，我还是对它进行了重新分类。

<!-- more -->

## 算术运算符

算术运算符就是小学用于四则运算的那些符号：`+`、`-`、`*`、`/`、`()`，以及经常用在程序设计语言中的几个运算符：`%`、`++`、`--`。
这些运算符中，`+`和`*`都可以用于字符串运算；其中`+`还可以用于连接数组和哈希表，`*`还可以用于复制数组。不过这些都不属于算术运算的范畴，所以这里暂时不作说明。
运算符的优先级和小学的时候学的一样，括号优先，然后是乘除，最后是加减。这里`%`和优先级和乘除一样，而`++`和`--`的优先级需要特别说明。除此之外，还有一些需要特别说明的地方：

1. `-`，它实际是两个运算符：它即可以作为单目运算符表示对数值或变量取负，也可以用作双目运算符，表示两个值相减。当`-`作为取负运算符的时候，它的优先级高于乘除和取余。
2. `%`，这是取余运算符，用法和优先级都与/号完全一样，只是结果不同。`/`号用于取商，而`%`号用于取余数。爱动脑筋的朋友这里会发现 2 个问题：
   1. `/`号用于取商，得到的结果是整数部还是精确的实数结果呢？
   2. `%`号能取实数除法的余数么？
      做个实验就明白了：
      ```powershell
      PS F:\> 3 / 2 # 得到的是实数商 
      1.5 
      PS F:\> 3.2 % 2 # 余数居然可以是小数呢 
      1.2 
      PS F:\> 
      ```
      由于实验结果对第 1)个问题的解答，我们不得不面对第 3)个问题：
   3. 如果想得到整数商，该怎么办？
      如果做过 `C`/`C++`/`C#`/`Java` 开发，一定会想到一个办法：强制转换。  
      Powershell 的强制转换有 2 种方式，一种是直接类型强制转换，另一种是通过 `-as` 运算符进行转换
      ```powershell
      PS F:\> [int] (3 / 2) # 直接类型强制转换 
      2 
      PS F:\> (3 / 2) -as [int] # -as运算符进行类型转换 
      2 
      PS F:\> 
      ```
      天啊，强制转换的结果是四舍五入计算的。幸好我们是用 `3 / 2` 来做实验，如果用了 `4 / 3`，你一定会认为这种方法挺有效的。
      不过现在我们需要找另一种方法来解决问题——取不大于值的最大整数，用 `.NET` 类中 `Math` 类的 `Floor` 方法可以实现。
      ```powershell
      PS F:\> [math]::floor(3 / 2) 
      1 
      PS F:\> 
      ```
      但这种方法只对正数有效。如果是负数，就要用 `[math]::ceiling` 了，取不小于参数值的最小整数。
3. `++`和`--`，自增和自减运算符。这两个运算符本来是属于赋值运算符，因为它们只能对变更进行运算，并将结果回赋给变量。不过很多时候它们也用于算术表达式中，所以就在这里一并说了。了解 C/Java 语系语法的都明白这两个运算符的用法，不了解的，做个实验也就明白了

```powershell
PS F:\> $a = 5 
PS F:\> $a++ # $a自已+1，并将结果回赋给自己 
PS F:\> $a 
6 
PS F:\> $a-- # $a自己-1，并将结果回赋给自己 
PS F:\> $a 
5 
PS F:\> 
```

`++`和`--`运算符在算术表达式中的优先级完全取决这两个运算符相对于它们运算的变量的位置。如果它们用在变量之后，那么它们将在整个表达式的最后进行计算；如果它们用在变量之前，则在整个表达式的最前进行计算，比如

```powershell
PS F:\> $a = 5 
PS F:\> 3 + $a++ # 先运算了3+$a(5)，之后$a再自加1 
8 
PS F:\> $a 
6 
PS F:\> 6 - --$a # $a先自减1，值变为5之后，再进行6-$a(5)的运算 
1 
PS F:\> $a 
5 
PS F:\> 
```

## 赋值运算符

最常见的赋值运算符，当然是`=`。除此之外还有`+=`、`-=`、`\*=`、`/=`、`%=`，以及被 Powershell 单独列为一类的`++`和`--`（这两个运算符已经在上面说过咯）。
`=`运算符很好理解，就是把右边的值赋给左边的变量。其它 5 个含`=`号的赋值运算符对 C/Java 系的同学们来说也不陌生。它们是将符号左边的变量值，与右边的表达式结果进行相应的运算（注意`=`号前面那个符号就是它的运算符）之后，再将结果赋值给左边的变量。比如

```powershell
PS F:\> $a = 5 
PS F:\> $a += 3 
PS F:\> $a 
8 
PS F:\> 
```

## 条件运算符

条件运算符就是用于组成条件表达式的运算符。Powershell 的比较运算符和逻辑运算符都是条件运算符。它们都有一个共同点：结果一定是布尔值 `True` 或者 `False`。

- 比较运算符包括：`-eq`（相等）、`-ne`（不等）、`-lt`（小于）、`-gt`（大于）、`-le`（小于等于）、`-ge`（大于等于），它们可以用于比较两个数值，或者两个字符串。另外还有一套专门用于比较/匹配字符串的比较运算符，比如-match、-like、-ieq、-ceq 等，将在字符串运算符（就是下一节）里进行介绍。
- 逻辑运算符主要用于连接各条件表达式，这些运算符包括：`-and`（和/与）、`-or`（或）、`-xor`（异或）、`-not`（非）、`!`（简化的`-not`）。

举两个例子：

```powershell
PS F:\> (2 -lt 3) -and (3.2 -gt 3) 
True 
PS F:\> !(2 -lt 3) 
False 
```

## 字符串运算符

Powershell 对字符串的处理功能是非常强大的，这些处理基本上都通过字符串运算符表现出来了。字符串运算符主要包括两类，一类是用于产生字符串的，另一类是用于比较和匹配字符串的。

1. 比较/匹配类运算符

   - `-eq`、`-ne`、`-lt`、`-gt`、`-le`、`-ge`，比较字符串，不区分大小写
   - `-ieq`、`-ine`、`-ilt`、`-igt`、`-ile`、`-ige`，比较字符串，不区分大小写
   - `-ceq`、`-cne`、`-clt`、`-cgt`、`-cle`、`-cge`，比较字符串，区分大小写

   从这三组共 18 个比较运算符可以看出来字符串比较类运算符的规律：有一组默认的，默认的都不区分大小写；还有一组带 `i` 前缀的，意思是 `ignore case`，仍然是不区分大小写；最后一组带 `c` 前缀，意思是 `case sensitive`，区分大小写。

   - `-like`、`-notlike`，使用通配符(\*)进行匹配，支持 i 和 c 前缀。
   - `-match`、`-notmatch`，使用正则表达式进行匹配，支持 i 和 c 前缀。

   以上所有用于字符串比较/匹配的运算符，用于字符串比较时，返回 `True` 或者 `False`。它们也可以用于对字符串数组进行过滤，并将数组所有测试值为 `True` 的字符串组成一个新的字符串数组返回。比如

   ```powershell
   PS F:\> $a = "James Fancy", "abcdefg", "gfedcba", "ABCDEFG" 
   PS F:\> $a[0] -cmatch "a." # 数组的第1个元素，是个字符串，返回布尔值 
   True 
   PS F:\> $a -like "a*" # 整个数组进行匹配，返回匹配成功的 
   abcdefg 
   ABCDEFG 
   PS F:\> $b = $a -like "a*" # 将匹配结果赋值给变量$b 
   PS F:\> $b.getType().fullName #查看$b的类型，是数组类型 
   System.Object[] 
   PS F:\> $b.length # $b的长度为2 
   2 
   PS F:\> $b = $a -clike "a*" # 看看数组中只有1项匹配的时候会怎么样 
   PS F:\> $b.getType().fullName # $b仍然是数组 
   System.Object[] 
   PS F:\> $b.length # $b是长度为1（只有1个元素）的数组 
   1 
   PS F:\> 
   ```

2. 产生字符串的运算符
   `+`、`+=`，用于连接字符串。如

   ```powershell
   PS F:\> "James" + " Fancy" 
   James Fancy 
   PS F:\> $a = "Hello " 
   PS F:\> $a += "James" 
   PS F:\> $a 
   Hello James 
   PS F:\> 
   ```

   `*`、`*=`都可以用于产生重复一定数量的字符串。比如

   ```powershell
   PS F:\> "ABCD" * 5 
   ABCDABCDABCDABCDABCD 
   PS F:\> $spliter = "-" 
   PS F:\> $spliter *= 40 
   PS F:\> $spliter 
   ---------------------------------------- 
   PS F:\> 
   ```

   `-replace`用于替换掉字符串中的匹配项，并返回新的字符串，支持 i 和 c 前缀。-replace 可以按正则表达式进行匹配。如

   ```powershell
   PS F:\> $a = "Hello Mr. James" 
   PS F:\> $a -replace "james", "Fancy" 
   Hello Mr. Fancy 
   PS F:\> $a = "Hello Mr. James and Mr. Fancy" 
   PS F:\> $a -replace "Mr.\s*(.*?)\b", "$1" # -replace可以按正则表达式匹配 
   Hello James and Fancy 
   PS F:\> 
   ```

   `-split`和`-join`分别用于拆分字符串（为数组）和联接字符串（从数组）。-split 支持通过正则表达式匹配分隔符。如

   ```powershell
   PS F:\> $a = "Hello, James Fancy. How are you?" 
   PS F:\> $b = $a -split "[,\s\.]+" 
   PS F:\> $b 
   Hello 
   James 
   Fancy 
   How 
   are 
   you? 
   PS F:\> $b -join ";" 
   Hello;James;Fancy;How;are;you? 
   PS F:\> 
   ```

   `-f`通过格产生字符串，类似.NET 框架中的 String.Format 函数。比如

   ```powershell
   PS F:\> "{0}; {1:yyyy-MM-dd}；HEX: {2:X4}" -f "J.Fan", $(get-date), 7654321 
   J.Fan; 2011-10-07；HEX: 74CBB1 
   PS F:\> [string]::format("{0}; {1:yyyy-MM-dd}；HEX: {2:X4}", "J.Fan", $(get-date), 7654321) 
   J.Fan; 2011-10-07；HEX: 74CBB1 
   PS F:\> 
   ```

## 数组和哈希表运算符

`@()`，产生数组对象。如果括号里没有内容，产生一个空数组。如果括号里有多个元素，用逗号进行分隔——对了，这里用到了所谓的逗号`,`运算符。其实，多个元素的时候，连`@()`都省了，直接写列表就是数组。
`..`（两个点号），范围运算符，产生整型数组的另一种方式，只需要给定上下限整数，就可以产生一个包含连续整数的数组。
数组是以 0 为起始下标的，对数组元素的访问是中括号，以及包含在中括号中的下标号。比如

```powershell
PS F:\> $a = @(1,2,3,4,5) # 也可以是 $a = 1,2,3,4,5 
PS F:\> $a.length 
5 
PS F:\> $a[1] 
2 
PS F:\> @(1..2) 
1 
2 
PS F:\> 3..1 
3 
2 
1 
PS F:\> 
```

`@{}`，产生哈希表对象。大括号内没有内容，产生一个空的哈希表对象。大括号中是以键值对为单位，键和值之间用=号分隔。如果大括号里有多个键值对，用分号分隔。
对哈希表中元素的访问也是通过中括号，不过中括号中的是键名而不是下标号。如果键名是合法的标识符，那么还可以通过“`.键名`”的方式来访问。比如

````powershell
PS F:\> $a = @{abc=1; "bcd"=2; 3="James Fancy"} 
PS F:\> $a["abc"] 
1 
PS F:\> $a.bcd = "Hello" 
PS F:\> "$($a['bcd']) $($a[3])" # $(...) 表示运算表达式 
Hello James Fancy 
PS F:\>
``` 

`+`和`+=`，可以联接两个数组并产生一些新的数组；它也可以将一个元素联连到数组上。

```powershell
PS F:\> @("hello") + "james", "fancy" 
hello 
james 
fancy 
PS F:\> $a = "hello", "james" 
PS F:\> $a += "fancy" 
PS F:\> $a 
hello 
james 
fancy 
PS F:\> 
````

`*`和`*=`，将数组重复指定次数，并将所有这些元素作为一个新的数组返回。

```powershell
PS F:\> "james", "fancy" * 2 
james 
fancy 
james 
fancy 
PS F:\> $a = @("j.fan") 
PS F:\> $a *= 3 
PS F:\> $a 
j.fan 
j.fan 
j.fan 
PS F:\> 
```

`-contains`, `-notcontains`，用于判断数组中是否有某个数据，支持 `i` 和 `c` 前缀用于字符串比较。

```powershell
PS F:\> "abc", "bcd" -contains "BCD" 
True 
PS F:\> "abc", "bcd" -ccontains "BCD" 
False 
PS F:\> 
```

## 位运算符

Powershell 有 4 个位运算符，`-band`（按位与）、`-bor`（按位或）、`-bxor`（按位异或）、`-bnot`（按位取反）。很不幸，没有移位运算符。

```powershell
PS F:\> (0x6b -band 0xf0).toString("X") 
60 
PS F:\> (0x6b -bor 0x0f).toString("X") 
6F 
PS F:\> (0x6b -bxor 0xff).toString("X") 
94 
PS F:\> (-bnot 0x6b).toString("X") 
FFFFFF94 
PS F:\> 
```

## 类型运算符

类型运算符一共就 3 个，两个用于判断类型：`-is`、`-isnot`；还有一个用于转换类型：`-as`。

```powershell
PS F:\> 1 -is [int] 
True 
PS F:\> 1 -isnot [int] 
False 
PS F:\> "0xff" -as [int] 
255 
PS F:\> [int] "0xff" # 强制类型，和上句同样效果 
255 
PS F:\> 
```

## 重定向运算符

关于重定向，这是所有控制台中的一个重要话题，还是找个时间专门来记录下吧。这次，只把几个关于重定向的运算符列出来。

- `>`，将输出发送到指定文件。
- `>>`，将输出追加到指定文件的内容。
- `2>`，将错误发送到指定文件。
- `2>>`，将错误追加到指定文件的内容。
- `2>&1`，将错误发送到成功输出流。

## 其它运算符

`&`，调用运算符。如果后面接一个命令，那它和没带&符号，直接输入命令没啥区别。但是，如果有一个保存着命令名称的变量，`&`就很有用了……还有一点需要注意的是，这个变量只能是命令本身，不能带参数，不然会出错的。

```powershell
PS F:\> $cmd = "echo Hello James" 
PS F:\> & $cmd # 哇哦，这个会出错哦 
无法将“echo Hello James”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。请检查名称的拼写，如果 
包括路径，请确保路径正确，然后重试。 
所在位置 行:1 字符: 2 
+ & <<<< $cmd 
+ CategoryInfo : ObjectNotFound: (echo Hello James:String) [], CommandNotFoundExcepti 
on 
+ FullyQualifiedErrorId : CommandNotFoundException 
 
PS F:\> $cmd = "echo" 
PS F:\> & $cmd Hello James # 这样就对啦 
Hello 
James 
PS F:\> 
```

`::`（双冒号），静态成员运算符。这个其实以之前的示例中已经用过了，就是调用静态成员的。比如之前用到的`[string]::format`，`[math]::floor` 等。再比如

```powershell
PS F:\> [system.text.encoding]::utf8.toString() 
System.Text.UTF8Encoding 
PS F:\> [guid]::newGuid() 
 
Guid 
---- 
76e2b9ed-71f7-4b91-89c6-1c329df82e96 
 
 
PS F:\> 
```

`.`（点号），访问对象的成员的运算符。这个也用过很多次了,再举个例子：

```powershell
PS F:\> $r = new-object random 
PS F:\> $r.next() # 获取一个随机整数 
397489906 
PS F:\> $r.getType().fullName 
System.Random 
PS F:\> 
```

`.`（点号），还有一个作用，用于获取来源——就是有点像 `C`/`C++`中的`#include`。这个时候它的后面接一个脚本文件，比如

```powershell
PS F:\> echo "`$a = `"Hello J.Fan`"" > hello.ps1 
PS F:\> cat .\hello.ps1 # 显示hello.ps1的内容 
$a = "Hello J.Fan" 
PS F:\> .\hello.ps1 # 不用.号调用脚本。注意：这里的点号是代表当前目录 
PS F:\> $a 
PS F:\> . .\hello.ps1 # 用.号引入脚本 
PS F:\> $a 
Hello J.Fan 
PS F:\> 
```

总算把运算符搞定了，真没想到居然这么多！
