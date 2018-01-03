# 4 python数据分析

+ [准备数据与numpy](#准备数据与numpy)
+ [python数据分析主力pandas](#python数据分析主力pandas)
+ [数据获取与处理](#数据获取与处理)
+ [数据可视化处理matplotlib](#数据可视化处理matplotlib)
+ [使用NLTK进行Python文本分析](#使用nltk进行python文本分析)
+ [python社交网络分析igraph](#python社交网络分析igraph)
+ [python机器学习scikit-learn](#python机器学习scikit-learn)
+ [数据科学网站案例](#数据科学网站案例)
+ [python分布式计算](#python分布式计算)

## 准备数据与numpy

- 参考书
  - Linear Algebra with Application 线性代数  (图灵)
- 案例:距离求和

```python
import numpy as np
import numpy.linalg as la
import time

X = np.array([range(0, 500), range(500, 1000)])
m, n = X.shape

t = time.time()
D = np.zeros([n, n])
for i in xrange(n):
    for j in xrange(i + 1, n):
        D[i, j] = la.norm(X[:, i] - X[:, j]) ** 2
        D[j, i] = D[i, j]
print time.time() - t

t = time.time()
D = np.zeros([n, n])
for i in xrange(n):
    for j in xrange(i + 1, n):
        d = X[:, i] - X[:, j]
        D[i, j] = np.dot(d, d)
        D[j, i] = D[i, j]
print time.time() - t

t = time.time()
G = np.dot(X.T, X)
D = np.zeros([n, n])
for i in xrange(n):
    for j in xrange(i + 1, n):
        D[i, j] = G[i, i] - G[i, j] * 2 + G[j,j]
        D[j, i] = D[i, j]
print time.time() - t

t = time.time()
G = np.dot(X.T, X)
H = np.tile(np.diag(G), (n, 1))
D = H + H.T - G * 2
print time.time() - t
```

## python数据分析主力pandas

## 数据获取与处理

## 数据可视化处理matplotlib

## 使用NLTK进行Python文本分析

## python社交网络分析igraph

## python机器学习scikit-learn

## 数据科学网站案例

## python分布式计算