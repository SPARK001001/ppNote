pip install -r xxx.text: 安装包批量

参考：https://github.com/Asabeneh/30-Days-Of-Python/blob/master/04_Day_Strings/04_strings.md

1. string:

   1. 转义符

      1. ```
         1. \n: new line  换行
         2. \t: Tab means(8 spaces) 空格
         3. \\: Back slash
         4. \': Single quote (')
         5. \": Double quote (")
         ```

   2. 文本格式化

      1. 方式1（old）.   %s %d %f 

         1. ```python
            formated_string = 'I am %s %s. I teach %s' %(first_name, last_name, language)
            
            formated_string = 'The area of circle with a radius %d is %.2f.' %(radius, area) # 2 refers the 2 significant digits after the point
            
            ```

      2. 方式2(new)： str.format

         1. ```python
            print('{} / {} = {:.2f}'.format(a, b, a / b)) # limits it to two digits after decimal
            formated_string = 'I am {} {}. I teach {}'.format(first_name, last_name, language)
            
            
            ```

      3. 方式3： f-strings(python 3.6+)

         1. ```python
            a = 4
            b = 3
            print(f'{a} + {b} = {a +b}')
            print(f'{a} / {b} = {a / b:.2f}')
            
            ```

   3. string 是字符序列，可以按list的方式使用。根据索引取字符，切片

      1. ```python
         language = 'Python'
         last_letter = language[-1] #n
         first_three = language[0:3] # starts at zero index and up to 3 but not include 3  #  Pyt
         
         ```

   4. 翻转字符串： language[::-1]

   5. 跳跃字符skip characters while slicing:  language[0:6:2]  # Pto

   6. 常用函数

      1. ```python
         capitalize():  首字母大写 
         count(substring, start=..,end=..) 查找substring出现次数
         endwith(substring)   是否以substring结尾
         expandtabs(size): 替换\t空格符为size大小空格
         find(str):  查找str出现的首个位置index,找不到返回-1
         rfind(str):找最后一个出现的位置,找不到返回-1
         format(): 格式化字符串  sentence = 'I am {} {}. I am a {}. I am {} years old. I live in {}.'.format(first_name, last_name, age, job, country)
         index(string):   找到返回最小的index， 找不到返回error
          rindex(string, start=.., end=..)： 找到返回最大的index,找不到返回error
         isalnum(): 判断是否只包含 字母和数字
           isalpha(): 判断是否只包含字母
             isdecimal(): 判断是否只包含数字0-9
           isdigit(): 判断是否之包含数字0-9 和 unicode字符比如\u00B2
             isnumeric(): 在isdigit基础上 包含 更多unicode字符 '\u00BD'  # 1/2
            isidentifier(): 判断是否合法变量名（包含字母数字下划线，以字母或下划线开头）
             islower(): 判断所有字母是否都是小写(数字 空格 不判断)
             isupper() : 判断所有字母是否都是大写
             join(list): 拼接列表中元素
                 			web_tech = ['HTML', 'CSS', 'JavaScript', 'React']   result = '# '.join(web_tech)
         						print(result) # 'HTML# CSS# JavaScript# React'
         	** strip(substring): 去除字符串首尾出现的substring中的字符。challenge = 'thirty days of pythoonnn'     print(challenge.strip('noth')) # 'irty days of py'， 去除出现的 n  o  t  h这4个字符
          split(): 分割字符串，不传参数默认空格
             title(): 单词首字母大写 'thirty days of python'.title()   # Thirty Days Of Python
           swapcase():  所有字符串中的字符小写大写相互转换
            startswith(substring): 判断是否以substring开头。
             
         ```

   7. 

