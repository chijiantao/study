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
2. 迭代

3. 