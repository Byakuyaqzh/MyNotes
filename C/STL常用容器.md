[TOC]





## STL

​	STL：Standard Template Library，标准模板库。内置了一些高效的C++程序库，为C++程序员们提供了一个可扩展的应用框架。

​	STL提供了六大组件:容器，算法，迭代器，仿函数，适配器(配接器)，空间配置器

​	**容器**（Container）：各种数据结构，如vector、list、map等

​	**算法**（Algorithm）：各种常用的算法，如sort、find等

​	**迭代器**（iterator）：扮演了容器与算法之间的胶合剂（类似于指针等）

​	**仿函数**：行为类似函数，可作为算法的某种策略

​	**适配器**（adapter）：一种用来修饰容器或者仿函数或迭代器接口的东西

​	**空间配置器**：负责空间的配置与管理

STL六大组件的交互关系，容器通过空间配置器取得数据存储空间，算法通过迭代器存储容器中的内容，仿函数可以协助算法完成不同的策略的变化，适配器可以修饰仿函数。





#### 容器

​	分为 **序列式容器** 和 **关联式容器**

**序列式容器**：序列式容器就是容器元素在容器中的位置是由元素进入容器的时间和地点来决定

**关联式容器**：关联式容器是指容器已经有了一定的规则，容器元素在容器中的位置由容器的规则来决定

#### 算法

​	分为 **质变算法** 和 **非质变算法**

质变算法：是指运算过程中会更改区间内的元素的内容，如替换、删除

非质变算法：是指运算过程中不会更改区间内的元素内容，如查找、计数

#### 迭代器

​	主要有 **双向迭代器** 和 **随机访问迭代器** 等。不支持迭代器随机访问的容器，只能用自增或自减。

双向迭代器：++, --可以访问下一个元素和上一个元素

随机访问迭代器：+2，可以跳2个元素访问元素

​	

**算法** 需要使用 **迭代器** 才能访问 **容器** 中的内容









------------------------

### 容器

#### 1 string  字符串

​	string的行为与普通容器类似，但是并不能说它是个**容器，**因为无法接受所有类型的数据，其内部数据类型只能为 char

```c++
//  头文件
#include<string>
```

```C++
//  初始化
string s;

//  拷贝构造
string s = "abcde";  //  拷贝初始化
string s("abcde");  //  直接初始化

//  拷贝构造
char * s = "abcde";
string s1(s);  //  直接初始化

//  按数量构造
//  s = "aaaaa"
string s(5, 'a');  //  直接初始化
string s = string(5, 'a');  //  拷贝初始化

//  使用 assign()
//  注意：若s中已有数据，会直接覆盖原有数据
string s0 = "abcde";
//  全部插入
s1.assign(s0);
//  插入一部分  s2 = "abc"   前闭后开
s2.assign(s0, 0, 3);
//  按数量构造
//  s3 = "aaaaa"
s3.assign(5, 'a');
```

​	常见算法:

​			1、 + ,  append()  字符串拼接

​			2、  substr()  截取字符串中的一部分

​			3、 find()  查找

​			4、  replace()  替换

​			5、 compare()   比较

​			6、 insert()   插入

​			7、 erase()  删除



```C++
//  1	+  字符串拼接
//  补充：append() 也可以用于拼接，方法与assign()类似

string s1 = "abc";
string s2 = "def";
//  直接使用 “+” 拼接
string s3 = s1 + s2;  //  s3 = "abcdef"
s1 += s2;     //  s1 = "abcabcdef"
```

```C++
//  2	substr()  截取字符串中的一部分

string s = "abcdef";
//  [0,3) 前闭后开， s1 = "abc"   即 0 1 2
string s1 = s.substr(0, 3);

//  只写一个参数，默认n到最后一位
string s2 = s.substr(3);  //  s2 = "def"
```

