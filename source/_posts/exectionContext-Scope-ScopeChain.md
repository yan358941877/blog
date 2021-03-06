---
title: 执行环境、作用域链、作用域
subtitle:   个人笔记
date: 2017-05-25 21:54:39
auther: 闫鑫鑫
catalog: true
comments: true
# header-img: "post-bg-unix-linux.jpg"
tags:
  - JavaScript基础
---

## 执行环境

* 执行环境中定义了变量和函数有权访问的其他数据，决定了他们各自的行为。
* 当JavaScript解释器初始化执行代码时，它首先默认进入全局执行环境，从此刻开始，函数的每次调用都会创建一个新的执行环境。 
* 每个函数都有自己的执行环境。当执行流进入一个函数时，函数的环境就会被推入一个环境栈中（execution stack）。在函数执行完后，栈将其环境弹出，把控制权返回给之前的执行环境。ECMAScript程序中的执行流正是由这个便利的机制控制着。 
* 执行环境可以分为创建、执行、销毁三个阶段。在创建阶段，解析器首先会创建一个变量对象（variable object），它由定义在执行环境中的变量、函数声明、和参数组成。**在这个阶段，作用域链会被初始化，this的值也会被最终确定**。在执行阶段，代码被解释执行。 某个执行环境中的所有代码执行完毕后，该环境被销毁，保存在其中的所有变量和函数定义也随之销毁

## 作用域链

* 当代码在一个执行环境中执行时，会创建变量对象的一个作用域链
* 作用域链的作用是：保证对 **当前执行环境权访问的所有变量和函数**的有序访问
* 作用域的前端始终是当前执行的代码所在环境的变量对象
* 作用域链的最后始终是全局执行环境的变量对象
* 作用域链里只包含上一级的变量对象，但并不包括下一级的变量对象
* 标识符解析的是沿着作用域链一级一级地搜索标识符的过程，搜索始终从作用域链的前端开始(当前环境的变量对象)，逐级向后查找(上级环境的变量对象)，直至找到标识符为止
* 内部环境可以通过作用域链访问所有外部环境，但是外部环境无法访问内部环境中的任何变量和函数
* 延长作用域链：
    * 在作用域链的前端(自己的变量对象之前)临时增加一个变量对象，该变量对象会在(这段)代码执行后被移除
    * try-catch语句中的catch块
    * with语句：


```JavaScript
function builder(){
    var str = "advd"
    // 在作用域链的前端临时增加了一个变量对象，这样在当前执行环境中就可以访问loaction的属性和方法了
    with(location){
        var url = href + str
    }
    // 当with代码执行后，作用域链中的临时变量对象被移除，此时无法访问href
    console.log(href) //  Uncaught ReferenceError: href is not defined
    return url
}
```

## 作用域

* 我认为作用域链是对变量对象/执行环境而言的，当执行环境中出现一个变量时，应该按照怎样的搜索方式(沿着作用域链)去找到这个变量
* 作用域是对于变量而言的，指明了这个变量在哪些地方可以被访问到，例如某一变量处于全局作用域中，则该变量可以在代码的任何地方被访问到
* 全局作用域：
    * 最外层函数和最外层函数外面定义的变量拥有全局作用域
    * 所有 **未定义** （要理解这个未定义的含义） 直接赋值的变量自动声明为拥有全局作用域
    * window对象的属性拥有全局作用域
* 函数作用域：
    * 在函数中定义的变量
    * 给函数传递的参数