# matplotlib

在matplotlib中又两种画图方式：

* plt.figure(): "plt.***"系列。这是通过matplotlib提供的一个api，这个plt提供了很多基本的function可以让你很快的画出图来，但是如果你想要更细致的精调，就要使用另外一种方法。
* fig, ax = plt.subplots(): 这个就是正统的稍微复杂一点的画图方法了。指定figure和axes，然后对axes单独操作。(建议统一使用这种方式操作)

## 名词解析

<img src="C:\Users\nayun\Desktop\project_file\markdown-笔记\matplotlib\微信截图_20230513234128.png" style="zoom:60%;" />

Figure:可以理解为一块画布，画图的第一件事是需要创建一块画布。

Axes:一个图像的对象，对图像中各种元素进行操作。

**个人习惯**

用subplots来创建一个figure和axes对象

```python
fig, ax = plt.subplots(rows, cols, **kwargs)
```

用plot来显示图像

```python
ax.plot()
```

## 线条颜色和风格

plot()函数可以接受额外参数来指定。

线条颜色：color='xxx'			指定颜色名称

>ax.plot(color='blue')

别的写法

```python
plt.plot(x, np.sin(x - 0), color='blue')        # 通过颜色名称指定
plt.plot(x, np.sin(x - 1), color='g')           # 通过颜色简写名称指定(rgbcmyk)
plt.plot(x, np.sin(x - 2), color='0.75')        # 介于0-1之间的灰阶值
plt.plot(x, np.sin(x - 3), color='#FFDD44')     # 16进制的RRGGBB值
plt.plot(x, np.sin(x - 4), color=(1.0,0.2,0.3)) # RGB元组的颜色值，每个值介于0-1
plt.plot(x, np.sin(x - 5), color='chartreuse'); # 能支持所有HTML颜色名称值
```

通过`linestyle`关键字参数可以指定线条的风格

```python
plt.plot(x, x + 0, linestyle='solid')
plt.plot(x, x + 1, linestyle='dashed')
plt.plot(x, x + 2, linestyle='dashdot')
plt.plot(x, x + 3, linestyle='dotted');

# 还可以用形象的符号代表线条风格
plt.plot(x, x + 4, linestyle='-')  # 实线
plt.plot(x, x + 5, linestyle='--') # 虚线
plt.plot(x, x + 6, linestyle='-.') # 长短点虚线
plt.plot(x, x + 7, linestyle=':');  # 点线
```

\* 可以将`color`和`linestyle`两个参数合并在一起简写

```python
plt.plot(x, x + 0, '-g')  # 绿色实线
plt.plot(x, x + 1, '--c') # 天青色虚线
plt.plot(x, x + 2, '-.k') # 黑色长短点虚线
plt.plot(x, x + 3, ':r');  # 红色点线
```

## 坐标轴范围

使用`plt.xlim()`和`plt.ylim()`函数可以调整坐标轴的范围

如果某些情况下你希望将坐标轴反向，可以通过上面的函数实现，将参数顺序颠倒即可:

```python
plt.plot(x, np.sin(x))

plt.xlim(10, 0)
plt.ylim(1.2, -1.2);
```

\* `plt.axis()`函数：一个函数调用完成 x 轴和 y 轴范围的设置，传递一个`[xmin, xmax, ymin, ymax]`的列表参数 & 该函数不仅能设置范围，还能像下面代码一样将坐标轴压缩到刚好足够绘制折线图像的大小。

```python
plt.axis('tight')
plt.axis('equal')
```

## 标签使用

推荐写法

```python
ax.set_xlabel()
ax.set_ylabel()
ax.set_xlim()
ax.set_ylim()
ax.set_title()
```

常见的使用`ax.set()`方法来一次性设置所有的属性：

```python
fig, ax = plt.subplots()
ax.plot(x, np.sin(x))
ax.set(xlim=(0, 10), ylim=(-2, 2),
       xlabel='x', ylabel='sin(x)',
       title='A Simple Plot');
```

`plt.legend()`函数绘制的图例线条与图中的折线无论风格和颜色都保持一致。

## 样式美化(plt.style.use)定制画布风格

```python
print(plt.style.available) # 打印样式列表
['bmh', 'classic', 'dark_background', 'fast', 
'fivethirtyeight', 'ggplot', 'grayscale', 'seaborn-bright', 
'seaborn-colorblind', 'seaborn-dark-palette', 'seaborn-dark', 'seaborn-darkgrid',
 'seaborn-deep', 'seaborn-muted', 'seaborn-notebook', 'seaborn-paper', 
'seaborn-pastel', 'seaborn-poster', 'seaborn-talk', 'seaborn-ticks',
 'seaborn-white', 'seaborn-whitegrid', 'seaborn', 'Solarize_Light2', 
'tableau-colorblind10', '_classic_test']
```

[数据分析最有用的 25 个 Matplotlib 图表 (qq.com)](https://mp.weixin.qq.com/s?__biz=MzA5ODM5MDU3MA==&mid=2650873392&idx=1&sn=427358f10a2087d1583f41b12f3baec6&sharer_sharetime=1683509400057&sharer_shareid=30182868cdd0f39cda7b1af2df2cc87a#rd)

### 散点图

#### 常用符号

```python
rng = np.random.RandomState(0)
fig, ax = plt.subplots()
for marker in ['o', '.', 'x', '+', '^', 'v', '>', '<', 's', 'd']:
    ax.plot(rng.rand(3), rng.rand(3), marker, label="marker='{0}'".format(marker))
ax.legend(numpoints=1)
ax.set_xlim(0, 1.8)
```

![散点图](https://github.com/nayun-hub/markdown-/blob/master/matplotlib/%E6%95%A3%E7%82%B9%E5%9B%BE1.png)
