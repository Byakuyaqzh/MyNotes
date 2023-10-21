

### 常用技巧

#### 初始化：

```C++
int n = INT_MIN;
int n = INT_MAX;

int n = 0x3f3f3f3f;  //  替代最大值，防止运算中溢出
    
memset(nums, -1, sizeof(nums));  //  初始化数组
```



#### 字符串操作

```C++
isdigit(c);  //  判断c是不是数字
isalpha(c);  //  判断c是不是字母
isalnum(c);  //  判断c是不是数字或字母

tolower(c);  //  转为小写
toupper(c);  //  转为大写
```



#### 字符串和数值间的转换

```C++
int num = 100;
string s = to_string(num);  //  数字 转化为 字符串

string s = "100";
int num1 = stoi(s);  //  字符串 转化为 整形
int num2 = stol(s);  //  字符串 转化为 长整形
```



#### 查看变量类型

```c++
#include<typeinfo>

int a = 20;
cout << typeid(a).name() << endl;
//  int
```



#### 十进制转二进制

```c++
#include <bitset>

int a = 20;
string bin = bitset<32>(i).to_string();
//  bin = 00000000000000000000000000010100
//  typeid(bin).name()  class std::bitset<32>
```





#### 匿名函数

```C++
vector<int> nums = { 1,4,5,2,3 };
sort(nums.begin(), nums.end(), [](int a, int b){
    return a > b;
});

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





#### 折叠表达式

折叠表达式（Fold Expression）是C++17引入的一项新特性，它允许在编译期间对参数包（variadic pack）中的元素进行操作，例如求和、连接字符串、判断所有元素是否满足某个条件等。折叠表达式通常使用于模板编程，能够极大地简化代码，提高可读性。

在折叠表达式中，`(... op pack)` 或 `(pack op ...)` 的形式，其中 `op` 是二元操作符。折叠表达式的语法规则包括：

- **左折叠表达式（Left Fold）：** `(... op pack)`，表示将二元操作符 `op` 从左往右依次作用于参数包 `pack` 中的元素。
- **右折叠表达式（Right Fold）：** `(pack op ...)`，表示将二元操作符 `op` 从右往左依次作用于参数包 `pack` 中的元素。

在折叠表达式中，可以使用不同的二元操作符，比如加法 `+`、乘法 `*`、逗号 `,` 等。以下是一些折叠表达式的示例：

#####  1. **左折叠求和：**

```c++
template <typename... Args>
int sum(Args... args) {
    return (... + args);
}

int result = sum(1, 2, 3, 4, 5); // 结果为 15
```

##### 2. **右折叠连接字符串：**

```c++
template <typename... Args>
std::string concatenate(Args... args) {
    return (args + ...);
}

std::string result = concatenate("Hello, ", "World", "!");
// 结果为 "Hello, World!"
```

##### 3. **左折叠判断所有元素是否为真：**

```c++
template <typename... Args>
bool allTrue(Args... args) {
    return (... && args);
}

bool result = allTrue(true, true, true, false); // 结果为 false
```

折叠表达式的引入使得处理可变数量参数的模板函数变得更加简洁和易读。请注意，折叠表达式要求编译器支持C++17或更高的标准。







### 头文件

#### #include\<functional>

```C++
//  用于创建一个对象，存储一个可调用对象
//  可调用对象包括函数、函数指针、lambda表达式
#include <functional>

int a = 5, b = 8;
function<void(int&, int&)> f = [](int& a, int& b) {
    a += 10;
    b += 10;
};

f(a, b);
cout << a << "   " << b << endl;
```

#### #include\<numeric>

1  `accumulate()`

2 `iota()`

```c++
#include<numeric>

//  accumulate()
//  T accumulate(InputIt first, InputIt last, T init);
//  计算初始值+数组元素累加值
int a[5] = {0,1,2,3,4};
int ans = accumulate(a, a + 5, 10);
//  结果：10 + 0 + 1 + 2 + 3 + 4 = 20

//  iota()
//  void iota(ForwardIt first, ForwardIt last, T value);
//  为数组内元素赋一段累加的值，初始值为value
int a[5];
iota(a, a + 5, 0);  //  0 1 2 3 4
iota(a, a + 5, 5);  //  5 6 7 8 9
```



























