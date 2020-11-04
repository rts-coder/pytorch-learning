---
typora-copy-images-to: 笔记保存图片
---

# IPython  学习

## IPython介绍

`ipython`是一个`python`的交互式`shell`，比默认的`python shell`好用得多，支持变量自动补全，自动缩进，支持`bash shell`命令，内置了许多很有用的功能和函数。学习`ipython`将会让我们以一种更高的效率来使用`python`。同时它也是利用Python进行科学计算和交互可视化的一个最佳的平台。

## 安装

安装ipython很简单，可以直接使用pip管理工具即可:

```
pip install ipython
```

这条命令会自动安装IPython以及它的各种依赖包

如果我们也想在notebook中或者在Qt console中使用IPython，我们还需要安装Jupyter，如下命令：

```
pip install jupyter
```

## 运行

在cmd中输入ipython即可启动IPython

![image-20201021111147425](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021111147425.png)

![image-20201021111231674](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021111231674.png)

或者输入`ipython qtconsole`进入ipython图形交互界面：

![image-20201021111800345](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021111800345.png)

输入exit命令或者"Ctrl+D"  快捷键可推出IPython。

## Tab键自动补全

在shell中输入表达式时，只要按下Tab键，当前命名空间中任何与输入的字符串相匹配的变量(对象或者函数等)就会被找出来：

![image-20201021112018650](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021112018650.png)

## 内省

在一个变量的前面或者后面加上一个问好？，就可以将该对象的一些通用信息显示出来。

![image-20201021112126315](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021112126315.png)

如果对象是一个函数或者实例方法，则它的docstring也会被显示出来

```python
#定义一个函数
In [3]: def add(a,b):
   ...:
   ...:
   ...:     """
   ...:     Add Two  numbers
   ...:     """
   ...:     return a+b
   ...:

#使用一个问号，可以查看该方法的内省信息：        
In [4]: add?
Signature: add(a, b)
Docstring: Add Two  numbers
File:      c:\users\administrator\<ipython-input-3-dca3c5508364>
Type:      function

   
#使用两个问号，就可以显示出该方法的源码
In [5]: add??
Signature: add(a, b)
Source:
def add(a,b):


    """
    Add Two  numbers
    """
    return a+b
File:      c:\users\administrator\<ipython-input-3-dca3c5508364>
Type:      function
```

另外，我们可以使用通配符字符串查找出所有与该通配符字符串相匹配的名称，比如我们查找`re`模块下所有的包含`find`的函数：

```python
In [6]: import re

In [7]: re.*find*?
re.findall
re.finditer
```

## 历史命令

在IPython shell 中，使用历史的命令可以简单地使用上下翻页键即可，另外也可以使用hist命令查看所有历史输入。

```python
In [7]: re.*find*?
re.findall
re.finditer

In [8]: hist
x=[1,2,3]
x?
def add(a,b):


    """
    Add Two  numbers
    """
    return a+b
add?
add??
import re
re.*find*?
hist

```

如果在`hist`命令之后加上`-n`，即`hist -n`也可以显示出输入的序号：

```python
In [9]: hist -n
   1: x=[1,2,3]
   2: x?
   3:
def add(a,b):


    """
    Add Two  numbers
    """
    return a+b
   4: add?
   5: add??
   6: import re
   7: re.*find*?
   8: hist
   9: hist -n
```

在任何的交互会话中，我们的输入历史和输出历史都会被保存在`In`和`Out`变量中，并被**序号**进行索引。

另外，`_`，`__`，`___`和`_i`，`_ii`，`_iii`变量保存着最后三个输出和输入对象。`_n`和`_in`(这里的n表示具体的数字)变量返回第n个输出和输入的历史命令。比如：

```python
In [10]: _i
Out[10]: 'hist -n'


In [12]: _ii
Out[12]: '_i'

In [13]: _iii
Out[13]: '_i'
```

## 使用%run命令运行脚本

