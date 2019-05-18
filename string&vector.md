
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
    string s1= "hello", s2= "world";     // 在s1和s2中都没有标点符号
    string s3 =s1 + ", " + s2+ '\n';      // 当把string对象和字符字面值及字符串混在一起时，每个“+”符的两侧的运算对象至少有一个是string。
    
    eg: 
     string s4 =s1+ ", ";        // true
     string s5= "hello" +","       // false: 两个运算对象都不是string
     string s6= s1+ ", "+ s2       //true
     string s7= "hello" + ", "+ s2   // false： 第一个加号加号两侧都不是string
     
     
（8）处理string对象中的字符

. 常用的string函数：

 ![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-16%2011.15.57.png)


. 处理每个字符： （for loop）

      string str("some string") ;
      for (auto c : str){      //对于str中每个字符
        cout<< c<< endl;}      // 输出当前字符，后面紧跟一个换行符
  
for loop把变量c和str 联系了起来。此例中，我们使用auto 关键字让编译器来决定变量c的类型，这里c的类型是char. 每次迭代，str 中的每个字符被拷贝给c。输出一个，然后换行。

. 使用范围for 语句改变字符串中的字符：

如果想改变string对象中字符的值，必须把循环变量定义成引用类型【（参见2.3.1）补充】。所谓的引用只是给定对象的一个别名， 因此当使用引用作为循环控制变量时，这个变量实际上被依次绑定到了序列的每个元素上。使用这个变量我们就能改变绑定他的字符。
eg:

      string s("Hello World!!!"); 
      //转换大写形式
      for (auto &c : s){      //对于s中的每个字符
      c = toupper(c);}        //c是一个引用， 因此赋值语句将变成s中字符的值
      cout<<s<<endl;           //HELLO, WORLD!!!

. 只处理部分字符

处理string对象中每一个字符，使用范围for loop是个好主意。 然而有时我们需要访问的只是其中一部分字符， 这时有两种方法： （1）访问下标； （2） 使用迭代器（3.4 和第九章）

> 下标运算符（[ ]) ：
其接受的输入参数是string::size_type类型的值，这个参数表示访问的位置，返回值是该位置上字符的引用。
string对象的下标从0开始计。 如果string 对象s至少包含两个字符，则s[0]是第一个字符， s[1] 是第二个字符， s[s.size()-1]是最后一个字符。

eg: 
string s("some string") 
if (!s.empty())
  s[0] = toupper(s[0]);
cout<<s<<endl;          //Some string

>使用迭代器

      //依次处理s中的字符直到遇到空格
      for (decltype(s.size())  index=0; index !=s.size() && !isspace(s[index]); ++index)
            s[index] = toupper[s[index]];      
      cout<<s<<endl;          // SOME string
 
 此过程中， for循环变量使用index作为s的下标， index的类型是由decltype关键字决定的。 首先index初始化为0， 这样迭代器就从s的首字母开始；之后每次迭代index都加1得到s中的在一个字符，直到末尾或者空格结束。
 
 > 使用下标执行随机访问
 
 通过计算得到某个下标值，然后直接获取对应位置的字符
 
# 标准库类型 vector

标准库类型vector表示对象的集合， 其中所有对象的类型都相同。 集合中的每个对象都有一个与之对应的索引， 所用于访问对象。 因为 vector“容纳着”其他对象， 所以他也被称作容器（container）。

(1)使用vector： 

      #include <vector>
      using std::vector;
  
(2) c++ 语言中有： 类模版（class template）， 和 函数摸版。 其中vector是class template。

** 模版本身不是类或者函数，可以将模版看作为编译器声成类或函数编写的一份说明。编译器根据模版创建类或者函数的过程称为实例化（instantiation), 当使用模版时，需要指出编译器应把类或函数实例化成什么类型。

对于模版来说，我们通过提供一些额外信息来指定模版实例化成什么样的类，需要提供哪些信息需要模版来决定。提供信息的方式：在模版名字后边跟一对尖括号，在括号内放上信息。
eg: 

      vector<int> ivec;      //ivec 保存int 类型的对象
      vector<vector<string>> file;          //该向量元素是vector对象
** 

vector能容纳绝大多数类型的对象作为其元素，但是因为引用不是对象，所以不存在包含引用的vector。 除此之外，其他大多数（非引用）内置类型和类类型都可以构成vector对象， 甚至组成vector的元素也可以是vector。

# 定义和初始化vector对象
. vector模版控制着定义和初始化向量的方法。 常用方法：

      vector <T> v1           //v1 是一个空vector，它潜在元素类型是T，执行默认初始化
      vector <T> v2(v1)        //v2 中包含v1的副本
      vector <T>  v2=v1        //等价于v2（v1)
      vector <T>  v3(n,val)    //v3包含了n个重复元素，每个元素值是val
      vector <T>  v4(n)        //v4包含了n个重复执行了值初始化的对象
      vector <T>v5{a,b,c,...}  //v5包含了初始值个数的元素，每个元素被赋予相应的初始值
      vector <T> v5={a,b,c,...}  //同vector <T>v5{a,b,c,...} 
  

