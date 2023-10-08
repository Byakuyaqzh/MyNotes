





#### 基础内容

##### 		基础语句

​	一般来讲，C#中所有字段都按照驼峰式命名法，首字母小写，其他单词首字母大写；所有属性、方法、类名都遵循Pascal命名法，要求每个单词的首字母大写。

```C#
//  输入语句
string name = Console.ReadLine();

//  输出语句：line自带回车
Console.WriteLine("Hello World");
//  不带回车
Console.Write("Hello World");

//  等待  system("pause");
Console.ReadKey(); 

//  var，不定类型，类似C++的auto
```

```C#
//  初始化数组
int[] arr = new int[5];
int[] arr = new int[]{1, 2, 3};
//  数组基本操作
//  a的长度
Console.WriteLine(arr.Length);


//  二维数组
int[,] arr2 = new int[5,5];
int[,] arr2 = new int[,] { { 1, 2, 3 }, { 4, 5, 6 } };

//  数组基本操作
//  直接写length 是总大小
Console.WriteLine(arr.Length);  //  =  6
Console.WriteLine(arr.GetLength(0));  //  = 2
Console.WriteLine(arr.GetLength(1));  //  = 3
```

```C#
//  类型转换  Convert，  转换条件：看着像就行
string num_1 = "3.1415";
string num_2 = "6";
double num_3 = Convert.ToDouble(num_1);
int num_4 = Convert.ToInt32(num_2);
```

```C#
//  返回多个值   out关键字
//  虽然是一个void函数，但是输入两个值，返回两个值
static void MyFunc(int a, int b, out int sum, out double mean) {
    sum = a + b;
    mean =  (a + b) / 2;
}

int a = 10; int b = 20;
int sum;
double mean;
MyFunc(a, b, out sum, out mean); 
//  结果：sum = 30， mean = 15
```



##### 		值传递与引用传递

```C#
//  值传递
int a = 10;
int b = a;
b = 20;
Console.WriteLine("a = {0}, b = {1}", a, b);
//  a = 10, b = 20

//  引用传递
int[] a = new int[] {10, 20};
int[] b = a;
b[0] = 20;
Console.WriteLine("a[0] = " + a[0]);  //  a[0] = 20
a[0] = 30;
Console.WriteLine("b[0] = " + b[0]);  //  b[0] = 30

//  注意：
//  函数调用时也是按照这个标准调用的
//  比如，传入一个 int 类型  ->  值传递
//  传入一个 int[] 数组  ->  引用传递

//  强制使用引用传递
//  ref 关键字
//  在形参和实参位置 都要添加ref

static void MyFunc(ref int a) {
    a += 10;
}

int n = 10;
MyFunc(ref n);
//  结束后 n = 20
```



##### 		string	字符串常用操作

```C#

ToUpper()    //  将字母变成大写，返回处理后的字符串
ToLower()    //  将字母变成小写，返回处理后的字符串
Equals(name)    //  判断两个字符串是否相等
Substring(i, n)    //  截取字符串的一部分，从角标为i的字符开始，截取n个字符
IndexIf(key)    //  查找某个字符(串)在字符串中第一次出现的位置，不存在则返回-1
LastIndexOf(key)    //  查找某个字符(串)在字符串中最后一次出现的位置，不存在则返回-1
StartsWith(l)    //  是否以字符(串)l开始，是 -> true，否 -> false
EndsWith(l)    //  是否以字符(串)l结束，是 -> true，否 -> false
Replace(a, b)    //  把字符串中的a换成b
Contains(key)    //  判断字符串中是否包含key，是 -> true，否 -> false
Trim()    //  删除字符串开头和末尾处的空格，返回处理后的字符串
TrimStart()    //  删除字符串开头处的空格，返回处理后的字符串
TrimEnd()    //  删除字符串末尾处的空格，返回处理后的字符串

string.IsNullOrEmpty(s)  //  判断字符串是否为空，空 -> true， 非空 -> fasle。注：空格是字符，非空
    
//  补充 Split(c)
//  以c分割字符串，返回字符串类型的数组
    
string address = "中国|北京|上海|深圳";
string[] ans = address.Split("|");
for(int i = 0; i < ans.Length; i++) {
    Console.Write(ans[i] + " ");
}
//  中国 北京 上海 深圳
```