所有的文件都可以通过%run`命令当做Python程序来运行，输入`%run 路径+python文件名称即可。

```python

In [14]: %run D:\Pycharm\python练习\A.py
hello,world

```

## %timeit命令快速测量代码运行时间

在一个交互式会话中，我们可以使用`%timeit`魔法命令快速测量代码运行时间。相同的命令会在一个循环中多次执行，多次运行时长的平均值作为该命令的最终评估时长。`-n` 选项可以控制命令在单词循环中执行的次数，`-r`选项控制执行循环的次数。

```python
In [15]: %timeit [x*x for x in range(100000)]
7.15 ms ± 107 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
Compiler time: 0.34 s
```

## **使用`%debug`命令进行快速debug**

ipython带有一个强大的调试器。无论何时控制台抛出了一个异常，我们都可以使用`%debug`魔法命令在异常点启动调试器。接着你就能调试模式下访问所有的本地变量和整个栈回溯。使用`u`和`d`向上和向下访问栈，使用`q`退出调试器。在调试器中输入`?`可以查看所有的可用命令列表。

我们也可以使用`%pdb`魔法命令来激活IPython调试器，这样，每当异常抛出时，调试器就会自动运行。

## **使用Pylab进行交互式计算**

`%pylab`魔法命令可以使`Numpy`和`matplotlib`中的科学计算功能生效，这些功能被称为基于向量和矩阵的高效操作，交互可视化特性。它能够让我们在控制台进行交互式计算和动态绘图。

```python
In [1]: %pylab
Using matplotlib backend: Qt5Agg
Populating the interactive namespace from numpy and matplotlib

In [2]: x = linspace(-10,10,1000)

In [3]: plot(x,sin(x))
Out[3]: [<matplotlib.lines.Line2D at 0x7db95f9640>]
```

在该示例中，我们首先定义了一个-10到10的线性空间中的1000个数值的向量，接着我们绘制了(x,sin(x))图像，这样我们就成功绘制出了`sin(x)`的函数图像：

![image-20201021152601182](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021152601182.png)

在IPython中使用系统shell

我们可以在IPython中直接使用系统shell，并获取读取结果作为一个Python字符串列表。为了实现这种功能，我们需要使用感叹号`!`作为shell命令的前缀。比如现在在我的windows系统中，直接在IPython中ping百度

```python
In [4]: !ping baidu.com

正在 Ping baidu.com [220.181.38.148] 具有 32 字节的数据:
来自 220.181.38.148 的回复: 字节=32 时间=34ms TTL=46
来自 220.181.38.148 的回复: 字节=32 时间=47ms TTL=46
来自 220.181.38.148 的回复: 字节=32 时间=28ms TTL=46
来自 220.181.38.148 的回复: 字节=32 时间=26ms TTL=46

220.181.38.148 的 Ping 统计信息:
    数据包: 已发送 = 4，已接收 = 4，丢失 = 0 (0% 丢失)，
往返行程的估计时间(以毫秒为单位):
    最短 = 26ms，最长 = 47ms，平均 = 33ms
```

## IPython  Notebook

使用浏览器作为界面，向后台的IPthon服务器发送请求。最终要的特点：可重复性的互动计算。这意味着我们可以重复更改并且执行曾经的输入记录。它可以保存成其他很多格式，比如Python脚本，HTML，PDF等，所以它可以记录我们的演算过程。很多课程，博客以及书籍都是用Notebook写的。



### 运行

当上面的中文的IPthon后，IPython Notebook就已经算是安装好了。使用win+r打开运行窗口，输入ipython notebook，如果正确安装的话，这个命令就会默认在本地8888端口启动一个web服务，并自动打开浏览器，打开`http://localhost:8888/tree`页面，在这个页面我们可以看到当前目录下的所有文件夹以及`ipynb`文件。

![image-20201021154308456](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021154308456.png)

![image-20201021154440164](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021154440164.png)



可以自己设置相应的目录打开，首先在cmd中进入相应的目录，然后输入ipython notebook即可进入。

