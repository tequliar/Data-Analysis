# P7_Python面向对象高级

#### 这里是Python数据分析学习的第七篇笔记

本文包括了构造函数、继承、多重继承和操作符重载

---
## 构造函数
构造函数是一种特殊类型的方法(函数)，它在类的实例化对象时被调用。 构造函数通常用于初始化(赋值)给实例变量。 构造函数还验证有足够的资源来使对象执行任何启动任务。

### 创建一个构造函数
构造函数是以双下划线(`__`)开头的类函数。构造函数的名称是`__init__()`。

创建对象时，如果需要，构造函数可以接受参数。当创建没有构造函数的类时，Python会自动创建一个不执行任何操作的默认构造函数。

每个类必须有一个构造函数，即使它只依赖于默认构造函数。

### 示例
创建一个名为`ComplexNumber`的类，它有两个函数:`__init__()`函数用来初始化变量，`getData()`方法用来显示数字。

```
class ComplexNumber:

    def __init__(self, r = 0, i = 0):
        """"初始化方法"""
        self.real = r 
        self.imag = i 

    def getData(self):
        print("{0}+{1}j".format(self.real, self.imag))

if __name__ == '__main__':
    c = ComplexNumber(5, 6)
    c.getData()
```
执行上面代码，得到以下结果:
```
5+6j
```
可以为对象创建一个新属性，并在定义值时进行读取。但是不能为已创建的对象创建属性。
```
class ComplexNumber:

    def __init__(self, r = 0, i = 0):
        """"初始化方法"""
        self.real = r 
        self.imag = i 

    def getData(self):
        print("{0}+{1}j".format(self.real, self.imag))

if __name__ == '__main__':
    c = ComplexNumber(5, 6)
    c.getData()

    c2 = ComplexNumber(10, 20)
    # 试着赋值给一个未定义的属性
    c2.attr = 120
    print("c2 = > ", c2.attr)

    print("c.attr => ", c.attr)
```
执行上面代码，得到以下结果:
```
5+6j
c2 = >  120
Traceback (most recent call last):
  File "D:\test.py", line 23, in <module>
    print("c.attr => ", c.attr)
AttributeError: 'ComplexNumber' object has no attribute 'attr'
```

---
## 继承
继承用于指定一个类将从其父类获取其大部分或全部功能。 它是面向对象编程的一个特征。 这是一个非常强大的功能，方便用户对现有类进行几个或多个修改来创建一个新的类。新类称为子类或派生类，从其继承属性的主类称为基类或父类。

子类或派生类继承父类的功能，向其添加新功能。 它有助于代码的可重用性。

下图表示：
![图一](http://www.yiibai.com/uploads/images/201706/2706/955200640_89651.png)

![图二](http://www.yiibai.com/uploads/images/201706/2706/847200644_72619.png)

### 语法一
```
class DerivedClassName(BaseClassName):  
    <statement-1>  
    .  
    .  
    .  
    <statement-N>
```

### 语法二
```
class DerivedClassName(modulename.BaseClassName):  
    <statement-1>  
    .  
    .  
    .  
    <statement-N>
```

### 参数说明
必须在包含派生类定义的范围中定义名称 `BaseClassName` 。还可以使用其他任意表达式代替基类名称。 当在另一个模块中定义基类时要指定模块的名称。

### 示例
在这个示例中使用两个类：`Animal`和`Dog`。`Animal`是父类或基类，`Dog`是`Animal`的子类。

在这里，在`Animal`类中定义了`eat()`方法，`Dog`类中定义了`bark()`方法。在这个例子中，我们创建`Dog`类的实例，并且仅通过子类的实例调用`eat()`和`bark()`方法。 由于父属性和行为自动继承到子对象，所以通过子实例也可以调用父类和子类的方法。

```
class Animal:   
    def eat(self):  
      print 'Eating...'  
class Dog(Animal):     
   def bark(self):  
      print 'Barking...'  

d=Dog()  
d.eat()  
d.bark()
```

执行上面代码，得到以下结果:

```
Eating...  
Barking...
```

---
## 多重继承
与C++一样，一个类可以从Python中的多个基类派生出来。这被称为多重继承。

![图片一](http://www.yiibai.com/uploads/images/201706/2706/451080631_51525.jpg)

在多重继承中，所有基类的特征都被继承到派生类中。多重继承的语法类似于单继承。

### 示例
```
class Base1:
    pass

class Base2:
    pass

class MultiDerived(Base1, Base2):
    pass
```

