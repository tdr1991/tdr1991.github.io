---
layout: post
title: python小技巧
date: 2018-06-22
categories: 
- python
tags: 
- python
---
python小技巧
<!--more-->

```python
import numpy as np
import pandas as pd
```

# 只要一行代码生成列表生成器


```python
x = [1, 2, 3, 4]
out = [item**2 for item in x]
print(out)
```

    [1, 4, 9, 16]
    

# lambda表达式
![](/assets/images/python/lambda.jpg)
要记住，Lambda 表达式创造的函数和普通的 def 构建的函数没什么不同，只不过函数体只有单独一个表达式而已。


```python
double = lambda x: x * 2
print(double(5))
```

    10
    

# map 和 filter 函数
 map() 函数接收一个列表，和一个函数，它对列表里的每个元素调用一个函数进行处理，再将结果放进一个新列表里。而 filter() 函数略有不同，它接收一个列表，和一个规则函数，在对列表里的每个元素调用这个规则函数之后，它把所有返回值为假的元素从列表中剔除，然后返回这个过滤后的子列表。


```python
# Map
seq = [1, 2, 3, 4, 5]
results = list(map(lambda var: var * 2, seq))
print(results)
```

    [2, 4, 6, 8, 10]
    


```python
# Filter
seq = [1, 2, 3, 4, 5]
results = list(filter(lambda var: var > 2, seq))
print(results)
```

    [3, 4, 5]
    

# arange 和 linspace 函数
arange() 函数按照指定的步长返回一个等差数列。linspace() 返回的是将给定区间进行若干等分以后的等分点组成的数列。


```python
# np.arange
arr = np.arange(3, 7, 2)
print(arr)
```

    [3 5]
    


```python
# np.linspace
arr = np.linspace(2.0, 3.0, num=5)
print(arr)
```

    [ 2.    2.25  2.5   2.75  3.  ]
    

# pandas 中坐标轴（axis 参数）的意义
处理行，axis设为1，处理列，axis设为0

# 用 contact、merge 和 join 来合并数据表
concat() 可以把一个或多个数据表按行（或列）的方向简单堆叠起来（看你传入的 axis 参数是 0 还是 1 咯）。  
merge() 将会以用户指定的某个名字相同的列为主键进行对齐，把两个或多个数据表融合到一起。  
join()和 merge() 很相似，只不过 join() 是按数据表的索引进行对齐，而不是按某一个相同的列。当某个表缺少某个索引的时候，对应的值为空（NaN）。

# apply 函数
apply() 函数作用是，将一个函数应用到某个数据表中你指定的一行或一列中的每一个元素上。



```python
df = pd.DataFrame([[4, 9],] * 3, columns=["A", "B"])
print(df)
# 应用平方根函数 np.sqrt（df）
sq = df.apply(np.sqrt)
print(sq)
# 对列求和
sc = df.apply(np.sum, axis=0)
print(sc)
# 对行求和
sr = df.apply(np.sum, axis=1)
print(sr)
```

       A  B
    0  4  9
    1  4  9
    2  4  9
         A    B
    0  2.0  3.0
    1  2.0  3.0
    2  2.0  3.0
    A    12
    B    27
    dtype: int64
    0    13
    1    13
    2    13
    dtype: int64
    


```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
sr = np.sum(arr, axis=0)
print(sr)
sc = np.sum(arr, axis=1)
print(sc)
```

    [5 7 9]
    [ 6 15]
    

# 数据透视表
