---
title: knowledge Point
date: 2024-05-02 15:28:03
tags: piecemeal
---


## 2024.5.2

### 动态绑定机制
- 调用对象方法的时候，会到运行类型中找（方法会和对象内存地址/运行类型绑定）
- 调用对象属性的时候，哪里有找哪里，没有动态绑定机制。
> *f:父类A和子类B，A a = new B（），子类重写了父类的方法，当调用该方法时候发现，有两个可用的方法，用子类还是父类的方法*
> *当然是子类的，因为运行类型是子类B*

### Equals 方法和 “==”


- Equals : 没有重写equals方法，比较地址  *(引用类型的变量所指向的对象的地址)*
- “==” : *基本数据类型*时比较的是表面*值内容*，两个*对象*比较的是两个对象的*内存地址值* 



- “==” 适用于基本类型和引用类型，Equals只适用于引用类型。
- 默认重写equals方法的类 : String、Date、File,Wrapper 类，数组类，Collection类
- 重写Equals方法，实现比较传入对象的参数是否相同
```bash
      public boolean equals(Object obj)
        {

            if (this == obj) {
                return true;
            }
            if(obj instanceof Person p){
              //Person p = obj(向下转型)
                return  this.age==p.age&&this.name.equals(p.name)&&this.saraly==p.saraly;
            }
            return false;
        }

```

### toString--HashCode--Finalize

- toString 重写toString方法用来，输出对象 
> 方法如果不重写，默认输出，包名+类名+地址（十六进制的）
> 当直接输出该对象的时候，默认调用该方法。


- hashCode 方法，生成一个int类型的值（根据地址号来的），可以用以比较两个对象是否相等
> 由于hash值的生成问题，可能导致不同的对象，hash值相同。
> 该方法可以提高哈希结构的容器效率

- finalize 方法 用以在回收对象前，释放资源
> 1. 对象回收时系统会自动调用该对象的finalize方法，子类可以重写该方法。
> 2. 当对象没有任何引用的时候，jvm会根据垃圾回收机制，销毁该对象，并调用finalize方法，释放资源。
> 3. 当对象没有任何引用的时候，并不会立即回收，（GC算法）控制，但是可以通过System.gc()，主动触发垃圾回收。