2. List

   1. python中四种集合类型，List  Tuple  Set   Dictionary

      1. List: 有序，可变，允许重复
      2. Tuple： 有序，不可变，允许重复
      3. Set: 无序不可被索引， 不可变，不允许重复
      4. Dictionary:无序，可变，不可重复，可索引

   2. List 的2种创建方式： lst=list()   lst=[]

   3. 一个list中元素可以不同类型  lst = ['Asabeneh', 250, True, {'country':'Finland', 'city':'Helsinki'}] # list containing different data types

   3. 通过下标索引元素，正数从0开始； 负数从-1开始，表示从后开始
   
   3. unpacking list: 拆list
   
      ```python
      first, second, third,*rest, tenth = [1,2,3,4,5,6,7,8,9,10]
      print(first)          # 1
      print(second)         # 2
      print(third)          # 3
      print(rest)           # [4,5,6,7,8,9]
      print(tenth)          # 10
      ```
      
   6. slicing 分片,下标，正负
   
      ```python
      fruits = ['banana', 'orange', 'mango', 'lemon']
      all_fruits = fruits[0:4] # it returns all the fruits
      # this will also give the same result as the one above
      all_fruits = fruits[0:] # if we don't set where to stop it takes all the rest
      orange_and_mango = fruits[1:3] # it does not include the first index
      orange_mango_lemon = fruits[1:]
      orange_and_lemon = fruits[::2] # here we used a 3rd argument, step. It will take every 2cnd item - ['banana', 'mango']
      
      fruits = ['banana', 'orange', 'mango', 'lemon']
      all_fruits = fruits[-4:] # it returns all the fruits
      orange_and_mango = fruits[-3:-1] # it does not include the last index,['orange', 'mango']
      orange_mango_lemon = fruits[-3:] # this will give starting from -3 to the end,['orange', 'mango', 'lemon']
      reverse_fruits = fruits[::-1] # a negative step will take the list in reverse order,['lemon', 'mango', 'orange', 'banana']
      ```
   
      
   
   7. 修改list : 根据索引修改，最后一个索引为 len(list) - 1      # fruits[0] = 'avocado'
   
   8. 判断元素是否在list中：in  操作符      ‘banana’ in fruits
   
   9. 添加元素到末尾：  append()方法
   
   10. 指定索引插入元素： insert(index , item)方法 ,index及之后元素向后移动
   
   11. 删除一个元素，指定元素： remove(item)方法， 删除第一个出现的元素
   
   12. 删除指定索引的元素： pop(index)方法， 不传参数删除最后一个
   
   13. 删除指定索引元素，或索引范围，或删除整个list： del关键字   
   
       ```python
       fruits = ['banana', 'orange', 'mango', 'lemon', 'kiwi', 'lime']
       del fruits[0]
       print(fruits)       # ['orange', 'mango', 'lemon', 'kiwi', 'lime']
       del fruits[1]
       print(fruits)       # ['orange', 'lemon', 'kiwi', 'lime']
       del fruits[1:3]     # this deletes items between given indexes, so it does not delete the item with index 3!
       print(fruits)       # ['orange', 'lime']
       del fruits
       print(fruits)       # This should give: NameError: name 'fruits' is not defined
       ```
   
       
   
   14. 清空集合元素： clear()方法， 返回空集合[]
   
   15. 复制集合： copy()方法   new_lst = lst.copy()
   
   16. 合并集合：
   
       1. plus operator (+):  lst + lst2
   
       2. extend()方法 ： lst.extend(lst2)
   
          
   
   17. 查看元素出现次数： count(item) 方法
   
   18. 查看元素第一次出现索引： index(item) 方法
   
   19. 翻转一个list:   reverse()方法
   
   20. 排序：sort()方法     sorted()内置函数
   
       1. sort() ：改变原list,    升序   sort(reverse=True) 降序
   
       2. sorted(): 返回一个新list，不改变原list.  
   
       3. ```python
          fruits = ['banana', 'orange', 'mango', 'lemon']
          fruits.sort()
          print(fruits)             # sorted in alphabetical order, ['banana', 'lemon', 'mango', 'orange']
          fruits.sort(reverse=True)
          print(fruits) # ['orange', 'mango', 'lemon', 'banana']
          ages = [22, 19, 24, 25, 26, 24, 25, 24]
          ages.sort()
          print(ages) #  [19, 22, 24, 24, 24, 25, 25, 26]
          
          ages.sort(reverse=True)
          print(ages) #  [26, 25, 25, 24, 24, 24, 22, 19]
          
          
          
          fruits = ['banana', 'orange', 'mango', 'lemon']
          print(sorted(fruits))   # ['banana', 'lemon', 'mango', 'orange']
          # Reverse order
          fruits = ['banana', 'orange', 'mango', 'lemon']
          fruits = sorted(fruits,reverse=True)
          print(fruits)     # ['orange', 'mango', 'lemon', 'banana']
          ```
   
          
   
   21. 



3. Tuple: 有序，不可变，可重复
   1. 2种创建方式： empty_tuple=tuple()     empty_tuple=(1,2,3)
   2. 长度 ： len(e_tup)
   3. 访问元素： 通过正负索引  e_tup[1]
   4. 分片： 同list
   5. 把tuple变成list: lst = list(e_tup)
   6. 判断是否存在元素： in 
   7. 拼接tuple : +
   8. 删除： 无法单独删除元素， 但可以删除整个tuple,  del e_tup
   9. 

4. Sets: 无序，不可索引，不可重复

   1. 2种创建方式： st={}   st=set()
   2. 获取长度： len(st)
   3. 访问元素： 没法通过下标索引，得通过循环查找
   4. 判断是否存在： in 
   5. 新增单个元素： add(item) 方法
   6. 新增多个元素  ： update(list)方法，参数是一个list或tuple或set
   7. 移除指定元素： remove(item)，不存在报错，移除前判断是否存在，或使用discard()方法
   8. 随机移除元素： pop()方法，返回移除的元素
   9. 清空元素： clear()方法
   10. 删除set: del st
   11. list 转换成set, 去重   st = set(lst)
   12. 合并set: union()方法，st3 =  st1.union(st2), 不改st1，st2.   st1.update(st2)方法,改变了st1.
   13. 取交集： intersection()方法，  st1.intersection(st2)
   14. 是否子集或父集： issubset() 方法 和 issuperset()方法
   15. 看两set的差集： difference()方法； st1.difference(st2)   返回 st1中有而st2中没有的元素
   16. 看两set中相同元素之外的所有元素，symmetric difference:    symmertric_difference()方法
   17. 判断两set是否有交集： isdisjoint()方法,无返回true。

   

5. Dictionaries:   无序，可变，键值对

   1. 创建方式：dct={}  dct={'key1':'value1', 'key2':['value2',value22]},value可为任意类型
2. 长度  ： len(dct) 内置方法
   3. 访问元素： dct['key1']   dct['key2']【0】  key不存在会报错，先判断。或通过get(key)方法访问元素，不存在返回None
4. 新增元素： dct['key3'] = 'value3'
   5. 修改元素： dct['key3'] = 'new_value'
6. 判断key是否存在： key  in dct  
   7. 删除键值对：  dct.pop(key) 删除指定  dct.popitem():删除最后一个   del dct['key'] 删除指定
8. 转成list: dct.items()    print(dct.items()) # dict_items([('key1', 'value1'), ('key2', 'value2'), ('key3', 'value3'), ('key4', 'value4')])
   8. 删除一个dict: del dct
