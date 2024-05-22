---
title: 5.19-kn0wledge
date: 2024-05-20 17:42:21
tags: piecemeal
---

## String类

- 实现了Serializable ： 可以串行化实现网络传输
- 实现了Comparable：可以比较
- String的字符使用Unicode字符编码，一个字符占两个字节
- String 是final 类，不能被其他的类继承
- String 有属性 private final char value[]；用于存放字符串内容
- 一定要注意：value 是一个final类型， 不可以修改(指的是地址不可被修改)，单独的内容改变是允许的

### String类的两种创建方式
方式一：直接赋值 String s ="prd";
方式二: 调用构造器 String s2 = new String("prd")

> 方式一：先从常量池查看是否有"prd”数据空间，如果有，直接指向；如果没有则重新创建，然后指向。最终指向的是常量池的空间地址
> 方式二：先在堆中创建空间，里面维护了value属性，指向常量池的prd空间。如果常量池没有"prd”，重新创建，如果有，直接通过value指向。最终指向的是堆中的空间地址。

```bash
String a = "abc";
String b ="abc";
System.out.println(a.equals(b));//True
System.out.println(a==b);//True
```
a.equals(b):是将常量池中的字符串abc中的字符，挨个比较，如果都相同就返回T
a==b：两个对象比较地址，因为都是指向abc，所以为真；

### String类的一些特性示例
1. 以下语句创建了几个对象？
> String s1 ="hello";s1="haha";//创建了2个对象.
过程是先 在常量池创建 "hello"，s1指向"hello"，再创建"haha"，s1重新指向"haha"
因此创建两个对象  


2.  String a="heLlo"；
    String b ="abc";
    String c = a + b
>创建3个对象    
过程如下：
    1. StringBuilder ok = StringBuilder()
    2. 执行 ok.append("hello");
    3. ok.append("abc");
    4. String c= ok.toString()
    //最后其实是c 指向堆中的对象（String）vaLue[] -> 池中 “heLloabc"String c = a + b;


**常量相加看的是【常量池】，变量相加看的是 【堆】**
**每调用方法的时候会，新开一个【栈】**


###  String Builder和String Buffer

- String 的效率比较低，每次更新都需要开辟新的空间。
- StringBuilder 线程不安全，在单线程的时候使用、速度快
- StringBuffer 线程安全

#### 1. String Buffer 是可变字符长度，可对字符长度进行增删、还是一个容器
- 1. StringBuffer 的直接父类 是 AbstractStringBuilder
- 2. StringBuffer 实现了 Serializable，即StringBuffer的对象可以串行化
- 3. 在父类中 AbstractStringBuilder 有属性 char[] value，不是finalII该 Value 数组存放 字符串内容，引出存放在堆中的
- 4. StringBuffer 是一个 final类，不能被继承
```bash
StringBuffersstringBuffer = new StringBuffer("hello");
```

```bash
//看 String-->StringBuffer
//方式1使用构造器//注意： 返回的才是StringBuffer对象，对str 本身没有影响
String str = "hello tom";
StringBuffer stringBuffer= new StringBuffer(str);
//方式2使用的是append方法
StringBuffer stringBuffer1 = new StringBuffer();
stringBuffer1 = stringBuffer1.append(str);
//看看 StringBuffer ->String
StringBuffer stringBuffer3 = new StringBuffer（"bdadhfka"）;
//方式1 使用StringBuffer提供的 toString方法
String s = stringBuffer3.toString();
//方式2：使用构造器来搞定
String s1 = new String(stringBuffer3);
```
String Buffer example

```bash
String price = "8123564.59";
StringBuffer sb = new StringBuffer(price);

//int i = sb.lastIndexof(".");
//sb = sb.insert(i - 3, ",");

for(int i=sb.lastIndex0f(".")-3;i > 0;i -= 3)
{
    sb = sb.insert(i, ",");
    
}
System.0ut.println(sb);//8,123,564.59
```
---
#### 2.StringBuilder
- 1.  StringBuilder 继承 **AbstractStringBuilder 类**
- 2.  实现了 SerialLizable，说明stringBuilder对象是可以串行化（对象可以网络传输，可以保存到文件）
- 3.  StringBuilder **是final类，不能被继承**
- 4.  StringBuilder 对象字符序列仍然是存放在其父类 AbstractStringBuilder的 **"char[] value"** (属性);因此，字符序列是堆中
- 5.  StringBuilder 的方法，没有做互斥的处理，即没有synchronized 关键字，因此在单线程的情况下使用

String|StringBuffer|StringBuilder
:--|:--|:---|
不可变字符序列|可变字符序列|可变字符序列|
效率低|效率搞（增删）|效率最高|
复用率高|线程安全|线程不安全|
###|多线程|单线程

**String使用注意说明**：
>string s="a";的手创建了一个字符串s+=“b"；
实际上原来的”a"字符串对象已经丢弃了，现在**又产生**了**一个字符串**s+“b”（也就是"ab"）。如果**多次执行**这些**改变串内容的操作**，会导致大量副本**字符串对象存留在内存中**，降低效率。如果这样的操作放到循环中，会极大影响程序的性能

*结论：如果我们对String 做大量修改,不要使用String*