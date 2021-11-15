### Basics

display results

```python
print("The area for the circle of raidus", radius, 'is', area)
print(item1,item2,...,itemk)
# print without the newline
print("AAA", end = '')
# formatting
format(content,'<10.2f') 
# < left-justify左对齐 ^ 居中 > right-justify右对齐(默认)
# string - s, float - f, scientific notation - e, percentage - %, decimal - d
# octal - o, hexadecimal - x, binary - b

```

assign value

```python
radius = 20
i = j = k = 1
# simultaneous assignments
x, y = y, x
# in python, it will swap x with y
```

read from input

```python
variable = input("Enter a value: ")
# the value entered is a string
# convert it to numbers
eval()
eval('003')❌
raidus = eval(input("Enter a value for radius: "))
# if there's a math formula in the braces, it will automatically calculate the result
```

line continuation - use backslash \'\\'

```python
sum = 1 + 2 + 3 + 4 + \
			5 + 6
```

identifier naming rules

1. use letters, digits, and underscores \'_\'
2. must start with a letter or an underscore
3. cannot be a keyword
4. any length is available
5. case sensitive

numeric data types ( int, float )

```python
# can write in scientific notation
variable = 1.2345e+10
variable = 1.23423E-2
```

numeric operators

![image-20201223151130510](/Users/tablee/Library/Application Support/typora-user-images/image-20201223151130510.png)

augmented assignment operators

![image-20201223151634362](/Users/tablee/Library/Application Support/typora-user-images/image-20201223151634362.png)

Type conversions

```python
int(value)
int('003') # =3
int(32.34) # =32 no rounding
# round 四舍五入
round(5.6) # = 6
# 错误用法
int('3.4') ❌

# to string
s = str(3.4)
```

display the current time

```python
import time
currentTime = time.time()
# acquire the total seconds with millisecond precision since 00:00:00 on January 1, 1970 GMT
```

### mathematical functions, strings, objects

```python
import math
```

![image-20201223155703378](/Users/tablee/Library/Application Support/typora-user-images/image-20201223155703378.png)

![image-20201223155744241](/Users/tablee/Library/Application Support/typora-user-images/image-20201223155744241.png)

strings and characters

```python
# ’ or " both will do
letter = 'A'
numChar = '4'
message = 'morning'
# ord and chr functions
ord(ch) # return the ASCII code
chr(98) # return the character

# combining strings
# use plus mark directly
message = 'welcome' + 'to' + 'python'
message += 'hello'
message += message2

# some functions
s.lower() # lowercase all the letter
s.upper() # uppercase all the letter
s.strip() # remove the whitespace from both ends of a string (including ' ', \t, \f, \r, \n)
```

escape sequences

![image-20201223160915704](/Users/tablee/Library/Application Support/typora-user-images/image-20201223160915704.png)

```python
# single quote within double quote can be written directly
print("hello this is my father's house")
# double quote cannot be converted within single quote
print('great \"bonus\" ')❌
```

objects and methods

```python
# each object has a unique integer
id(variable)
# what type of object
type(variable)
```

### selections

Boolean values True/False

![image-20201223195524501](/Users/tablee/Library/Application Support/typora-user-images/image-20201223195524501.png)

