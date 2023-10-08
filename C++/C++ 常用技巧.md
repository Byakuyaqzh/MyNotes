初始化：

```C++
int n = INT_MIN;
int n = INT_MAX;

int n = 0x3f3f3f3f;  //  替代最大值，防止运算中溢出
    
memset(nums, -1, sizeof(nums));  //  初始化数组
```



字符串操作

```C++
isdigit(c);  //  判断c是不是数字
isalpha(c);  //  判断c是不是字母
isalnum(c);  //  判断c是不是数字或字母

tolower(c);  //  转为小写
toupper(c);  //  转为大写
```



字符串和数值间的转换

```C++
int num = 100;
string s = to_string(num);  //  数字 转化为 字符串

string s = "100";
int num1 = stoi(s);  //  字符串 转化为 整形
int num2 = stol(s);  //  字符串 转化为 长整形
```



function

```C++
#include <functional>


int a = 5, b = 8;
function<void(int&, int&)> f = [](int& a, int& b) {
    a += 10;
    b += 10;
};

f(a, b);
cout << a << "   " << b << endl;
//  a = 15, b = 18;

/*
	[]不自动捕捉变量，只捕捉调用函数时传入的变量。
    [=]表示值传递方式捕捉所有父作用域的变量包, 括this
    [&s]表示引用传递捕捉变量s
    [&]表示引用传递方式捕捉所有父作用域的变量, 包括this
    [this]表示值传递方式捕捉当前的this指针
    可以连用如:[=,&a,&b]表示以引用传递的方式捕捉变量a和b，以值传递方式捕捉其它所有变量
    注意:捕捉列表不允许变量重复传递比如[&,&a]
*/
```



查看变量类型

```c++
#include<typeinfo>

int a = 20;
cout << typeid(a).name() << endl;
//  int
```





十进制转二进制

```c++
#include <bitset>

int a = 20;
string bin = bitset<32>(i).to_string();
//  bin = 00000000000000000000000000010100
//  typeid(bin).name()  class std::bitset<32>
```















