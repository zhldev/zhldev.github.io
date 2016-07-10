---
layout: post
title: 利器：swift闭包
date: 2016-07-09
categories: blog
tags: [swift,zhldev]
description:

---


* 1、闭包基础概念
* 2、闭包的循环引用
* 3、(闭包的返回值和参数) -> () in



##1、闭包基础概念

Closures是自包含的功能块。它可以捕获和存储其所在上下文的常量和变量的引用。全局函数和嵌套函数其实都是闭包。闭包有以下三种形式：

全局函数：有函数名，但不能获取任何外部值
嵌套函数：有函数名，同时可以从其上下文中捕获值
闭包表达式：闭包表达式(匿名函数) -- 能够捕获上下文中的值

类似于OC语言的block


>语法: in关键字的目的是便于区分返回值和执行语句
闭包表达式的类型和函数的类型一样, 是参数加上返回值, 也就是in之前的部分
{
    (参数) -> 返回值类型 in
    执行语句
}



##2、闭包的循环引用

在swift下要给属性赋初始值

	//当前写法代表闭包返回值可以是nil
    var finished: (()->())?


在视图初始方案里面调用闭包，OC block 和 swift 解决方案对比
   
	override func viewDidLoad() {
        super.viewDidLoad()
        //OC中的解决方案
        weak typeof(self) weakSelf = self
         weak var weakSelf = self
         loadData {
             print("回到主线程，更新UI")
             weakSelf!.view.backgroundColor = UIColor.redColor()
         }
     }

定义一个闭包方法，并且给一个循环 self 循环属性
   
 	 func loadData(finished:()->()){
         print("执行耗时操作")
         self.finished = finished
         finished()
     }


循环引用示意图

![闭包循环引用](http://oa1viup98.bkt.clouddn.com/bibaoxunhuanyinyong.png)


     //出栈会被释放，相当于OC中的dealloc
     deinit{
         print("退出栈，回退")
     }


##3、(闭包的返回值和参数) -> () in




—End—

##迭代
<!--
- 2015-09-14 01:52:09 再改
* 2015年6月19日 19:36:49 四稿
* 2015年6月17日 19:51:24 三稿
-->

* 2016年7月9日 12:13 完成循环引用章节
* 2016年7月8日 23:11 构建文章框架



---

### **【知行合一，为执行方能进步】**


心态软弱，在认为你的言论正确。你的正确，仅仅只是正确而已，我并需要那种东西。




----



<!--（题图：saurabh mohnot by Nik FC）-->
