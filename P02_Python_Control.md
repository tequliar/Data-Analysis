# P2_Python控制结构

#### 这里是Python数据分析学习的第二篇笔记
本文介绍了Python中条件和循环两大重要的控制结构

---
## 条件语句
- 通过一条或多条语句的执行结果(True或者False)来决定执行的代码块
```
if 判断条件：
    执行语句……
else：
    执行语句……
```
- 需要注意判断条件后面的冒号以及执行语句前的缩进一致
- 使用elif可以实现多次条件判断
```
if 判断条件1:
    执行语句1……
elif 判断条件2:
    执行语句2……
elif 判断条件3:
    执行语句3……
else:
    执行语句4……
```
- python不支持switch语句，对于多条件判断可以使用and、or来连接
```
num = 9
if num >= 0 and num <= 10:    # 判断值是否在0~10之间
    print 'hello'

num = 10
if num < 0 or num > 10:    # 判断值是否在小于0或大于10
    print 'hello'
else:
	print 'undefine'
```
- 可以使用括号来决定条件判断的先后顺序
```
num = 8
# 判断值是否在0~5或者10~15之间
if (num >= 0 and num <= 5) or (num >= 10 and num <= 15):
    print 'hello'
else:
    print 'undefine'
```
- 如果只需要在条件成立时执行语句，可以将if语句写在同一行来简化代码
```
var = 100  
if ( var  == 100 ) : print "变量 var 的值为100" 
```

---
## 循环语句
- 循环语句允许我们执行一个语句或者语句组多次

### 循环类型
#### while 循环
- while 语句用于循环执行程序，即在某条件下，循环执行某段程序，以处理需要重复处理的相同任务
```
count = 0
while (count < 9):
   print 'The count is:', count
   count = count + 1
```
- break 语句用于在语句块执行过程中终止循环，并跳出整个循环
```
i = 1
while 1:            # 循环条件为1必定成立
    print i         # 输出1~10
    i += 1
    if i > 10:     # 当i大于10时跳出循环
        break
```
- continue 语句用于在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环
```
i = 1
while i < 10:   
    i += 1
    if i%2 > 0:     # 非双数时跳过输出
        continue
    print i         # 输出双数2、4、6、8、10
```
- 注意在while循环中必须使循环变量有所变化，否则会使其陷入死循环中
```
var = 1
while var == 1 :  # 该条件永远为true，循环将无限执行下去
   num = raw_input("Enter a number  :")
   print "You entered: ", num

print "Good bye!"
```
- while...else 语句用于在循环体执行完毕时执行else内的语句(通过break跳出循环时else语句不会执行)
```
count = 0
while count < 5:
   print count, " is  less than 5"
   count = count + 1
else:
   print count, " is not less than 5"
```
- 与if语句类似，当while循环体内仅有一条语句时，可以将他们写在一行以精简代码
```
flag = 1
while (flag): print 'Given flag is really true!';flag=0;
print "Good bye!"
```

#### for循环
- for 循环通过对某一数值的控制实现重复执行语句的效果，它可以遍历任何序列的项目，如一个列表或者一个字符串
```
for iterating_var in sequence:
   statements(s)
```
- for 循环可以遍历字符串和列表
```
for letter in 'Python':     # 遍历字符串
   print '当前字母 :', letter

fruits = ['banana', 'apple',  'mango']
for fruit in fruits:        # 遍历列表
   print '当前水果 :', fruit
```
- 可以通过序列的索引进行迭代
```
fruits = ['banana', 'apple',  'mango']
for index in range(len(fruits)):
   print '当前水果 :', fruits[index]
```
- for...else 语句与while...else 语句类似，在循环体结束时调用else语句中的内容，同样如果使用break进行跳出的话不会执行else中的内容
```
for num in range(10,20):  # 迭代 10 到 20 之间的数字
   for i in range(2,num): # 根据因子迭代
      if num%i == 0:      # 确定第一个因子
         j=num/i          # 计算第二个因子
         print '%d 等于 %d * %d' % (num,i,j)
         break            # 跳出当前循环
   else:                  # 循环的 else 部分
      print num, '是一个质数'
```

#### 嵌套循环
- 在while循环内添加while语句或者在for循环内添加for语句
- 嵌套循环允许在while循环体中嵌套for循环
```
i = 2
while(i < 100):
   j = 2
   while(j <= (i/j)):
      if not(i%j): break
      j = j + 1
   if (j > i/j) : print i, " 是素数"
   i = i + 1
```

### 控制语句
#### break 语句
- 在循环结构中打破最小封闭循环的语句，用来终止循环的执行
```
for letter in 'Python': 
   if letter == 'h':
      break
   print 'Current Letter :', letter
  
var = 10 
while var > 0:              
   print 'Current variable value :', var
   var = var -1
   if var == 5:
      break
```

#### continue 语句
- continue 语句用于在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环
```
for letter in 'Python':
   if letter == 'h':
      continue
   print '当前字母 :', letter

var = 10 
while var > 0:              
   var = var -1
   if var == 5:
      continue
   print '当前变量值 :', var
```

#### pass 语句
- pass 语句是空语句，不进行任何操作，只是是为了保持程序结构的完整性或者用于下一步的代码重构
```
# 输出 Python 的每个字母
for letter in 'Python':
   if letter == 'h':
      pass
      print '这是 pass 块'
   print '当前字母 :', letter
```

