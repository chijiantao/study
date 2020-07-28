1. 切片
   ```
   L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
   L[0:3]表示，从索引0开始取，直到索引3为止，但不包括索引3。即索引0，1，2，正好是3个元素。
   L[-1] 表示最后一个元素
   L[-2:] ['Bob', 'Jack']
   L[:10:2] 前10个，每2个取1个
   
   #!/usr/bin/env python3
   def trim(s):
       while (s and s[:1] == ' '):
           s = s[1:]
       while (s and s[-1:] == ' '):
           s = s[:-1]
       return s
   
   print(len(trim('hello  ')))
   ```
2. 迭代:如果给定一个list或tuple，我们可以通过for循环来遍历这个list或tuple，这种遍历我们称为迭代（Iteration）。默认情况下，dict迭代的是key。如果要迭代value，可以用for value in d.values()，如果要同时迭代key和value，可以用for k, v in d.items()。
```
for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
```

3. isinstance('abc', Iterable) # str是否可迭代 判断类型是否是可迭代的
4. 列表生成式

```
[x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]

[x for x in range(1, 11) if x % 2 == 0]
[x if x % 2 == 0 else -x for x in range(1, 11)]
在一个列表生成式中，for前面的if ... else是表达式，而for后面的if是过滤条件，不能带else。

L1 = ['Hello', 'World', 18, 'Apple', None]
L2 = [s.lower() for s in L1 if isinstance(s, str)]
```

5. 生成器，所以，如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节省大量的空间。在Python中，这种一边循环一边计算的机制，称为生成器：generator。

```
g = (x * x for x in range(10)) 创建一个生成器
for n in g:
    print(n)
  
通过生成器生成杨辉三角  
def tri(n):
    L=[1]
    while True:
        print(len(L))
        yield L
        L = [ L[x] + L[x+1] for x in range(len(L)-1)]
        L.insert(0,1)
        L.append(1)
        if len(L) > n:
            break

a = tri(10)
for i in a:
    print(i)
```

6. 迭代器，这些可以直接作用于for循环的对象统称为可迭代对象：Iterable。可以使用isinstance()判断一个对象是否是Iterable对象



