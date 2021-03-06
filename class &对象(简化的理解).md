# C++ 类 & 对象
C++ 在 C 语言的基础上增加了面向对象编程，C++ 支持面向对象程序设计。类是 C++ 的核心特性，通常被称为用户定义的类型。

类用于指定对象的形式，它包含了数据表示法和用于处理数据的方法。类中的数据和方法称为类的成员。函数在一个类中被称为类的成员。

# C++ 类定义
定义一个类，本质上是定义一个数据类型的蓝图。这实际上并没有定义任何数据，但它定义了类的名称意味着什么，也就是说，它定义了类的对象包括了什么，以及可以在这个对象上执行哪些操作。

类定义是以关键字 class 开头，后跟类的名称。类的主体是包含在一对花括号中。类定义后必须跟着一个分号或一个声明列表。例如，我们使用关键字 class 定义 Box 数据类型，如下所示：

      
            class Box
            {
               public:
                  double length;   // 盒子的长度
                  double breadth;  // 盒子的宽度
                  double height;   // 盒子的高度
            };

关键字 public 确定了类成员的访问属性。在类对象作用域内，公共成员在类的外部是可访问的。您也可以指定类的成员为 private 或 protected，这个我们稍后会进行讲解。

# 定义 C++ 对象
类提供了对象的蓝图，所以基本上，对象是根据类来创建的。声明类的对象，就像声明基本类型的变量一样。下面的语句声明了类 Box 的两个对象：

      Box Box1;          // 声明 Box1，类型为 Box
      Box Box2;          // 声明 Box2，类型为 Box
对象 Box1 和 Box2 都有它们各自的数据成员。

# 访问数据成员
类的对象的公共数据成员可以使用直接成员访问运算符 (.) 来访问。为了更好地理解这些概念，让我们尝试一下下面的实例：

      #include <iostream>

      using namespace std;

      class Box
      {
         public:
            double length;   // 长度
            double breadth;  // 宽度
            double height;   // 高度
      };

      int main( )
      {
         Box Box1;        // 声明 Box1，类型为 Box
         Box Box2;        // 声明 Box2，类型为 Box
         double volume = 0.0;     // 用于存储体积

         // box 1 详述
         Box1.height = 5.0; 
         Box1.length = 6.0; 
         Box1.breadth = 7.0;

         // box 2 详述
         Box2.height = 10.0;
         Box2.length = 12.0;
         Box2.breadth = 13.0;

         // box 1 的体积
         volume = Box1.height * Box1.length * Box1.breadth;
         cout << "Box1 的体积：" << volume <<endl;

         // box 2 的体积
         volume = Box2.height * Box2.length * Box2.breadth;
         cout << "Box2 的体积：" << volume <<endl;
         return 0;
      }
      当上面的代码被编译和执行时，它会产生下列结果：

      Box1 的体积：210
      Box2 的体积：1560
    
    需要注意的是，私有的成员和受保护的成员不能使用直接成员访问运算符 (.) 来直接访问。我们将在后续的教程中学习如何访问私有成员和受保护的成员。
    
# 类的成员函数

类的成员函数是指那些把定义和原型写在类定义内部的函数，就像类定义中的其他变量一样。类成员函数是类的一个成员，它可以操作类的任意对象，可以访问对象中的所有成员。

让我们看看之前定义的类 Box，现在我们要使用成员函数来访问类的成员，而不是直接访问这些类的成员：

            class Box
            {
               public:
                  double length;         // 长度
                  double breadth;        // 宽度
                  double height;         // 高度
                  double getVolume(void);// 返回体积
            };
            
成员函数可以定义在类定义内部，或者单独使用范围解析运算符 :: 来定义。在类定义中定义的成员函数把函数声明为内联的，即便没有使用 inline 标识符。所以您可以按照如下方式定义 Volume() 函数：

第一种（定义在类体内部）：
           
           class Box
            {
               public:
                  double length;      // 长度
                  double breadth;     // 宽度
                  double height;      // 高度

                  double getVolume(void)
                  {
                     return length * breadth * height;
                  }
            };

第二种方法（用::)：

            您也可以在类的外部使用范围解析运算符 :: 定义该函数，如下所示：

            double Box::getVolume(void)
            {
                return length * breadth * height;
            }

在这里，需要强调一点，在 :: 运算符之前必须使用类名。调用成员函数是在对象上使用点运算符（.），这样它就能操作与该对象相关的数据，如下所示：

            Box myBox;          // 创建一个对象

            myBox.getVolume();  // 调用该对象的成员函数
            