![image-20201021154932878](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021154932878.png)

进入到相应的浏览器页面，这个文件夹的内容会显示在上面。

![image-20201021155017292](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021155017292.png)



可以打开已有的notebook文件，也可以新建一份

![image-20201021155359156](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021155359156.png)

### 操作

1、ctrl+enter 会显示运行结果而不会创建新的输入框

2、shift+enter 小格子内的所有代码会运行，运行结果会立即出现在输出区域显示，且会创建一个新的输入框。

3、在一个输入框即Cell中使用回车即`Enter`键，表示换行，也就是说一个Cell中可以输入多条语句。

![image-20201021160952662](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021160952662.png)

可以选择是文本格式，还是代码格式

![image-20201021161720228](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201021161720228.png)



## jupyter

### 基本操作

使用conda  list查看所有conda中安装的酷

![image-20201030203939232](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201030203939232.png)

jupyter主要依靠的是这个包

![image-20201030204030792](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201030204030792.png)

进入到pytorch虚拟环境，我们选择在虚拟环境中安装jupyter

进入虚拟环境：conda activate pytorch

之后再输入代码   ： conda  install  nb_conda   进行安装

![image-20201030205538416](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201030205538416.png)

在pytorch环境中输入jupyter notebook  即可进入

![image-20201030205613656](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201030205613656.png)

下面为打开的页面

![image-20201030205638492](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201030205638492.png)



使用虚拟环境的pytorch创建案例

![image-20201030205801530](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201030205801530.png)

检验是否能运行，操作和使用ipython  notebook 进入的页面一样

![image-20201030205915388](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201030205915388.png)



添加标题，通过选择格式添加标题

![image-20201031155437467](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201031155437467.png)

通过在前面添加不同数量的#  号来表示这是几级标题

![image-20201031155628540](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201031155628540.png)

增添行

用鼠标点击已经运行的行，按键盘上的A、B 分别为向上添加一行或者向下添加一行。![image-20201031155954672](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201031155954672.png)



![image-20201031160228097](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201031160228097.png)



改变块的种类快捷键：Y M R。y是代码块，M是标签，R是块。

![image-20201031160624345](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201031160624345.png)

按H会出现快捷键栏

![image-20201031161704589](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201031161704589.png)

![image-20201031161716544](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201031161716544.png)

![image-20201031161726480](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201031161726480.png)



### 改变jupyter风格

参考：https://www.cnblogs.com/6b7b5fc3/p/13488264.html



在虚拟环境中。在conda中进入到相应的虚拟环境中。

conda activate pytorch

进入jupyter：jupyter notebook

使用下列代码安装jupyter_themes(如果是控制台，则将conda换成pip)

```
conda install jupyterthemes
```

使用以下命令可以查看所有的主题：

```
jt -l
```

```
(pytorch) C:\Users\Administrator>jt -l
Available Themes:
   chesterish
   grade3
   gruvboxd
   gruvboxl
   monokai
   oceans16
   onedork
   solarizedd
   solarizedl
```

使用以下命令选择要使用的主题：

```
jt -t 主题名称
```



![image-20201103132613128](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103132613128.png)



chesterish：适合夜间

![image-20201103132704349](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103132704349.png)

grade3：主题为灰色

![image-20201103132835067](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103132835067.png)

gruvboxd:主题为黄色

![image-20201103133048081](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103133048081.png)

gruvboxl：暖黄色

![image-20201103133303597](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103133303597.png)

monokai：主题篇荧光色

![image-20201103133456222](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103133456222.png)

ocean 16

![image-20201103133651822](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103133651822.png)

onedork

![image-20201103133817012](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103133817012.png)

solarizedd：比较模糊

![image-20201103133926815](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103133926815.png)

 solarizedl

![image-20201103134049678](D:\任太帅的日常文件\研究生学习课程\深度学习笔记\pytorch学习笔记\笔记保存图片\image-20201103134049678.png)

