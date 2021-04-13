---
title: Java知识点整理-02
date: 2020-05-05 19:51:51
tags:
 - Java
 - Java Core
 - Java开发
 - Java基础
comments: true
categories: Java开发
img: https://blog-imgs-1253907084.cos.ap-beijing.myqcloud.com/blog-cover-imgs/java-articles-cover-image.jpg
---
<center> <h1>Java知识点整理-02</h1> </center>
<center> <h2> <font color = lightgray>Java条件和判断语句</font> </h2> </center>

## 前言

今天想写一下关于条件和循环语句的一些知识点，Java中的条件语句主要有if相关语句和switch语句。循环语句主要有while相关语句和for循环语句。Java利用这些语句，来实现对程序流程的控制。

## Java条件语句

### 1. if条件语句

    1. if语句顾名思义，就是如果满足某个条件，就执行某段程序。基本用法是；

        if (条件) {
            // 条件满足后执行的代码
        }

    上述中，如果条件的返回结果是true，则继续执行大括号内内容。

    2. if语句执行块只有一行代码，可以省略大括号：

        if (条件)
            // 满足条件后的执行代码

    3. if语句块后，可以跟着else语句，如果if语句块条件判断为true，则执行if语句块内的代码，否则，执行else中代码，比如：

        if (条件) {
            // 条件=true，执行这里
        } else {
            // 条件=false，执行这里
        }

    4. if和else之间可以用多个else if来串联，比如下面这个示例：

        if (条件1) {
            // 条件1=true，执行这里
        } else if (条件2){
            // 条件2=true，执行这里
        } else if (条件3){
            // 条件3=true，执行这里
        } else {
            // 三个条件都不满足，执行这里
        }

    上述例子中的所有条件，可以是表达式，某个变量等，只要最终结果是boolean结果或者可以转成boolean结果，一般都行。

    5. if语句是从上往下来判断执行的，因此如果上面的条件包含后面语句的条件，则后面的判断块内代码执行不了，比如：
        
        int score = 87
        if (score >= 60) {
            System.out.println("及格");
        } else if (score >= 90){
            System.out.println("优秀");
        } else if (score >= 75){
            System.out.println("良好");
        } else {
            System.out.println("不及格");
        }
    
        上述代码结果是：及格

    上述可以看出，如果score是89分，我们的本意是想划分为良好，但是由于score >= 60在最上面，只要score大于60，则会执行其代码块内的代码，因此上述代码结果是"及格"，而不是我们想要的良好。因此写代码一定要注意，几个互相有重叠的条件，范围大的条件语句要放在下面。