```C++
//  3	find()  查找
//  find()从左往右查找，rfind()从右往左查找
//  find的构造函数中有第二个参数:int pos = 0, 默认从第0个位置开始查找

//          01234567
string s = "abcdefde";

//  pos1 = 3  rpos1 = 6
int pos1 = s.find("de");
int rpos1 = s.rfind("de");

//  当查找失败时，会返回 nops，表示 string 的结束位置
//  s 中不包含k，查找失败，结果为string::nops
if(s.find(k) == string::nops){
    return false;
}
```

```C++
//  4	replace()  替换
//  构造函数：replace( pos, num, str )
//	从第 pos 个位置起，将接下来的 num 个数字，替换为 str

//          01234
string s = "abcde";

//  替换后：s = "abxyze"
s.replace(2, 2, "xyz")
```

```C++
//  5	compare()   比较
//  本质上是一个一个一个比较的

string s1 = "abc";
string s2 = "abc";
string s3 = "cbc";

//  res1 = 0
int res1 = s1.compare(s2);

//  res2 = -1
int res2 = s1.compare(s3);

//  res3 = 1
int res3 = s3.compare(s1);
```

```C++
//  6	insert()   插入
//  在某一位置下插入一段字符

//           01234
string s1 = "abcde";
string s2 = "abcde";

//  插入后 s1 = "ab111cde"
s1.insert(2, "111");

//  插入后 s2 = "abaaaaacde"
//  在 pos 后插入 num 个 str
s2.insert(2, 5, 'a');
```

```C++
//  7    erase()  删除

string s = "abcdefg";

//  删除 a 的 第 [1] 到第 [4] 个元素，即删除 [1,5) 内的元素，前闭后开
//  0   1   2  3   4  5  6
//  a  *b  *c *d  *e  f  g
a.erase( s.begin() + 1 , a.begin() + 5 );
```





#### 2 vector  动态数组

​	本质上是一个**顺序表**，底层实现用的是三个指针，然后利用这三个指针相互加减，达到存储效果。

​	vector数组的扩展并非在原有基础上扩展，而是寻找新的空间，将原有数据复制过去，并释放原来的空间。

```C++
//  头文件
#include<vector>
```

```C++
//  初始化
vector<typename> name;

//  直接赋值
vector<int> a = { 1, 2, 3, 4 };

//  按数量构造
//  长度为 10，数组中的数据都是 -1
vector<int> a(10,-1);

//  拷贝构造
//  数组
b1[5] = { 1, 2, 3, 4, 5 };
vector<int> a1( b , b + 5 );
//  其他vector数组
vector<int> b2 = { 1, 2, 3, 4, 5 };
vector<int> a2( b0.begin() , b0.end() );

//  截取数其他数组的一部分, 前闭 后开
//                0  1  2  3  4  5  6
vector<int> b = { 1, 2, 3, 4, 5, 6, 7 };
//  a = { 3, 4 }
vector<int> a( b.begin() + 2, b.begin() + 4 );
//  全部拷贝可以使用  vector<int> a(b);
//  也可以直接  a = b;

//  使用assign()初始化，不常用，不再赘述
```

​	常见算法

​			0 、 常用操作

​			1、  resize()  重新指定大小

​			2、  insert()   插入元素

​			3、  erase()  删除元素

​			4、  swap()  交换两个容器中的所有元素

```C++
//  0  常用操作 

front();  //  返回第一个元素
back();  //  返回最后一个元素
empty();  //  判断是否为空，空 -> true，非空 -> false
size();  //  返回大小
capacity();  //  返回实际容量

push_back(a);  //  在末尾插入一个元素 a
pop_back();  //  删除最后一个元素
clear();  //  清空
```

```C++
//  1  resize()  重新指定大小
//  若容器变大，以默认值填充新位置
//  若容器变小，末尾超出长度的数据将被删除
//  注意：resize()仅指定大小，若容器变小，尽管大小改变，但容量不会改变

vector<int> a = {1,2,3,4,5};
//  变长，以新数据填充  注：第二个参数可省略，省略后默认填充0
//  a = {1,2,3,4,5,10,10,10}
a.resize(8, 10);
```