. 一般先建一个空vector，然后当运行时获取到元素的值后再逐一添加。

  当然也可以在定义vector对象时指定元素的初始值，例如把一个vector对象的元素拷贝给另外一个vector的对象。此时，新vector对象元素就是原vector对象对应元素的副本。注意两个vector对象的类型必须相同。
eg:

    vector<int> ivec;              //初始状态
    vector<int> ivec2(ivec);       //把ivec的元素拷贝给ivec2
    vector<int> ivec3=ivec;        //把ivec的元素拷贝给ivec3
    vector<string> svec(ivec2);    //错： 两者对象的类型不一样
 
 . 列表初始化vector对象
   c++ 11 提供了另外一种为vector对象的元素赋值法，及列表初始化。 用花括号括起来的0个或多个初始元素值背负给vector对象。
   
     vector<string> v1{"a","an", "the"}   //right: 列表初始化
     vector<string> v2("a","an", "the")    //false， 没用花括号
     
. 创建指定个数 

     vector<int> ivec(10,-1)     // 10个int类型的元素， 每个元素值被初始化为-1
     vector<string> svec(10,"hi")    //10个string类型的元素， 每个元素值被初始化为hi
  
 . 值初始化
 
  通常情况下，可以只提供vector对象容纳的元素数量而不去略去初始值。此时库会创建一个值初始化的（value-initialized) 元素初始值，并把它赋给容器中的所有元素。这个值的类型由vector对象中的元素类型决定。
    
    vector<int> ivec(10)；   //10个元素，每个初始化为0
    vector<string> ivec(10)   //10个元素，每个初始化为空string对象
    vector<int> v1=10           //false,只有元素数量没有设定初始值
 . 列表初始值还是元素数量  
  
  在某些情况下，初始化的真实依赖于传递初始值时用的是花括号还是圆括号。
  圆括号，提供的值是用来构造（construct）vector 对象的
  花括号表示我们想要列表初始化 （list initialize) vector 对象
  
    vector<int> v1(10);        //v1有10个元素，每个元素值为0
    vector<int> v2{10};        //有一个元素， 元素值为10
    vector<int> V3(10,1);       //有10个元素， 每个值为1
    vector<int> V4{10,1};       //有两个元素，值为10，1
  
  如果初始化时使用了花括号的形式但是提供的值又不能用来列表初始化，就要考虑用这样的值来构造vector对象了。
     
     vector<string> v5{"hi"};          // 列表初始化： 有一个元素
     vector<string> v6("hi");          //false： 不能使用字符串字面值构建vector
     vector<string> v7{10};           //有10个默认初始化的元素
     vector<string> v8{10,"hi"};        //有10个值为“hi"的元素
     
 # 向vector中添加元素
 利用push_back 成员函数向其中添加元素。 push_back 负责把一个值当成vector对象的尾元素“压到（push)" vector 对象的尾端：
 
       vector<int> v2;                 //build an empty vector 
       for (int i=0; i!=00; ++i){         
          v2.push_back(i);}               //依次把整数值放到v2尾端
          //循环结束后， v2 有100个元素，值从0到99

. vector 能方便高效的加入新元素，很多程序得到简化。但是要求：其中一条就是保证所写的循环正确无误，特别是在循环在有可能改变vector对象容量的时候。
  
  如果循环体内部包含有向vector对象添加元素的语句，则不能使用for循环（ for 循环语句内不应该改变其遍厉序列的大小。
  
  # vector 其他操作
  
  ![](https://github.com/linbearababy/primer-c-/blob/master/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-05-18%2017.15.20.png)
     
（1) 访问vector 对象中的元素方法也是通过元素在vector 对象中的位置。

    vector<int> v{1,2,3,4,5,6,7,8,9};
    for (auto &i: v){           //对于v中每个元素（注意是引用，之前提到过）
      i*=i;}                    // 求元素值的平方
    for (auto i:v){             // 对于v中的每个元素
      cout<< i<< " ";}           //输出该元素
    cout<<endl;

(2)vector 的empty & size 功能和用法与string 完全一样
但注意 ： 要使用size_typ， 需要确定它是由哪种类型定义的。vector对象的类型总是包含着元素的类型

    vector<int> ::size_type            //正确
    vector::size_type                  //错误

（3）
两个vector 相等， 当且仅当他们所含的元素个数相同，而且对应位置的元素值也相同。
如果两者的容量不同，但是相同位置上的元素值一样。则元素较少的小于元素较多的
元素值有区别：则大小关系由第一对相异的元素值的大小关系决定

当只有元素的值可比较时。vector对象才能被比较。

（4）计算vector内对象的索引
和string 一样，vector 也是使用下标运算符。
eg: 
