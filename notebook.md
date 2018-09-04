# Notebook for Python and Code

本笔记的组织形式：
每天的笔记会记在最前面，方便查阅。每一条相关的软件或者package会写在小标题里。

这个笔记其实用处并不算很大，只是想提醒自己：切莫自己造轮子。

## 2018.08.28

#### scikit-learn：SVM

这个包用来做SVM很棒，除此以外，还可以利用sklearn的metrics包中的
classification_report函数，得到诸如precision，recall等参数。




## 2018.08.27




#### python: map
map() 会根据提供的函数对指定序列做映射。
第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

Python 2.x 返回列表。
Python 3.x 返回迭代器。

examples:map(function, iterable, ...)
```
d = sio.loadmat('ex5data1.mat')
return map(np.ravel, [d['X'], d['y'], d['Xval'], d['yval'], d['Xtest'], d['ytest']])
```


## 2018.08.24

#### 能不循环就不循环！！！


#### numpy:argmax
Returns the indices of the maximum values along an axis.

同理，argmin就是返回最小值的indices。。。注意，是所有最小值的序号的第一个。

#### 关于矢量化运算的debug

>**Debugging Tip:** Vectorizing code can sometimes be tricky. One com- mon strategy for debugging is to print out the sizes of the matrices you are working with using **the size function**. For example, given a data ma- trix X of size 100 × 20 (100 examples, 20 features) and θ, a vector with dimensions 20×1, you can observe that Xθ is a valid multiplication oper- ation, while θX is not. Furthermore, if you have a non-vectorized version of your code, you can compare the output of your vectorized code and non-vectorized code to make sure that they produce the same outputs.

#### 整个练习2最后告诉我一件事😂，那就是sklearn这个包可以用一行命令来解决！！！

```
from sklearn import linear_model#调用sklearn的线性回归包
model = linear_model.LogisticRegression(penalty='l2', C=1.0)
model.fit(X2, y2.ravel())
```

结果如下

LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
          intercept_scaling=1, max_iter=100, multi_class='ovr', n_jobs=1,
          penalty='l2', random_state=None, solver='liblinear', tol=0.0001,
          verbose=0, warm_start=False)


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

#### 这种一行的代码，虽然很难写，但看上去蛮酷的😂：
```
correct = [1 if ((a == 1 and b == 1) or (a == 0 and b == 0)) else 0 for (a, b) in zip(predictions, y)]
```



