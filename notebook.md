# Notebook for Python



## 2018.08.23

#### pandas: isin
```
path = 'ex2data1.txt'
data = pd.read_csv(path, header=None, names=['Exam 1', 'Exam 2', 'Admitted'])
data.head()
positive = data[data['Admitted'].isin([1])]
negative = data[data['Admitted'].isin([0])]
```
这里`isin`指的就是is in，返回的事一个真值表，这里的positive和negative按照真值表取数据。


#### pandas: insert
```
a=pd.Series([1,2,2,3,3,2])
data.insert(0, 'aaa', a)
```

insert 在第0列插入a序列，并且head为aaa

#### pandas: 筛选！
[筛选请看](https://blog.csdn.net/liuweiyuxiang/article/details/78241530)

#### numpy: avoid matrix
numpy现在已经不再更新matrix这个package，所以要避免使用这个package，进行矩阵运算以及其他线性代数计算的时候，应当直接使用array及其运算函数，之前matrix下可以用`＊` 来进行矩阵乘法，现在替换成了`np.dot`。


#### scipy: optimize
optimize是scipy中的一个package
> The scipy.optimize package provides several commonly used optimization algorithms. A detailed listing is available: scipy.optimize (can also be found by help(scipy.optimize)).

比如今天用到的fmin_tnc:
>Minimize a function with variables subject to bounds, using gradient information in a truncated Newton algorithm. 

这里是这样使用的：
```
import scipy.optimize as opt
result = opt.fmin_tnc(func=cost, x0=theta, fprime=gradient, args=(X, y))
```
大概看明白了,这里fmin_tnc函数寻找的是func＝cost的最优解，x0就是初始值，fprime指的是利用什么函数去求解最优解什么的，比如这里它就是gradient，然后args是fprime后面所需要的参数，fprime这里在运算的时候，写的应该就是：fprime(x,X,y),其中x是从x0开始的自变量，X和y是计算需要的参数。

#### python: zip
可以将两个数组合并，并且是一一对应组合：
>In [1]: a = b = c = range(20)

>In [2]: zip(a, b, c)

>Out[2]: 
[(0, 0, 0),
 (1, 1, 1),
 ...
 (17, 17, 17),
 (18, 18, 18),
 (19, 19, 19)]

这种一行的代码，虽然很难写，但看上去蛮酷的😂：
```
correct = [1 if ((a == 1 and b == 1) or (a == 0 and b == 0)) else 0 for (a, b) in zip(predictions, y)]
```



