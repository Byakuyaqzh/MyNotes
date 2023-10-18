



#### struct



#### typedef

为数据类型创建一个新的名称（别名）

```c
typedef int Integer;  // 定义一个名为Integer的int类型别名
typedef float RealNumber;  // 定义一个名为RealNumber的float类型别名
```

使用别名后，可以在代码中使用`Integer`代替`int`，`RealNumber`代替`float`。

```c
typedef struct{
    string name;
    int age;
}person;  // // 定义一个结构体别名person

person p1;
```





#### enum

枚举，是一种自定义数据类型

```c
enum Day {
    //  枚举类型的取值默认从0开始，但也可以显式地指定每个枚举常量的值
    Sunday,    // 0
    Monday,    // 1
    Tuesday,   // 2
    Wednesday, // 3
    Thursday,  // 4
    Friday,    // 5
    Saturday   // 6
};

//  定义
Day today = Sunday;
```

```c
//  显式指定
enum Day {
	a = 5,   // 5
	b,       // 6 
	c = 20,  // 20
	d        // 21
};
```