使用上面提到的概念来设置和获取类中不同的成员的值：

            #include <iostream>

            using namespace std;

            class Box
            {
               public:
                  double length;         // 长度
                  double breadth;        // 宽度
                  double height;         // 高度

                  // 成员函数声明
                  double getVolume(void);
                  void setLength( double len );
                  void setBreadth( double bre );
                  void setHeight( double hei );
            };

            // 成员函数定义
            double Box::getVolume(void)
            {
                return length * breadth * height;
            }

            void Box::setLength( double len )
            {
                length = len;
            }

            void Box::setBreadth( double bre )
            {
                breadth = bre;
            }

            void Box::setHeight( double hei )
            {
                height = hei;
            }

            // 程序的主函数
            int main( )
            {
               Box Box1;                // 声明 Box1，类型为 Box
               Box Box2;                // 声明 Box2，类型为 Box
               double volume = 0.0;     // 用于存储体积

               // box 1 详述
               Box1.setLength(6.0); 
               Box1.setBreadth(7.0); 
               Box1.setHeight(5.0);

               // box 2 详述
               Box2.setLength(12.0); 
               Box2.setBreadth(13.0); 
               Box2.setHeight(10.0);

               // box 1 的体积
               volume = Box1.getVolume();
               cout << "Box1 的体积：" << volume <<endl;

               // box 2 的体积
               volume = Box2.getVolume();
               cout << "Box2 的体积：" << volume <<endl;
               return 0;
            }
            当上面的代码被编译和执行时，它会产生下列结果：

            Box1 的体积： 210
            Box2 的体积： 1560

# 类的访问修饰符


数据封装是面向对象编程的一个重要特点，它防止函数直接访问类类型的内部成员。类成员的访问限制是通过在类主体内部对各个区域标记 public、private、protected 来指定的。关键字 public、private、protected 称为访问修饰符。

一个类可以有多个 public、protected 或 private 标记区域。每个标记区域在下一个标记区域开始之前或者在遇到类主体结束右括号之前都是有效的。成员和类的默认访问修饰符是 private。

      class Base {
               public:
              // 公有成员

               protected:
              // 受保护成员  

               private:
              // 私有成员
            };
      
(1)公有（public）成员
公有成员在程序中类的外部是可访问的。您可以不使用任何成员函数来设置和获取公有变量的值

(2)私有（private）成员
私有成员变量或函数在类的外部是不可访问的，甚至是不可查看的。只有类和友元函数可以访问私有成员。

默认情况下，类的所有成员都是私有的。例如在下面的类中，width 是一个私有成员，这意味着，如果您没有使用任何访问修饰符，类的成员将被假定为私有成员：

            class Box
            {
               double width;
               public:
                  double length;
                  void setWidth( double wid );
                  double getWidth( void );
            };
            
实际操作中，我们一般会在私有区域定义数据，在公有区域定义相关的函数，以便在类的外部也可以调用这些函数，如下所示:

            #include <iostream>

            using namespace std;

            class Box
            {
               public:
                  double length;
                  void setWidth( double wid );
                  double getWidth( void );

               private:
                  double width;
            };

            // 成员函数定义
            double Box::getWidth(void)
            {
                return width ;
            }

            void Box::setWidth( double wid )
            {
                width = wid;
            }

            // 程序的主函数
            int main( )
            {
               Box box;

               // 不使用成员函数设置长度
               box.length = 10.0; // OK: 因为 length 是公有的
               cout << "Length of box : " << box.length <<endl;

               // 不使用成员函数设置宽度
               // box.width = 10.0; // Error: 因为 width 是私有的
               box.setWidth(10.0);  // 使用成员函数设置宽度
               cout << "Width of box : " << box.getWidth() <<endl;

               return 0;
            }
            当上面的代码被编译和执行时，它会产生下列结果：

            Length of box : 10
            Width of box : 10
            
保护（protected）成员
保护成员变量或函数与私有成员十分相似，但有一点不同，保护成员在派生类（即子类）中是可访问的。(这里牵扯了继承）


# 类的构造函数
类的构造函数是类的一种特殊的成员函数，它会在每次创建类的新对象时执行。

构造函数的名称与类的名称是完全相同的，并且不会返回任何类型，也不会返回 void。构造函数可用于为某些成员变量设置初始值。

下面的实例有助于更好地理解构造函数的概念：

            #include <iostream>

            using namespace std;

            class Line
            {
               public:
                  void setLength( double len );
                  double getLength( void );
                  Line();  // 这是构造函数

               private:
                  double length;
            };

            // 成员函数定义，包括构造函数
            Line::Line(void)
            {
                cout << "Object is being created" << endl;
            }

            void Line::setLength( double len )
            {
                length = len;
            }

            double Line::getLength( void )
            {
                return length;
            }
            // 程序的主函数
            int main( )
            {
               Line line;

               // 设置长度
               line.setLength(6.0); 
               cout << "Length of line : " << line.getLength() <<endl;

               return 0;
            }
            当上面的代码被编译和执行时，它会产生下列结果：

            Object is being created
            Length of line : 6