```C++
//  2  insert()  在某一位置下插入一段字符
//  有返回值，返回值是 指向插入的第一个数据位置的迭代器

//                0 1 2 3 4
vector<int> a1 = {1,2,3,4,5};
vector<int> a2 = {1,2,3,4,5};

//  插入后 a1 = {1,2,100,3,4,5}
a1.insert(a.begin() + 2, 100);

//  插入后 a2 = {1,2,10,10,10,3,4,5}
//  在 pos 后插入 num 个 number
s2.insert(a.begin() + 2, 3, 10);
```

```C++
//  3  erase()  删除元素
//  有返回值，返回删除后下一个元素的位置

vector<int> a = {1,2,3,4,5,6,7};

//  删除 a 的 第 [1] 到第 [4] 个元素，即删除 [1,5) 内的元素，前闭后开
//       0    1    2    3    4   5   6
//  a = {1,  *2,  *3,  *4,  *5,  6,  7}
//  *it = 6
vector<int>::iterator it = a.erase( a.begin() + 1 , a.begin() + 5 );
```

```C++
//  4  swap()  交换两个容器中的所有元素

vector<int> a1 = {1,2,3,4,5};
vector<int> a2 = {9,8,7};

//  交换两个容器的 大小 和 所有元素
a1.swap(a2);

//  注意：交换时将会重置容量，可以利用这个效果收缩内存
//  若有以下情况：
//	a  ->  vector<int>
//  a.size()  ->  10
//	a.capacity()  ->  20
//  可使用 swap() 收缩内存
vector<int> (a).swap(a);
//  结果为：
//  a.size()  ->  10
//	a.capacity()  ->  10
//  原理： 
//  vector<int> (a) 是一个匿名对象，该对象的值与 a 相同，且容量恰好为 a 的大小
//  vector<int> (a).swap(a) 将这个匿名对象与 a 交换，交换后 a 的容量缩小为 a 的实际大小
```





#### 3 stack 栈

​	栈，只有栈顶元素可以被操作，先进后出。不允许遍历、排序等算法。

```C++
//  头文件
#include<stack>
```

```C++
//  初始化
stack<typename> name;

//  一个空的栈
stack<int> s1;

//  拷贝构造
stack<int> s2(s1);
//  或  stack<int> s2 = s1;
```

​			常用操作

```C++
//  常用操作

push();  //  压入元素
top();  //  返回顶部元素
pop();  //  弹出栈顶元素，无返回值
size();  //  返回栈的大小
empty();  //  判断是否为空，空 -> true，非空 -> false
```





#### 4 queue 队列

​	队列，是一种操作受限的线性表，其特点是先进先出。不允许遍历、排序等算法。

​	在STL中，queue作为一种适配器，其底层容器一般为deque(双端队列)和list(双向链表)，其中deque为默认底层容器。

```c++
//  头文件
#include<queue>
```

```c++
//  初始化
queue<typename> name;

//  使用双端队列为底层容器创建一个空的queue队列对象q
queue<int> q;

//  以双端队列为底层容器创建一个空的queue队列对象q
queue<int,list<int>> q;

//  拷贝构造
queue<int> q1(q);
//  或  queue<int> q1 = q;
```

​			常用操作

```C++
//  常用操作

q.push(a);      //  将元素 a 从队尾插入
q.pop();        //  删除队首元素，无返回值
q.front();      //  返回队首元素
q.back();       //  返回队尾元素
q.size();       //  返回队中元素个数
q.empty();      //  判断是否为空（空返回 1，非空返回 0）
```



###### 补充：priority_queue

​	priority_queue优先队列，又称最大堆/最小堆，是一种容器适配器，采用了堆这样的数据结构，保证了第一个元素总是整个优先队列中**最大的**(或**最小的**)元素。priority_queue在插入时会自动排序。

