# numpy

核心：**n维array**

## numpy和list的异同点

相同点：**同样都是容器，都能快速的取值的修改值，但是插入和删除会慢一点**。

numpy的优点：

  * 跟紧凑，特别是在多维数据中
		* 数据向量化时比list更快
		* 通常是同质化的，数据相同时处理更快

## 向量

### 向量初始化

通过list转化，自动变成np

```python
a = np.array([1, 2, 3, 4., 's'])
```

所有创建包含固定值*vector*的方法都有***_like***函数

|   原函数   |      _like      |
| :--------: | :-------------: |
| np.zeros() | np.zeros_like() |
| np.ones()  | np.ones_like()  |
| np.empty() | np.empty_like() |
| np.full()  | np.full_like()  |

`arange`和`linspace`方法

```python
np.arange(start, stop, step)
np.linspace(start, stop, num)
```

### 生成随机array

```python
np.random.randint(start, stop, num)
# uniform \in [start, stop)

np.random.rand(num)
# uniform \in [0, 1)

np.random.uniform(start, stop, num)
# uniform \in [start, stop)

np.random.randn(num)
# normal, \mu = 0, \sigma = 1

np.random.normal(mu, sigma, num)
```

### 向量索引

> a = np.array([1, 2, 3, 4, 5, 6])
>
> a[1]  ----------> 2
>
> a[2:4] -------------> [3, 4]
>
> a[-2:] -------------> [5, 6]
>
> a[: : 2] -----------> [1, 3, 5]
>
> a[[1, 3, 4]] -----------> [2, 4, 5]

布尔操作

`np.any()`和`np.all()`

`.where()`方法

```python
a = np.array([1, 2, 3, 4, 5, 6, 3, 2])
print(np.where(a>4))
# (array([4, 5], dtype=int64),)
```

`.clip()方法`

> 用于截取数组中小于或者大于某值的部分，并使得被截取部分等于固定值。函数的参数有 a, a_min, a_max, out=None，其中 a 是输入矩阵，a_min 是被限定的最小值，a_max 是被限定的最大值，out 是可选的输出矩阵。

### 向量操作

numpy的优势就是把vector当做数做整体运算，避免循环运算。

数学运算

|                      ----                      |     ---     |
| :--------------------------------------------: | :---------: |
|                   $\sqrt{a}$                   |  np.sqrt()  |
|                     $e^a$                      |  np.exp()   |
|                     $lna$                      |  np.log()   |
| $\overrightarrow{a} \cdot \overrightarrow{b} $ |  np.dot()   |
| $\overrightarrow{a} \times \overrightarrow{b}$ | np.cross()  |
|                    三角函数                    |             |
|                    np.sin()                    | np.arcsin() |

整体取整

>np.floor()						# 向下取整
>
>np.ceil()							# 向上取整
>
>np.round()						# 四舍五入

排序操作

```python
a = np.random.randint(1, 10, 6)
print(a)
print(np.sort(a))
# [6 2 6 6 7 3]
# [2 3 6 6 6 7]
```

### 查找操作

有3中方法

