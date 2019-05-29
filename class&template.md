这是基于C++ Primer的第七章 class （类）（& template）
# 定义抽象数据类型 ； 访问控制与封装； 累的其他特性； 类的作用域； 构造函数； 类的静态成员
# 模版（第16章）

# 类的介绍：（第二章 2.6 自定义数据结构，7 章，13章（控制对象拷贝，移动，赋值，销毁），14章（自定义运算）
c++ 语言中，我们想要使用类来定义自己的数据类型。通过定义新的类型来反映待解决问题中的各种概念，可以使我们更容易编写，调试和修改程序。

# 自定义数据结构： 

从基本的层面理解，数据结构是吧一组相关的数据元素组织起来然后使用他们的策略和方法。

c++ 熏晕用户以类的型 his自定义数据类型，而库类型 string,istream, ostream 等都是以类的形式定义的。

在本块儿，我将用一个例子来详细讲述一下：

这个例子是书上的------- Sales_data 

（1） 定义sales_data 类型

初步想法是用户能直接访问其中的元素，实现一些基本操作：

    struct Sales_data {
      std::string bookNo;
      usigned units_sold =0;
      double revenue = 0.0;
      };
我们的类以关键词struct开始，紧跟着类的名字和类体。类体由花括号包围形成了一个新的作用域。类内部定义的名字必须唯一，但是可以和类外部定义的名字重复。

类右侧表示结束的花括号后必须写一个分号，这是因为类体后面可以紧跟变量名以示对该类型对象的定义，所以分号不能少：

    struct Sales_data { /* ... */ } accum, trans, *salesptr;
    struct Sales_data { /* ... */ } ;   //推荐使用
    Sales_data accum, trans, *salesptr;
分号表示声明符（通常为空）的结束。一般来说，最好不要把对象的定义类型和类的定义放在一起。

（2） 类数据成员

类体定义的成员，我们的类只有数据成员。类的数据成员定义了类的对象的具体内容，每个对象都有自己一份数据成员拷贝。修改一个对象的数据成员，不会影响其他的对象。

定义数据成员的方法和定义普通变量一样：首先说明一个基本类型，随后紧跟一个活多个声明符。例如， 我们sales_data 类中由3个数据成员： bookNo 的 string 成员, unites_sold 的 unsigned成员, revenue的double成员。

c++11 新标准规定，可以给数据成员提供一个类内初始值（in-class initializer）。创建对象时，类内初始值将用来初始化数据成员。没有初始值的成员将被默认初始化。因此 bookNo将初始化为空字符串， unites_sold 和revenue都被初始化为0.

对类内初始值的限制：放在花括号里，或者放在等号右边， 记住不能用圆括号。

用户也可以使用c++的另外一个关键字class来定义数据结构。第七章会介绍。

（3）使用Sales_data类

程序输入两条交易记录：

    0-201-78345-X 3 20.00
    0-201-78345-X 3 25.00
每笔交易记录着图书的ISBN编号，售出数量和单价。

添加两个Sales_data对象

    #include <iostream>
    #include <string>
    #include "Sales_data.h"
    int main(){
      Sales_data data1, data2;
      //读入data1 and data2的代码
      //检查data1 and data2 的ISBN是否相同
      //如果相同，求data1 and data2的总和
      }

![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-23%2011.00.51.png)

# 类（class）

类的基本思想是数据抽象（data abstraction) 和 封装(encapsulation)。数据抽象是一种依赖于接口（inference) 和实现（implementation)分离的编程计术。类的接口包括用户能执行操作；类的实现则包括类的数据成员，负责接口实现的函数体以及定义类所需的各种私有函数。

封装实现了类的接口和实现的分离。封装后的类隐藏了她的实现细节，也就是说，类的用户只能使用接口而无法访问实现部分。

类要想的实现数据抽象和封装，需要首先定义一个抽象数据类型(abstract data tyoe).在抽象数据类型中，由类的设计者负责考虑类的实现过程；使用该类的程序员则只需抽象的思考类型做了什么，无需了解类型的工作细节。

# 定义抽象数据类型
在本块儿，我将用一个例子来详细讲述一下：
这个例子是书上的------- Sales_data 

