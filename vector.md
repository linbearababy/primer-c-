
# 想把string和vector这一块写一下，让自己加深一下。
# 内容：
  # . introduction of string&vecotr
  # . vector 常见用法

. c++ 定义了一个内容丰富的抽象数据类型库，其中最重要的是 string & vector。
      string 支持可变长字符串； vector 表示可变长集合

.还有一种标准库的类型是迭代器： 他是string和vector 的配套类型，常被用于访问string和vector中的元素

. 内置数组是一种更基础的类型， string和vector都是对他的某种抽象。内置数组和其他内置类型一样， 数组的实现与硬件密切相关。所以相对于标准库类型string和vector， 数组灵活性不足。

# 命名空间using声明
目前用到的库的函数都属于命名空间std. eg: std::cin   ("::"--操作符， 表示编译器从操作符左边名字的作用域中寻找操作符右侧的名字）

using 就是简化这个操作符的一个方法。 using namespace::name; 一旦声明了这个陈述句， 就可以直接命名空间中的名字 
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
使用：

      #include <string>
      using std::string 

  
