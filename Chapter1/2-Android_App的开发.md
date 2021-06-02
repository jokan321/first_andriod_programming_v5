# 02.Android APP的开发
安卓是使用Java或者Kotlin进行开发的，以前是只支持Java的，但是在谷歌在2017年的I/O大会上宣布将Kotlin添加为Android的标准语言，在Android Studio3.0版本往后开始正式支持Kotlin。
安卓APP全体的构成如下
<table>
    <tr>
        <td>
        </td>
        <td>
            APP
            使用Java或者Kotlin记述。就是我们开发的部分
        </td>
    </tr>
    <tr>
        <td>
        </td>
        <td>
            安卓框架
            APP要用的库。
            记住这个库的使用方法来开发APP的页面以及机能。
        </td>
    </tr>
    <tr>
        <td>
        </td>
        <td>
            AndroidRuntime
            JVM以及具有互换性的虚拟机。从安卓5.0棒棒糖开始将以前一直用的Dalvik虚拟机换成了ART（Android Runtime），运行速度也得到了提升
        </td>
    </tr>
    <tr>
        <td>
        </td>
        <td>
            Linux内核
            提供控制端末的最基本机能
        </td>
    </tr>
</table>
安卓整体作为多种技术的集合体，对于萌新来说是有着很难理解的词汇的，在这里我们没有必要理解那些词汇。我们开发APP所使用的仅是安卓框架提供的各种各样的机能（API）而已。将这些机能组合使用就能开发APP了。
熟悉编程语言Java，Kotlin以及安卓框架的使用方法的话，开发安卓APP也就没有什么障碍了吧。

### 🤖安卓开发必要的东西
<div id="Android_APP开发所必要的东西"></div>
安卓开发需要以下的工具。除了电脑之外全部都是免费的，只要有台电脑今天就能开发APP也是安卓开发的魅力之一。

+ _安卓开发所必要的工具_
<table>
    <tr>
        <td rowspan="2">
            PC
            (*摘自时间点为2020年11月的Android Studio Web页面)
        </td>
        <td>
            Windows的场合
            Windows 7/8/10（64-bit）
            内存4G（推荐8G）
            2G的空硬盘容量（推荐4G以上）
            1280×800的显示器像素
        </td>
    </tr>
    <tr>
        <td>
            macOS的场合
            10.10到10.14（macOS Mojave）
            内存4G（推荐8G）
            2G的空硬盘容量（推荐4G以上）
            1280×800的显示器像素           
        </td>
    </tr>
    <tr>
        <td>Android Studio</td>
        <td>安卓APP的综合开发环境</td>
    </tr>
    <tr>
        <td>安卓SDK</td>
        <td>为了开发安卓的软件开发包。其中包括了编译，debug，模拟器等等开发所必要的机能</td>
    </tr>
</table>
其它例如Linux，Chrome OS等各种各样的操作系统也是能进行开发的。并且内存的话还是推荐要8G以上比较好。内存不够可能会导致模拟器比较卡。还有，如果主要使用模拟器进行开发的话，推荐使用CPU很好的电脑。

<b>■　使用虚拟化技术的高速模拟器</b>
安卓SDK是与为了测试开发当中的APP而存在的模拟器捆绑在一起的，这里运用了许多的虚拟化技术达到了高速运行。
首先在搭载了Intel CPU的Windows电脑上使用了Intel HAXM（Intel Hardware Accelerated 。Intel HAXM的使用前提条件是CUP要对应VT-x，EM64T，XD Bit，在BIOS把那些设定全部打开。只要不是特别老的机器，这些条件都应该是满足的。
CUP是AMD Ryzen的话是不能使用Intel HAXM的。取而代之的是用Windows的虚拟化技术——Windows虚拟机监控程序平台（Windows Hypervisor Platform）来实现高速化运行。这个要是Windows10 April 2018 Update之后才能用。一般是关着的，按照以下手顺打开。「开始」右键菜单按钮→选择「应用与功能」在设定的应用与功能页面点击相关设置的「程序与功能」<font color=red>打开控制面板。点击左边的「启用或关闭Windows功能」打开「Windows功能」页面，勾选「Windows虚拟机监控程序平台」之后重新启动。</font>
搭载Intel CUP的苹果电脑会自动选择Intel HAXM与Hypervisor.Frame（苹果的虚拟化技术）当中的其中一个。但是macOS 10.10（Yosemite）之前的版本是用不了Hypervisor.Frame的。并且苹果还卖搭载Apple SiliconCUP的电脑，这是不能使用Intel HAXM的，在原稿执笔之时它是不能用使用了虚拟化技术的高速虚拟器的。

### 👽Column 开发推荐使用的器材是？？？
> 从购买电脑开始探讨的话，恐怕Windows的电脑绝对是候补首选吧。但是最近使用搭载了Intel CPU的Mac的开发者也是变多了。要说为什么的话，是因为在Mac开发安卓有以下几点好处（当然这只是个人喜好，没有什么理由的）。
>+ __连接真机的时候不要驱动__
>+ __因为Mac是基于BSD UNIX的，所以比Windows更适合开发程序__
>+ __有一台Mac的话，既能开发安卓又能开发iOS__
>
>如果你想追求极致的手机APP的开发，想把开发手机APP作为你的工作，强烈推荐你备一台Mac。
>（*本书执笔过程当中搭载Apple Silicon（M1 CUP）的Mac已经开始发售了，虽然CPU很斯巴拉西，但是在原稿执笔期间还没有导入Android Studio的运行环境，也不能运行Intel HAXM的高速模拟器。在Apple Silicon的过度期间不推荐入手新Mac。）

### 🤖从Java到Kotlin
<div id="从Java到Kotlin"></div>
在这之前Java是开发安卓APP唯一的选择，但是伴随着Android Studio 3.0的发布，对新语言Kotlin的支持也开始了。谷歌在他自己主办的开发者活动「Google I/O 2019」当中发表了他们在安卓更进一步强化了「Kotlin fast」这一事。因为今后最新版本提供的机能最初都是面向Kotlin的，所以从现在开始安卓的开发的话推荐使用Kotlin开发。本书也是，示例程序都是用Kotlin写的。
Kotlin不单能在JVM上运作，与Java之间还有着100%的互换性。因此对于有Java开发经验的人来说是个很容易学习的语言。而且Java的Lib也能就这样直接用。
而且比起Java，Kotlin能写出更简洁的程序。比如说，Java当中准备getter与setter是「惯例作法」，但在Kotlin当中通过「属性」让其更简洁了。其它一些近年主流的语言比如Python，Swift所持有的很潮的机能也是采用了的。
Kotlin具有以下几个特征
+ 代码简洁
+ Null安全
+ 采用了lambda表达式等函数式编程的概念
+ 根据扩展函数扩展类
+ 与Java的相互运用性高，Java写的Lib包能直接拿来用

根据这些特征，Java技术者能很顺畅平移到Kotlin，Kotlin人气暴涨也是有理由的。而且Kotlin与开发环境Android Studio是完全整合的。因为开发Kotlin的跟开发IntelliJ IDEA(Android Studio就是以这个为基础开发的)的都是JetBrains，十分期待他们今后持续的整合支持。