```c++
//  构造函数
//  1、默认构造
priority_queue<T> pq;
//  2、指定比较规则的排序
//  Container是底层容器类型，默认为 std::vector<T>
//  Compare是比较规则的类型，可以是函数指针、函数对象或者 lambda 表达式，
//         默认情况下，如果不指定 Compare，则使用less<T>，即最大堆（队头元素最大）
priority_queue<T, Container, Compare> pq;

//  3、使用现有元素构造
vector<int> vec = {1, 2, 3, 4, 5};
priority_queue<int, vector<int>> pq(vec.begin(), vec.end());
```

```c++
//  自定义排序规则，创建最小堆（队头元素最小）
vector<int> vec = {1, 2, 3, 4, 5};
function<bool(int, int)> f = [](int a, int b) { return a > b; };

//  使用自定义排序规则时，需要在参数中传递f。使用less<int>或greater<int>时不需要
priority_queue<int, vector<int>, decltype(f)> pq(vec.begin(), vec.end(), f);

//  或：
priority_queue<int, vector<int>, decltype(f)> pq(f);
for(auto num : vec){
    pq.push(num);
}
```





#### 5 deque 双端队列

​	内部实际上分为多块，由一个中控器管理，维护每一段数据。deque的迭代器支持随机访问，支持排序。

```C++
//  头文件
#include<deque>
```

```C++
//  初始化
stack<typename> name;

//  一个空的双端队列
deque<int> dq1;

//  拷贝构造
deque<int> dq2(dq1);

//  按数量构造
//  长度为 10，内部的数据都是 -1
deque<int> dq3(10, -1);

//  使用assign()初始化，不常用，不再赘述
```



​			0、 常用操作

​			1、  resize()  重新指定长度

​			2、  insert()  在指定位置插入

​			3、  erase()   删除元素

```C++
//  0  常用操作

front(); //  返回第一个元素
back();  //  返回最后一个元素
empty();  //  判断是否为空，空 -> true，非空 -> false
size();  //  返回的大小


push_front(a);  //  在的首部插入一个元素 a
pop_front();  //  删除第一个元素
push_back(a);  //  在末尾插入一个元素 a
pop_back();  //  删除最后一个元素
clear();  //  清空
```

```C++
//  1  resize()  重新指定长度
//  若容器变大，以默认值 在尾部填充新位置
//  若容器变小，末尾超出长度的数据将被删除

deque<int> dq = {1,2,3,4,5};
//  变长，以新数据填充  注：第二个参数可省略，省略后默认填充0
//  a = {1,2,3,4,5,10,10,10}
dq.resize(8, 10);
```

```C++
//  2  insert()  在指定位置插入
//  有返回值，返回值是 指向插入的第一个数据位置的迭代器

//                0 1 2 3 4
deque<int> dq1 = {1,2,3,4,5};
deque<int> dq2 = {1,2,3,4,5};

//  第一个参数指定位置，第二、三个参数指定插入的数据，前闭后开
//  插入后 dq1 = {1, 2, *2, *3, 3, 4, 5}
dq1.insert(dq1.begin()+2, dq2.begin()+1, dq2.begin()+3);

//  插入后 dq2  = {1,2,10,10,10,3,4,5}
//  在 pos 后插入 num 个 number
dq2.insert(dq2.begin() + 2, 3, 10);
```

```C++
//  3  erase()  删除元素
//  有返回值，返回删除后下一个元素的位置

deque<int> dq = {1,2,3,4,5,6,7};

//  删除 dq 的 第 [1] 到第 [4] 个元素，即删除 [1,5) 内的元素，前闭后开
//        0    1    2    3    4   5   6
//  dq = {1,  *2,  *3,  *4,  *5,  6,  7}
//  *it = 6
vector<int>::iterator it = dq.erase( dq.begin() + 1 , dq.begin() + 5 );
```





