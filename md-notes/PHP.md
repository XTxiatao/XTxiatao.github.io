### PHP笔记

#### 编程语言概述

从汇编语言到编译型语言再到解释型语言，随着语言离硬件越来越远，语言能到达的对硬件性能的极致压榨就越来越低，但是相对的，其开发成本和效率就越来越高。现在系统开发基本是以C语言为主，原因在于其性能和安全性高，而计算机操作系统开发方都愿意投入大量高级人才和资金、时间来将其性能打磨到极致；C++在C的基础上有更多扩展，有面向对象的特点，所以大型项目的开发效率上比C更高，相对的使用的框架和模板越多，能针对细节进行性能优化的空间就越少，所以在更底层的系统开发上，C++更常作为辅助而不是主力语言；C#在桌面应用开发上对C++做减法，提升开发效率和学习难度，桌面游戏便捷开发项目很多都能用到C# ，相对的对于性能要求较高的大型项目则不如C++；java通过虚拟机实现了各个平台上优秀的可移植性，生态好，可扩展性强，在各个领域都有其应用，在安卓应用开发上占绝对领导地位；python由于其语言的可阅读性极高，伪代码式的灵活的语法使得其很适合作为黏着剂，在各种专业领域使用python可以快速实现业务逻辑，在逻辑实现为重点，性能极致化为其次的场景非常适合python，今年在人工智能、机器学习等先进算法的领域，python非常火爆，工程师可以花更多精力完成逻辑设计而不用在语言实现上耗费过多精力；JavaScript在前端运行，可以减轻后端计算压力，能简单快速实现大量脚本功能，且几乎所有浏览器都对其支持良好；PHP针对web后端开发设计，相比于更底层的语言，其性能无法做到极致，但是由于其对网页应用场景做了大量优化和模块，开发效率非常高，性能也非常够用，而且有着长久以来的用户积累，所以现在绝大部分的网页后端开发还是以PHP为主。

![web language rank](images/web language rank.png)

#### Linux下php的安装与配置

在centos 7及以后的版本，直接配置好yum源用yum安装即可，若不要求特定php版本，可以直接用

`yum install php`

yum会在配置源中搜索存在的最新版本的php，并解决最基础的安装依赖软件，若要安装指定版本，则要先在网上找到并更新对应rpm包，再安装。对于需要使用到的php扩展模块，可以按需求安装，具体模块及作用网上搜索以下即可。

安装好php后，启动php-fpm

`systemctl start php-fpm.service`

`systemctl enable php-fpm.service`

然后重新加载nginx，

`nginx -s reload`

在安装php时nginx会在相关配置目录下增加php的配置文件，例如/etc/nginx/conf.d/php-fpm.conf和/etc/nginx/default.d/php.conf，必须重启才能载入这些配置，使nginx能够将php文件交给php-fpm。

此时，查看/etc/nginx/nginx.conf或根据其加载的其他项找到代理server块，例如代理端口为8080，则对应访问地址为127.0.0.1：8080。同时查看nginx代理的目录地址即配置文件中的root路径，在对应目录中创建info.php或者建立一个hello.php文件。

直接用

`curl 127.0.0.1:8080/hello.php`

查看输出的html页面，若内容正确，则说明配置完成。

#### php与nginx配合的错误处理

当浏览器或者curl访问php文件出错时，可以查看nginx的error.log文件和access.log文件；一般情况若错误码为4开头如404，那么可能是文件路径填错，或者nginx配置中的root信息错误，或者.\php块的配置中缺失路径信息（加上root即可）等；若是5开头，说明问题出现在nginx找到对应文件，把他交给php服务器到从php服务器返回信息的期间，可能是nginx的权限问题。总之，根据nginx的日志可以到网上所搜到类型的问题，参考进行排查解决。

#### 常用操作

##### 查看版本信息和扩展模块

若一开始安装php是使用最简单的yum指令安装，在后期使用到一些扩展库功能时可能会有问题，此外对于php相关的各种配置也时长需要查看，所以直接用info.php借助

`echo phpinfo();`

输出相关信息在浏览器查看是非常方便实用的。(若不通过web服务器，也可以用php的命令行接口php-cli，以php --info获得同样的信息，但是阅读起来不如浏览器页面)

