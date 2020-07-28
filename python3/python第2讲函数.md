1. 函数参数类型检查
```
 if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
```
2. 定义函数时，需要确定函数名和参数个数；
   如果有必要，可以先对参数的数据类型做检查；
   函数体内部可以用return随时返回函数结果；
   函数执行完毕也没有return语句时，自动return None。
   函数可以同时返回多个值，但其实就是一个tuple。
3. 函数的参数
   1. 位置参数  def power(x) : 
   2. 默认参数  def power(x, n=2) : 一是必选参数在前，默认参数在后，否则Python的解释器会报错,当函数有多个参数时，把变化大的参数放前面，变化小的参数放后面。变化小的参数就可以作为默认参数。
   3. Python函数在定义的时候，默认参数L的值就被计算出来了，即[]，因为默认参数L也是一个变量，它指向对象[]，每次调用该函数，如果改变了L的内容，则下次调用时，默认参数的内容就变了，不再是函数定义时的[]了。定义默认参数要牢记一点：默认参数必须指向不变对象！
   ```
   def add_end(L=[]):
    L.append('END')
    return L
    
   add_end()
   ['END']
   add_end()
   ['END', 'END']
   ```
   
   ```
   def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L
   ```
    4. 可变参数,定义可变参数和定义一个list或tuple参数相比，仅仅在参数前面加了一个*号。在函数内部，参数numbers接收到的是一个tuple，因此，函数代码完全不变。但是，调用该函数时，可以传入任意个参数，包括0个参数.Python允许你在list或tuple前面加一个*号，把list或tuple的元素变成可变参数传进去
    ```
    def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
    ```
    5. 关键字参数
    ```
    def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
    ```
    6. 命名关键字参数，和关键字参数**kw不同，命名关键字参数需要一个特殊分隔符*，*后面的参数被视为命名关键字参数
    ```
    def person(name, age, *, city, job):
    print(name, age, city, job)
    ```
    7. 如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了
    ```
    def person(name, age, *args, city, job):
    print(name, age, args, city, job
    ```
    8. 对于任意函数，都可以通过类似func(*args, **kw)的形式调用它，无论它的参数是如何定义的。