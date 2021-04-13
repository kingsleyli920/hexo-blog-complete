---
title: Java知识点整理-03
date: 2020-05-12 23:58:00
tags:
 - Java
 - Java Core
 - Java开发
 - Java基础
comments: true
categories: Java开发
img: https://blog-imgs-1253907084.cos.ap-beijing.myqcloud.com/blog-cover-imgs/java-articles-cover-image.jpg
---
<center> <h1>Java知识点整理-03</h1> </center>
<center> <h2> <font color = lightgray>Java面向对象-01</font> </h2> </center>

## 前言

今天这篇文章写一下关于Java面向对象的知识点。Java是一种面向对象语言，英文是Object-Oriented Programming，缩写是OOP。要说面向对象，得先说下面向过程语言。C语言就是一种面向过程语言，面向过程，本质就是一步一步执行代码，完成一个程序。比如你需要操作打印机打印东西，面向过程就是：

    1. 链接打印机
    2. 打开文档
    3. 开始打印
    4. 打印结束

而如果是面向对象语言呢，每个程序都有一个或者若干对象（实例），完成一段程序，就是对象之间互动。比如上述例子：

    1. 创建电脑实例
    2. 创建打印机实例
    3. 电脑和打印机通信
    4. 电脑调用打印
    5. 请求转到打印机接口并打印

其实这么简单的例子，看起来区别不大，甚至面向对象好像还麻烦一点。但是面向对象语言的实现方式，很接近我们的现实生活，因此更容易理解。

## Java面向对象的基础

要想讲面向对象，应该得先了解Java的类和实例。

    1. 类（class）

    类是一种对象的模版，它定义了如何创建对象。class在Java中也是一种数据类型。比如下面这个例子：

        class Food {
            public int weight;
            public String taste;
        }

    类的定义方式就是：

        class 类名 {
            修饰字段 类型字段 名称； //类内的字段的定义方式
        }

    一个类中可以有包含多个字段，字段的定义方式类似上述。其中在我们的例子中，修饰字段用的是public，这个修饰字段是表示字段是否能被外部访问。

    通常public修饰的话，是可以被任何方式访问，其它方式还有，比如：
    
        protected：允许当前类，子孙类和同一个package下的类访问
        
        default（或者不写任何修饰字段）：当前类和同一个package下可见。
        
        private：仅当前类可见

    类中字段的类型字段是相应的字段类型，比如可以是基本类型，int，double等，也可以是引用类型，比如String，Person，Food这种类类型。

    2. 实例/对象（instance）

    实例是对于类模版的一种实现，一个类可以有很多实例，每个实例可能会包含不同的属性。

    定义了类仅是定义了一个模版，如果要使用这个类的功能，必须要创建该类的实例。Java中创建类的实例的方法是通过new这个关键字，比如上述Food例子：

        Food food = new Food();
    
    然后通过food.weight就可以获得实例对应的字段的值了。

## Java面向对象 - 方法

