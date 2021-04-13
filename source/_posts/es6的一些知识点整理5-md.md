---
title: es6的一些知识点整理5
date: 2020-02-26 23:29:47
tags:
 - JavaScript
 - ECMAScript 6
 - 前端开发
 - Web开发
comments: true
categories: 前端开发
img: https://blog-imgs-1253907084.cos.ap-beijing.myqcloud.com/blog-cover-imgs/frontend-js-article1.jpeg
---
<center> <h1>es6的一些知识点整理5</h1> </center>
<center> <h2> <font color = lightgray>基础部分</font> </h2> </center>

## 前言

今天准备说下ES6的新增的功能 - 箭头函数。其实箭头函数在很多其它语言中已经存在了，比如Java。箭头函数是匿名的，而且箭头函数的存在，省却了很多常用的操作。简化了代码，但是在说箭头函数之前，我准备先说下function命名的函数。

## 函数

普通函数自然是在ES5版本就已经存在了，相比于箭头函数，普通函数的兼容性自然好很多，下面是普通函数的定义：

    function func() {
        console.log("func");
    }

    let func2 = function() {
        console.log("func2");
    }

    func();
    func2();

结果是；

    func
    func2

显而易见，函数是有两种定义方式的，一种是常规的方式，function关键字后跟着函数名，之后是参数列表，然后是是函数体。第二种是表达式方式，就是函数名在等号左边，函数定义在等号右边。普通函数会绑定this，arguments等关键字，比如下方的例子：

    function a(a) {
         console.log("this: ", this, "\n arguments: ", arguments);
    }

    a(1,2,3,4);

结果是：

    this:  Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …} 
    arguments:  Arguments(4) [1, 2, 3, 4, callee: ƒ, Symbol(Symbol.iterator): ƒ]

普通函数的this指向的是调用他的对象，如上述代码，是直接写在script标签内的，是全局调用的，因此调用他的时候，this对应的是window。当然这是非严格模式下的，如果是定义为严格模式，也就是在代码前加入"use strict"，这个this会指向undefined。下面例子能让我们理解更清晰：

    let obj = {
        name: "name1",
        func: function() {
            console.log(this.name);
        }
    }

    obj.func();

结果是：

    name1

显而易见了，func函数是obj调用的。总之只要记住，普通函数的this指向其调用对象，不管他是函数，对象还是默认的window，就足够了。接着说下arguments，从之前的代码，我们能看到，arguments是普通函数绑定的关键字，类似于this，你不需要自己定义。arguments对应的是传入的所有参数。当然，普通函数还绑定super，指向其父类，这涉及到面向对象的知识，之后我会写专题。至于为什么有的时候普通函数的this并不好用呢，下面的例子可以说明：

    function Person() {
        this.a = 20;
        setInterval(function setA() {
            this.a++;
        }, 1000);
        console.log(this.a);
    }

    let p =new Person();

结果是：

    20

根据结果能看出来，Person构造函数的内部有个异步函数，1秒后a+1，但是通过打印结果能看出，这个函数并没有作用于Person这个构造函数中的a变量。因此如果这种情况想要改变Person中的a变量，只能引入一个变量指向Person中的this，如下：

    function Person() {
        this.a = 20;
        let that = this;
        setInterval(function setA() {
            that.a++;
            console.log(that.a);
        }, 1000);
        
    }

    let p =new Person();

上述代码中，我们引入了that指向Person函数的this，这样setA函数就能利用that来访问Person函数中的a了。但是这种写法比较麻烦，而且容易出错。箭头函数的一些特性，就是为了简化普通函数的this的使用，以及相关面向对象的使用，使函数看起来不那么像面向对象语言的函数用法。

## 箭头函数

顾名思义，就是用箭头表示的函数，它比普通函数更简洁，它没有绑定this，arguments和super。由于它的特性，它在面向对象编程中，不能用于定义构造函数。

