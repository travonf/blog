---
title: 理解 GNU screen 的 hardstatus strings
date: 2010-01-01 08:00:00
updated: 2010-01-01 08:00:00
tags: ["linux", "screen"]
categories: "linux"
---

原文链接： http://www.kilobitspersecond.com/2014/02/10/understanding-gnu-screens-hardstatus-strings/

我最近的开发工作主要围绕着 Vim 和 GNU screen 展开。我一开始使用 screen 只是为了保持几天之间（ssh）会话，或者是万一网络断开了也能保持会话。但是最近我有兴趣的尝试了在 screen 里面使用不同的窗口。为了让这件事更容易，我希望有有一个状态行能够标签式的显示所有的窗口。
配置这个状态行（“hard­ware sta­tus line”，或者像我这样叫“hard­sta­tus”）可以在  ~/.screenrc  文件中用一行，通常很长的字符串来完成，这行字符串最开始看上去完全让人困惑：

<!-- more -->

```
hardstatus string "%{= KW} %H [%`] %{= Kw}|%{-} %-Lw%{= bW}%n%f %t%{-}%+Lw %=%C%a %Y-%M-%d"
```

就像这样。
令我沮丧的是，基本上我通过 Google 找到的都是仅仅是别人的给出的字符串，很少或者完全没有关于为什么这么做的解释-很容易想象到发帖的这些人也很少有人知道为什么这么做的原因。[GNU 的官方文档](http://www.gnu.org/software/screen/manual/html_node/String-Escapes.html)基本上没有多大帮助。
在最终破译了这些字符串一大部分的涵义之后，我想告诉到处寻找这个巫术蛛丝马迹的人,关于这里面的秘密。在这里有一些（或者更多？）的东西我没有包括在内，当然包括-跳转和条件，命名-但是这已经足够领你们入门了。
下面是我的`hardstatus string`，包含了对于在它（`hardstatus string`）里面每个小单元的注释。

```
hardstatus string "%{= KW} %H [%`] %{= Kw}|%{-} %-Lw%{= bW}%n%f %t%{-}%+Lw %=%C%a %Y-%M-%d"
```

|         | http://www.gnu.org/software/screen/manual/html_node/String-Escapes.html             |
| ------- | ----------------------------------------------------------------------------------- |
| %{= wK} | set colors to bright white (W) on bright black (K) and keep current text styles (=) |
| %H      | hostname                                                                            |
| [       | opening bracket character                                                           |
| %`      | print output of 'backtick' command (defined elsewhere in .screenrc)                 |
| ]       | closing bracket character                                                           |
| %{= wW} | set colors to white (w) on bright black (K) and keep current text styles (=)        |
| \|      | bar character                                                                       |
| %{-}    | restore colors to previous colors / undo last color change                          |
| %-Lw    | list windows before current window (L [optional] = "include flags")                 |
| %{= bW} | set colors to bright white (W) on blue (b) and keep current text styles (=)         |
| %f      | window flags                                                                        |
| %t      | window title                                                                        |
| %{-}    | restore colors to previous colors / undo last color change                          |
| %+Lw    | list windows after current window (L [optional] = "include flags")                  |
| %=      | expand to fill all space (used here to make remaining content flush right)          |
| %C      | current time (12-hr; 24-hr is %c)                                                   |
| %a      | am/pm (lowercase; uppercase is %A)                                                  |
| %Y      | current year                                                                        |
| -       | hyphen character                                                                    |
| %m      | current month (0-padded; %M for "Jan" etc.)                                         |
| -       | hyphen character                                                                    |
| %d      | current date (0-padded)                                                             |

这样配置之后的结果就像这样：

```
development-sandbox [47121.kbps] | 0$ vim  1-$ bash          10.03am 2014-Feb-10
```

让我们近距离看一下这些关于这些起作用的单元的类型。

## 文本的样式

