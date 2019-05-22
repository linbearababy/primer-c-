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

在要求使用基类型对象的地方，我么可以用继承类型的对象来代替。这意味着，接受一个iostream 类型引用（或指针）参数的函数，可以使用一个对应的fstream(或sstream)类型来调用。也就是说，如果有一个函数接受一个ostream&参数，我们在调用这个函数时，可以传递给他一个ofstream对象，对istream& 和 ifstream 也是类似的。

# 常用方法

（1）打开文件

在从文件读取信息或者向文件写入信息之前，必须先打开文件。ofstream 和 fstream 对象都可以用来打开文件进行写操作，如果只需要打开文件进行读操作，则使用 ifstream 对象。

下面是 open() 函数的标准语法，open() 函数是 fstream、ifstream 和 ofstream 对象的一个成员。

    void open(const char *filename, ios::openmode mode);
    在这里，open() 成员函数的第一参数指定要打开的文件的名称和位置，第二个参数定义文件被打开的模式。
    
    模式标志	描述
    ios::app	追加模式。所有写入都追加到文件末尾。
    ios::ate	文件打开后定位到文件末尾。
    ios::in	    打开文件用于读取。
    ios::out	打开文件用于写入。
    ios::trunc	如果该文件已经存在，其内容将在打开文件之前被截断，即把文件长度设为 0。

您可以把以上两种或两种以上的模式结合使用。例如，如果您想要以写入模式打开文件，并希望截断文件，以防文件已存在，那么您可以使用下面的语法：

    ofstream outfile;
    outfile.open("file.dat", ios::out | ios::trunc );
    
类似地，您如果想要打开一个文件用于读写，可以使用下面的语法：

    ifstream  afile;
    afile.open("file.dat", ios::out | ios::in );

（2） 关闭文件

当 C++ 程序终止时，它会自动关闭刷新所有流，释放所有分配的内存，并关闭所有打开的文件。但程序员应该养成一个好习惯，在程序终止前关闭所有打开的文件。

下面是 close() 函数的标准语法，close() 函数是 fstream、ifstream 和 ofstream 对象的一个成员

    void close();
    
（3）读取文件

在 C++ 编程中，我们使用流提取运算符（ >> ）从文件读取信息，就像使用该运算符从键盘输入信息一样。唯一不同的是，在这里您使用的是 ifstream 或 fstream 对象，而不是 cin 对象。

（4）写入文件

在 C++ 编程中，我们使用流插入运算符（ << ）向文件写入信息，就像使用该运算符输出信息到屏幕上一样。唯一不同的是，在这里您使用的是 ofstream 或 fstream 对象，而不是 cout 对象。

（5）读取&写入 示例

下面的 C++ 程序以读写模式打开一个文件。在向文件 afile.dat 写入用户输入的信息之后，程序从文件读取信息，并将其输出到屏幕上：

        #include <fstream>
        #include <iostream>
        using namespace std;

        int main ()
        {

           char data[100];

           // 以写模式打开文件
           ofstream outfile;
           outfile.open("afile.dat");

           cout << "Writing to the file" << endl;
           cout << "Enter your name: "; 
           cin.getline(data, 100);

           // 向文件写入用户输入的数据
           outfile << data << endl;

           cout << "Enter your age: "; 
           cin >> data;
           cin.ignore();

           // 再次向文件写入用户输入的数据
           outfile << data << endl;

           // 关闭打开的文件
           outfile.close();

           // 以读模式打开文件
           ifstream infile; 
           infile.open("afile.dat"); 

           cout << "Reading from the file" << endl; 
           infile >> data; 

           // 在屏幕上写入数据
           cout << data << endl;

           // 再次从文件读取数据，并显示它
           infile >> data; 
           cout << data << endl; 

           // 关闭打开的文件
           infile.close();

           return 0;
        }

        上面的代码被编译和执行时，它会产生下列输入和输出：
        $./a.out
        Writing to the file
        Enter your name: Zara
        Enter your age: 9
        Reading from the file
        Zara
        9

上面的实例中使用了 cin 对象的附加函数，比如 getline()函数从外部读取一行，ignore() 函数会忽略掉之前读语句留下的多余字符。



