1. 把函数作为参数传入，这样的函数称为高阶函数，函数式编程就是指这种高度抽象的编程范式。
2. map\(\)函数接收两个参数，一个是函数，一个是Iterable，map将传入的函数依次作用到序列的每个元素，并把结果作为新的Iterator返回，reduce把一个函数作用在一个序列\[x1, x2, x3, ...\]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算
3. map\(\)类似，filter\(\)也接收一个函数和一个序列。和map\(\)不同的是，filter\(\)把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素。

```
def not_empty(s):
 return s and s.strip()
list(filter(not_empty, ['A', '', 'B', None, 'C', '  ']))
结果: ['A', 'B', 'C']
```

```py
from functools import reduce

def str2float(s):
    CHAR_TO_FLOAT = {
    '0': 0,
    '1': 1,
    '2': 2,
    '3': 3,
    '4': 4,
    '5': 5,
    '6': 6,
    '7': 7,
    '8': 8,
    '9': 9,
    '.': -1
    }

    numbers = map(lambda x: CHAR_TO_FLOAT[x] , s)

    point = 0

    def to_float(f , n):
        nonlocal point
        if n == -1:
            point = 1
            return f
        if point == 0:
            return f * 10 + n
        else:
            point = point * 10
            return f + n / point

    return reduce(to_float, numbers)

print('str2float(\'123.456\') =', str2float('123.456'))
if abs(str2float('123.456') - 123.456) < 0.00001:
    print('测试成功!')
else:
    print('测试失败!')
```

4. 排序可以指定key的排序函数
```py
sorted([36, 5, -12, 9, -21], key=abs)
[5, 9, -12, -21, 36]
```

5. 返回函数
```
def count():
    fs = []
    for i in range(1, 4):
        def f():
             return i*i
        fs.append(f)
    return fs

f1, f2, f3 = count()

f1（） f2() f3()都等于9全部都是9！原因就在于返回的函数引用了变量i，但它并非立刻执行。等到3个函数都返回时，它们所引用的变量i已经变成了3，因此最终结果为9。返回闭包时牢记一点：返回函数不要引用任何循环变量，或者后续会发生变化的变量

正确方法

def count():
    def f(j):
        def g():
            return j*j
        return g
    fs = []
    for i in range(1, 4):
        fs.append(f(i)) # f(i)立刻被执行，因此i的当前值被传入f()
    return fs
    
闭包实现函数计数器 
def createCounter():
    L = [0]
    def counter():
       L[0] += 1
       return L[0]  
        
    return counter

```

6. 匿名函数,匿名函数有个限制，就是只能有一个表达式，不用写return，返回值就是该表达式的结果。
```
L = list(filter(lambda n : n % 2 == 1, range(1, 20)))

```