##### 	StringBuilder  字符串

​	由于string字符串在修改时并不是在原有基础上修改，而是重新开辟了新的空间，因此在大量修改的状态下，会占用许多无用空间。

​	可以使用 StringBuilder 规避这种情况。

```C#
//  命名空间
using System.Text;
```

```C#
//  初始化
StringBuilder a = new StringBuilder();

a.Append("awdawdawd");
a.Append(123);
a.Append('\n');
a.Append(true);

Console.WriteLine(a.ToString());  // 注意：这里是创建了一个匿名变量tmp=a.ToString()，a本身未改变
//  输出结果
//  awdawdawd123
//  True
```

​	常用操作

```C#
a.clear();  //  清空
a.ToString();  //  转化为字符串，并返回。注意：a本身未改变，而是将改变后的结果作为返回值返回
```





##### 	 enum 枚举

​	用户自定义类型

```C#
public enum Week {
    星期一,星期二,星期三,星期四,星期五,星期六,星期天, 
}

Week we = Week.星期一;
Console.WriteLine(we);
//  打印结果：星期一
```



##### 预编译

​	区域指令

```C#
#region 这一段的描述
    ··· ···
    ··· ···
#endregion

//  使用后可以按照描述折叠这部分代码（物理），方便查看整体内容与逻辑
```







##### 	计时器  Stopwatch

```C#
//  命名空间
using System.Diagnostics;
```

```C++
//  初始化
Stopwatch sw = new Stopwatch();

//  基本操作
sw.Start();
sw.Stop();

//  输出结果
Console.WriteLine(sw.Elapsed);
```









#### 	static 关键字

​	static关键字，用于修饰类、字段、属性、方法、构造方法等，被static修饰的内容成为静态类/静态成员等

##### 	静态字段

```C#
//  - 静态字段不属于任何对象，只属于类
//  - 使用 类名.静态字段名 访问，无法使用 对象名.静态字段名 访问
//  - 静态字段在内存中只有一份

class Animal {
	public string name;  //  普通字段
    public static int age;  //  静态字段
}
```

##### 	静态属性

```C#
//  - 静态字段 只能封装 静态字段，不能封装非静态字段
//  - 使用 类名.静态属性 访问，无法使用 对象名.静态属性 访问

class Animal {
	public string name;  //  普通字段
    public static int age;  //  静态字段
    
    public string Name {    //  普通属性
        get { return name; }
        set { name = value; }
    }
    
    public static int Age {    //  静态属性  
        get { return age; }
        set { age = value; }
    }
}
```

##### 	静态方法

```C#
//  - 静态方法只能使用 类名.静态方法名 调用
//  - 在静态方法中不能调用非静态方法

class Func{
    public void func1() {  //  普通方法
        Console.WriteLine("1");
    }

    public static void func2() {  //  静态方法
        Console.WriteLine("2");
    }
}

//  静态方法在程序运行时就已存在，只能使用 类名.方法名 调用
//  普通方法将在实例化对象后，使用 对象名.方法名 调用
```

##### 	静态构造方法

```C#
//  - 静态构造方法用于初始化静态成员，一个静态类只能有一个静态构造方法
//  - 静态构造方法 没有访问修饰符，没有参数
//  - 静态构造方法可以定义在静态类中，也可以定义在非静态类中

class Animal {
    //  构造方法
    public Animal(string name){
        this.name = name;
    }
    //  静态构造方法
    public static Animal(){
        age = 0;
    }
    
	public string name;  //  普通字段
    public static int age;  //  静态字段
    
    public string Name {    //  普通属性
        get { return name; }
        set { name = value; }
    }
    
    public static int Age {    //  静态属性  
        get { return age; }
        set { age = value; }
    }
}
```

##### 	静态类

```C#
//  - 当类中的成员全都是静态成员的时候，可以把类声明为静态类
//  - 静态类不能存在非静态成员
//  - 静态类不能实例化对象
```





#### 类与对象

