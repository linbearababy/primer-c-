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

例如，我们可以用


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

# cin ; get ; cin.get ;  cin.getline ; getline  用法（这是我引用的一片博主的文章，觉得写得不错）：

在学习C++的过程中，经常会遇到输入输出的问题，以下总结一下下面几个函数的用法： 

        1)、cin 
        2)、cin.get() 
        3)、cin.getline() 
        4)、getline() 
        5)、gets()

1、cin>> 
　　用法1：最基本，也是最常用的用法，输入一个数字：

      #include <iostream>
      using namespace std;
      main ()
      {
      int a,b;
      cin>>a>>b;
      cout<<a+b<<endl;
      }

　　输入：2[回车]3[回车] 
　　输出：5

　　用法2：接受一个字符串，遇“空格”、“TAB”、“回车”都结束

       #include <iostream>
      using namespace std;
      main ()
      {
      char a[20];
      cin>>a;
      cout<<a<<endl;
      }

　　输入：jkljkljkl 
　　输出：jkljkljkl 
　　输入：jkljkl jkljkl //遇空格结束 
　　输出：jkljkl 
　　 
2、cin.get() 
　　用法1： cin.get(字符变量名)可以用来接收字符

       #include <iostream>
      using namespace std;
      main ()
      {
      char ch;
      ch=cin.get();   //或者cin.get(ch);
      cout<<ch<<endl;
      }
      
　　输入：jljkljkl 
　　输出：j 
　　用法2：cin.get(字符数组名,接收字符数目)用来接收一行字符串,可以接收空格

       #include <iostream>
      using namespace std;
      main ()
      {
      char a[20];
      cin.get(a,20);
      cout<<a<<endl;
      }

　　输入：jkl jkl jkl 
　　输出：jkl jkl jkl 
　　输入：abcdeabcdeabcdeabcdeabcde （输入25个字符） 
　　输出：abcdeabcdeabcdeabcd （接收19个字符+1个’\0’） 
　　用法3：cin.get(无参数)没有参数主要是用于舍弃输入流中的不需要的字符,或者舍弃回车,弥补cin.get(字符数组名,接收字符数目)的不足. 
　　 
3、cin.getline() // 接受一个字符串，可以接收空格并输出

      #include <iostream>
      using namespace std;
      main ()
      {
      char m[20];
      cin.getline(m,5);
      cout<<m<<endl;
      }

　　输入：jkljkljkl 
　　输出：jklj 
接受5个字符到m中，其中最后一个为’\0’，所以只看到4个字符输出； 
　　如果把5改成20： 
　　输入：jkljkljkl 
　　输出：jkljkljkl 
　　输入：jklf fjlsjf fjsdklf 
　　输出：jklf fjlsjf fjsdklf 
　　//延伸： 
　　//cin.getline()实际上有三个参数，cin.getline(接受字符串的看哦那间m,接受个数5,结束字符) 
　　//当第三个参数省略时，系统默认为’\0’ 
　　//如果将例子中cin.getline()改为cin.getline(m,5,’a’);当输入jlkjkljkl时输出jklj，输入jkaljkljkl时，输出jk 
　　当用在多维数组中的时候，也可以用cin.getline(m[i],20)之类的用法：

       #include<iostream>
      #include<string>
      using namespace std;          
      main ()
      {
      char m[3][20];
      for(int i=0;i<3;i++)
          {
          cout<<"\n请输入第"<<i+1<<"个字符串："<<endl;
          cin.getline(m[i],20);
          }
      cout<<endl;
      for(int j=0;j<3;j++)
      cout<<"输出m["<<j<<"]的值:"<<m[j]<<endl;
      }

　 请输入第1个字符串： 
　　kskr1 
　　请输入第2个字符串： 
　　kskr2 
　　请输入第3个字符串： 
　　kskr3 
　　输出m[0]的值:kskr1 
　　输出m[1]的值:kskr2 
　　输出m[2]的值:kskr3

4、getline() // 接受一个字符串，可以接收空格并输出，需包含“#include”

      #include<iostream>
      #include<string>
      using namespace std;
      main ()
      {
      string str;
      getline(cin,str);
      cout<<str<<endl;
      }

