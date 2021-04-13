---
title: Java知识点整理-04
date: 2020-05-17 16:06:39
tags:
 - Java
 - Java Core
 - Java开发
 - Java基础
comments: true
categories: Java开发
img: https://blog-imgs-1253907084.cos.ap-beijing.myqcloud.com/blog-cover-imgs/java-articles-cover-image.jpg
---
<center> <h1>Java知识点整理-04</h1> </center>
<center> <h2> <font color = lightgray>Java面向对象-02</font> </h2> </center>

## 前言

今天继续写一些关于构造方法的知识点。有时候我们会看到，在创建一个实例的时候，会给实例一个初始值，比如：

    Food food = new Food("Beef");

这句话如果按照上一个文章的写法是：

    Food food = new Food();
    food.setRecipe("Beef");

可见如果能在创建实例的时候就给这个实例相应的内容，会简单很多。而帮我们完成这个目标的函数，就是构造函数。

## Java构造函数

### 构造函数
    实际上，每次创建一个实例时，是通过构造方法来创建实例，比如上述例子：

        class Food {

            String recipe:

            public Food(String recipe) {
                this.recipe = recipe;
            }
        }

    从上述例子我们能看出，构造函数的基本形式是：

        修饰字段 类名(想要初始化的参数列表) {
            // 构造函数内容
        }

    构造函数的名字和类名一样，首字母也是大写的，这点和其它函数不同。构造函数没有返回值和返回类型，只有访问可见性的修饰字段。大部分时间，在简单的项目和代码中我们就直接定义构造函数为public，但是构造函数也可以用其它修饰类型，比如private来修饰的。构造函数的参数列表并没有要求，想要在创建实例的时候初始化的字段，都可以放在参数列表。

### 默认构造函数

    但是类似我们上一篇文章中的例子，比如：

        class Person {
            String name;
            int age;

            // ...其它一些方法
        }

    我们并没有写任何构造函数，但是还是可以创建上述类的实例。这是因为，如果当我们没有定义构造函数时，Java会帮我们生成一个默认的构造函数，这个构造函数不传入任何参数。因此上述例子实际是这样：

        class Person {
            String name;
            int age;

            // 默认构造函数
            public Person() {

            }
            // ...其它一些方法
        }

    当我们自定义构造函数时，Java便不会执行默认构造函数，因此上述Food类的例子，我们无法创建一个不传入任何参数的实例。

    如果想既可以创建带参数的实例，又可以创建不带参数的实例，便只需要把这些构造函数都定义出来。这涉及到另一个概念 - 函数的重载，在后面我会展开说。

    没有在构造函数中初始化的参数，引用类型默认值时null，int类型是0，boolean类型是false，double是0.0。

    当类中有多个构造方法的时候，Java可以通过识别参数个数和类型来判断在创建实例时候，需要调用哪一个构造函数。

## 方法重载

上面我提到了一种概念，叫做函数/方法的重载，具体意思就是如果一个类中需要一系列的作用类似，参数不同的方法，则可以把它们定义成一个名字，例如：

    class Food {

        public void addFood(String name, int weight) {
            //
        } 

        public void addFood(String Name) {
            //
        }

        public void addFood(String[] names, int[] weights) {
            //
        }
    }

上述例子中，我们重载了addFood方法，重载方法的参数不同，但是通常返回类型是相同的。这样我们在使用某个方法时，更灵活，也不会因为定义过多的不同方法名的函数而显得混乱。

## 结语

这篇文章比较短，因为想继续写后面的内容，但是发现后面想写的内容，比较复杂内容比较多，因为我接下来想讲一下面向对象的一个很重要的特性 - 继承和多态。因此这篇文章就这样结尾吧，下一篇文章，便是Java的重头戏之一，继承和多态。
    