8. 复制： dct.copy()
   8.  获取key的list:   dct.keys()
8. 获取value的list: dct.values()
   8. 




6. condition

   1. if  elif else
   2. short hand 简写: code **if** condition **else** code
   3. condition **and** condition; condition **or** condition

7. loop循环

   1. 两种方式：while loop  &&    for loop

   2. while 可结合  else   continue  break 使用

   3. **for** i  **in** sequence:    可结合else使用，表示for结束后执行的code

   4. range function:  

      ```python
      lst = list(range(11)) 
      print(lst) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
      st = set(range(1, 11))    # 2 arguments indicate start and end of the sequence, step set to default 1
      print(st) # {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
      
      lst = list(range(0,11,2))
      print(lst) # [0, 2, 4, 6, 8, 10]
      st = set(range(0,11,2))
      print(st) #  {0, 2, 4, 6, 8, 10}
      ```

   5. pass:  表不执行任何操作，占位预留

   6. 

8. functions 函数：

   1. 声明函数的关键字keyword: def
   2. 函数被调用才被执行
   3. 函数的参数类型： number, string , boolean, list, tuple, dictionary, set
   4. 多个参数可以用键值对传参数，那么顺序就可以不按参数顺序来了
   5. 函数没返回值 默认返回None, 返回值类型 string, number, boolean ,list
   6. 函数设置参数默认值：   def function_name(param = value):
   7. 任意多个参数： *arg     def function_name(param ， *arg):
   8. 函数参数 可以是另一个 函数名

9. modules: 模块

   1. 模块： 是一个文件，包含一些方法或代码

   2. 创建模块：创建.py文件  mymodule.py

   3. 引入模块： import mymodule。 文件名

   4. 引入模块中的函数，并重命名：from mymodule import generate_full_name as fullname, sum_two_nums as total, person as p, gravity as g

   5. 引入内置模块： math,datetime,os,sys,random,statistics,colletions,json,re

      1. os

         ```python
         # import the module
         import os
         # Creating a directory
         os.mkdir('directory_name')
         # Changing the current directory
         os.chdir('path')
         # Getting current working directory
         os.getcwd()
         # Removing directory
         os.rmdir()
         ```

         

      2. sys

         ```python
         import sys
         #print(sys.argv[0], argv[1],sys.argv[2])  # this line would print out: filename argument1 argument2
         print('Welcome {}. Enjoy  {} challenge!'.format(sys.argv[1], sys.argv[2]))
         python script.py Asabeneh 30DaysOfPython
         Welcome Asabeneh. Enjoy  30DayOfPython challenge! 
         
         # to exit sys
         sys.exit()
         # To know the largest integer variable it takes
         sys.maxsize
         # To know environment path
         sys.path
         # To know the version of python you are using
         sys.version
         
         ```

         

      3. statistics 统计

         ```python
         from statistics import * # importing all the statistics modules
         ages = [20, 20, 4, 24, 25, 22, 26, 20, 23, 22, 26]
         print(mean(ages))       # ~22.9
         print(median(ages))     # 23
         print(mode(ages))       # 20
         print(stdev(ages))      # ~2.3
         ```

         

      4. math

         ```python
         import math
         print(math.pi)           # 3.141592653589793, pi constant
         print(math.sqrt(2))      # 1.4142135623730951, square root
         print(math.pow(2, 3))    # 8.0, exponential function
         print(math.floor(9.81))  # 9, rounding to the lowest
         print(math.ceil(9.81))   # 10, rounding to the highest
         print(math.log10(100))   # 2, logarithm with 10 as base
         
         from math import *
         ```

         

      5. string 

         ```python
         import string
         print(string.ascii_letters) # abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
         print(string.digits)        # 0123456789
         print(string.punctuation)   # !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
         ```

         

      6. random

         ```python
         from random import random, randint
         print(random())   # it doesn't take any arguments; it returns a value between 0 and 0.9999
         print(randint(5, 20)) # it returns a random integer number between [5, 20] inclusive
         ```

         

10. list comprehension 列表解析：

    1. 语法：[i for i in iterable if expression]

       ```python
       # Generating numbers
       numbers = [i for i in range(11)]  # to generate numbers from 0 to 10
       print(numbers)                    # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
       
       # It is possible to do mathematical operations during iteration
       squares = [i * i for i in range(11)]
       print(squares)                    # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
       
       # It is also possible to make a list of tuples
       numbers = [(i, i * i) for i in range(11)]
       print(numbers)                             # [(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
       
       # Generating even numbers
       even_numbers = [i for i in range(21) if i % 2 == 0]  # to generate even numbers list in range 0 to 21
       print(even_numbers)                    # [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
       
       # Generating odd numbers
       odd_numbers = [i for i in range(21) if i % 2 != 0]  # to generate odd numbers in range 0 to 21
       print(odd_numbers)                      # [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
       # Filter numbers: let's filter out positive even numbers from the list below
       numbers = [-8, -7, -3, -1, 0, 1, 3, 4, 5, 7, 6, 8, 10]
       positive_even_numbers = [i for i in range(21) if i % 2 == 0 and i > 0]
       print(positive_even_numbers)                    # [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
       
       # Flattening a three dimensional array
       list_of_lists = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
       flattened_list = [ number for row in list_of_lists for number in row]
       print(flattened_list)    # [1, 2, 3, 4, 5, 6, 7, 8, 9]
       ```

       

    2. lambda 函数： 类型匿名函数

       ```python
       # syntax
       x = lambda param1, param2, param3: param1 + param2 + param2
       print(x(arg1, arg2, arg3))
       
       # Named function
       def add_two_nums(a, b):
           return a + b
       
       print(add_two_nums(2, 3))     # 5
       # Lets change the above function to a lambda function
       add_two_nums = lambda a, b: a + b
       print(add_two_nums(2,3))    # 5
       
       # Self invoking lambda function
       (lambda a, b: a + b)(2,3) # 5 - need to encapsulate it in print() to see the result in the console
       
       square = lambda x : x ** 2
       print(square(3))    # 9
       cube = lambda x : x ** 3
       print(cube(3))    # 27
       
       # Multiple variables
       multiple_variable = lambda a, b, c: a ** 2 - 3 * b + 4 * c
       print(multiple_variable(5, 5, 3)) # 22
       
       def power(x):
           return lambda n : x ** n
       
       cube = power(2)(3)   # function power now need 2 arguments to run, in separate rounded brackets
       print(cube)          # 8
       two_power_of_five = power(2)(5) 
       print(two_power_of_five)  # 32
       
       ```

       