　　输入：jkljkljkl 
　　输出：jkljkljkl 
　　输入：jkl jfksldfj jklsjfl 
　　输出：jkl jfksldfj jklsjfl 
　　和cin.getline()类似，但是cin.getline()属于istream流，而getline()属于string流，是不一样的两个函数

5、gets() // 接受一个字符串，可以接收空格并输出，需包含“#include”

      #include<iostream>
      #include<string>
      using namespace std;
      main ()
      {
      char m[20];
      gets(m);     //不能写成m=gets();
      cout<<m<<endl;
      }

　　输入：jkljkljkl 
　　输出：jkljkljkl 
　　输入：jkl jkl jkl 
　　输出：jkl jkl jkl 
　　类似cin.getline()里面的一个例子，gets()同样可以用在多维数组里面：

　　   #include<iostream>
      #include<string>
      using namespace std;
      main ()
      {
      char m[3][20];
      for(int i=0;i<3;i++)
          {
          cout<<"\n请输入第"<<i+1<<"个字符串："<<endl;
          gets(m[i]);
          }
      cout<<endl;
      for(int j=0;j<3;j++)
      cout<<"输出m["<<j<<"]的值:"<<m[j]<<endl;
      }

　　请输入第1个字符串： 
　　kskr1 
　　请输入第2个字符串： 
　　kskr2 
　　请输入第3个字符串： 
　　kskr3 
　　输出m[0]的值:kskr1 
　　输出m[1]的值:kskr2 
　　输出m[2]的值:kskr3 
　　自我感觉gets()和cin.getline()的用法很类似，只不过cin.getline()多一个参数罢了；
这里顺带说明一下，对于本文中的这个kskr1,kskr2,kskr3的例子，对于cin>>也可以适用，原因是这里输入的没有空格，如果输入了空格，比如“ks kr jkl[回车]”那么cin就会已经接收到3个字符串，“ks,kr,jkl”；再如“kskr 1[回车]kskr 2[回车]”，那么则接收“kskr,1,kskr”；这不是我们所要的结果！而cin.getline()和gets()因为可以接收空格，所以不会产生这个错误。
   --------------------- 
（作者：木顶思上 
来源：CSDN 
原文：https://blog.csdn.net/JIEJINQUANIL/article/details/50802902 
版权声明：本文为博主原创文章，转载请附上博文链接！）

# string 流：
sstream 头文件定义了三个类型来支持内存IO，这些类型可以向string写入数据，从string读取数据，就像string是一个io流一样：

istringstream: 从string读取数据
ostringstream: 向string写入数据
stringstream:  既可以从string读数据，也可以向string写数据。

# istringstream

当我们的某些工作是对整行文本进行处理，而其他一些工作是处理行内的单个单词时，通常可以使用 istringstream。

考虑这样一个例子，假设有一个文件，列出了一些人和他们的电话号码。某些人只有一个号码，而另一些人则有多个 ---家庭电话，工作电话，移动电话等。我们输入的文件看起来可能是这样的：

        Morgan  2015552368   8625550123
        drew    9735550130
        lee     6095550132   8005550000
        
首先定义一个简单的类：
//成员默认为公有：

    struct PersonInfo{
        string name;
        vector<string> phones;
    };

类型PersonInfo 的对象会有一个成员来表示人名，还有一个vector来保存此人的所有电话号码。

我们的程序会读取数据文件，并创建一个PersonInfo 的vector。 vector 中每个元素对应文件中的一条记录。我们在一个循环中处理输入数据，每个循环步读取一条记录，提取出一个人名和若干电话号码：

    string line, words;                        //分别保存来自输入的一行和单词
    vector<PersonInfo>people;                   //保存来自输入的所有记录
    //逐行输入读取数据，直至cin 遇到文件尾（或其他错误）
    while (getline(cin,line)){
        PersonInfo info;                        //创建一个保存此记录数据的对象
        isstringstream record(line);            
        record >> info.name;
        while (record >> word)
            info.phone.push_back(word);
        people.push_back(info);
    }
    
我们用getline 从标准库输入读取整条记录。如果getline调用成功，那么line只将保存着从输入文件而来的一条记录。