### 2. switch条件语句

    1. 其实switch语句用的相对较少，而且switch语句是可以翻译成if相关语句来表示的。switch语句的最简单的表达方式是：

        switch(表达式) {
            case 表达式1:
                break;
            case 表达式2:
                break;
        }

    2. switch小括号中的表达式以前只能是数字，现在也可以是字母，字符串之类的了。程序进入switch语句后，直到遇到break才会结束，因此如果类似下方的例子：

        int opt = 1;
        switch(opt) {
            case 1:
                System.out.println(opt);
            case 2:
                System.out.println(opt);
                break;
        }

    上述代码我们的本意是打印相对应的输入，比如输入数字1就打印1，输入数字2就打印2。但是由于case 1中没有break，代码会继续执行case 2。因此，如果没有break，代码会继续向下方的case执行，直到遇到break，这种现象叫做case语句的穿透性。

    3. 如果switch表达式在case中没有对应的选项，那程序会从上到下判断所有case，发现没符合的，就结束了。但是如果我们想要输出一些东西，就需要用到另一个关键字 - default。

        int score = 78;
        switch(score) {
            case 1:
                System.out.println(opt);
                break;
            case 2:
                System.out.println(opt);
                break;
            default:
                System.out.println(opt);
                break;
        }

    上述代码中，78不符合所有case，因此程序会执行default中的代码，依旧可以打印相应的数字。

    4. 如果两个case可以使用一种处理方式，那么两个case可以连着写，比如：

        int score = 1 // 2;
        switch(score) {
            case 1:
            case 2:
                System.out.println("Valid Option");
                break;
            default:
                System.out.println("Invalid Option");
                break;
        }


    上述代码无论是输入score = 1还是2，都会得到Valid Option这个结果。

    5. switch语句如果保证有break，则case语句的顺序就不重要了。但是为了便于阅读，建议还是按照自然顺序去写。

    6. 以前的switch语句表达式只能是整数，现在可以是字符串和字符。如果是字符串，switch语句表达式和case后的表达式匹配时，比较的是内容。

        String food = "cake";
        switch(food) {
            case "cake":
                System.out.println("Option: " + food);
                break;
            case "bread":
                System.out.println("Option: " + food);
                break;
            default:
                System.out.println("Option: " + food);
                break;
        }
    
    上述代码输出的是cake。

    7. switch也可以接收枚举类型作为表达式。

    8. Java12之后，switch加入了类似模式匹配的表达方式，这种情况下，可以省略break。比如如下代码：

        String food = "cake";
        switch(food) {
            case "cake" -> System.out.println("Option: " + food);
            case "bread" -> System.out.println("Option: " + food);
            default -> {
                System.out.println("Option: " + food);
                System.out.println("Option: " + food);
            }
        }
    
    9. switch语句可以用来给变量赋值，如下方代码：

        int opt = -1;
        String food = "cake";
        switch(food) {
            case "cake":
                opt = 1;
                break;
            case "bread":
                opt = 2;
                break;
            default:
                opt = 3;
                break;
        }

    程序执行结束后，opt被赋值为1。

    10. 使用switch新语法，不但不需要使用break，还可以直接通过返回值来给参数赋值。

        int opt = -1;
        String food = "cake";
        opt = switch(food) {
            case "cake" -> 1
            case "bread" -> 2
            default -> 3
        }

    上述代码执行结束后，opt的值也是1。这种赋值方式简洁了很多。而且也不会因为忽略break而产生问题。

    11. 如果需要返回复杂语句执行后的结果，上述方式则不好用了，这时候可以使用yield关键字来返回所需的内容。

        int opt = -1;
        String food = "apple";
        opt = switch(food) {
            case "cake" -> 1
            case "bread" -> 2
            default -> {
                int temp = opt * 10 + 1 / 2;
                yield temp;
            }
        }

    上述代码返回结果是temp计算出来的结果。这样，不管语句多复杂，我们都可以顺利获得想要的返回值。

## Java循环语句
### 1. while，do while循环语句

    1. 循环语句的用途是非常广泛的，如果需要多次运行同一段程序，则需要用到循环语句。比如下列代码：

        int sum = 0;
        sum = sum + 1;
        sum = sum + 2;
        sum = sum + 3;
    
    上述代码得到的结果是1+2+3的和。这样写很麻烦，但是用循环，就简单很多了：

        int sum = 0;
        int num = 1;
        while (num <= 3) {
            sum = sum + num;
            num++;
        }

    上述代码的结果还是1+2+3的和。但是上述用到了while循环，代码就简单很多了。
    
    2. 由上述代码我们能看出while循环的基本形式是：

        while(条件表达式) {
            // 循环语句
        }

    while每次循环开始前，都会判断条件表达式是否成立，只有条件表达式返回true，才会进入循环体。否则就跳出循环，执行后面的代码。由于while循环是先判断，后进入循环体，因此可能一次循环都不执行。while循环条件很多时候是变化的，比如自增或者自减，因此需要特别注意边界问题。

    3. 所有循环语句，不论是while，for，还是do while，都会存在死循环的问题。死循环的产生原因是，条件永远符合。比如：

        int sum = 0;
        int num = 1;
        while (num <= -1) {
            sum = sum + num;
            num++;
        }

    上述代码会一直执行下去，直到内存溢出。而且这样无限循环下去，cpu占用会很高，电脑会变卡。其实上述代码到了一定程度仍然会退出，因为当num达到int类型最大值后，num会变为负数，循环还是会退出，因此上述只是模拟一个类似死循环。

    4. do while其实相对while，用的少很多，do while和while最大的区别在于最少执行次数。while循环体最少执行0次，因为while是先判断后进入循环。而do while循环体最少执行1次，因为do while是先执行循环体，后判断。do while的基本书写形式是：

        do {
            // 循环体
        } 　while (表达式);

    如果用do while计算1+2+3的和的话，代码是：

        int sum = 0;
        int num = 1;
        do {
           sum = sum + num;
           num++;
        } 　while (num <= 3);
    
    其实上述代码看起来和while区别不大，但是比如后面的例子，do while和while执行后会有区别。

        int num1 = 1;
        int num2 = 1;

        while (num1 < 1) {
            num1++;
        }

        do {
            num2++;
        } while (num2 < 1);

    上述代码执行结束后，num1的结果还是1，但是num2的结果是2了，因此能看出do while比while多执行了一次。