综上所述，我们想要一个带有这些功能的Sales_data:
![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-23%2017.18.52.png)

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-24%2014.06.38.png)

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-24%2014.07.57.png)

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-24%2014.12.37.png)

# this 指针

引入 this：

当我们调用成员函数时，实际上是替某个对象调用它。

成员函数通过一个名为 this 的额外隐式参数来访问调用它的那个对象，当我们调用一个成员函数时，用请求该函数的对象地址初始化 this。例如，如果调用 total.isbn()则编译器负责把 total 的地址传递给 isbn 的隐式形参 this，可以等价地认为编译器将该调用重写成了以下形式：

        //伪代码，用于说明调用成员函数的实际执行过程
        Sales_data::isbn(&total)
其中，调用 Sales_data 的 isbn 成员时传入了 total 的地址。

在成员函数内部，我们可以直接使用调用该函数的对象的成员，而无须通过成员访问运算符来做到这一点，因为 this 所指的正是这个对象。任何对类成员的直接访问都被看作是对 this 的隐式引用，也就是说，当 isbn 使用 bookNo 时，它隐式地使用 this 指向的成员，就像我们书写了 this->bookNo 一样。

对于我们来说，this 形参是隐式定义的。实际上，任何自定义名为 this 的参数或变量的行为都是非法的。我们可以在成员函数体内部使用 this，因此尽管没有必要，我们还是能把 isbn 定义成如下形式：

        std::string isbn() const { return this->bookNo; }
因为 this 的目的总是指向“这个”对象，所以 this 是一个常量指针（参见2.4.2节，第56页），我们不允许改变 this 中保存的地址。

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-24%2014.13.04.png)

# 类的作用域和成员函数

在类的成员函数的定义嵌套在类的作用域中，成员函数体可以随意使用类中的其他成员元，无须次序。因为编译器是先编写成员声明，然后才轮到成员函数体。

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-27%2003.35.10.png)

# 在类外部定义成员函数：

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-27%2003.35.32.png)

# 定义一个返回this对象的函数

在这里举一个combine函数的例子

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2016.22.31.png)

# 定义类相关的非成员函数

一般类的作者需要定义一些辅助函数，比如add, read, print等。尽管这些函数定义的操作从概念上说属于类的接口的组成一部分，但他们实际上不属于类。

我们定义非成员函数的方式与定义其他函数一样，通常把函数的声明和定义分离开来。如果在概念上属于类但是不定义在类中，则他一般应与类声明在同一个头文件内。在这种方式下，用户使用接口的任何部分都只需引入一个文件。

比如：在你main函数有多个不同的类函数，就把类弄到头文件里

# 定义read和print函数

read 函数就是从给定流中将数据读入或者输入给对象中； print函数就是将给定对象的内容打印到给定流中。

另外，（1）read 和 print 分别接受一个各自的IO类型的引用作为参数，这是因为IO类属于不能被copy的类型，因此只能通过引用来传递他们。而且，因为读取和写入操作会改变流的内容，所以这两个函数接受的都是普通引用，而非对常量的引用。

print函数不负责换行。执行输出任务的函数应尽量减少对格式的控制，这样可确保由用户代码来决定是否换行。

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2017.20.23.png)

# 定义add函数

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2017.29.48.png)

注意： 这里面定义了一个新的Sales_data 对象并将其命名为sum，宿命用于存放两笔交易之和。
# 构造函数

每个类都分别定义了他的对象被初始化的方式， 类通过一个或几个特殊的成员函数来控制其对象的初始化过程。 这些函数叫做成员函数。构造函数的任务是初始化类对象的数据成员，无论何时只要类的对象被创建，就会执行构造函数。

构造函数的名字和类的名字相同。

构造函数：
（1） 没有返回类型； 和其他函数一样，构造函数也有一个（可能为空）参数列表和一个函数体（可能为空）。不同的构造函数之间必须在参数数量或者参数类型上有所区别。

（2）构造函数不能被声明成const的。 当创建类的一个const对象时，直到构造函数完成初始化过程，对象才能真正取得其“常量”特性。