11. higher order functions 高阶函数：

    1. 函数当作另一个函数的参数

    2. 函数当作一个返回值

       ```python
       def square(x):          # a square function
           return x ** 2
       
       def cube(x):            # a cube function
           return x ** 3
       
       def absolute(x):        # an absolute value function
           if x >= 0:
               return x
           else:
               return -(x)
       
       def higher_order_function(type): # a higher order function returning a function
           if type == 'square':
               return square
           elif type == 'cube':
               return cube
           elif type == 'absolute':
               return absolute
       
       result = higher_order_function('square')
       print(result(3))       # 9
       result = higher_order_function('cube')
       print(result(3))       # 27
       result = higher_order_function('absolute')
       print(result(-3))      # 3
       ```

       

    3. python closures

       ```python
       def add_ten():
           ten = 10
           def add(num):
               return num + ten
           return add
       
       closure_result = add_ten()
       print(closure_result(5))  # 15
       print(closure_result(10))  # 20
       ```

       

    4. python decorators 装饰器

       1. 创建decorators

       ```python
       
       '''These decorator functions are higher order functions
       that take functions as parameters'''
       
       # First Decorator
       def uppercase_decorator(function):
           def wrapper():
               func = function()
               make_uppercase = func.upper()
               return make_uppercase
           return wrapper
       
       # Second decorator
       def split_string_decorator(function):
           def wrapper():
               func = function()
               splitted_string = func.split()
               return splitted_string
       
           return wrapper
       
       @split_string_decorator
       @uppercase_decorator     # order with decorators is important in this case - .upper() function does not work with lists  装饰器执行也是有顺序的
       def greeting():
           return 'Welcome to Python'
       print(greeting())   #['WELCOME', 'TO', 'PYTHON']
       
       带参数的装饰器
       def decorator_with_parameters(function):
           def wrapper_accepting_parameters(para1, para2, para3):
               function(para1, para2, para3)
               print("I live in {}".format(para3))
           return wrapper_accepting_parameters
       
       @decorator_with_parameters
       def print_full_name(first_name, last_name, country):
           print("I am {} {}. I love to teach.".format(
               first_name, last_name, country))
       
       print_full_name("Asabeneh", "Yetayeh",'Finland')
       '''I am Asabeneh Yetayeh. I love to teach.
       I live in Finland'''
       
       ```

       

    5. 内置的高阶函数： map, filter, reduce

       1. map

       ```python
       语法： map(function, iterable)， function可以是lambda表达式
       
       names = ['Asabeneh', 'Lidiya', 'Ermias', 'Abraham']  # iterable
       
       def change_to_upper(name):
           return name.upper()
       
       names_upper_cased = map(change_to_upper, names)
       print(list(names_upper_cased))    # ['ASABENEH', 'LIDIYA', 'ERMIAS', 'ABRAHAM']
       
       # Let us apply it with a lambda function
       names_upper_cased = map(lambda name: name.upper(), names)
       print(list(names_upper_cased))    # ['ASABENEH', 'LIDIYA', 'ERMIAS', 'ABRAHAM']
       ```

       2. filter

          ```python
           # syntax
              filter(function, iterable)
              
              # Lets filter only even nubers
          numbers = [1, 2, 3, 4, 5]  # iterable
          
          def is_even(num):
              if num % 2 == 0:
                  return True
              return False
          
          even_numbers = filter(is_even, numbers)
          print(list(even_numbers))       # [2, 4]
          ```

          

       3. reduce: 先导入模块  from functools import reduce;  返回一个具体的值

          ```python
          numbers_str = ['1', '2', '3', '4', '5']  # iterable
          def add_two_nums(x, y):
              return int(x) + int(y)
          
          total = reduce(add_two_nums, numbers_str)
          print(total)    # 15
          ```

          

12. python error types  错误类型

    1. SyntaxError: 语法错误  print ‘dfd’
    2. NameError: name is not defined
    3. IndexError: list index out of range
    4. ModuleNotFoundError:   no module named 'maths'
    5. AttributeError: module 'math' has no attribute 'PI'
    6. KeyError:   'country', 查一个dict中不存在的key
    7. TypeError:    TypeError: unsupported operand type(s) for +: 'int' and 'str'
    8. ImportError:    ImportError: cannot import name 'power' from 'math'
    9. ValueError:  ValueError: invalid literal for int() with base 10: '12a'
    10. ZeroDivisionError: ZeroDivisionError: division by zero

    