```C#
class Person{
    //  构造方法，一般必须是public，只有在单例模式下才可以用private
    public Person() {}
    public Person() {
        this.name = name;
        this.age = age;
	}
    
    //  公共属性
    public string name;
    
    
    //  私有属性  设置 get/set 方法
    private int age;
    //  在程序中调用 p.Age，可以获取/修改age的值
    public int Age{
        get{ return age; }
        set{ 
            if (value > 0 && value < 100){
                age = value; 
            }
            else{
                age = 0;
            }
        }
    }
    
    //  默认状态下，get、set 方法可以简写
    private string address;
    public string Address { get; set; }
}
```

##### 	继承

```C#
//  继承
//  子类中可以访问到父类中的public属性，访问时使用 base.字段名
//  子类无法访问父类中的private属性
//  父类
public class Animal {
    //  父类的构造函数
    //  构造函数一般为 public
    public Animal() { }
    public Animal(string name, int age) {
        this.name = name;
        this.age = age;
    }
	//  get/set方法
    public string Name {
        get { return this.name; }
        set { this.name = value; }
    }
    public int Age {
        get { return this.age; }
        set { this.age = value; }
    }
	//  私有属性
    private string name;
    private int age;
}
//  子类
public class Cat : Animal {
    //  子类的构造方法
    public Cat() { }
	//  有参构造，将内容传递给父类(base)
    public Cat(string name, int age)
        : base(name, age)
        { }
}
```

##### 	多态

```C#
//  多态
//  虚方法   抽象方法
//  虚方法写在普通类中，抽象方法写在抽象类中

//  --  虚方法
//  父类
public class Animal {
    public Animal() { }
	//  虚方法，在 void 前加上 virtual，意味着这个函数可以被子类重写，虚方法中可以写方法体
    public virtual void DoSpeak() {
        Console.WriteLine("Animal");
    }
}

public class Cat : Animal {
    public Cat() { }
	//  重写父类的虚方法，在 void 前加上 override
    public override void DoSpeak() {
        Console.WriteLine("Cat");
    }
}

public class Dog : Animal {
    public Dog() { }
	//  在重写子类中，可以使用 base. 调用父类的这个方法（注：抽象方法中无法调用）
    public override void DoSpeak() {
        base.DoSpeak();
        Console.WriteLine("Dog");
    }
}

//  --  虚方法 -> 抽象方法  --
//  若虚方法已经无法确定方法体，可以将这个虚方法调整为抽象方法
//  抽象类 无法被实例化，但可以存储子类对象，如 Animal c = new Cat();
//  抽象类中不一定有抽象方法，但抽象方法必须被创建在抽象类里
//  抽象方法 没有方法体，直接以分号结尾

//  创建类时，加 abstract，这个类变为抽象类
public abstract class Animal {
    //  抽象方法，加 abstract ，直接以分号结尾
    public abstract void DoSpeak();
    
    //  非抽象方法，可以被子类调用
    public void DoSleep() {
        Console.WriteLine("睡着了");
    }
}

public class Cat : Animal {
    public Cat() { }
	//  同样的，使用 override
    public override void DoSpeak() {
        Console.WriteLine("Cat");
    }
}

//  --  抽象方法 -> 接口  -- 
//  当抽象类中所有方法都是抽象方法时，可以将这个类以接口的形式表现，接口同样不能被实例化
//  接口中只有抽象方法，没有实例字段，且不允许添加类型修饰符，默认public
//      接口中不能创建实例字段，比如 private int a; 属于实例字段，无法创建
//      接口中全是抽象方法，但是不需要 abstract 修饰

//  实现USB接口，能读和写
//  这些方法将在继承接口的子类中实现
interface IUSB {
    void read(string val);
    void write();
}


//  总结   虚方法，抽象方法，接口
/*
	虚方法：父类中有普通字段、普通方法、虚方法，父类中可以写虚方法的实现，父类可以实例化，子类可以调用父类的虚方法，子类可以重写/覆盖父类中的虚方法。
	抽象类：父类中有普通字段和抽象方法，抽象方法不能写实现。
	接口：接口中只有抽象方法，抽象方法不能写实现。
*/
```

##### 	访问修饰符

