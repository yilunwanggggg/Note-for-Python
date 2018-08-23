# Notebook for Python



##2018.08.23

####pandas: isin
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


