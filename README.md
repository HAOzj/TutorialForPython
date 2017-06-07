# TutorialForPython

python3.5+的介绍攻略.

## 起因

python3.5+攻略,3.5以后新加了大量新特性和语法糖,包括原生的协程,typehint,zipapp等,
再加上本身字符串的语义变化和metaclass的语法变化,以至于和python2的断层大到完全可以认为是两种语言了,
因此才有了重写攻略的想法.

## 为什么定在python3.5?

python3出来很久了,但在3.5版本之前使用上与python2将差无几,3.5版本是个转折点.

定在3.5的原因有以下这些:

+ 新增了async await和原生的协程概念,不再与生成器混淆使用且无法向前兼容,
使用原生协程的异步框架和工具现在也都出现了,数量不少发展也算迅速,也已经出现了uvloop这种大规模提高异步事件循环性能的包.

+ 新增了type hint,虽然只是注释语法,但可以配合一些工具做类型检测,类似typescript,
以后很可能会有jit支持,cython的一个issue中也提到打算利用这一特性搞点事,目前无法向前兼容

+ zipapp工具的出现,为应用分发提供了良好的支持,配合自带的虚拟环境已经可以做到比较不错的环境隔离,大大降低了运维成本

+ metaclass早就无法向前兼容了,string的语义变化也无法向前兼容

+ numpy系列科学工具包在python3.5上很稳定很成熟

+ 目前windows上的tensorfolw只支持3.5版本

+ pypy目前正在开发针对3.5版本的pypy3.现在在beta版本,估计近两年会成熟.

## 为什么不是3.6?

2017年初python3.6版本发布了,它也确实有些令人欣喜的语法糖,但并没有3.5的冲击巨大,且都有替代方式实现.基于3.5写的代码可以保证在python3.6上使用,而相反却不行.

3.5之后版本的特性也会写出来,但会做出标记,如果以后哪个版本又有了关键字层面或者大的语法层面的改变,本教程也会迁移过去.

## 怎么学python3.5+?

+ 首先,忘记python2.7,忘记3.5-的python怎么用的,从头开始学.本教程也不会有与之前的对比.一切从新开始

+ 其次,边做边练,本教程并不打算像之前一样先浅再深分级别来讲,也不打算脱离标准库或者一些"半标准"的实用库,然后库介绍另起炉灶讲,本教程的写法可能更像
<python cookbook> 但面向的层面更低些.

+ 善用`help()`方法,和之前的教程不同本教程不罗列api,光介绍工具和使用场景,细节api请自己`help()`查看

+ 边学边玩跟例子做,本文代码[托管在github](https://github.com/hsz1273327/TutorialForPython3.5plus)上可以自己下下来自己本地跑,
我就不提供服务器端的运行环境了,怕脚本注入.但可以使用[brpython](http://www.brython.info/)在服务器端运行一些例子.而静态版本则放在这个网址[]




## 学了能干嘛?

python3.5+貌似没什么大公司在用,也没见啥大项目是基于3.5开发的,那学了干嘛?

简单说这种问题太功利了,学一门编程语言目的当然是编程,python在所有计算机语言中都算是好学好用的,
自己写东西感觉是很方便的.

具体来说有以下几点:

+ 成熟: 因为有悠久的历史,遗产很多,虽然3.5版本的代码很多时候不能让之前的版本兼容,
但大多数时候3.5以上的版本都可以向下兼容之前的老代码.当然了因为历史原因这些代码一般都是同步阻塞的基于线程模型,
异步工具就比较少了,这点和js不同.

+ 有一套自己的规范和哲学但又非常灵活: 我们可以和javascript以及java对比下:

    + java出了名的呆板,javadoc,设计模式,规范到千人一面,瀑布式的开发方式非常依赖架构师,用户写java没有乐趣可言
    + js则是另一个极端,js项目碎片化比android手机都厉害,光模块化编程的方案就一大堆,浏览器支持和语法实现也进度各异,虽然v8引擎强无敌,
    node.js单核性能优异内存消耗很小,但老实说js不好学,为啥?没有规范,没人告诉你什么情况下该用啥,选择太多意味着无从选择.
    虽然新版本标准语法很cool,箭头函数,不变量,但身为一个脚本语言为了适配不同的浏览器,代码竟然要编译后才能运行...
    如果想真当脚本一样写,可能用户只能使用简陋的低版本语法,没有const,没有箭头函数,甚至变量作用域连块的概念都没有.
    老实说写ES6或者typescript代码很爽,非常灵活.但就是因为规范没有权威性而非常扯淡.
    + python有官方实现,有规范的pep文档,多数东西都是官方的,有规范.而非官方的实现往往都只是替代方案.总的来说,规范性上非常靠谱.
    而且多数规范是非强制的,只是因为代码风格的问题不自觉的用户就会去遵循规范.
    而语法上,糖够多,写起来方便,不用考虑大括号,逗号这些问题,由于是鸭子类型完全面向对象,python代码灵活性很高,但也不会高到看起来像天书.
    因为规范和本身的缩进语法,代码看起来一目了然,当然代价就是匿名函数只能一行.

+ 语法简单便于维护:我们写个啥最怕过了几个月不知道自己写的是啥了,而python的缩进语法强制性的让你的代码有条理,
文档生成工具也非常成熟,按规范写好注释的情况下都不需要额外的做文档工作.

## 本文包括些什么?

+ 工具链

+ python的数据模型

+ 元编程

+ python的并发模型

+ python与C/C++语言扩展

我尽量让各个部分内聚避免耦合,这样可以不用按顺序看

## 那么好了开始吧!
