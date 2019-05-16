
# 想把string和vector这一块写一下，让自己加深一下。
# 内容：
  #. introduction of string&vecotr
  #. vector 常见用法

# 简介
  . c++ 定义了一个内容丰富的抽象数据类型库，其中最重要的是 string & vector。
        string 支持可变长字符串； vector 表示可变长集合

  .还有一种标准库的类型是迭代器： 他是string和vector 的配套类型，常被用于访问string和vector中的元素

  . 内置数组是一种更基础的类型， string和vector都是对他的某种抽象。内置数组和其他内置类型一样， 数组的实现与硬件密切相关。所以相对于标准库类型      string和vector， 数组灵活性不足。

# 命名空间using声明
目前用到的库的函数都属于命名空间std. eg: std::cin   ("::"--操作符， 表示编译器从操作符左边名字的作用域中寻找操作符右侧的名字）

using 就是简化这个操作符的一个方法。 using namespace::name; 一旦声明了这个陈述句， 就可以直接命名空间中的名字 
每个名字都要独立using声明
每个名字都要独立using声明字符串
每个名字都要独立using声明
eg:

      #include <iostream>
      using namespace::name;
      using std::cin;
      int main(){
        int i: 
        cin>>i;
        cout<< i;   // 错误没有声明
        std::cout<<i;
        return 0;
        }
  
  
# 标准库类型string

. 使用：

      #include <string>
      using std::string 

. 定义和初始化string :
如何初始化类的对象是由类的本身决定的。 一个类可以定义很多初始化对象的方式， 只不过这些方式之间必须有区别：初始值的数量不同，初始值的类型不同；

初始化string对象的方式：

      string s1       默认初始化， s1是个空串
      string s2(s1)       s2是s1的副本       
      string s2=s1          等价于s2是s1的副本
      string s3("value"）        s3 是字面值“value” 的副本，除了字面值最后那个空字符外
      string s3 = "value"        等价于 string s3("value"）
      string s4(n,'c')        把s4初始化为连续n个字符c组成的串
      
“=”初始化一个变量--拷贝初始化（copy initilization);   否则是直接初始化（direct initialization)

# string 的操作
（1）读写 用IO操作符直接读写 （cin, cout)

（2）getline 读取
getline 函数的参数是一个输入流和一个string对象。 函数从给定的输入流中读入内容，直到遇到换行符为止（注意换行符也读入了）， 然后把所读的内容存入到那个string对象去（不存换行符）。 getline 读取的换行符在返回结果时被去掉了。

      #include <string>
      #include <iostream>
      #include <sstream>

      int main()
      {
          // greet the user
          std::string name;
          std::cout << "What is your name? ";
          std::getline(std::cin, name);
          std::cout << "Hello " << name << ", nice to meet you.\n";

          // read file line by line
          std::istringstream input;
          input.str("1\n2\n3\n4\n5\n6\n7\n");
          int sum = 0;
          for (std::string line; std::getline(input, line); ) {
              sum += std::stoi(line);
          }
          std::cout << "\nThe sum is: " << sum << "\n";
      }
      Possible output:

      What is your name? John Q. Public
      Hello John Q. Public, nice to meet you.

      The sum is 28


输出一整行：

      int main(){
        string line;
        //每次输入一整行， 直到文件末尾
        while (getline(cin, line)){
          cout<< line<<endl;}
        return 0;}
        
（3）string size() &empty

. empty 函数根据string是否为空返回一个对应的bool值

. size 函数返回string对象的长度

 (4) string::size_type类型
 
 size 函数返回的是string::size_type类型的值
 
 auto len = line.size(); //len的类型是string::size_type类型
 
 （5） 比较string对象
 
 . 对大小写敏感， 在比较一个字母的大写形式和小写形式是不同的
 . == 和 != 分辨检验两个string相等或者不等
 . string 相等： 长度相同， 所包含的字符也都相同 （依照大小写敏感的字典顺序）
      如果长度不， 且短的string对象的每个字符都和较长的string对象的每个字符对应位置相同 则短string对象小于长的string对象
      如果两个string对象在某些对应位置上不一样， 则按对象中第一个相异字母比较的结果
      
（6）string对象相加
eg:

      string s1 = "hello," , s2= "world/n";     
      string s3 = s1+s2;                // s3 的内容是hello, world/n
      s1+=s2;                           // 等于 s1=s1+s2

(7) 字面值和string对象相加



 
#

