---
layout: post
title: 在对象内部尽量直接访问实例变量
category: Objective-C
--- 

我们在对象的内部访问成员时通常有两种方法：

+ self.member
+ _member

过去我经常纠结该使用哪种，现在终于有了答案。

## self.member方式

self关键字在OC中相当于this在C++中的作用，就是代表类的对象，而我们知道点调用方式调用的是对象的setter和getter方法，因此self.member与我们在外部通过类的实例访问对象成员没有差别。

## _member方式

这种方式相当于C语言中用箭头符直接访问结构体成员的方式，也就是说用下划线访问成员不经过getter方法，因此使用这种方式可以更快地访问成员。

## 需要考虑的情况

由于不经过setter方法，因此在有些情况下直接访问实例会出现一些问题。

+ 获取copy修饰的成员变量
+ 获取懒加载的实例
+ 其他重写setter方法或是getter方法的情况

其实只要是重写了setter或是getter方法的对象，我们都应该使用点调用，否则重写就没意义了。

此外，直接访问成员不会触发KVO，并且在使用它的时候实际上也隐式调用了self，忽略它容易造成Block的循环引用。

可以发现，尽管直接访问实例成员速度更快，但它并不是在所有情况下都是好的，因此我们在编写代码时要注意此处使用直接访问会不会出现问题。

## 本篇到此为止，希望这对你有帮助，如果有错误或是有需要补充的地方，望告知。