### 2. for循环语句 

    1. for循环的使用感觉比while的使用还要广泛，for循环的基本形式是：

        for (循环条件初始化; 循环条件判断; 更新循环条件) {
            // 执行语句
        }
    
    循环条件初始化，就是类似之前while循环之前，定义一个计数器，比如int num = 0;通常for使用计数器实现循环，别的其它条件的，比如用一个参数是true或者false，一个数组长度是不是0来判断，则用while比较好。for循环的执行顺序是：循环条件初始化 -> 循环条件判断 -> 循环体内执行语句 -> 更新循环条件。

    2. for循环写1+2+3的和：

        int sum = 0;
        for (int i = 1; i <= 3; i++) {
            sum = sum + i;
        }

    上述代码我们能看出，如果用计数器实现循环，for循环的代码比while循环的代码更简洁，也不容易出错。比如while循环中，很容易漏掉更新计数器这一步。

    3. for循环的小括号内分号分开的三个部分不是必须的。省略任何一个，两个或者三个都省略，是可以的。比如下面几个例子：
        例1: 
            int sum = 0;
            int i = 1;
            for (; i <= 3; i++) {
                sum = sum + i;
            }
        例2: 
            int sum = 0;
            int i = 1;
            for (; i <= 3; ) {
                sum = sum + i;
                i++;
            }

        例3: 
            int sum = 0;
            int i = 1;
            for (;;) {
                sum = sum + i;
                i++;
            }
    
    上述几个例子是for循环的一些使用，例3可能会导致死循环，通常不推荐，造成的结果和上面while循环死循环类似，只不过上面while循环可以停下来，for这个真的停不下来。

    4. for循环是通过使用计数器来实现循环，比如要是获取一个数组的所有元素，for循环写法是：

        int[] arr = {1,2,3,4,5};
        for (int i = 0; i < arr.length; i++) {
            System.out.println(arr[i]);
        }
    
    上述可见，我们定义一个循环计数器，以数组角标为循环计数器，这种做法是最普遍的。然后判断角标不要越界，每次循环体执行完毕，更新循环计数器。

    5. 但是如果我们不需要角标，还有更简单直观的写法，就是for each循环的写法：

        int[] arr = {1,2,3,4,5};
        for (int num : arr) {
            System.out.println(num);
        }

    for each 循环写法可以直接获取数组内的元素，for each是基于迭代器来获取元素的。因此只要是能被迭代的数据结构，都能用for each来循环。for each的基本形式是：

        for (数据类型 变量名 ：待循环数据结构) {
            // 执行代码
        }
    
    for each循环获取数据结构内元素非常方便，但是由于获取不到角标，因此需要操作角标的操作，则不能用for each。
        


### 3. break和continue

    1. 接下来说两个循环中最常用的关键字：break和continue。break语句是用来跳出这个循环的，类似switch语句的break。continue顾名思义，跳过这次循环，继续下一次循环。下面代码展示了它们两个的使用场景：

        例1:
            int[] arr = {1, 2, 3};
            for (int i = 0; i < 3; i++) {
                if (i == 2) break;
                System.out.println(arr[i]);
            }

            结果是：
                1
                2
    上述例子，打印结果没有最后一个数字，因为当角标等于2，程序直接break跳出循环，没有继续执行打印语句。

        例2:
            int[] arr = {1, 2, 3};
            for (int i = 0; i < 3; i++) {
                if (i == 1) continue;
                System.out.println(arr[i]);
            }

            结果是：
                1
                3
    
    上述例子，打印结果没有2，因为当角标等于1，程序进入if语句，执行continue，跳过本次循环继续下一次循环，没有继续执行打印语句。

    2. 多层循环嵌套的话，break总是跳出自己所在的那层循环，continue也是作用于自己所在的那层循环，它们不会直接影响到其它内层或者外层的循环。

## 结语

今天写了些关于条件语句和循环语句的知识点。都很简单，而且也都很常用。接下来，下一篇，我要开始写一下Java的核心 - 面向对象相关的知识点了。
    