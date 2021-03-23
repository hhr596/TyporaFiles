1.1

```python
print('Welcome to Python')
print('Welcome to Computer Science')
print('Programming is fun')
```

1.2

```python
print('Welcome to Python')
print('Welcome to Python')
print('Welcome to Python')
print('Welcome to Python')
print('Welcome to Python')
```

1.3

```python
print("FFFFFFF    U     U    NN    NN")
print('FF         U     U    NNN   NN')
print('FFFFFFF    U     U    NN N  NN')
print('FF          U   U     NN  N NN')
print('FF           UUU      NN   NNN')
```

1.4

```python
print('a    a^2   a^3')
print('1    1     1')
print('2    4     8')
print('3    9     27')
print('4    16    64')
```



1.5

```python
print(( 9.5 * 4.5 - 2.5 * 3)/( 45.5 - 3.5 ))
```

1.6

```python
print(1+2+3+4+5+6+7+8+9)
```

1.7

```python
def calculate(max):
    sum = 0
    switch = False  # plus/minus loop
    for i in range(1,max+1,2):
        if switch == False:
            sum += 1/i
            switch = True
        else:
            sum -= 1/i
            switch = False
    sum *= 4
    return sum

print(calculate(11))
print(calculate(15))
```

