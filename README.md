## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/helloliangxw/Python/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/helloliangxw/Python/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.



---
title: Python-基础-函数与递归
date: 2017-04-19 17:33:00
mathjax: true
categories: "Python-基础"

---

# 函数

## 函数定义


```python
def func(arg1, arg2):
    # 返回元组
    return arg1, arg2

t = func(1, 2)
print(t)
print(type(t))
```

    (1, 2)
    <class 'tuple'>
    

## 默认参数


```python
def func(arg1, arg2 = 200):
    return arg1, arg2

print(func(1))
print(func(1, 2))

# 调用时可以改变参数顺序
print(func(10, arg2 = 2))
print(func(arg2 = 2, arg1 = 1))

# 下面这种调用方式会出错
# func(arg2 = 2, 10)
```

    (1, 200)
    (1, 2)
    (10, 2)
    (1, 2)
    

## 变长参数

变长参数必须放在参数列表的最后。  
一共有两种形式。  
第一种将变长参数包装成tuple：


```python

def func(name, *args):
    # 变长参数自动包装成tuple
    print(type(args))
    print(args)
    print(args[0])

func('Tom', 1, 2 ,'abc')
```

    <class 'tuple'>
    (1, 2, 'abc')
    1
    

第二种将变长参数包装成dict：


```python
def func(name, **args):
    # 变长参数自动包装成dict
    print(type(args))
    print(args)
    print(args['China'])
    
func('Tom', China='Beijing', UK='London')
```

    <class 'dict'>
    {'China': 'Beijing', 'UK': 'London'}
    Beijing
    


```python
def func(a, b, c = 0, *args0, **args1):
    print(a, b, c)
    print(args0)
    print(args1)

func(1, 2)
print("--------------------------------------")
func(1, 2, 3)
print("--------------------------------------")
func(1, 2, 3, 'a', 'b', 'c')
print("--------------------------------------")
func(1, 2, 3, 'a', 'b',  China='Beijing', UK='London')
print("--------------------------------------")
func(1, 2, 3, *('a', 'b'),  **{'China':'Beijing', 'UK':'London'})
```

    1 2 0
    ()
    {}
    --------------------------------------
    1 2 3
    ()
    {}
    --------------------------------------
    1 2 3
    ('a', 'b', 'c')
    {}
    --------------------------------------
    1 2 3
    ('a', 'b')
    {'China': 'Beijing', 'UK': 'London'}
    --------------------------------------
    1 2 3
    ('a', 'b')
    {'China': 'Beijing', 'UK': 'London'}
    

## 函数作为变量

Python中一切皆对象，因此函数也可以最为变量：


```python
def func(args):
    print(args*2)

f = func
f('a')
```

    aa
    


```python
# 根据比较方法参数cmpMethod，对列表进行排序
def theSort(dataList, cmpMethod = None):
    if not cmpMethod:
        return dataList
    else:
        return cmpMethod(dataList)

    
# 从小到大排序（冒泡排序）
def bubbleSortAscent(dataList):
    length = len(dataList)
    for i in range(0, length):
        for j in range(i + 1, length):
            if dataList[j] < dataList[i]:
                temp = dataList[i]
                dataList[i] = dataList[j]
                dataList[j] = temp
    return dataList

# 从大到小排序（冒泡排序）
def bubbleSortDescent(dataList):
    length = len(dataList)
    for i in range(0, length):
        for j in range(i + 1, length):
            if dataList[j] > dataList[i]:
                temp = dataList[i]
                dataList[i] = dataList[j]
                dataList[j] = temp
    return dataList

print(theSort([1, 3, 2, 5, 0]))
print(theSort([1, 3, 2, 5, 0], bubbleSortAscent))
print(theSort([1, 3, 2, 5, 0], bubbleSortDescent))
```

    [1, 3, 2, 5, 0]
    [0, 1, 2, 3, 5]
    [5, 3, 2, 1, 0]
    


```python
def Do(datas, method):
    return method(datas)

print(Do([1, 2, 3], sum))
print(Do([1, '2', 3], set))
```

    6
    {1, 3, '2'}
    

## 命名关键字参数


```python
def func(a, b, c, *, China, UK):
    print(China, UK)

func(1, 2, 3, China = 'Beijing', UK = 'London')
```

    Beijing London
    

# 递归

函数定义中使用函数自身的方法。  
经典例子：阶乘。

\\(\pi\\)

$\left\{\begin{matrix} 1  \\ n(n-1)! \end{matrix}\right.$

$$\left\{\begin{matrix}
1  \\
n(n-1)! 
\end{matrix}\right.$$
 
$$\left\{\begin{matrix}
1  \\\\ 
n(n-1)! 
\end{matrix}\right.$$
 
$$n!=n(n-1)(n-2)...1=\left\{\begin{matrix}
1 && n=0 \\\\ 
n(n-1)! && otherwrise
\end{matrix}\right.$$

其中\\(n=0\\)称为该递归的**基例**。


递归特征：
1. 递归不是循环
2. （一个或多个）基例不需要递归，否则递归就会无限循环
3. 所有的递归链都要以一个基例结尾

PS：Python默认“递归深度的最大值”为900，达到900次调用时，程序就会终止。

## 阶乘


```python
def fact(n):
    if n==0:
        return 1
    else:
        return fact(n-1) * n

fact(3)
```




    6



## 求和


```python
def MySum(i):
    if i < 0:
        raise ValueError
    elif i <= 1:
        return i
    else:
        return i + MySum(i-1)

print(MySum(3))
```

    6
    

## 字符串反转


```python
def strReverse(string):
    if string == "":
        return string
    else:
        return strReverse(string[1:])+string[0]
strReverse("123456789")
```




    '987654321'



## 斐波那契数列


```python

def fib(n):
    if n < 1:
        raise ValueError
    elif n <= 2:
        return 1
    else:
        return fib(n-1) + fib(n-2)

print fib(1), fib(2), fib(3), fib(4), fib(5), fib(6), fib(7)
```

## 汉诺塔问题


```python

def hnt(n, source, target, helper):
    if n == 1:
        print source + '=>' + target
    else:
        hnt(n-1, source, helper, target)
        print source + '=>' + target
        hnt(n-1, helper, target, source)

hnt(3, 'A', 'B', 'C')
```