#### 6 list 链表

​	链表，链式存储，是一种非连续的存储结构，数据元素的逻辑顺序是通过指针链接实现的，迭代器可以自增或自减，但不能增加指定步数，不支持随机访问。但可以使用**自带的 sort()** 排序。

​	STL中的链表是一种**双向循环**链表。 

```C++
//  头文件
#include<list>
```

```C++
//  初始化
list<typename> name;

//  直接赋值
list<int> l1 = {1,2,3,4,5};

//  拷贝构造
//  截取一部分
list<int> l2(l1.begin(), l1.end());
//  复制全部
list<int> l3(l1);
//  或  list<int> l3 = l1;

//  按数量构造
//  l4 = {10,10,10,10,10}
list<int> l4(5,10);

//  使用assign()初始化，不常用，不再赘述
```

​			0、  常用操作

​			1、  swap()   交换

​			2、  resize()    重新指定大小

​			3、  insert()    插入元素

​			4、  erase()    删除元素

​			5、  remove()    删除所有特定的元素

```C++
//  0  常用操作

front();  //  返回第一个元素
back();  //  返回最后一个元素
empty();  //  判断是否为空，空 -> true，非空 -> false
size();  //  返回大小

push_front(a);  //  在的首部插入一个元素 a
pop_front();  //  删除第一个元素
push_back(a);  //  在末尾插入一个元素 a
pop_back();  //  删除最后一个元素

reverse();  //  反转
clear();  //  清空
sort();   //  排序
//  链表不支持随机访问，不能使用sort(l.begin(), l.end())排序
//  但是list内置了sort()函数，使用方法： l.sort()
```

```C++
//  1  swap()   交换

list<int> l1 = { 1,2,3,4,5 };
list<int> l2 = { 5,4,3,2,1 };

//  交换l1和l2
l1.swap(l2);
```

```C++
//  2  resize()  重新指定长度
//  若容器变大，以默认值 在尾部填充新位置
//  若容器变小，末尾超出长度的数据将被删除

list<int> l = { 1,2,3,4,5 };
//  变长，以新数据填充  注：第二个参数可省略，省略后默认填充0
//  l = {1,2,3,4,5,10,10,10}
l.resize(8, 10);
```

```C++
//  3  insert()  插入元素
//  有返回值，返回值是 指向插入的第一个数据位置的迭代器

//              0 1 2 3 4
list<int> l1 = {1,2,3,4,5};
list<int> l2 = {1,2,3,4,5};

//  第一个参数指定位置，第二、三个参数指定插入的数据，前闭后开
//  插入后 l1 = {1, 2, *2, *3, 3, 4, 5}
l1.insert(l1.begin()+2, l2.begin()+1, l2.begin()+3);

//  插入后 l2  = {1,2,10,10,10,3,4,5}
//  在 pos 后插入 num 个 number
l2.insert(l2.begin() + 2, 3, 10);
```

```C++
//  4  erase()  删除元素
//  有返回值，返回删除后下一个元素的位置

list<int> l = {1,2,3,4,5,6,7};

//  删除 dq 的 第 [1] 到第 [4] 个元素，即删除 [1,5) 内的元素，前闭后开
//       0    1    2    3    4   5   6
//  l = {1,  *2,  *3,  *4,  *5,  6,  7}
//  *it = 6
list<int>::iterator it = l.erase( l.begin() + 1 , l.begin() + 5 );
```

```C++
//  5  remove()   删除所有特定的元素

list<int> l = {1,1,2,2,3,3};
//  l = {1,1,3,3}
l.remove(2);
```





#### 7 set/multiset

​	set/multiset 属于关联式容器，底层实现为二叉树，迭代器可以自增或自减，但不能增加指定步数，不支持随机访问。

​	两者的区别是，set 不允许有重复元素，而multiset 允许有重复元素。