对于面向对象来说，类很重要，而另一个也很重要的内容是方法（method）。方法的用途就是提供一些途径去处理类中字段或者其它用户需求的内容。

    1. 方法

    有时候直接把字段暴露在外这种做法并不好，因为其他人能随意篡改，破坏了Java的一大特性 - 封装性。因此大多数情况，我们会用private修饰字段，因为private修饰的字段，只能在类内可见。因此在外部是无法调用的。所以我们可以用public修饰相应的操作字段的方法。比如下列代码：

        class Person {
            private String name;
            private int age;

            public void setPerson(String name, int age) {
                this.name = name;
                this.age = age;
            }
        }
    
    上述代码，当我们直接用person实例调用name或者age字段时，会报错，如果想修改字段，需要调用setPerson方法：

        Person p = new Person();
        p.setPerson("Bob", 12);

    从上述代码我们能看出，方法的基本定义方式如下：

        修饰符 返回类型 方法名(参数列表){
            // 方法体
            // 返回值
        }

    修饰符基本就是public，private这些，还有static，abstract这些，等后面再说。

    返回类型可以是Java基本类型，比如int，double，也可以是引用类型，比如Person，String。

    方法名一般没什么要求，但是尽量有意义，方法名的定义规则是第一个单词首字母小写，后面跟着的单词首字母大写，比如setName。这不是强制规定，但是已经形成了业界最基本的书写习惯。

    参数列表用来罗列出需要传入方法的参数，比如setName方法，你需要传入你想设置的名称，那么setName方法要写成setName(String name)这种形式，参数要写成“参数类型 参数名”这种形式。

    特别注意，方法通常在执行完是要有return语句返回结果的，比如：

        public int getAge() {

            return age;
        }

    返回的数据类型要和方法返回类型对应。有时候我们会看到，方法的返回类型被定义为void，这个关键字的意思是空类型。当遇到void时候，通常不需要写return，如果要写，需要写成“return;”。

    同变量一样，方法也可以用private，protected，default（或者没有修饰符）等修饰。可见性也是一样的，因此如果一个方法是private的，这个方法只能被类内其它方法调用，通常我们会把一些不想要用户使用的方法，设置成private。

    2. this变量

    在上述例子中，我们看到了类似this.name = name;的这种使用。this是用来指向类的当前实例。通常this的最常用用法，就是当方法参数名和类内字段名（变量名）冲突，为了区别，使用“this.变量名 = 参数名”这种方式。因为如果少了this，变量可能被认为是局部变量。

    3. 可变参数

    在上述例子中，方法参数我们是用“(String name, int age)”这种方式来表示。但是如果我们传入的参数不定，这种方式就不行了。我们可以用可变参数的方式：

        class Person {
            String[] names;
            public void setNames(String... names) {
                this.names = names;
            }
        }

        Person p = new Person();
        p.setNames("Bob", "Alice", "Kate");
        p.setNames("Happy", "Birthday");
        p.setNames("Hello World");

    上述代码我们能看出，setNames接收的是可变变量，可以把传入的参数打包成一个String类型的数组传入方法。上述代码的最常用写法是：

        class Person {
            String[] names;
            public void setNames(String[] names) {
                this.names = names;
            }
        }

        Person p = new Person();
        p.setNames(new String[] {"Bob", "Alice", "Kate"});
        p.setNames(new String[] {"Happy", "Birthday"});
        p.setNames(new String[] {"Hello World"});

    4. 参数绑定

    参数绑定指调用一个方法时，传入参数，按位置和方法对应的参数绑定。比如：

        class Person {
            String name;
            public void setName(String name) {
                this.name = name;
            }
        }

        Person p = new Person();
        p.setName("Tony");
        
    上述代码"Tony"字符串会绑定在setName方法的name参数上。

    当传入的值是基本数据类型时，传入的是值的复制。因此在外部修改传入值，对方法内参数没影响：

        class Person {
            private int age;

            public void setAge(int age) {
                this.age = age;
            }

            public int getAge() {
                return age;
            }
        }

        int age = 15;
        Person p = new Person();
        p.setAge(age);
        System.out.println(p.getAge());
        age = 20;
        System.out.println(p.getAge());

    上述代码运行后，打印结果都是15。可以看出，虽然传入的age在外部被改变了，但是也没有影响传入的值。

    而传入的是引用类型时，外部值改变会影响传入函数的值：

        class Person {
            private String[] names;

            public void setName(String[] names) {
                this.names = names;
            }

            public String[] getNames() {
                return names;
            }
        }

        String[] names = {"Andrew", "Bob"};
        Person p = new Person();
        p.setNames(names);
        System.out.println(Arrays.toString(p.getNames()));
        names[0] = "Luke";
        System.out.println(Arrays.toString(p.getNames()));
    
    上述代码的结果是“Andrew, Bob”和“Luke, Bob”。因为当传入参数是引用类型，函数内的局部变量则指向引用类型参数值所在的地址，而不是获得了相应的值。等于传入后，方法局部参数和外部传入的参数指向同一个内存地址，因此外部参数修改了内存地址中的内容后，也会影响到函数内部的参数值。

    当然，如果传入String类型，会出现和传入一个基本类型一样的结果，就是外部变量改变，内部的变量值不会被影响。这是因为，参数传入方法后，外部变量和函数局部变量都指向同一个字符串，而当外部变量改变时，并不是改变了指向地址的字符串值，而是改变了它自己的指向，因此方法内局部变量仍然指向原来指向的字符串，且字符串值并没有变。


## 结语

今天写了点关于面向对象的基本概念，同时说了下关于类，实例，变量，参数，方法等面向对象语言很重要的基础部分。本想继续说下关于构造函数。但是感觉文章篇幅不想太长。那就下一篇，先说下构造函数，再说下方法重载，因为重载在构造函数中用途很广。如果篇幅不长，下一篇中还会写Java的核心中的核心 - 继承和多态的知识点。
    