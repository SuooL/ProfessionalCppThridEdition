# 第一章 C++和 STL 速成

## 常用的预处理命令

* 类型

| 预处理指令     | 功能及常见用法                                      |
| ------------- |---------------------------------------------------|
| #include [file]  |将指定的文件插入到代码中指令所在的位置,几乎都是用来包含头文件|
| #define [key] [value]| 每个指定的 key 都被替换为指定的值,它可以定义符号常量、<br>函数功能、重新命名、字符串的拼接等各种功能。|
| #ifndef, #endif; #ifdef,#endif| 主要是进行编译时进行有选择的挑选，注释掉一些指定的代码，<br>以达到版本控制、防止对文件重复包含的功能。 |
| #progma [xyz]|xyz因编译器而异,如果在预处理期间执行到这一条指令,通常会显示一条警告或者错误信息;<br>布局控制,主要功能是为编译程序提供非常规的控制流信息|

* 常见的预处理命令
 - #define         宏定义
 - #undef          取消宏
 - #include        文本包含
 - #ifdef            如果宏被定义就进行编译
 - #ifndef          如果宏未被定义就进行编译
 - #endif           结束编译块的控制
 - #if                表达式非零就对代码进行编译
 - #else            作为其他预处理的剩余选项进行编译
 - #elif              这是一种#else和#if的组合选项
 - #line             改变当前的行数和文件名称
 - #error            输出一个错误信息
 - #pragma        为编译程序提供非常规的控制流信息


## 编译控制指令
这些指令的主要目的是进行编译时进行有选择的挑选，注释掉一些指定的代码，以达到版本控制、防止对文件重复包含的功能。使用格式，如下:

```cpp
       // 如果identifier为一个定义了的符号，your code就会被编译，否则剔除
       #ifdef   identifier
                your code
       #endif
       //如果identifier为一个未定义的符号，your code就会被编译，否则剔除  
       #ifndef identifier
               your code
       #endif
       //如果expression非零，your code就会被编译，否则剔除
       #if   expression
            your code
       #endif
       //如果identifier为一个定义了的符号，your code1就会被编译，否则your code2就会被编译
       #ifdef identifier
              your code1
       #else
              your code2
       #endif
       //如果epression1非零，就编译your code1，否则，如果expression2非零，就编译your code2，否则，就编译your code3
       #if    expressin1
             your code1
       #elif expression2
             your code2
       #else
             your code3
       #enif
```

### 其他预编译指令

除了上面我们说的集中常用的编译指令，还有3种不太常见的编译指令：#line、#error、#pragma，我们接下来就简单的谈一下。

- \#line的语法如下 :


    \#line number filename

例如：

    \#line 30   a.h      //其中，文件名a.h可以省略不写。

这条指令可以改变当前的行号和文件名，例如上面的这条预处理指令就可以改变当前的行号为30，文件名是a.h。初看起来似乎没有什么用，不过，他还是有点用的，那就是用在编译器的编写中，我们知道编译器对C++源码编译过程中会产生一些中间文件，通过这条指令，可以保证文件名是固定的，不会被这些中间文件代替，有利于进行分析。

- \#error语法如下：


    \#error   info

例如：

    #ifndef UNIX
        #error This software requires the UNIX OS.
    #endif

这条指令主要是给出错误信息，上面的这个例子就是，如果没有在UNIX环境下，就会输出This software requires the UNIX OS.然后诱发编译器终止。所以总的来说，这条指令的目的就是在程序崩溃之前能够给出一定的信息。

至于#pragma,#pragma是非统一的，他要依靠各个编译器生产者，例如，在SUN C++编译器中：

    // 下列指令类似于 #ifndef .. #endif
    #progma once

### 预定义标识符

为了处理一些有用的信息，预处理定义了一些预处理标识符，虽然各种编译器的预处理标识符不尽相同，但是他们都会处理下面的4种：

    __FILE__   正在编译的文件的名字
    __LINE__   正在编译的文件的行号
    __DATE__   编译时刻的日期字符串，例如： "25 Dec 2000"
    __TIME__   编译时刻的时间字符串，例如： "12:30:55"

例如：
    cout<<"The file is :"<<__FILE__"<<"! The lines is:"<<__LINE__<<endl;