​	所有元素在插入时会按key自动排序。

```C++
//  头文件  set中包含了multiset，只用一个头文件即可
#include<set>
```

```C++
//  初始化
set<typename> name;

//  set不允许有重复元素，插入重复元素时，不会报错，会自动丢弃
//  插入数据时，set将会自动排序

//  直接赋值
//  s = {1, 2, 3}
set<int> s = {3,1,2};

//  set插入数据时，只能使用insert()方式
set<int> s;
s.insert(2);
s.insert(1);
s.insert(2);
//  结果为 s = {1, 2}

//  拷贝构造
set<int> s2(s1);
//  或  set<int> s2 = s1;
```

​			0、  常用操作

​			1、  insert()    插入元素

​			2、  erase()    删除元素

​			3、  重载操作符，指定排序规则

```C++
//  0  常用操作

size();  //  返回大小
empty();  //  判断是否为空，空 -> true，非空 -> false
swap(st);  //  与 st 交换
find(key);  //  查找 key 是否存在，返回一个迭代器，存在 返回指向 key 的迭代器，不存在 返回 s.end()
count(key);  //  统计 key 元素的个数，对于set而言，结果只能是0或1，对于multiset而言，结果可能大于1
```

```C++
//  1  insert()  插入元素
//  若插入对象为set，则返回一个pair对组，结构为 pair<iterator, bool>
//  	这个pair对组中，iterator代表插入位置，bool代表是否成功
//  若插入对象为multiset，则返回一个指向插入元素的迭代器
//  	若有相同的元素，则在该元素后插入

set<int> s = {1,2,3,4,5};
auto res = s.insert(3);
//  结果 res = pair( it , false );  其中 it 是一个指向重复数字 3 的迭代器

multiset<int> s = {1,2,3,4,5};
auto res = s.insert(3);
//  结果 res = pair( it , false );  其中 it 是一个指向插入数字 3 的迭代器
//  s = { 1 , 2 , 3 , *3 ,  4 , 5 };

set<int> s1 = {1,2,3,4,5};
set<int> s2 = {3,4,5,6,7};
//  第一个参数指定位置，第二、三个参数指定插入的数据，前闭后开
//  插入后 s1 = {1, 2, 3, 4, 5, 6, 7}，由于部分数字已存在，程序不会报错，但也不会插入
//  这种插入方式没有返回值
s1.insert(s2.begin(), s2.end());
```

```C++
//  2  erase()  删除元素
//  使用 迭代器 或 指定的数字 删除一个元素， 有返回值
//  传入的是迭代器时，返回指向下一个元素的迭代器，注意：若删除的是最后一个元素，可能无法接受返回的迭代器
//  传入的是数字时，返回值是 unsigned_int64 类型，删除成功返回 1，删除失败返回 0

//  使用 迭代器 或 指定的数字 删除一个元素
list<int> l = {1,2,3,4,5,6,7};

l.erase(l.begin());  //  结果  l = {2,3,4,5,6,7};
l.erase(5);          //  删除指定数字，结果  l = {2,3,4,6,7};  在multiset中，会删除所有值为5的元素
l.erase(l.find(5));  //  删除指定数字，结果  l = {2,3,4,6,7};  在multiset中，仅删除第一个找到的值
```

```C++
//  3  重载操作符，指定排序规则
//  set 默认从小到大排序

class MyCompare {
public:
    template<typename T>
    //  重载 ()
    bool operator()(const T& a, const T& b)const {
        return a > b;
    }
};

set<int, MyCompare> s = {1,2,4,5,3};
//  结果： s = {5,4,3,2,1}
```



**补充：unordered_set**

```c++
//  头文件
#include <unordered_set>
```

​	unordered_set内部实现了一个哈希表（也叫散列表，通过把关键码值映射到Hash表中一个位置来访问记录，查找的时间复杂度可达到O(1)。其元素的排列顺序是无序的。
​	应用场景：对于查找较多的问题，unordered_map会更加高效一些。



