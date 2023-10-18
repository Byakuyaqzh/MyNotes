







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











#### function

```C++
#include <functional>

int a = 5, b = 8;
function<void(int&, int&)> f = [](int& a, int& b) {
    a += 10;
    b += 10;
};

f(a, b);
cout << a << "   " << b << endl;

```



