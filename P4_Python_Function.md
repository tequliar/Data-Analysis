# P4_Python自定义函数

#### 这里是Python数据分析学习的第四篇笔记
本文包括了自定义函数，代码规范，函数参数，匿名函数，return语句和变量的作用范围

---
## 自定义函数
- 自定义函数使用者定义的、专门用于解决一种或一类问题的函数
```
def functionname( parameters ):
   "函数_文档字符串"
   function_suite
   return [expression]		
```

### 代码规范
- 函数代码块以def关键词开头，后接函数标识符名称和圆括号().
- 函数内容以冒号起始，并且缩进
- 调用时直接使用函数名加参数即可
```
def printme( str ):
   "打印传入的字符串到标准显示设备上"
   print str
   return
   
#函数调用
printme("我要调用用户自定义函数!");
printme("再次调用同一函数");
```
- 函数的第一行语句可以选择性地使用文档字符串来存放**函数说明**
```
# 可写函数说明
def changeme( mylist ):
   "修改传入的列表"
   mylist.append([1,2,3,4]);
   print "函数内取值: ", mylist
   return
 
# 调用changeme函数
mylist = [10,20,30];
changeme( mylist );
print "函数外取值: ", mylist
```
- 任何传入参数和自变量必须放在圆括号中间。圆括号之间可以用于定义参数。

- Return[expression]结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回None

### 函数参数
- 主要包括四种：必备参数、命名参数、缺省参数和不定长参数
- 必备参数必须以正确的顺序传入到函数中，其数量必须与函数中的一致
```
def printme( str ):
   "打印任何传入的字符串"
   print str;
   return;

printme();
# 未传入参数，程序报错
```

- 命名参数和函数的调用关系十分密切，调用方通过函数的命名确认参数值
- 因为python的解释器可以匹配参数名称和参数值，故可以跳过不传的参数或乱序传入参数，只要对参数名称和值进行匹配即可
```
# 单一参数
def printme( str ):
   "打印任何传入的字符串"
   print str;
   return;
 
printme( str = "My string");

# 多个参数
def printinfo( name, age ):
   "打印任何传入的字符串"
   print "Name: ", name;
   print "Age ", age;
   return;
 
printinfo( age=50, name="miki" );
```

- 缺省参数在调用时如果没有参数传入的话，就会使用默认值
```
def printinfo( name, age = 35 ):
   "打印任何传入的字符串"
   print "Name: ", name;
   print "Age ", age;
   return;
 
printinfo( age=50, name="miki" );
printinfo( name="miki" );
```

- 不定长参数允许处理比声明时更多的参数
```
def functionname([formal_args,] *var_args_tuple ):
   "函数_文档字符串"
   function_suite
   return [expression]
```
- 在声明不定长参数时并不会对其进行命名，需要使用*号来对其进行标识
```
def printinfo( arg1, *vartuple ):
   "打印任何传入的参数"
   print "输出: "
   print arg1
   for var in vartuple:
      print var
   return;
 
# 调用printinfo 函数
printinfo( 10 );
printinfo( 70, 60, 50 );
```

### 匿名函数
- 匿名函数仅使用一次，不占用栈内存，提高运行效率
- python中通过lambda创建匿名参数
```
lambda [arg1 [,arg2,.....argn]]:expression
```
- lambda的主体是表达式而不是代码块，仅在其中封装有限的逻辑，仅占据一行
```
sum = lambda arg1, arg2: arg1 + arg2;

print "相加后的值为 : ", sum( 10, 20 )
print "相加后的值为 : ", sum( 20, 20 )
```

### return语句
- return语句用于表示退出自定义函数的编辑，选择性的向调用方返回一个表达式
```
def sum( arg1, arg2 ):
   # 返回2个参数的和."
   total = arg1 + arg2
   print "函数内 : ", total
   return total;
 
total = sum( 10, 20 );
print "函数外 : ", total 
```
### 变量的作用范围
- 函数的作用范围决定了访问权限，常见的作用域可分为全局变量和局部变量
- 定义在函数外面的变量具有全局的作用域
- 函数内部的值不会带到函数外去
```
total = 0; # 这是一个全局变量
# 可写函数说明
def sum( arg1, arg2 ):
   #返回2个参数的和."
   total = arg1 + arg2; # total在这里是局部变量.
   print "函数内是局部变量 : ", total
   return total;
 
sum( 10, 20 );
print "函数外是全局变量 : ", total 
```
