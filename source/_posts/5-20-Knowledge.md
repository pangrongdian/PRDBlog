---
title: 5.20-Knowledge
date: 2024-05-20 16:58:35
tags: piecemeal
---

## Warpper（包装）类

8个基本类型中的每一个都有对应的包装器类。

原始类型|包装类|上一级
:----|:-----|:-----|
boolean|	Boolean|I:Comparable,Serializable,C:Object
char	|Character|I:Comparable,Serializable,C:Object
byte	|Byte|I:Comparable,C:Number->Serializable,C:Number->Object
double|	Double|I:Comparable,C:Number->Serializable,C:Number->Object
float	|Float|I:Comparable,C:Number->Serializable,C:Number->Object
int	|Integer|I:Comparable,C:Number->Serializable,C:Number->Object
long|	Long|I:Comparable,C:Number->Serializable,C:Number->Object
short|	Short|I:Comparable,C:Number->Serializable,C:Number->Object

`byte-short数字类的都是从Number继承来的`


```bash
//jdk5前是手动装箱和拆箱
//手动装箱int->Integer
int n1 = 100;
Integer integer =new Integer(n1);
Integer integer1 = Integer.value0f(n1);
//手动拆箱//Integer -> int
int i = integer.intValue()
//jdk5后，就可以自动装箱和自动拆箱
int n2 = 200;
//自动装箱 int->Integer
Integer integer2 = n2; 
//底层使用的是 Integer.valueQf(n2)
 ```
```bash
 Double d = 100d;等价于 Double.value0f（100d）;
 Float f = 1.5f;等价于Float.value0f（1.5f）;
 Object obj1 =true？new Integer（1）：new Double（2.0）;
 //三元运算符System.out.println（obj1）；// 什么？ 1.0
 Object obj2;if(true)obj2 = new Integer(1);else obj2 = new Double(2.0);System.out.println(obj2);//1
 ```

 ### Warpper类转String
```bash
//包装类（Integer)->String
Integeri=100;
/方式1
String str1 = i + "";
/方式2
String str2 = i.toString();
/方式3
String str3 = String.value0f(i);
```
 ### String转Warpper类
``` bash
//string -> 包装类（Integer）
 String str4 = "12345";
 Integer i2 =Integer.parseInt(str4);//这里的parseInt返回的是Int类型，自动转换
 Integer i3 = new Integer(str4);//构造器，Integer自带这样的构造器
 ```

### Integer类小知识

```bash
 Integer i = new 1Integer(1);
 Integer j = new Integer(1);
 System.out.println(i == j); 
 //False 这里主要是看范围-128～127就是直接返回
 Integer m =1；
 Integer n = 1;
 //上面两个底层是 Integer.value0f(1);
 System.out.println(mm==n); //True
 //所以，这里主要是看范围-128~127就是直接返回
 //，否则，就new Integer（xx）;
 Integer x = 128;
 Integer y = 128;
 System.out.println(xx==y);//False
 ```
- Integer.valueOf,没超过127 就是直接在Integer的cache中