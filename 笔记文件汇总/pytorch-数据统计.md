# pytorch-数据统计

## 统计属性

常用操作

![image-20201110210528466](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110210528466.png)

### norm

范数

**向量范数**：除了两个无穷范数以外，剩下的范数都是一个规律，即n范数就是一堆数字的n次方之和再开个n次方的根号；或者说，n范数就是一堆数字的n次方之和的n次方根。这里所谓的“一堆数字”，实际上是一个向量的多个维度的坐标。我们假设这个向量x = (x1, x2, x3, x4, x5)，这一堆数字实际上就是x1, x2, x3, x4, x5，就是向量x在空间中的五个维度上的度量（或“刻度值”）。x的2-范数表示了x这个点与空间原点的距离，也相当于x这个向量的长度。

正负无穷范数分别表示所有向量元素绝对值中的最大值和最小值。

1-范数是所有数据的绝对值求和

![image-20201110213706740](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110213706740.png)

矩阵范数：

默认的frobenius范数，即为矩阵元素的绝对值平方和再开根号。

![image-20201110213746160](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110213746160.png)

相关公式：

![image-20201110215103313](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110215103313.png)

norm:

```
norm(input, p='fro', dim=None, keepdim=False, out=None, dtype=None)

input:输入tensor

p:(int, float, inf, -inf, 'fro', 'nuc', optional)：范数计算中的幂指数值。默认为'fro'。

dim (int，2-tuple，2-list， optional): 指定计算的维度。如果是一个整数值，向量范数将被计算；如果是一个大小为2的元组，矩阵范数将被计算；如果为None，当输入tensor只有两维时矩阵计算矩阵范数；当输入只有一维时则计算向量范数。如果输入tensor超过2维，向量范数将被应用在最后一维

keepdim（bool，optional）：指明输出tensor的维度dim是否保留。如果dim=None或out=None,则忽略该参数。默认值为False，不保留

out（Tensor, optional）:tensor的输出。如果dim=None或out=None,则忽略该参数。

dtype（torch.dtype，optional）：指定返回tensor的期望数据类型。如果指定了该参数，在执行该操作时输入tensor将被转换成 :attr:’dtype’
```

![image-20201110215934964](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110215934964.png)

p的参数值：当参数为1时是所有绝对值求和，当参数为2时是所有数平方和再开放，参数为3时是所有数立方再开三次根号。

![image-20201110222121476](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110222121476.png)

dim：在那个维度上求范数。则会将这个维度的数据消去。比如，（2，4），当dim为0的时候返回的shape是[4]，于是对不不同行但列相同的位置进行了绝对值求和运算，之后返回一个一维四列的张量；当dim=1，返回的shape是[2]，即将不同列的但是其他行相同的数据进行了绝对值求和运算，并返回了一个新的张量。

在那个维度进行范数运算，则返回的是总的参数中除去这个维度参数之后的形状。



![image-20201110222250816](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110222250816.png)

对于多维的张量指定dim之后的运算也是如此。返回的是消去这个维度之后的shape。例如（2，3，4）形状的张量，在dim=0，计算之后返回的是（3，4）形状张量。运算过程就是在除了该维度外，其他维度位置相同的数据的运算（p为1则表示绝对值求和，p为2表示绝对值平方求和再开方）。

![image-20201110223146239](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110223146239.png)

### 基本

mean、sum、min、max、prod（累乘）、argmax(最大值索引）、argmin。

argmax这里返回的索引值是7，是将原来的张量转换成一维张量后再进行的索引。对于没有给出dim值，该函数都会将其转换为一维度的张量后再进行计算。

![image-20201110224253367](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110224253367.png)







