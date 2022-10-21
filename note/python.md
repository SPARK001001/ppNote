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
             isnumeric(): 在isdigit基础上 包含 更多字符串 '\u00BD'  # 1/2
            isidentifier(): 判断是否合法变量名（包含字母数字下划线，以字母或下划线开头）
             islower(): 判断所有字母是否都是小写(数字 空格 不判断)
             isupper() : 判断所有字母是否都是大写
             join(list): 拼接列表中元素
                 			web_tech = ['HTML', 'CSS', 'JavaScript', 'React']   result = '# '.join(web_tech)
         						print(result) # 'HTML# CSS# JavaScript# React'
         	** strip(substring): 去除字符串首尾出现的substring中的字符。challenge = 'thirty days of pythoonnn'     print(challenge.strip('noth')) # 'irty days of py'
          split(): 分割字符串，不传参数默认空格
             title(): 单词首字母大写 'thirty days of python'.title()   # Thirty Days Of Python
           swapcase():  所有字符串中的字符小写大写相互转换
            startswith(substring): 判断是否以substring开头。
             
         ```

      2. 

   7. 

   8. 

      1. ```
         
         ```

      2. 
