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