```C#
//  C# 中类型/成员修饰符（访问修饰符）共有五种
//  public， private， protect， internal 和  protected internal
/*
1  public
	当前类、子类、实例对象 都可以访问
2  private
	只有当前类内部可以访问，子类、实例对象 都无法访问
3  protect
	当前类内部和 子类可以访问，实例对象无法访问
4  internal
	在同一个项目中，访问权限与 public 相同，项目外无法访问
5  protected internal
	在同一项目中，当前类内部和 子类可以访问
*/

//  只有 public 和 internal 可以修饰类，类的默认修饰符是 internal
//  五种修饰符都可以修饰类内成员，类中成员的默认修饰符是 private
```

##### 	单例模式

​	单例模式，保证整个程序运行过程中只存在一个实例对象。

- 声明一个静态且私有的当前类 类型的字段

- 创建无参私有构造方法

- 创建一个静态方法，用于创建此类的唯一对象


```C#
class Byakuya {
    //  创建一个名字为当前类类型的字段
    private static Byakuya instance;
    //  私有无参构造函数
    private Byakuya() { }
	//  创建静态方法，创建唯一一个对象
    public static Byakuya Instance() {
        if(instance == null){
            instance = new Byakuya();
        }
        return instance;
    }
}

//  创建对象
Byakuya me = Byakuya.Instance();
```

#####     嵌套类、匿名类、密封类

```C#
//  嵌套类
//  嵌套类与普通类相同，只是声明在了一个类的内部，使用 外部类名.内部类名 访问
//  一般不建议用
```

```C#
//  匿名类
//  使用匿名方式创建一个类，这种类一般用于存储一组 “只读” “属性”。

var p = new { Name = "name", Age = 20 };
Console.WriteLine(p.Name + " " + p.Age);
```

```C#
//  密封类
//  被 sealed 修饰的类 不可以被继承，不可以有子类
```

##### 	Object类

​	在C#中，Object类是所有类的父类，所有类都直接或间接继承自Object类。

```C#
//  ToString()
//  Object类中的方法，将结果转化为字符串
//  可以重写此方法，以适应不同的类

class Person {
    //  构造方法
    public Person(string name, int age) {
        this.name = name;
        this.age = age;
    }
    //  私有字段及其 get/set 方法
    private string name;
    public string Name { get; set; }
    private int age;
    public int Age { get; set; }
    //  重写ToString()，
    public override string ToString() {
        return string.Format("this name is {0}, and age is {1}", this.name, this.age);
    }
}

//  使用
Person me = new Person("name", 10);
Console.WriteLine(me.ToString());
```

##### 	装箱与拆箱

​	只有两个类型出现继承关系是，才可能出现装箱或者拆箱操作

```C#
//  装箱    值类型 -> 引用类型
//  拆箱    引用类型 -> 值类型

int a = 10;

object b = a;  //  装箱，值类型 -> 引用类型

a = (int)b;  //  拆箱，引用类型 -> 值类型

//  装箱/拆箱本质上是堆与栈之间的转换，应减少或或避免频繁的装箱
```







#### 面向对象六大原则

```C#
/*
1、单一职责原则
2、开闭原则
3、里式转换原则
4、依赖倒置原则
5、接口隔离原则
6、迪米特原则
*/
/*--------------------------------------*/
//  1、单一职责原则
	



 
//  3、里式转换原则
    
//  - 子类对象可以直接赋值给父类对象
//  Cat继承了Animal，那么：
Animal c = new Cat();

//  - 子类对象可以调用父类成员，但父类对象不能调用子类成员
Animal c = new Cat();
c.Cat::name()  //  错误，即使是存储的是子类对象，但仍无法调用子类的方法

//  - 如果父类对象中存储的是子类对象，那么父类可以强制转化为子类对象
Animal c = new Cat();
Cat c2 = (Cat)c;    //  强制转化

//  补充： is/as 类型转化
//  is  如果转换成功，则返回true，转换失败返回false
Animal c = new Cat();
bool flg1 = c is Cat;  //  flg1 -> true, 同时将 c 转化为Cat
bool flg2 = c is Dog;  //  flg2 -> false, c 仍然是 Animal
//  as  转换成功返回对应的对象，转换失败返回null
Animal c = new Cat();
Cat? c1 = c as Cat;  //  转化。 Cat后加? 表示 c1可能为null
//  可以使用下面的方法转化
Cat c2;
if (c as Cat != null) {
    c2 = c as Cat;
    Console.WriteLine("转化成功！");
}
else {
    Console.WriteLine("转化失败！");
}



```