#### 8 map/multimap

​	map是STL中的一个关联容器，其底层实现是红黑树，迭代器可以自增或自减，但不能增加指定步数，不支持随机访问。

​	map 类型变量中的元素是由对组pair组成的键-值对，map没有重复的键，multimap允许有重复的键。

​	所有元素在插入时会按照键值自动从小到大排序。

```c++
//  头文件
#include<map>
#include<unordered_map>
```

```c++
//  初始化
map<typename, typename> name;

//  直接赋值       ↓ 这个等号可以省略
map<int, char> m = {
    {2, 'a'}, {3, 'c'}
};

//  使用 [] 直接插入
map<int, char> m;
m[4] = 'a';

//  使用insert 
map<int, string> m;
a.insert(pair(1,"abc"));

//  拷贝构造
map<int, string> m1;
map<int, string> m2(m1);
//  或  map<int, string> m2 = m1;
```

​			0、  常用操作

​			1、  erase()  删除元素

​			2、  重载操作符，指定排序规则

```C++
//  0  常用操作

size();  //  返回大小
empty();  //  判断是否为空，空 -> true，非空 -> false
swap(m);  //  与 m 交换
clear();  //  清空

count(key);  //  统计 key 元素的个数，对于map而言，结果只能是0或1，对于multimap而言，结果可能大于1
find(key);  //  查找某个键key，并返回key对应的迭代器
```

```C++
//  1  erase()  删除元素

//  使用 迭代器 或 指定的数字 删除一个元素， 有返回值
//  传入的是迭代器时，返回指向下一个元素的迭代器，注意：若删除的是最后一个元素，可能无法接受返回的迭代器
//  传入的是数字时，返回值是 unsigned_int64 类型，删除成功返回 1，删除失败返回 0

//  使用 迭代器 或 指定的数字 删除一个元素
map<int, char> m = {
    {1, 'a'}, {2, 'b'}, {3, 'c'}, {4, 'd'}, {5, 'e'}
};

//  使用迭代器删除
m.erase(l.begin());  //  结果  m = {{2, 'b'}, {3, 'c'}, {4, 'd'}, {5, 'e'}}
auto it = m.find(3);
it = m.erase(it);  //  结果  m = {{2, 'b'}, {3, 'c'}, {5, 'e'}}, it -> {5, 'e'}
m.erase(3)  //  结果  m = {{2, 'b'}, {5, 'e'}}
```

```C++
//  2  重载操作符，指定排序规则
//  map 默认按键值从小到大排序

class MyCompare {
public:
    template<typename T>
    //  重载 ()
    bool operator()(const T& a, const T& b)const {
        return a > b;
    }
};

map<int, char, MyCompare> m = {{1, 'a'}, {2, 'b'}, {3, 'c'}, {4, 'd'}, {5, 'e'}};
//  结果： m = {{5, 'e'}, {4, 'd'}, {3, 'c'}, {2, 'b'}, {1, 'a'}}
```





**补充：unordered_map**

```c++
//  头文件
#include <unordered_map>
```

​	unordered_map使用哈希表而非红黑树。哈希表通过把关键码值映射到Hash表中一个位置来访问记录，查找的时间复杂度可达到O(1)。其元素的排列顺序是无序的。

**map**

​	优点：

​		**有序性**，这是map结构最大的优点，其元素的有序性在很多应用中都会简化很多的操作；

​		**红黑树**，内部实现一个红黑树使得map的很多操作在O(logn)的时间复杂度下就可以实现，因此效率非常的高。

​	缺点：

​		**空间占用率高**，因为map内部实现了红黑树，虽然提高了运行效率，但是因为每一个节点都需要额外保存父节点、孩子节点和红/黑性质，使得每一个节点都占用大量的空间

​	应用场景：对于那些有顺序要求的问题，用map会更高效一些