#### 手写笔记pdf

 [变量-基础](pdf/变量-基础.pdf) 

 [变量-可变变量](pdf/变量-可变变量.pdf) 

 [变量-外来变量](pdf/变量-外来变量.pdf) 

 [变量与类型相关扩展-数组](pdf/变量与类型相关扩展-数组.pdf) 

 [变量-作用域](pdf/变量-作用域.pdf) 

 [常量-魔术常量](pdf/常量-魔术常量.pdf) 

 [常量-语法](pdf/常量-语法.pdf) 

 [函数-参数传递](pdf/函数-参数传递.pdf) 

 [函数-自定义函数](pdf/函数-自定义函数.pdf) 

 [函数-可变函数](pdf/函数-可变函数.pdf) 

 [函数-匿名函数（闭包函数)](pdf/函数-匿名函数（闭包函数）.pdf) 

 [函数-箭头函数](pdf/函数-箭头函数.pdf) 

 [类与对象-简介](pdf/类与对象-简介.pdf) 

 [类与对象-基本概念](pdf/类与对象-基本概念.pdf) 

 [类和对象-属性 拷贝](pdf/类和对象-属性 拷贝.pdf) 

 [类和对象-属性](pdf/类和对象-属性.pdf) 

 [类和对象-类常量](pdf/类和对象-类常量.pdf) 

 [类和对象-构造函数](pdf/类和对象-构造函数.pdf) 

 [类和对象-访问控制](pdf/类和对象-访问控制.pdf) 

 [类和对象-继承](pdf/类和对象-继承.pdf) 

 [类和对象-范围解析](类和对象-范围解析（：：）.pdf) 

 [类和对象-抽象类和对象接口](pdf/类和对象-抽象类和对象接口.pdf) 

 [类和对象-遍历类属性](pdf/类和对象-遍历类属性.pdf) 

 [类和对象- final关键字](pdf/类和对象- final关键字.pdf) 

 [类与对象-对象比较](pdf/类与对象-对象比较.pdf) 

 [流程控制- goto](pdf/流程控制- goto.pdf) 

 [流程控制-文件调用](pdf/流程控制-文件调用.pdf) 

 [流程控制- return](pdf/流程控制- return.pdf) 

 [流程控制- switch](pdf/流程控制- switch.pdf) 

  [流程控制- break-continue ](pdf/流程控制- break-continue .pdf) 

 [流程控制- foreach](pdf/流程控制- foreach.pdf) 

 [流程控制- for](pdf/流程控制- for.pdf) 

 [流程控制- while-do while](pdf/流程控制- while-do while.pdf) 

 [流程控制- if- elseif- else-endif](pdf/流程控制- if- elseif- else-endif；.pdf) 

 [运算符-类型运算符](pdf/运算符-类型运算符.pdf) 

 [运算符-数组运算符](pdf/运算符-数组运算符.pdf) 

 [运算符-执行运算符](pdf/运算符-执行运算符.pdf) 

 [运算符-比较运算符](pdf/运算符-比较运算符.pdf) 

 [运算符-位运算符](pdf/运算符-位运算符.pdf) 

 [运算符-运算符优先级](pdf/运算符-运算符优先级.pdf) 

 [类型-object ](pdf/类型-object .pdf) 

 [类型- array](pdf/类型- array.pdf) 

 [类型-string](pdf/类型-string.pdf) 

 [类型-float](pdf/类型-float.pdf) 

 [类型-integer](pdf/类型-integer .pdf) 

 [类型- boolead](pdf/类型- boolean.pdf) 

 [类型-简介](pdf/类型-简介.pdf) 

 [基本语法-注释](pdf/基本语法-注释.pdf) 

 [基本语法-指令分隔符](pdf/基本语法-指令分隔符.pdf) 

 [基本语法-从html分离](pdf/基本语法-从html分离.pdf) 

 [基本语法- PHP标记](pdf/基本语法- PHP标记.pdf) 

 [数据库扩展- mysql-mysqli](pdf/数据库扩展- mysql-mysqli(1).pdf) 

 [数据库扩展- PDO](pdf/数据库扩展- PDO.pdf) 

 [数据库扩展- mysql- overview of mysql PHP drivers](pdf/数据库扩展- mysql- overview of mysql PHP drivers.pdf) 

 [其他服务-网络](pdf/其他服务-网络.pdf) 

 [变量与类型相关扩展-数组](pdf/变量与类型相关扩展-数组.pdf) 

 [文本处理-PCRE](pdf/文本处理-PCRE.pdf) 

 [文本处理-字符串-其他](pdf/文本处理-字符串-其他.pdf) 

 [文本处理-字符串-拆分与组合](pdf/文本处理-字符串-拆分与组合.pdf) 

 [文本处理-字符串-格式化](pdf/文本处理-字符串-格式化.pdf) 

 [文本处理-字符串-替换](pdf/文本处理-字符串-替换.pdf) 

 [文本处理-字符串-检索字符串](pdf/文本处理-字符串-检索字符串.pdf) 

 [文本处理-字符串-比较字符串](pdf/文本处理-字符串-比较字符串.pdf) 

 [文本处理-字符串-获取字符串长度](pdf/文本处理-字符串-获取字符串长度.pdf) 

 [文本处理-字符串-转义和还原字符串](pdf/文本处理-字符串-转义和还原字符串.pdf) 

 [文本处理-字符串-裁剪首尾特殊字符](pdf/文本处理-字符串-裁剪首尾特殊字符.pdf) 
