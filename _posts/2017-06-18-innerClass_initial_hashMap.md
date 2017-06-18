---
layout: post
title: 匿名内部类初始化HashMap
categories: Java
description: Activemq, Spring
keywords: Tool, Java, Activemq, Spring
---

### 0.必备的知识

* 内部类
* 实例化代码块

### 1.引言

```text
 Map<String, String> map = new HashMap<String, String>() {{
    put("key1", "value1");
    put("key2", "value2");
 }};
```
不知道你第一次看到这代码时候什么感觉，我当时是懵逼了。。此文解决！

### 2.浅谈匿名内部类

以下几点明白啥是匿名内部类

* 匿名内部类是局部内部类的变种
* 匿名内部类是匿名的，不能重复new
* 匿名内部类必须实现一个接口or继承一个类

### 3.常用的地方

#### 3.1 java awt 中 常用的实现监听器的动作

实现Listener接口的匿名类
代码略

#### 3.2 线程实现处理方法

实现Runnable接口的匿名类：
```java
Thread thread = new Thread(new Runnable() {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(i);
        }
    }
});
```
#### 3.3 如引言所示

```text
 Map<String, String> map = new HashMap<String, String>() {{
    put("key1", "value1");
    put("key2", "value2");
 }};
```
``3.1``和``3.2``都明白，但两对大括号什么鬼？
分析：

* 此匿名内部类是继承HashMap
* 但并没有重写HashMap方法
* 之前被外表的假象所迷惑，继承方法可以添加方法嘛，只是方法比较特殊，是实例化代码块

**至此问题解决**