这是基于C++ Primer的8.1 & 8.2 & 8.3的IO 库。 主要包括 IO 类， 文件输入输出， string 流。

# IO 类

![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-22%2012.58.09.png)

# io 类型间的关系

![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-22%2013.15.19.png)

# IO 对象无拷贝或赋值

![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-22%2013.16.17.png)

# 条件状态

![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-22%2013.16.31.png)

![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-22%2013.16.53.png)


# 文件输入和输出

头文件fstream 定义了三个类型来支持文件 IO: ifstream从一个给定文件读取数据， ofstream向一个给定文件写入数据，以及fstream 可以读写给定文件。

这些类型提供的操作和我们之前说的对象cout and  cin 的操作一样。我们可以用io运算符（ << 和 >>) 来读写文件，可以用getline从一个ifstream 读取数据。

除了继承自iostream类型的行为之外， fstream中定义的类型还增加了一些新的成员来管理与流关联的文件。我们可以对fstream, ifstream, ofstream对象调用这些操作，但不能对其他io类型调用这些操作。

![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-22%2013.38.24.png)

# 使用文件流对象

当我们想要读取一个文件时，可以定义一个文件流对象，并将对象与文件关联起来。每个文件流都定义了一个名为open的成员函数，他完成了以一些系统相关的操作，来定位给定的文件，并视情况打开为读写模式。

创建文件流对象时，我们可以提供文件名。如果提供了一个文件名，则open会自动被调动：

    ifstream  in(infile);                 //构造一个ifstream 并打开给定文件
    ofstream  out;                        //输出文件流未并关联到任何文件

这段代码定义了一个输入流in，它被初始化为从文件读取数据，文件名由string类型的参数ifle 指定。第二条语句定义了一个输出流out, 未与任何文件并联。

# 用fstream 代替iostream&

 

