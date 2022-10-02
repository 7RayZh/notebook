# 初识对象

1. 设计一个类

   ```python
   class Student:
   	name = None
   ```

   

2. 创建一个对象

   ```python
   stu_1 = Student()
   ```



3. 对象属性进行赋值

   ```python
   stu_1.name = '马俊杰'
   stu_1.gender = '男'
   ```



# 类的成员方法

1. 定义语法

   ```python
   class Clock():
       id = None
       price = None
   
       def ring(self):
           import winsound
           winsound.Beep(1000, 1000)
   
   
   clock_1 = Clock()
   clock_1.id = '04204007'
   clock_1.price = 30
   print(f'闹钟id:{clock_1.id},价格{clock_1.price}')
   clock_1.ring()
   ```






# 魔术方法

## 构造方法

1. 创建类对象的时候，==自动执行==

2. 创建类对象的时候，==将传入参数自动传递给**init**方法使用==

   ```python
   class Student:
   
       def __init__(self, name, age, tel):
           self.name = name
           self.age = age
           self.tel = tel
   
   student_1 = Student('周某', 18, 120)
   ```

## 字符串方法

1. 当类对象需要被转换为字符串时，会输出其内存地址，需要用字符串方法，控制类转换为字符串的行为

   ```python
   class Student:
       def __init__(self, name, age):
           self.name = name
           self.age = age
   
       def __str__(self):
           return f'Student类对象,name:{self.name}, age:{self.age}'
   
   student = Student('周某', 15)
   print(student)
   ```

## lt、le、eq方法

1. 使用lt方法，可以对两个对象进行比较==( 用于 < 和 > )==

2. 使用le方法 ==( 用于<= 和 >= )==

3. 使用eq方法 ==( 用于 == 符号，若不使用eq方法，默认比较两个对象的**内存地址** )==

   ```python
   class Student:
       def __init__(self, name, age):
           self.name = name
           self.age = age
   
       def __lt__(self, other):
           return self.age < other.age
   
   student1 = Student('周某', 15)
   student2 = Student('王某', 18)
   print(student1>student2)    # lt方法
   print(student>=student2)	# le方法
   # 结果为False
   ```



# 面向对象

##  封装

### 私有成员变量和私有成员方法

1. 定义：在开头加__

   私有成员无法被类对象使用，但是可以被类中的其他成员使用。

   ```python
   """
   演示面向对象封装思想中私有成员的使用
   """
   
   # 定义一个类，内含私有成员变量和私有成员方法
   class Phone:
       __current_voltage = 0.5 # 当前手机运行电压
   
       def __keep_single_core(self):
           print('让CPU以单核模式运行')
   
       def call_by_5g(self):
           # 可以调用私有成员
           if self.__current_voltage >= 1:
              print('5g通话已开启')
           else:
               self.__keep_single_core()
               print('电量不足，只能用单核模式')
   
   phone = Phone()
   # phone.__keep_single_core()  运行后报错
   phone.call_by_5g()
   ```



## 继承

1. 语法：

   ```python
   class 类名(父类1，父类2，.....父类N):
       类内容体
   ```

   输出同名属性时，按照继承顺序排序( 父类1>父类2 )

2. pass关键字

   语法要求，继承的类已经够，不需要添加新的，使用pass

### 复写

1. 定义：子类继承了父类后，对其不满意可以重写

2. 语法：在子类中用同名重新定义即可

3. 重写后还要调用父类的成员

   ```python
   # 方法1 ：
   	父类名.成员变量
       父类名.成员方法(self)
   # 方法2 ：
   	super().成员变量
       super().成员方法()
   ```

## 类型注解

### 变量的类型注解

1. 语法：	变量：类型

   ```python
   my_list: list[int] = [1, 2, 3]
   my_tuple: tuple[str, int, bool] = ('zhou', 10, True)
   my_set: set[int] = {1, 2, 3}
   my_dict: dict[str, int] = {'zhou': 11}
   ```


### 函数和方法类型注解

1. 形参注解

   ```python
   def 函数方法名(形参名：类型):
   	pass
   
   def add(x: int, y: int):
       return x+y
   
   def func(data: list):
   	pass
   ```

2. 对返回值进行类型注解

   ```python
   def 函数方法名(形参名：类型) -> 类型:
       pass
   def func(data: list) -> list:
       return data
   ```

### Union类型

1. Union[类型，类型]

   ```python
   from typing import Union
   
   my_list: list[Union[str, int]] = [1, 2, 'zhou']
   
   my_dict: dict[str, Union[str, int]] = {'name': 'zhou', 'age': 31}
   
   def func(data: Union[str,int]) -> Union[int,str]:
       pass
   ```

## 多态

1. 定义：同样的行为(函数)，传入不同的对象，得到不同的状态
2. 抽象类：
   - 含义：父类确定有哪些方法，具体的方法实现，由子类自行决定
   - 定义：
     - 含有抽象方法的类叫做抽象类
     - 方法是空实现的（ pass ）称之为抽象方法



# SQL

## SQL基础与DDL

查看数据库 

```sql
SHOW DATABASES;
```

使用数据库 

```sql
USE 数据库名称;
```

创建数据库

```sql
 CREATE DATABASE 数据库名称 [CHARSET UTF8];
```

删除数据库

```sql
DROP DATABASE 数据库名称;
```

查看当前使用的数据库

```sql
SELECT DATABASE();
```

查看有哪些表

```sql
SHOW TABLES;
```

删除表

```sql
DROP TABLE 表名称;
DROP IF EXISTS 表名称;
```

创建表

```sql
CREATE TABLE 表名称(
	列名称 列类型,
    列名称 列类型,
    ... ...
)
```

## SQL - DML

数据插入

```sql
# INSERT INTO 表[(列1,列2,......列N)] VALUES(值1,值2,......,值N)[,(值1,值2,......,值N)......,(值1,值2,......,值N)]

INSERT INTO student(id) VALUES(1),(2),(3);
INSERT INTO student VALUES(4,'周杰伦',31),(5,'林俊杰',33);
```

数据删除

```sql
# DELETE FROM 表名称 [WHERE 条件判断]
DELETE FROM student WHER
```

