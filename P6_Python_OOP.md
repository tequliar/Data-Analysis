# P6_Python面向对象

#### 这里是Python数据分析学习的第六篇笔记
本文包括了类和对象，构造函数，继承，多重继承和操作符重载。

---
## 类和对象
自从存在以来，Python一直是面向对象的语言。因此，创建和使用类和对象是非常容易的。

### 创建类
`class`语句创建一个新的类定义。类的名称紧跟在`class`关键字之后，在类的名称之后紧跟冒号。如下：
```
class ClassName:
    'Optional class documentation string'
    class_suite
```
- 该类有一个文档字符串，可以通过`ClassName.__doc__`访问。
- `class_suite`由定义类成员，数据属性和函数的所有组件语句

#### 示例
以下是一个简单的Python类的例子：
```
class Employee:
    'Common base class for all employees'
    empCount = 0
    
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
        Employee.empCount += 1
    
    def displayCount(self):
        print “Total Employee %d” % Employee.empCount
        
    def displayEmployee(self):
        print “Name : ”, self.name, “, Salary: ”, self.salary
```
- 变量`empCount`是一个类变量，其值在此类中的所有实例之间共享。这可以从类或类之外的`Employee.empCount`访问。
- 第一个方法`__init__()`是一种特殊的方法，当创建此类的新实例时，该方法称为Python构造函数或初始化方法。
- 声明其他类方法，如正常函数，但每个方法的第一个参数是self。Python将`self`参数添加到列表中;调用方法时不需要包括它。

### 创建实例对象
要创建类的实例，可以使用类名调用该类，并传递其`__init__`方法接受的任何参数。
```
## This would create first object of Employee class
emp1 = Employee(“Maxsu”, 2000)
## This would create second object of Employee class
emp2 = Employee(“Kobe”, 5000)
```

### 访问属性
可以使用带有对象的点(`.`)运算符来访问对象的属性。类变量将使用类名访问如下：
```
emp1.displayEmployee()
emp2.displayEmployee()
print (“Total Employee %d” % Employee.empCount)
```

现在把所有的概念放在一起：
```
class Employee:
   'Common base class for all employees'
   empCount = 0

   def __init__(self, name, salary):
      self.name = name
      self.salary = salary
      Employee.empCount += 1

   def displayCount(self):
     print ("Total Employee %d" % Employee.empCount)

   def displayEmployee(self):
      print ("Name : ", self.name,  ", Salary: ", self.salary)


#This would create first object of Employee class"
emp1 = Employee("Maxsu", 2000)
#This would create second object of Employee class"
emp2 = Employee("Kobe", 5000)
emp1.displayEmployee()
emp2.displayEmployee()
print ("Total Employee %d" % Employee.empCount)
```
当执行上述代码时，会产生以下结果：
```
Name :  Maxsu ,Salary:  2000
Name :  Kobe ,Salary:  5000
Total Employee 2
```
可以随时添加，删除或修改类和对象的属性
```
emp1.salary = 7000  # Add an 'salary' attribute.
emp1.name = 'xyz'  # Modify 'age' attribute.
del emp1.salary  # Delete 'age' attribute.
```
如果不是使用普通语句访问属性，可以使用以下函数：

- getattr(obj，name [，default]) - 访问对象的属性。
- hasattr(obj，name) - 检查属性是否存在。
- setattr(obj，name，value) - 设置一个属性。如果属性不存在，那么它将被创建。
- delattr(obj，name) - 删除一个属性。

下面是一些使用示例：
```
hasattr(emp1, 'salary')    # Returns true if 'salary' attribute exists
getattr(emp1, 'salary')    # Returns value of 'salary' attribute
setattr(emp1, 'salary', 7000) # Set attribute 'salary' at 7000
delattr(emp1, 'salary')    # Delete attribute 'salary'
```

### 内置类属性
每个Python类保持以下内置属性，并且可以像任何其他属性一样使用点运算符访问它们：
- `__dict__` - 包含该类的命名空间的字典。
- `__doc__` - 类文档字符串或无，如果未定义。
- `__name__` - 类名。
- `__module__` - 定义类的模块名称。此属性在交互模式下的值为“main”。
- `__bases__` - 一个包含基类的空元组，按照它们在基类列表中出现的顺序。

对于上述类，尝试访问所有这些属性：
```
class Employee:
   'Common base class for all employees'
   empCount = 0

   def __init__(self, name, salary):
      self.name = name
      self.salary = salary
      Employee.empCount += 1

   def displayCount(self):
     print ("Total Employee %d" % Employee.empCount)

   def displayEmployee(self):
      print ("Name : ", self.name,  ", Salary: ", self.salary)

emp1 = Employee("Maxsu", 2000)
emp2 = Employee("Bryant", 5000)
print ("Employee.__doc__:", Employee.__doc__)
print ("Employee.__name__:", Employee.__name__)
print ("Employee.__module__:", Employee.__module__)
print ("Employee.__bases__:", Employee.__bases__)
print ("Employee.__dict__:", Employee.__dict__ )
```
当执行上述代码时，会产生以下结果：
```
Employee.__doc__: Common base class for all employees
Employee.__name__: Employee
Employee.__module__: __main__
Employee.__bases__: (<class 'object'>,)
Employee.__dict__: {
   'displayCount': <function Employee.displayCount at 0x0160D2B8>, 
   '__module__': '__main__', '__doc__': 'Common base class for all employees', 
   'empCount': 2, '__init__': 
   <function Employee.__init__ at 0x0124F810>, 'displayEmployee': 
   <function Employee.displayEmployee at 0x0160D300>,
   '__weakref__': 
   <attribute '__weakref__' of 'Employee' objects>, '__dict__': 
   <attribute '__dict__' of 'Employee' objects>
}
```

