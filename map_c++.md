# Map
Maps are associative containers that store elements formed by a combination of a key value and a mapped value, following a specific order.

In a map, the key values are generally used to sort and uniquely identify the elements, while the mapped values store the content associated to this key. The types of key and mapped value may differ, and are grouped together in member type value_type, which is a pair type combining both:

 
        typedef pair<const Key, T> value_type;
        
# 性质

Container properties

Associative

Elements in associative containers are referenced by their key and not by their absolute position in the container.

Ordered

The elements in the container follow a strict order at all times. All inserted elements are given a position in this order.
Map

Each element associates a key to a mapped value: Keys are meant to identify the elements whose main content is the mapped value.

Unique keys

No two elements in the container can have equivalent keys.

Allocator-aware

The container uses an allocator object to dynamically handle its storage needs.

容器属性

联想

关联容器中的元素由其key引用，而不是由它们在容器中的绝对位置引用。

有序

容器中的元素始终遵循严格的顺序。 所有插入的元素按此顺序给出一个位置。

地图

每个元素将key与映射value相关联：key用于标识主要内容为映射值的元素。

独特的钥匙
容器中没有两个元素可以具有等效key。

分配器感知

容器使用allocator对象来动态处理其存储需求。

Map是c++的一个标准容器，提供了很好一对一的关系

# map最基本的构造函数；

   map<string , int >mapstring;         map<int ,string >mapint;
   map<sring, char>mapstring;         map< char ,string>mapchar;
   map<char ,int>mapchar;            map<int ,char >mapint；
   
# 常用方法
    . iterator: 
          begin
          end
    
    . capcity 
          size
          empty
          
    . modify
          insert
          erase
          swap
          clear
    . operation
          find
          lower_bound
          upper_bound
          
# map添加数据；



       map<int ,string> dic;  
       1.dic.insert(pair<int,string>(102,"aclive"));

       2.dic.insert(map<int,string>::value_type(321,"hai"));

       3, dic[112]="April";//map中最简单最常用的插入添加！
   

# map中元素的查找：

       find()函数返回一个迭代器指向键值为key的元素，如果没找到就返回指向map尾部的迭代器。        

       map<int ,string >::iterator lo;; 

       lo=dic.find(112);

       if(l_it==maplive.end())
                    cout<<"we do not find 112"<<endl;
       else cout<<"wo find 112"<<endl;
   
# map中元素的删除：erase

   如果删除112； 
   
       map<int ,string >::iterator l_it;;
       
       l_it=maplive.find(112);

       if(l_it==maplive.end())
            cout<<"we do not find 112"<<endl;
            
       else  maplive.erase(l_it);  //delete 112;
   

5,map中 swap的用法：

  Map中的swap不是一个容器中的元素交换，而是两个容器交换；
  
  map的sort问题：
  Map中的元素是自动按key升序排序,所以不能对map用sort函数：