所有在{大括号}里面的东西会改变在 hardstatus 里文本的外观，仅此而已。这个我稍后会谈到，到目前为止，我们先忽略掉这些字符串，使得剩下的这部分代码容易理解。我推荐你研究在其他任何东西的时候也这样做，而不仅仅是在研究 hardstatus strings 时候。

```
%H [%`] | %-Lw%n%f %t%+Lw %=%C%a %Y-%M-%d
```

## 窗口

任何东西和一个 w（或者 W）结合会处理 Scrren 的窗口标题的显示。在大部分 hard­sta­tus strings 中间的某一地方部分会像这样：

```
%-Lw%n%f %t%+Lw
```

这部分开始和结束是以  `%-Lw`  和  `%+Lw` 这两个字符串来标记的。这个意思，很简单，“打印（前一个/后一个）窗口”： `%-w` 标识前一个， `%+w` 标识下一个， L 指示出我们希望这些窗口的   [标记](http://aperiodic.net/screen/window_flags)   也出现（虽然这是可选的）。
如果我们把这部分拿走，我们就剩下这个了：

```
%n%f %t
```

这是当前活动窗口的标题的格式：序号，标记，（空格），和标题。就这么简单。

## 系统信息

把我们的窗口列表拿掉，我们就剩下这些：

```
%H [%`] | %=%C%a %Y-%M-%d
```

我们先过后一半，在窗口列表右面的东西。%C%a %Y-%M-%d 仅仅是时间和日期， %= 仅仅是告诉 screen 把它之后所有的东西都挤到终端右侧边缘（或多或少：这个字符串把文本“推开”直到它遇到 screen 的边缘或者另一个 %= ）。
现在所有剩下的就只是窗口列表左侧的东西：

```
%H [%`] |
```

%H 是我们所连接服务器的主机名；方括号就是方括号的字面意思，会原本的输出到屏幕上，就像竖线那样。（任何没有经过 `%` 处理的东西会原本的输出。）
反引号字符， %`，会输出你指派给 backtick 命令的结果。在我的情况下（在~/.screenrc 中定义）:

```
backtick 0 30 30 sh -c 'screen -ls | grep --color=no -o "\$PPID[^[:space:]]\*"'
```

这输出当前 Screen 会话的名称。我不清楚为什么这么做，和这是干神马的。我坦白这是从  [Super User](http://superuser.com/a/212520/151850)  里拿过来的。我的理解是 Screen 的以后的版本可以或将会这样做就像  [a sim­ple escape char­ac­ter](http://stackoverflow.com/a/14166128/2642773)  提到的相似的功能。

## 文本的样式（再来一次）

正如我说的，所有在{大括号}里的东西会影响文本的外观-包括格式（像加粗，下划线等等）和颜色。下面是一个例子：

```
%{+bu wW}
```

在括号里字符串的前半部分(“+bu”)告诉 hardstatus 显示接下来的文本为加粗和加下划线。更多的样式编码在[GNU 的文档](http://www.gnu.org/software/screen/manual/html_node/String-Escapes.html#String-Escapes)中获得列表。“+”表示我们希望“添加”这个属性；如果我们接下来取消加粗的文本，我们可以想这样做： %{-b} 。
字符串的后半部分(“wW”)告诉 hardstatus 要显示什么样的颜色，第一个字符是背景的颜色，第二个字符是文本（前景）的颜色。在这个例子中，我们中打印“高亮白色(?)”到“白色”（这个颜色显得稍微灰一点）上面。再说一遍，更多的样式编码可以在[GNU 的文档](http://www.gnu.org/software/screen/manual/html_node/String-Escapes.html#String-Escapes)中获得。
把文本样式重置为先前的状态（最近一次改变），你所有需要做的是加上“%{-}”。
希望以上的这些内容能够帮助你构建你自己的 hardstatus，而不是盲目的从 github 上复制其他人的代码。如果我有任何遗漏错误的地方请在留言中指出。
在 Stack Overflow 上面的[这个留言](http://stackoverflow.com/a/9557807/2642773)提供了额外的帮助。