### 销毁垃圾(垃圾收集)
Python自动删除不需要的对象(内置类型或类实例)以释放内存空间。 Python定期回收不再使用的内存块的过程称为垃圾收集。

Python的垃圾收集器在程序执行期间运行，当对象的引用计数达到零时触发。 对象的引用计数随着指向它的别名数量而变化。

当对象的引用计数被分配一个新名称或放置在容器(列表，元组或字典)中时，它的引用计数会增加。 当用`del`删除对象的引用计数时，引用计数减少，其引用被重新分配，或者其引用超出范围。 当对象的引用计数达到零时，Python会自动收集它。

```
a = 40      # Create object <40>
b = a       # Increase ref. count  of <40> 
c = [b]     # Increase ref. count  of <40> 

del a       # Decrease ref. count  of <40>
b = 100     # Decrease ref. count  of <40> 
c[0] = -1   # Decrease ref. count  of <40>
```

通常情况下，垃圾回收器会销毁孤立的实例并回收其空间。 但是，类可以实现调用析构函数的特殊方法 `__del__()` ，该方法在实例即将被销毁时被调用。 此方法可能用于清理实例使用的任何非内存资源。

#### 示例
这个 `__del__()` 析构函数打印要被销毁的实例的类名：
```
class Point:
   def __init__( self, x=0, y=0):
      self.x = x
      self.y = y
   def __del__(self):
      class_name = self.__class__.__name__
      print (class_name, "destroyed")

pt1 = Point()
pt2 = pt1
pt3 = pt1
print (id(pt1), id(pt2), id(pt3));   # prints the ids of the obejcts
del pt1
del pt2
del pt3
```
当执行上述代码时，会产生以下结果：
```
3083401324 3083401324 3083401324
Point destroyed
```
＞ 注意 - 理想情况下，应该在单独的文件中定义类，然后使用 `import` 语句将其导入主程序文件。

在上面的例子中，假定 `Point` 类的定义包含在 `point.py` 中，并且其中没有其他可执行代码。
```
import point
p1 = point.Point()
```

### 类继承
使用类继承不用从头开始构建代码，可以通过在新类名后面的括号中列出父类来从一个预先存在的类派生它来创建一个类。

子类继承其父类的属性，可以像类中一样定义和使用它们。子类也可以从父类代替代数据成员和方法。

#### 语法
派生类被声明为很像它们的父类; 然而，继承的基类的列表在类名之后给出：
```
class SubClassName (ParentClass1[, ParentClass2, ...]):
   'Optional class documentation string'
   class_suite
```

#### 示例
```
class Parent:        # define parent class
   parentAttr = 100
   def __init__(self):
      print ("Calling parent constructor")

   def parentMethod(self):
      print ('Calling parent method')

   def setAttr(self, attr):
      Parent.parentAttr = attr

   def getAttr(self):
      print ("Parent attribute :", Parent.parentAttr)

class Child(Parent): # define child class
   def __init__(self):
      print ("Calling child constructor")

   def childMethod(self):
      print ('Calling child method')

c = Child()          # instance of child
c.childMethod()      # child calls its method
c.parentMethod()     # calls parent's method
c.setAttr(200)       # again call parent's method
c.getAttr()          # again call parent's method
```
当执行上述代码时，会产生以下结果：
```
Calling child constructor
Calling child method
Calling parent method
Parent attribute : 200
```

以类似的方式，可以从多个父类来构建一个新的类，如下所示：

```
class A:        # define your class A
.....

class B:         # define your calss B
.....

class C(A, B):   # subclass of A and B
.....
```
可以使用 `issubclass()` 或 `isinstance()` 函数来检查两个类和实例之间的关系。
- `issubclass(sub，sup)` 布尔函数如果给定的子类`sub`确实是超类`sup`的子类返回True。
- `isinstance(obj，Class)` 布尔函数如果`obj`是类`Class`的一个实例，或者是类的一个子类的实例则返回 `True`。

### 重载方法
可以随时重载父类的方法。 重载父方法的一个原因是：您可能希望在子类中使用特殊或不同的方法功能。

#### 示例
```
class Parent:        # define parent class
   def myMethod(self):
      print ('Calling parent method')

class Child(Parent): # define child class
   def myMethod(self):
      print ('Calling child method')

c = Child()          # instance of child
c.myMethod()         # child calls overridden method
```

当执行上述代码时，会产生以下结果：
```
Calling child method
```

#### 基本重载方法
下表列出了可以在自己的类中覆盖的一些通用方法：