1. where，难懂且对于x处于array末端很不友好
2. next，相对较快，但需要[numba](https://link.zhihu.com/?target=https%3A//numba.pydata.org/)
3. searchsorted，针对于已排过序的array

```python
a = np.random.randint(1, 20, 15)
print(a)

if np.any(a=3):
    print(np.where(a==3))
# [ 3 19 17  3 10 10 12  8  5  3  5 11 18  7 13]
# (array([0, 3, 9], dtype=int64),)
```

## matrix矩阵

初始化与算术运算与上述相似。

改变形状：a.reshape()

三种向量，一维array，二维列vector，二维行向量

维度转换

```python
a = np.random.randint(1, 20, 15)
print(a)
print(a[None, :])
print(a[np.newaxis, :])
print(a.reshape(1, -1))

# [15 14 13 13  9  1 17  5 10 14  5  9  5 11 13]
# [[15 14 13 13  9  1 17  5 10 14  5  9  5 11 13]]
# [[15 14 13 13  9  1 17  5 10 14  5  9  5 11 13]]
# [[15 14 13 13  9  1 17  5 10 14  5  9  5 11 13]]
```

```python
a = np.random.randint(1, 20, 15)
print(a)
print(a[None, :].flatten())
print(a[np.newaxis, :].reshape(-1))
# [18  6 16 17 15 19 12  3  5  2 18  1 12 17 10]
# [18  6 16 17 15 19 12  3  5  2 18  1 12 17 10]
# [18  6 16 17 15 19 12  3  5  2 18  1 12 17 10]
```

### 矩阵操作

合并matrix，hstack横向，vstack纵向，也可以理解为堆叠

`np.hstack()` 和`np.vstack()`

反向操作`hsplit`和`vsplit`

```python
a = np.linspace(1, 12, 12, dtype=np.int).reshape(3, 4)
#[[ 1  2  3  4]
# [ 5  6  7  8]
# [ 9 10 11 12]]
b = np.linspace(1, 6, 6, dtype=np.int).reshape(3, 2)
#[[1 2]
# [3 4]
# [5 6]]
print(np.hstack((a, b)))
#[[ 1  2  3  4  1  2]
# [ 5  6  7  8  3  4]
# [ 9 10 11 12  5  6]]
c = np.linspace(1, 8, 8, dtype=np.int).reshape(2, 4)
#[[1 2 3 4]
# [5 6 7 8]]
print(np.vstack((a, c)))
#[[ 1  2  3  4]
# [ 5  6  7  8]
# [ 9 10 11 12]
# [ 1  2  3  4]
# [ 5  6  7  8]]
```

### 复制操作

整体复制

```python
a = np.random.randint(1, 7, size=(2, 2))
print(a)
print(np.tile(a, (2, 2)))
a=
[[4 2]
 [3 5]]
复制后
[[4 2 4 2]
 [3 5 3 5]
 [4 2 4 2]
 [3 5 3 5]]
```

单个复制

```python
a = np.random.randint(1, 7, size=(2, 2))
print(a)
print(a.repeat(3, axis=1))
print(a.repeat(3, axis=0))
输出1
[[6 4]
 [3 5]]
输出2
[[6 6 6 4 4 4]
 [3 3 3 5 5 5]]
输出3
[[6 4]
 [6 4]
 [6 4]
 [3 5]
 [3 5]
 [3 5]]
```

### 删除操作`.delete()`

```python
a = np.random.randint(1, 10, size=(3, 3))
print(a)
print(np.delete(a, 1, axis=0))
输出1
[[4 8 7]
 [7 3 6]
 [9 2 4]]
输出2
[[4 8 7]
 [9 2 4]]
```

插入`.insert()`,与`.delete()`类似

### 增加固定值`.pad()`

参数：

>第一个参数是待填充数组
>第二个参数是填充的形状，（2，3）表示前面两个，后面三个
>第三个参数是填充的方法

填充方法：

>constant连续一样的值填充，有关于其填充值的参数。constant_values=（x, y）时前面用x填充，后面用y填充。缺参数是为0000。。。
>edge用边缘值填充
>linear_ramp边缘递减的填充方式
>maximum, mean, median, minimum分别用最大值、均值、中位数和最小值填充
>reflect, symmetric都是对称填充。前一个是关于边缘对称，后一个是关于边缘外的空气对称
>wrap用原数组后面的值填充前面，前面的值填充后面
>也可以有其他自定义的填充方法

### matrix统计

| 函数        | 作用   |
| ----------- | ------ |
| `.min()`    | 最小值 |
| `.sum()`    | 求和   |
| `.max()`    | 最大值 |
| `.mean()`   | 均值   |
| `.median()` | 中位数 |

返回下标

>`.argmin()` & `.argmax()`

## 3维array

初始化

```python
a = np.random.randint(1, 20, size=(3, 5, 3))
输出
[[[16  7 13]
  [13 15 18]
  [ 9  5 17]
  [ 7 16 19]
  [18  3  2]]

 [[15 17 18]
  [19  5  4]
  [ 1  7  8]
  [ 1 18 18]
  [14  7 12]]

 [[17 18 11]
  [ 5  4  4]
  [10  5  1]
  [13 13  5]
  [ 6 18  7]]]
```

\* 跟1D和2D类似，zeros, ones, rand 等很多方法同样使用

维度堆叠另一种方法`.concatenate((a, b), axis=None)`