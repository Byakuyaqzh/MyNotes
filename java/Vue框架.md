#### Vue框架

Vue是一个前端JS框架

常用指令

```javascript
v-bind  //  为标签绑定属性值，比如设置href、css样式等
v-model  //  在表单元素上创建双向数据绑定
v-on  //  为标签绑定事件，可以简写为@
v-show  //   根据条件展示元素，可以控制display的值
v-if  //     根据条件渲染元素，不成立则不渲染
v-else-if  //  
v-else  //  
v-for  //    遍历容器的元素或对象的属性
```



##### **v-bind** 与 **v-model** 的使用

```html
<body>
    <div id="app">
        <!-- 将href的值绑定为url -->
        <a v-bind:href="url">链接</a>
        
        <!-- model提供双向绑定，当修改输入框中的数据时，url也会改变，并使a标签中的链接改变 -->
        <input type="text" v-model="url">
    </div>

</body>
<script>
    new Vue({
        el: "#app",  // vue接管区域，表示id为app的标签
        data:{
            url : "https://www.baidu.com",
        },
    })
</script>
```

##### **v-on** 的使用

```html
<body>
    <div id="app">
        <!-- 两种写法效果一致 -->
        <input type="button" value="点击" v-on:click="handle()">
        <input type="button" value="点击" @click="handle()">
    </div>

</body>
<script>
    new Vue({
        el: "#app",
        data:{
            
        },
        methods: {
            handle(){
                alert("点击了按钮");
            },
        },
    })
</script>
```

##### **v-if** 、 **v-else-if** 、 **v-else** 的使用

```html
<body>
    <div id="app">
        <!-- 通过控制输入框的数字，控制这三个span的显示 -->
        <input type="text" v-model="age">
        <span v-if="age < 30">年轻人</span>
        <span v-else-if="age < 60">中年人</span>
        <span v-else>老年人</span>
    </div>

</body>
<script>
    new Vue({
        el: "#app",
        data:{
            age: 20,
        },
    })
</script>
```

##### **v-show** 的使用

```html
<body>
    <div id="app">
        <!-- 通过控制输入框的数字，控制span的显示 -->
        <!-- 满足条件时显示 -->
        <input type="text" v-model="age">
        <span v-show="age > 35">开除！</span>
    </div>

</body>
<script>
    new Vue({
        el: "#app",
        data:{
            age: 20,
        },
    })
</script>
```

##### **v-for** 的使用

```html
<body>
    <div id="app">
        <!-- 每个for循环会生成3个div -->
        <div v-for="addr in addrs">{{addr}}</div>
        
        <!-- index从0开始 -->
        <div v-for="(addr, index) in addrs">{{index + 1}} : {{addr}}</div>
    </div>

</body>
<script>
    new Vue({
        el: "#app",
        data:{
            age: 20,
            addrs: ["北京", "上海", "深圳"],
        },
    })
</script>
```

##### Vue生命周期中的mounted()

```html
<script>
    new Vue({
        el: "#app",
        data:{
            
        },
        //  在vue挂载完成时自动运行
        mounted(){
        	alert("Vue挂载完毕");  
        },
    })
</script>
```



```javascript
new Vue({
    
}).$mount("#app")  //  与 el: "#app" 作用相同
```





















