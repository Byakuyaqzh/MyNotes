

#### JS基础

##### 定义

```javascript
//  可以定义任何对象，默认为全局变量。通过var可以重复定义
var obj;

//  可以定义任何对象，默认为局部变量，不能重复定义
let obj;
```



##### 函数

```javascript
//  不需要写返回值
function func(a){
    alert(a);
}

function func(a, b){
    return a + b;
}
```



##### 数组

```javascript
let a = new Array(1,2,3,4,"5");
let b = [1,2,4,'a'];
```



##### 字符串

```javascript
var a = new String("Hello world");
var b = "Hello world";

//  属性
a.length;

//  常用方法
a.charAt(4);  //  返回指定位置的字符
a.indexOf("ll");   //  检索字符串
a.trim();  //  去除两边的空格
a.substring(start, end);  //  截取字符串
```



##### 对象

```javascript
var 对象名 = {
    属性名1 ： 属性值1,  //  后面是逗号
    属性名2 ： 属性值2,
    属性名3 ： 属性值3,
    函数名 : function(){
        //  ...
    }
}
```





##### JSON

全称：JavaScript Object Notation，JavaScript对象标记法。

JSON是通过JavaScript对象标记法书写的**文本**

```javascript
//  数据格式
{
    "key1" : "value1",
    "key2" : "value2",
    "key3" : "value3",
}
//  value的数据类型可以是：
//    数字
//    字符串（使用双引号）
//    逻辑值（直接写true或false）
//    数组（使用方括号）
//    对象（使用花括号）
//    null
```

```javascript
//  定义字符串
var jsonStr = {"name":"Tom", "age":"20", "addr":["北京", "上海"]};

//  将字符串转化为json对象
var obj = JSON.parse(jsonStr);
alert(obj.name);

//  将json对象转化为字符串
var str = JSON.stringify(obj);
```





##### BOM

全称：Browser Object Model，浏览器对象模型，将浏览器的各个部分封装为对象

```javascript
//  Window ： 浏览器窗口对象
//  Navigator ： 浏览器对象，包括浏览器名称、版本、内核等
//  Screen ： 屏幕对象
//  History ： 历史记录对象
//  Location ： 地址栏对象
```

```javascript
//  Window 下的部分方法
//  1、  alert()  弹出一个警告框

//  2、  confirm()   弹出一个确认框
var flg = confirm("确认删除吗？");  //  return true or false

//  3、  setInterval()  周期性执行某一函数，第一个参数为函数体，第二个参数是时间（ms）
var i = 0;
setInterval(function(){
    i ++;
    console.log("定时器执行了" + i + "次");
}, 2000);

//  4、  setTimeout()  延迟时间后执行指定函数一次
setTimeout(function(){
    alert("缓存清理完毕");
}, 5000);
```

```javascript
//  Location 下的部分方法
//  location.href，设置或获取当前网页的地址
//  返回当前地址
var a = location.href;

//  执行当前代码后跳转至对应网页
locatuion.href = "www.baidu.com";
```



##### DOM

全称：Document Object Model，文档对象模型，将标记语言的各个部分封装成对应的对象

注：HTML：超文本标记语言

```javascript
//  Document ： 整个文档对象
//  Element ： 元素对象
//  Attribute ： 属性对象
//  Text ： 文本对象
//  Comment ： 注释对象
```

JavaScript通过DOM对象对HTML进行操作

```javascript
//  通过id值获取，返回单个Element对象
var h1 = document.getElementById("h1");

//  通过class属性值获取，返回Element对象数组
var clss = document.getElementsByClassName("cls");

//  通过name属性值获取，返回Element对象数组
var hobbys = document.getElementsByName("hobby");

//  通过标签名称获取，返回Element对象数组
var divs = document.getElementsByName("div");
```





#### Ajax

全称：**Asynchronous JavaScript And XML**，异步的**JavaScript**和**XML**

作用：

- 数据交换：通过Ajax可以向服务器发送请求，并获取服务器相应的数据
- 异步交互：可以在不更新整个页面的情况下，与服务器交换数据并更新部分网页





#### Axios

对原生ajax进行封装，简化开发流程

```javascript
function get(){
    axios.get("htttps://www.baidu.com").then((result) =>{  //  回调函数
        console.log(result.data);
    })
}

function post(){
    axios.post("htttps://www.baidu.com","id=1").then((result) =>{  //  回调函数
        console.log(result.data);
    })
}
```

获取某网址的数据，传回Vue对象

```javascript
new Vue({
    el: "#app",
    data: {
        emps: []
    },
    mounted() {
        //  发送异步请求，加载数据
        axios.get("https://www.baidu.com").then(result => {
            this.emps = result.data;
        })
    }
});
```





















