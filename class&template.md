这是基于C++ Primer的第七章 class （类）（& template）
# 定义抽象数据类型 ； 访问控制与封装； 累的其他特性； 类的作用域； 构造函数； 类的静态成员
# 模版（第16章）

# 类的介绍：（第二章 2.6 自定义数据结构，7 章，13章（控制对象拷贝，移动，赋值，销毁），14章（自定义运算）
c++ 语言中，我们想要使用类来定义自己的数据类型。通过定义新的类型来反映待解决问题中的各种概念，可以使我们更容易编写，调试和修改程序。

# 自定义数据结构： 

从基本的层面理解，数据结构是吧一组相关的数据元素组织起来然后使用他们的策略和方法。

c++ 熏晕用户以类的型 his自定义数据类型，而库类型 string,istream, ostream 等都是以类的形式定义的。

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
