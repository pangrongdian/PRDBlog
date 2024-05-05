---
title: 5.5-KnowledgePoint
date: 2024-05-05 14:13:04
tags: piecemeal
---

## 接口

### 接口基本知识

- 接口中的方法都是抽象方法（访问权限是公共的）（可以省略abstract关键字）（没有方法体）

- 接口中可以有默认实现方法，但需要default关键字（JDK 8 后）

- 接口中可以有静态方法，但需要Static关键字（JDK 8 后）

- 接口中的属性都是final， public static final 数据类型 属性（默认都有）
`int a =1 可以写在接口中，等价于public static final int a =1 （必须初始化）`

- 接口不能继承其他类，但是可以继承多个接口

- 接口的访问修饰符只能是public 和 默认

*访问修饰符*
访问权限|类|包|子类|其他包|备注
:-----:|:-:|:-:|:-:|:--:|:--:|
public|√|√|√|√|对任何都是可用
protect|√|√|√|×|继承的类可以访问
default|√|√|×|×|包访问权限整个包都可以被访问
private|√|×|×|×|除类型创建者和类型内部的方法之外任何人都不能访问

#### 接口多态

- 接口类型的变量可以指向，**实现了接口类的对象实例**
`类似于继承体现的多态：父类类型的变量可以指向，其子类的对象实例`

- 接口多态的传递性，当两个接口A，B，A extend B， B就可以指向A类型的对象实例；

```bash

    public static void main(String[] args) 
    {
        A a = new C();
        B b = new C();
    }
  interface  A extends B {}
  interface  B {}
  class C implements A{}

```

## 内部类

- 类的成员：属性、方法、构造器、代码块、内部类

*四种内部类：* 

内部类|位置|说明
:--:|:---|:---|
局部内部类|外部类局部位置|有类名
匿名内部类|外部类局部位置|无类名
成员内部类|外部类成员位置|无static
静态内部类|外部类成员位置|有static

### 局部内部类
- 通常定义在方法中
- 可以访问外部类的所有成员，包括私有的
- 可以被final修饰但是其他访问修饰符不可以
- 作用域：仅在定义他的方法或代码块中
- 外部类可以new 内部类；
- 外部类和内部类的成员重名，遵循就近原则，也可通过（外部类名.this.成员访问）

```bash

class A  {//外部类
    private  int a = 50;
    public  void  aVoid(){};

    public  void  innerMethod()
    {
        final  class InnerA //内部类
        {
            private  int a =1;
            public  void  f()
            {
                System.out.println("innerClass properties"+a+"outClass properties"+A.this.a);
            }
        }

        InnerA innerA = new InnerA();
        innerA.f();
    }


```

### 匿名内部类
- 当一个类只能使用一次（但是）对象还是可以使用，可以使用匿名内部类来简化。

```bash
class A
{

    public  void Anony()
    {
        /**
         *  接口是不能实例化的，但是这里是相当于
         *  创建了anony类后，实现了接口;
         */
        B anony = new B()
        {

            public void say()
            {
                System.out.println("annoy  is OK ");
            }
        };
        //这里的运行类型是 A（动态绑定）
        anony.say();
        System.out.println("anony runClass type is"+anony.getClass());
        OK ok = new OK(){};
        System.out.println("OK    runClass type is"+ok.getClass());

    }
}
interface  B
{
   public void  say ();
}

class OK{}
```
*输出结果：*
annoy  is OK 
anony runClass type isclass  A$1
OK    runClass type isclass  A$2
`A$1 这个地址是jvm给匿名内部类分配的地址`

- **基于基本类||抽象类，都可以在匿名类中重写方法，只不过抽象类必须要实现原有方法**


#### 匿名内部类的使用场景

- 当作参数传递

```bash
    fc(new AT()
        {
            @Override
            public void show() 
            {
                System.out.println("匿名内部类当参数传递");
            }
        });

public static void fc(AT at)
{
    at.show();
};

interface AT
{
    void show();
}
```

### 成员内部类

- 成员内部类是定义在外部类的成员位置

- 可以直接访问外部类的所有成员，包含私有的

- 可以添加任意访问修饰符（因为其本身就作为一个成员）

- 作用域：和其他成员一样

如何使用成员内部类

1. 外部类.成员内部类 引用 = 外部类引用.new 成员内部类（）；
2. 在成员内部类中创建一个方法，用以获取成员内部类的实例；


### 静态成员内部类

- 成员内部类是定义在外部类的成员位置 ，有Static修饰

- 可以创建一个静态方法直接访问，不用创建实例。

- 同上
