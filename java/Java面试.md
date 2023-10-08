#### Int和Integer的区别

int是java的基本数据类型之一，Integer是一个封装类。

- int可以直接定义、赋值；Integer需要使用new关键字创建
- 两者混合使用时，java会自动通过装箱、拆箱实现类型转换
- Integer作为一个对象类型，封装了一些方法和属性
- Integer的默认值是`null`，而int的默认值是`0`
- Integer是对象，存储在堆内存中，int是基本数据类型，存储在栈内存中

之所以要创建封装类，是因为java是面向对象语言，对象是java的基本操作元。比如集合中只能存储Object类型