**unordered_map**

​	优点：

​		**查找速度快**，因为内部实现了哈希表，因此其查找速度非常的快
​	缺点：

​		**建立花费时间**，哈希表的建立比较耗费时间
​	应用场景：对于查找问题，unordered_map会更加高效一些。







### 算法

```C++
//  头文件
#include<algorithm>
#include<numeric>
#include<functional>
```

​	algorithm是所有STL头文件中最大的一个，范围涉及比较、交换、遍历、复制、修改等。

​	numeric提及很小，只包括几个在序列上进行简单数学运算的模板。

​	functional定义了一些模板类，用以声明函数对象。

​	一般建议只使用`#include<algorithm>`



#### sort() 排序

```c++
//  构造函数
template< class RandomIt >
void sort( RandomIt first, RandomIt last )
 
template< class RandomIt, class Compare >
void sort( RandomIt first, RandomIt last, Compare comp )
```

​	 第一个参数是首地址，第二个参数是末尾地址，第三个参数是一个bool类型的比较函数，返回true时表示当前两个数字应保持原有顺序，返回false时表示当前两个数字应交换顺序，不写的情况下默认返回a<b，即升序。

```c++
//  数组排序
int a[7] = {1, 5, 3, 6, 7, 2, 4};
sort(a, a+7);

//  vector数组排序
vector<int> a = {1, 5, 3, 6, 7, 2, 4};
sort(a.begin(), a.end());
```

​		可以通过传入第三个参数控制排序方式

```c++
//  降序  从大到小排序

//  自定义比较方式
bool cmp(int i, int j){
    return i>j;
}
int a[7] = {1, 5, 3, 6, 7, 2, 4};
sort(a, a+7, cmp);dwa
int a[7] = {1, 5, 3, 6, 7, 2, 4};
sort(a, a+7, [](int i, int j) { return i>j; });
```

​	可以依靠这种方式，使数组按照其他结构体内的某一条属性排序。

```c++
int a[7] = {0, 1, 2, 3, 4, 5, 6};
int b[7] = {2, 6, 3, 5, 7, 1, 4};

sort(a, a+7, [&](int i, int j) { return b[i] < b[j]; });
//  排序后 a:  5  0  2  6  3  1  4
//  意为：b按从小到大排序后，原下标的顺序
```





### 补充： 迭代器

除了**使用下标**来访问对象的元素外，标准库还提供了另一种检测元素的方法：迭代器（iterator）。迭代器是一种允许使用者检查容器内元素，并实现元素遍历的数据类型。

​	**下面以 vector 为例*

初始化

```C++
vector<int> vec = { 1, 2, 3, 4 };

//  定义一个int型的向量，指向vec的第一个元素
vector<int>::iterator iter = vec.begin();

//  定义一个int型的向量，指向vec的最后一个元素的下一位
vector<int>::iterator iter = vec.end();

```

举例：

```c++
vector<int> vec = { 1, 2, 3, 4 };

//  下面两段for循环 效果相同
for( int i = 0 ; i < vec.size() ; i++ ){
    cout << vec[i];
}
for( vector<int>::iterator i = vec.begin() ; i != vec.end() ; i++ ){
    cout << *i;
}
```

const修饰的迭代器

```C++
//  const在前，it本身无法改变，无法自增或自减
const vector<int>::iterator it = a.begin();
it ++;  //  错误！it无法自增或自减
*it += 5;  //  正确，it指向的元素可以修改


//  const_iterator 表示it指向的元素无法改变
vector<int>::const_iterator it = a.begin();
it ++;  //  正确，it本身可以改变
*it += 5;  //  错误，无法修改const it指向的元素

//  另外，可以使用出 cbegin() 和 cend() 来代替const_iterator
auto it = a.cbegin();
it ++;  //  正确，it本身可以改变
*it += 5;  //  错误，无法修改it指向的元素
```





















