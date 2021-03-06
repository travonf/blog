---
title: 走进交换机“层”的世界
date: 2009-06-01 08:00:00
updated: 2009-06-01 08:00:00
tags: "switch"
categories: "Network"
---

无论你是否从事网络工作，你一定听过网络接入层、汇聚层、核心层，二层交换、三层交换、四层交换，这些“层”说的到底是什么？今天带您走进交换机“层”的世界。

首先，我们先说说这交换机为什么分这么多层，各层的交换机到底有什么区别。

<!-- more -->

从协议上看

所谓的一层、二层、三层、四层其实是按OSI协议划分的（关于OSI网络协议的内容有兴趣可以看我之前的文章《看江湖老炮用尽洪荒之力解读网络协议》）

一层交换机：只支持物理层协议（电话程控交换机算吧，其它我也没见过）

二层交换机：支持物理层和数据链路层协议

三层交换机：支持物理层、数据链路层、网络层协议（带路由功能的）

四层交换机：支持物理层、数据链路层、网络层、传输层协议。

从工作原理

看交换机技术原理度娘说的比我清楚，我理解中其实它就是一个快递工作。

比如说A和B都在一个城市，A要给B发件货，把快递单和包裹都给了快递员，（快递单上有收件人发件人的信息，相当于原地址和目标地址），每个快递员（交换机）都有一份地址关系表，记录了的地址和收件人发件人对应关系，这地址表哪来的呢？学来的，只有在它负责的区域和它有联系的顾客它都有相关信息，（这就是交换机的“学习功能，它对每个接入端口的设备都能能识别设备的Mac地址，并在本地存储了一份Mac地址表，这个表包含了端口和接入设备的对应信息。）快递员根据地址表查询目的地址，通过对应端口送达包裹，如果所负责的区域内没有此目的地址，他联系同区域的其它快递员查询目的地址，直到将包裹送达到指定地址。但是，二层交换机在相当于同城快递，跨省快递的活只能交给路由器或三层交换机了。

举个应用场景，便于大家理解。比如说A、B、C、D分别接在交换机的1、2、3、4口，A和B在一个VLAN，C和D在另一个VLAN，默认A和B可以通讯，C和D通讯，如果A和C要通讯，该怎么办。

一般有两种方法：

方法1、如果是二层交换机，需要通过路由器设置，做单臂路由解决不同vlan之前的通讯，二层交换解决不了不同VLAN的通讯需求，只能依靠路由器解决。

方法二、通过三层交换机直接解决此需求。当然它的功能不仅仅如此，

总的来说，二层交换机主要的功能体现在划分子网、限制广播、建立VLAN，但它的控制能力较小，灵活不够，缺乏路由功能。三层交换机因带有路由功能，可以建立跨省之前的关系，它相当于快递总部，不仅仅具备物流能力（二层交换机的能力），而且还有调度能力，通过它的调度选择最佳路径将货物以最快的方式跨省传递。当然，它也可以阻止跨省之间的传递，因为它有这个能力。

二层和三层交换机都是基于端口地址的端到端的交换过程。而四层提供的服务又升级了。

四层交换机最大的特点是提供VIP服务，也就是说它根据不同的应用协议分级，比如说在它的系统里会记录FTP是21端口，RDP 3389端口，它根据这些已订化的协议分级，目的就是为了提升服务质量（Qos),另外它还提供服务器负载均衡、统计信息等等功能。比如说，你快递一个重要物品，要求快递公司4小时到达、保价服务等等，这就属于规范协议内的VIP服务，你甚至可以查到此快递目前距离你的位置。这也就是四层提供的高级服务。

从网络架构看

了解了以上各层交换机的主要功能在说说接入层、汇聚层、核心层就比较好理解了。

■ 核心层——提供最优的区间传输 （4层交机换，总部VIP服务部+业务部）

■ 汇聚层——提供基于策略的连接 （3层交换机，总部调度部+业务部）

■ 接入层——为多业务应用和其他的网络应用提供用户到网络的接入 ，和用户端直接联系。（2层交换机，基层快递业务部）

从企业网络设计看，中小企业业有汇聚层+接入层即可，大的企业往往具备核心层、汇聚、接入3层架构，毕竟网络层次越高成本越高。

从常见设备看

Cisco:

Cisco对产品的命名有一定之规。就Catalyst交换机来说，产品命名的格式如下： Catalyst NNXX [-C] [-M] [-A/-EN] 　　其中，NN是交换机的系列号，XX对于固定配置的交换机来说是端口数，对于模块化交换机来说是插槽数，有-C标志表明带光纤接口，-M表示模块化，-A和-EN分别是指交换机软件是标准板或企业版。Cisco接入层有2900系列，汇聚层的有3500系列，核心层的6000系列，还有模块化的5K、7K系列。也不是绝对的，关键技术功能还要看说明书。-

华为：

华为的标识算是比较清晰的，它的命名一般按下面规范。第一位：是华为的产品线定位，比如，2 .3 .5 .6 .8系列； 第二位：表明是二层还是三层，其中0-4是二层，5-9是三层；第三四位:表示的是插槽数或端口数，比如3026表示，24个电口+2个光口，共26个属于二层交换机；3552呢，48个电口+4个光口，共计52个，属于3层交换机；

通过以上对“层”的世界了解，希望您对企业现有交换机设备的层次结构理解更加深刻，对今后网络设计规划有所帮助。

总之，我的建议是网络规划前，交换机的选择要分清层次，从长计议。