以下是箭头函数的表达方式[1]：

    (param1, param2, …, paramN) => { statements } 
    (param1, param2, …, paramN) => expression => 当只需要返回时，可以省略大括号
    //相当于：(param1, param2, …, paramN) =>{ return expression; }

    // 当只有一个参数时，圆括号是可选的：
    (singleParam) => { statements }
    singleParam => { statements }

    // 没有参数的函数应该写成一对圆括号。
    () => { statements }

当然它还有很多高级用法：

    let test = params => {
        return {foo: "bar"}
    };

    //加括号的函数体返回对象字面量表达式[1]
    let test2 = params => ({foo: "bar"}); ===》上面的简写版
    console.log(test(1)); //{foo: "bar"}
    console.log(test(2)); //{foo: "bar"}

对于参数方面，虽然箭头函数相对于普通函数没有arguments，但是箭头函数支持剩余参数和参数默认值，如下：


    let a = (item1, item2, ...items) => {
        console.log(item1, item2, items);
    }

    a(1, "a", 1, 2, "as", "c"); //打印结果：1 "a" (4) [1, 2, "as", "c"]
    
    let b = (item1, item2 = 2) => {
        console.log(item1, item2);
    }

    b(1); //打印结果：1 2
    b(1, 1); // 打印结果：1 1

首先通过第一个函数a能看出，最后的items通过展开运算符（...）接收了除了1和"a"之外的剩下的所有参数。而b函数则向我们展示了参数默认值的用法，b函数接收两个参数，item1和item2，item2有默认值2，第一次调用它，只传入了一个参数，则item1得到传入值1，item2则保持默认值2，第二次调用，传入两个1，则item2就会被赋予新值，不再保留默认值。但是注意，带默认值的参数，要放在参数列表的最后面。

接着可以看下下面代码：

    let obj1 = {
        name: "name",
        func: () => {
            console.log("obj1:",this);
        }
    }

    let obj2 = {
        name: "name",
        func: function() {
            console.log("obj2:",this);
        }
    }

    obj1.func();
    obj2.func();

运行结果是：

    obj1: Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …}
    bj2: {name: "name", func: ƒ}

显而易见，obj1内实现箭头函数，this指向Window，而普通函数的this指向了obj2这个对象。所以，箭头函数的优势如下：

    function outer() {
        this.i = 2;

        function inner() {
            console.log("this:",this,"i:",this.i);
        }
        inner();
    }

    var outer = new outer();

    function outer2() {
        this.i = 2;

        let inner = () => {
            console.log("this:",this,"i:",this.i);
        }
        inner();
    }

   var outer2 = new outer2();

结果是：

    this: Window {parent: Window, opener: null, top: Window, length: 0, frames: Window, …} i: undefined
    this: outer2 {i: 2} i: 2

显而易见，同样是外部函数作为构造函数，调用了名为inner的内部函数，但是this的指向结果却不同，如果内部函数是普通函数，则this指向全局，也就是Window，所以，第一个this指向Window。而箭头函数没有this，它的this继承自上一层，上一层是outer2的实例，this指向outer2，因此箭头函数的this也指向outer2。因此第一个i的值是undefined，第二个是获取到outer2中的i的值，也就是2.

如果内部函数为普通函数，也需要得到外部函数的变量，那么可以用下方代码实现：

    function outer() {
        this.i = 2;
        this.inner = function () {
            console.log("this:",this,"i:",this.i);
        }
        this.inner();
    }

    var outer = new outer();

或者：

    function outer() {
        this.i = 2;
        let that = this;
        var inner = function () {
            console.log("this:",that,"i:",that.i);
        }
        inner();
    }

    var outer = new outer();

结果都是：

    this: outer {i: 2} i: 2

## 结语

箭头函数的基本用法和理解差不多就这么多了，总之，箭头函数没有this，所以对象相关的一切用法，比如new，prototype等，箭头函数都没有。在某些场合，箭头函数确实简化了书写，或者由于箭头函数this继承自上层，因此在某些情况箭头函数用起来更方便，但是只要用到和对象相关的方法或者关键字等，均不能用箭头函数。

## 参考链接
[1] https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions/Arrow_functions