13. python datetime

    1. 获取datetime信息

       ```python
       from datetime import datetime
       now = datetime.now()
       print(now)                      # 2021-07-08 07:34:46.549883
       day = now.day                   # 8
       month = now.month               # 7
       year = now.year                 # 2021
       hour = now.hour                 # 7
       minute = now.minute             # 38
       second = now.second
       timestamp = now.timestamp()
       print(day, month, year, hour, minute)
       print('timestamp', timestamp)
       print(f'{day}/{month}/{year}, {hour}:{minute}')  # 8/7/2021, 7:38
       ```

       

    2. strftime: 格式化Date

       ```python
       from datetime import datetime
       # current date and time
       now = datetime.now()
       t = now.strftime("%H:%M:%S")
       print("time:", t)
       time_one = now.strftime("%m/%d/%Y, %H:%M:%S")
       # mm/dd/YY H:M:S format
       print("time one:", time_one)
       time_two = now.strftime("%d/%m/%Y, %H:%M:%S")
       # dd/mm/YY H:M:S format
       print("time two:", time_two)
       
       time: 15:41:12
       time one: 10/21/2022, 15:41:12
       time two: 21/10/2022, 15:41:12
       ```

       ![strftime](https://github.com/Asabeneh/30-Days-Of-Python/raw/master/images/strftime.png)

    3. 字符串转化成 time

       ```python
       from datetime import datetime
       date_string = "5 December, 2019"
       print("date_string =", date_string)
       date_object = datetime.strptime(date_string, "%d %B, %Y")
       print("date_object =", date_object)
       
       date_string = 5 December, 2019
       date_object = 2019-12-05 00:00:00
       ```

       

    4. using date from datetime

       ```python
       from datetime import date
       d = date(2020, 1, 1)
       print(d)
       print('Current date:', d.today())    # 2019-12-05
       # date object of today's date
       today = date.today()
       print("Current year:", today.year)   # 2019
       print("Current month:", today.month) # 12
       print("Current day:", today.day)     # 5
       ```

       

    5. time objects to represent time

       ```python
       from datetime import time
       # time(hour = 0, minute = 0, second = 0)
       a = time()
       print("a =", a)
       # time(hour, minute and second)
       b = time(10, 30, 50)
       print("b =", b)
       # time(hour, minute and second)
       c = time(hour=10, minute=30, second=50)
       print("c =", c)
       # time(hour, minute, second, microsecond)
       d = time(10, 30, 50, 200555)
       print("d =", d)
       
       a = 00:00:00
       b = 10:30:50
       c = 10:30:50
       d = 10:30:50.200555
       ```

       

    6. 时间差：

       1. Difference Between Two Points in Time Using

       ```python
       today = date(year=2019, month=12, day=5)
       new_year = date(year=2020, month=1, day=1)
       time_left_for_newyear = new_year - today
       # Time left for new year:  27 days, 0:00:00
       print('Time left for new year: ', time_left_for_newyear)
       
       t1 = datetime(year = 2019, month = 12, day = 5, hour = 0, minute = 59, second = 0)
       t2 = datetime(year = 2020, month = 1, day = 1, hour = 0, minute = 0, second = 0)
       diff = t2 - t1
       print('Time left for new year:', diff) # Time left for new year: 26 days, 23: 01: 00
       ```

       2. Difference Between Two Points in Time Using *timedelata*

          ```python
          from datetime import timedelta
          t1 = timedelta(weeks=12, days=10, hours=4, seconds=20)
          t2 = timedelta(days=7, hours=5, minutes=3, seconds=30)
          t3 = t1 - t2
          print("t3 =", t3)
          
          t3 = 86 days, 22:56:50
          
          ```

          

14. exception handling,异常处理

    1.  try   except   else  finally

       ```python
       try:
           code in this block if things go well
       except:
           code in this block run if things go wrong
           
           try:
           name = input('Enter your name:')
           year_born = input('Year you born:')
           age = 2019 - int(year_born)
           print(f'You are {name}. And your age is {age}.')
       except TypeError:
           print('Type error occur')
       except ValueError:
           print('Value error occur')
       except ZeroDivisionError:
           print('zero division error occur')
       else:
           print('I usually run with the try block')
       finally:
           print('I alway run.')
           
       Enter your name:Asabeneh
       Year you born:1920
       You are Asabeneh. And your age is 99.
       I usually run with the try block
       I alway run.
       
       
       ```

       

    2. unpacking, 解压集合

       1. unpacking lists:   加*号

          ```python
          def sum_of_five_nums(a, b, c, d, e):
              return a + b + c + d + e
          
          lst = [1, 2, 3, 4, 5]
          print(sum_of_five_nums(lst)) # TypeError: sum_of_five_nums() missing 4 required positional arguments: 'b', 'c', 'd', and 'e'
          
          print(sum_of_five_nums(*lst))  # 15
          
          numbers = range(2, 7)  # normal call with separate arguments
          print(list(numbers)) # [2, 3, 4, 5, 6]
          args = [2, 7]
          numbers = range(*args)  # call with arguments unpacked from a list
          print(numbers)      # [2, 3, 4, 5,6]
          
          countries = ['Finland', 'Sweden', 'Norway', 'Denmark', 'Iceland']
          fin, sw, nor, *rest = countries
          print(fin, sw, nor, rest)   # Finland Sweden Norway ['Denmark', 'Iceland']
          numbers = [1, 2, 3, 4, 5, 6, 7]
          one, *middle, last = numbers
          print(one, middle, last)      #  1 [2, 3, 4, 5, 6] 7
          ```

       2. unpacking dictionaries: 用**

          ```python
       def unpacking_person_info(name, country, city, age):
              return f'{name} lives in {country}, {city}. He is {age} year old.'
          dct = {'name':'Asabeneh', 'country':'Finland', 'city':'Helsinki', 'age':250}
          print(unpacking_person_info(**dct)) # Asabeneh lives in Finland, Helsinki. He is 250 years old.
          ```
       
          

     3. packing: 压缩

        ```python
        *args  压缩列表list
        **kwarges  压缩字典dictionaries
        def sum_all(*args):
            s = 0
            for i in args:
                s += i
            return s
        print(sum_all(1, 2, 3))             # 6
        print(sum_all(1, 2, 3, 4, 5, 6, 7)) # 28
        
        
        def packing_person_info(**kwargs):
            # check the type of kwargs and it is a dict type
            # print(type(kwargs))
        	# Printing dictionary items
            for key in kwargs:
                print(f"{key} = {kwargs[key]}")
            return kwargs
        
        print(packing_person_info(name="Asabeneh",
              country="Finland", city="Helsinki", age=250))
        
        name = Asabeneh
        country = Finland
        city = Helsinki
        age = 250
        {'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
        ```

        

     4. spreading in python: 扩展

        ```python
        lst_one = [1, 2, 3]
        lst_two = [4, 5, 6, 7]
        lst = [0, *list_one, *list_two]
        print(lst)          # [0, 1, 2, 3, 4, 5, 6, 7]
        country_lst_one = ['Finland', 'Sweden', 'Norway']
        country_lst_two = ['Denmark', 'Iceland']
        nordic_countries = [*country_lst_one, *country_lst_two]
        print(nordic_countries)  # ['Finland', 'Sweden', 'Norway', 'Denmark', 'Iceland']
        ```

        

     5. enumerate: 找索引和 元素的对应关系

        ```python
        for index, item in enumerate([20, 30, 40]):
            print(index, item)
            
           for index, i in enumerate(countries):
            print('hi')
            if i == 'Finland':
                print('The country {i} has been found at index {index}')
        ```

        

     6. zip: 组合 list输出

        ```python
        fruits = ['banana', 'orange', 'mango', 'lemon', 'lime']                    
        vegetables = ['Tomato', 'Potato', 'Cabbage','Onion', 'Carrot']
        fruits_and_veges = []
        for f, v in zip(fruits, vegetables):
            fruits_and_veges.append({'fruit':f, 'veg':v})
        
        print(fruits_and_veges)
        
        [{'fruit': 'banana', 'veg': 'Tomato'}, {'fruit': 'orange', 'veg': 'Potato'}, {'fruit': 'mango', 'veg': 'Cabbage'}, {'fruit': 'lemon', 'veg': 'Onion'}, {'fruit': 'lime', 'veg': 'Carrot'}]
        
        ```

        

15. 正则表达式 Regular expressions


    1. 使用正则，先 import re 模块

       ```python
       5个方法： match()   search()  findall()  split()   sub()
       
       # syntax
       re.match(substring, string, re.I)
       # substring is a pattern, string is the text we look for a pattern , re.I is case ignore flag
       import re
       
       txt = 'I love to teach python and javaScript'
       match = re.match('I like to teach', txt, re.I)
       print(match)  # None
       
       
       import re
       
       txt = '''Python is the most beautiful language that a human being has ever created.
       I recommend python for a first programming language'''
       
       # It returns an object with span and match
       match = re.search('first', txt, re.I)
       print(match)  # <re.Match object; span=(100, 105), match='first'>
       # We can get the starting and ending position of the match as tuple using span
       span = match.span()
       print(span)     # (100, 105)
       # Lets find the start and stop position from the span
       start, end = span
       print(start, end)  # 100 105
       substring = txt[start:end]
       print(substring)       # first
       
       
       txt = '''Python is the most beautiful language that a human being has ever created.
       I recommend python for a first programming language'''
       
       # It return a list
       matches = re.findall('language', txt, re.I)
       print(matches)  # ['language', 'language']
       
       
       txt = '''Python is the most beautiful language that a human being has ever created.
       I recommend python for a first programming language'''
       
       match_replaced = re.sub('Python|python', 'JavaScript', txt, re.I)
       print(match_replaced)  # JavaScript is the most beautiful language that a human being has ever created.
       # OR
       match_replaced = re.sub('[Pp]ython', 'JavaScript', txt, re.I)
       print(match_replaced)  # JavaScript is the most beautiful language that a human being has ever created.
       
       
       
       
       txt = '''I am teacher and  I love teaching.
       There is nothing as rewarding as educating and empowering people.
       I found teaching more interesting than any other jobs.
       Does this motivate you to be a teacher?'''
       print(re.split('\n', txt)) # splitting using \n - end of line symbol
       
       ['I am teacher and  I love teaching.', 'There is nothing as rewarding as educating and empowering people.', 'I found teaching more interesting than any other jobs.', 'Does this motivate you to be a teacher?']
       ```

       

    2. 模式pattern : r''

       ```python
       import re
       
       regex_pattern = r'apple'
       txt = 'Apple and banana are fruits. An old cliche says an apple a day a doctor way has been replaced by a banana a day keeps the doctor far far away. '
       matches = re.findall(regex_pattern, txt)
       print(matches)  # ['apple']
       
       # To make case insensitive adding flag '
       matches = re.findall(regex_pattern, txt, re.I)
       print(matches)  # ['Apple', 'apple']
       # or we can use a set of characters method
       regex_pattern = r'[Aa]pple'  # this mean the first letter could be Apple or apple
       matches = re.findall(regex_pattern, txt)
       print(matches)  # ['Apple', 'apple']
       
       
       
       regex_pattern = r'[Aa]pple' # this square bracket mean either A or a
       regex_pattern = r'[Aa]pple|[Bb]anana' # this square bracket means either A or a
       regex_pattern = r'\d'  # d is a special character which means digits
       regex_pattern = r'\d+'  # d is a special character which means digits, + mean one or more times
       regex_pattern = r'[a].'  # this square bracket means a and . means any character except new line
       txt = '''Apple and banana are fruits'''
       matches = re.findall(regex_pattern, txt)
       print(matches)  # ['an', 'an', 'an', 'a ', 'ar']
       
       regex_pattern = r'[a].+'  # . any character, + any character one or more times 
       matches = re.findall(regex_pattern, txt)
       print(matches)  # ['and banana are fruits']
       
       regex_pattern = r'[a].*'  # . any character, * any character zero or more times 
       txt = '''Apple and banana are fruits'''
       matches = re.findall(regex_pattern, txt)
       print(matches)  # ['and banana are fruits']
       
       更多看参考https://github.com/Asabeneh/30-Days-Of-Python/blob/master/18_Day_Regular_expressions/18_regular_expressions.md
       ```

       

16. 文件处理 file handling


    1. 语法

       ```python
       # Syntax
       f = open('filename', mode) # mode(r, a, w, x, t,b)  could be to read, write, update
       
       "r" - Read - Default value. Opens a file for reading, it returns an error if the file does not exist
       "a" - Append - Opens a file for appending, creates the file if it does not exist
       "w" - Write - Opens a file for writing, creates the file if it does not exist
       "x" - Create - Creates the specified file, returns an error if the file exists
       "t" - Text - Default value. Text mode
       "b" - Binary - Binary mode (e.g. images)
       ```

       

    2. 读取数据 open 


       1. f.read()读取所有数据

       2. f.read(10),读10个字节数据

       3. f.readline(), 读首行数据

       4. f.readlines() : 读所有行 并返回一个list of lines

       5. f.read().splilines()  与readlines()效果相同

       6. with open('filename') as f: 自动关闭 f

          ```python
          with open('./files/reading_file_example.txt') as f:   # 默认读模式
              lines = f.read().splitlines()
              print(type(lines))
              print(lines)
          ```

          

    3. 写模式  a / w

       ```python
       with open('./files/reading_file_example.txt','a') as f:
           f.write('This text has to be appended at the end')
       ```

       

    4. 删除文件

       ```python
       import os
       if os.path.exists('./files/example.txt'):
           os.remove('./files/example.txt')
       else:
           print('The file does not exist')
       ```

       

    5. 把json字符串改成dictionary

       ```python
       import json
       # JSON
       person_json = '''{
           "name": "Asabeneh",
           "country": "Finland",
           "city": "Helsinki",
           "skills": ["JavaScrip", "React", "Python"]
       }'''
       # let's change JSON to dictionary
       person_dct = json.loads(person_json)
       print(type(person_dct))
       print(person_dct)
       print(person_dct['name'])
       ```

       

    6. 把dict 变成json

       ```python
       import json
       # python dictionary
       person = {
           "name": "Asabeneh",
           "country": "Finland",
           "city": "Helsinki",
           "skills": ["JavaScrip", "React", "Python"]
       }
       # let's convert it to  json
       person_json = json.dumps(person, indent=4) # indent could be 2, 4, 8. It beautifies the json
       print(type(person_json))
       print(person_json)
       ```

       

    7. dict保存为json文件

       ```python
       import json
       # python dictionary
       person = {
           "name": "Asabeneh",
           "country": "Finland",
           "city": "Helsinki",
           "skills": ["JavaScrip", "React", "Python"]
       }
       with open('./files/json_example.json', 'w', encoding='utf-8') as f:
           json.dump(person, f, ensure_ascii=False, indent=4)
       ```

       

    8. csv 文件


       1. 读

          ```python
          import csv
          with open('./files/csv_example.csv') as f:
              csv_reader = csv.reader(f, delimiter=',') # w use, reader method to read csv
              line_count = 0
              for row in csv_reader:
                  if line_count == 0:
                      print(f'Column names are :{", ".join(row)}')
                      line_count += 1
                  else:
                      print(
                          f'\t{row[0]} is a teachers. He lives in {row[1]}, {row[2]}.')
                      line_count += 1
              print(f'Number of lines:  {line_count}')
              
              # output:
          Column names are :name, country, city, skills
                  Asabeneh is a teacher. He lives in Finland, Helsinki.
          Number of lines:  2
          ```

          

    9. xlsx 

       ```python
       import xlrd
       excel_book = xlrd.open_workbook('sample.xls)
       print(excel_book.nsheets)
       print(excel_book.sheet_names)
       ```

       

    10. xml

        ```python
        <?xml version="1.0"?>
        <person gender="female">
          <name>Asabeneh</name>
          <country>Finland</country>
          <city>Helsinki</city>
          <skills>
            <skill>JavaScrip</skill>
            <skill>React</skill>
            <skill>Python</skill>
          </skills>
        </person>
        
        import xml.etree.ElementTree as ET
        tree = ET.parse('./files/xml_example.xml')
        root = tree.getroot()
        print('Root tag:', root.tag)
        print('Attribute:', root.attrib)
        for child in root:
            print('field: ', child.tag)
          
          
        Root tag: person
        Attribute: {'gender': 'female'}
        field:  name
        field:  country
        field:  city
        field:  skills
        ```

        

17. pip: python package manager


    1. pip install numpy

    2. pip uninstall numpy

    3. pip list  ： 看安装的包

    4. pip show numpy  看一个包的详情   pip show --verbose numpy 看更详细的数据

    5. pip freeze:  gave us the packages used, installed and their version.  可以查出数据copy到requirements file中

    6. packaging 打包， 每个包 包含一个\__init__ .py文件（这个恩文件存储包的信息）， 表明这个文件夹是一个包，python才会去识别它

       ```python
       ─ mypackage
           ├── __init__.py
           ├── arithmetic.py
           └── greet.py
         
         
         from mypackage import greet
       ```

       

    7. 

18. reading from url


    1. pip install requests

       ```python
       get(): to open a network and fetch data from url - it returns a response object
       status_code: After we fetched data, we can check the status of the operation (success, error, etc)
       headers: To check the header types
       text: to extract the text from the fetched response object
       json: to extract json data Let's read a txt file from this website, https://www.w3.org/TR/PNG/iso_8859-1.txt.
       
       
       import requests # importing the request module
       
       url = 'https://restcountries.eu/rest/v2/all'  # countries api
       response = requests.get(url)  # opening a network and fetching a data
       print(response) # response object
       print(response.status_code)  # status code, success:200
       countries = response.json()
       #We use json() method from response object, if the we are fetching JSON data. For txt, html, xml and other file formats we can use text.
       
       
       print(countries[:1])  # we sliced only the first country, remove the slicing to see all countries
       ```

       

    2. 

19. classies and objects 类和对象


    1. python是面向对象的编程语言。类定义对象的属性和行为。

    2. type(obj)  看一个对象的类型

    3. 创建类

       ```python
       # syntax
       class ClassName:
         code goes here
       ```

       

    4. 创建对象

       ```
       p = Person()
       print(p)
       ```

       

    5. class constructor, 类的构造函数

       ```python
       class Person:
             def __init__ (self, name):
               # self allows to attach parameter to the class
                 self.name =name
       
       p = Person('Asabeneh')
       print(p.name)
       print(p)
       
       
       ```

       

    6. 构造函数默认值

       ```python
       class Person:
             def __init__(self, firstname='Asabeneh', lastname='Yetayeh', age=250, country='Finland', city='Helsinki'):
                 self.firstname = firstname
                 self.lastname = lastname
                 self.age = age
                 self.country = country
                 self.city = city
       
             def person_info(self):
               return f'{self.firstname} {self.lastname} is {self.age} years old. He lives in {self.city}, {self.country}.'
       
       p1 = Person()
       print(p1.person_info())
       p2 = Person('John', 'Doe', 30, 'Nomanland', 'Noman city')
       print(p2.person_info())
       
       # output
       Asabeneh Yetayeh is 250 years old. He lives in Helsinki, Finland.
       John Doe is 30 years old. He lives in Noman city, Nomanland.
       ```

       

    7. 继承；

       ```python
       class Student(Person):
           pass
       #继承了父类的所有
       
       s1 = Student('Eyob', 'Yetayeh', 30, 'Finland', 'Helsinki')
       s2 = Student('Lidiya', 'Teklemariam', 28, 'Finland', 'Espoo')
       print(s1.person_info())
       s1.add_skill('JavaScript')
       s1.add_skill('React')
       s1.add_skill('Python')
       print(s1.skills)
       
       print(s2.person_info())
       s2.add_skill('Organizing')
       s2.add_skill('Marketing')
       s2.add_skill('Digital Marketing')
       print(s2.skills)
       
       
       output
       Eyob Yetayeh is 30 years old. He lives in Helsinki, Finland.
       ['JavaScript', 'React', 'Python']
       Lidiya Teklemariam is 28 years old. He lives in Espoo, Finland.
       ['Organizing', 'Marketing', 'Digital Marketing']
       ```

       

    8. 继承，重写

       ```python
       class Student(Person):
           def __init__ (self, firstname='Asabeneh', lastname='Yetayeh',age=250, country='Finland', city='Helsinki', gender='male'):
               self.gender = gender
               super().__init__(firstname, lastname,age, country, city)
           def person_info(self):
               gender = 'He' if self.gender =='male' else 'She'
               return f'{self.firstname} {self.lastname} is {self.age} years old. {gender} lives in {self.city}, {self.country}.'
       
       s1 = Student('Eyob', 'Yetayeh', 30, 'Finland', 'Helsinki','male')
       s2 = Student('Lidiya', 'Teklemariam', 28, 'Finland', 'Espoo', 'female')
       print(s1.person_info())
       s1.add_skill('JavaScript')
       s1.add_skill('React')
       s1.add_skill('Python')
       print(s1.skills)
       
       print(s2.person_info())
       s2.add_skill('Organizing')
       s2.add_skill('Marketing')
       s2.add_skill('Digital Marketing')
       print(s2.skills)
       
       Eyob Yetayeh is 30 years old. He lives in Helsinki, Finland.
       ['JavaScript', 'React', 'Python']
       Lidiya Teklemariam is 28 years old. She lives in Espoo, Finland.
       ['Organizing', 'Marketing', 'Digital Marketing']
       ```

       

    9. 

20. python web scraping爬虫:    requests  beautifulsoup4

21. statistic analysis: numpy , 矩阵计算分析

22. pandas: data structures and data analysis tools , 格式化数据

23. python for web


    1. flask
    2. django
    3. 

24. Restful api