# 合成的默认构造函数

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2018.08.39.png)

# 定义Sales_data 的构造函数

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2018.17.39.png)

(1) =default 

因为构造函数不接受任何实参，所以他是一个默认构造函数。
在参数列表后面写上  “ = default ”， 来要求编译器生成构造函数。如果 =default 在类的内部，则默认构造函数是内联的，若在外部，则是外联的。

（2） 构造函数初始值列表

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2018.43.45.png)

(3)在类的外部定义构造函数

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2018.51.30.png)

# 访问控制与封装


之前介绍了类的接口。
之前我们定义了类的接口，但并没有任何机制强制用户使用这些接口。我们的类还没有封装，即用户可以直达Sales_data对象的内部并且控制它的具体实现细节。

（1） 访问说明符

c++中，我们使用 访问说明符 加强类的封装性。

    public & private
一个类可以包0个或者多个访问说明符，而且对于某个访问说明符能出现多少次也没有严格限定。每个访问说明符指定了接下来的成员的访问级别，其有效范围直到下一个访问符出现为止。

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2019.18.41.png)

（2）class & struct 

两者差不多含义和用法，唯一的区别在于，struct and class 的默认访问权限不一样。

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2019.18.56.png)

# 友元 

. 位置不限 

. 在类内部

. 允许访问非公有成员

. 把想要用的函数前加friend 

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-28%2019.57.41.png)

# 友元的声明

如上述例子

友元函数仅仅指定了访问权限，而非一个通常意义上的函数声明。如果我们希望类的用户能够调用某个友元函数，那我们必须在友元声明外在专门对函数进行声明。

为了是友元对类的用户可见，我们通常把友元的声明与类本身放在同一个头文件里。

# 类的其他特性

类型成员； 类的成员的类内初始值； 可变数据成员； 内联函数成员； 成员函数返回 *this

# 类的成员（2） 

举 screen and window_mgr 的例子来介绍：

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-29%2013.04.23.png)

![](https://github.com/linbearababy/primer-c-/blob/master/pictures/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-29%2013.05.05.png)

(1) inline 介绍 （内联函数）

当我们想要重复利用这个函数，但是变量类型不一样时，可以考虑inline

C++ 内联函数是通常与类一起使用。如果一个函数是内联的，那么在编译时，编译器会把该函数的代码副本放置在每个调用该函数的地方。

对内联函数进行任何修改，都需要重新编译函数的所有客户端，因为编译器需要重新更换一次所有的代码，否则将会继续使用旧的函数。

如果想把一个函数定义为内联函数，则需要在函数名前面放置关键字 inline，在调用函数之前需要对函数进行定义。如果已定义的函数多于一行，编译器会忽略 inline 限定符。

在类定义中的定义的函数都是内联函数，即使没有使用 inline 说明符。

但是一般建议在外部加上 inline， 这样好理解。

定义: 当函数被声明为内联函数之后, 编译器会将其内联展开, 而不是按通常的函数调用机制进行调用.

优点: 当函数体比较小的时候, 内联该函数可以令目标代码更加高效. 对于存取函数以及其它函数体比较短, 性能关键的函数, 鼓励使用内联.

缺点: 滥用内联将导致程序变慢. 内联可能使目标代码量或增或减, 这取决于内联函数的大小. 内联非常短小的存取函数通常会减少代码大小, 但内联一个相当大的函数将戏剧性的增加代码大小. 现代处理器由于更好的利用了指令缓存, 小巧的代码往往执行更快。

结论: 一个较为合理的经验准则是, 不要内联超过 10 行的函数. 谨慎对待析构函数, 析构函数往往比其表面看起来要更长, 因为有隐含的成员和基类析构函数被调用!

另一个实用的经验准则: 内联那些包含循环或 switch 语句的函数常常是得不偿失 (除非在大多数情况下, 这些循环或 switch 语句从不被执行).

# 重载成员函数

与非成员函数一样， 成员函数也可以被重载，只要函数在参数的数量和/或类型有区别就行。 eg: 



# 可变数据成员

# 数据成员的初始值

# 类的静态成员

