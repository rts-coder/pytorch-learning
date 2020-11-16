---

---

# Pytorch 基本数据类型

## 基本类型

在python中的数据类型在pytorch中基本都能一一对应，除了string

![image-20201108163412335](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108163412335.png)

pytorch并没有string类型，但是可以使用编码类型来表示。比如10表示小狗，01表示猫。在nlp中有专门的模块来解决这个问题。

![image-20201108140444027](https://i.loli.net/2020/11/08/j5yW3cgzYL2flqH.png)



pytorch中的数据类型

![image-20201108165053338](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108165053338.png)

## 查看类型

a.type()   是torch中的方法，可以返回详细的类型

type(a)   是python自带的方法，没有提供额外信息

isinstance(a,torch.FloatTensor)   一般用这种方法来比对类型

![image-20201108165146443](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108165146443.png)

数据放置于cpu和GPU上所表示的数据类型是不同的

![image-20201108165232186](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108165232186.png)

### dim0

torch.tensor(1.3) ：对于标量数据类型可以使用该方法来创建一个0维数组。

a.shape  ： 可以查看tensor张量的形状

a.size()   :   与a.shape 对应，不同之处在于一个直接是属性，另一个是函数。

![image-20201108165340645](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108165340645.png)



### dim1

一维数据的生成

torch.tensor([1])  : 这个方法圆括号里面有中括号，会根据里面的值生成一维张量。

torch.FloatTensor()  :   当里面只给出了一个数字，则会根据数字生成未初始化的相应一维张量。如果里面有中括号，则会根据中括号的内容生成一维张量。

![image-20201108165454724](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108165454724.png)



![image-20201108165755457](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108165755457.png)

将numpy中的一维数组转换为一维tensor张量。

![image-20201108165550471](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108165550471.png)





### dim2

下面使用随机正态分布创建了一个dim为2的张量。

size函数如果不给值，则返回整个的形状。如果给了参数，则返回的是该维度上的形状大小。

![image-20201108134412844](https://i.loli.net/2020/11/08/jhToHpysAnf9KeS.png)

dim3

下面使用随机均匀分布创建一个dim为3的张量。如20句话，每句话10个单词，每个单词用100个分量的向量表示，得到的Tensor就是shape=[20, 10, 100]

可以使用list方法直接将数据转换为列表。方便和python的交互。

三维数据适合文字处理。

![image-20201108134855997](https://i.loli.net/2020/11/08/qcIK7OVPjLiE1F4.png)

### dim4

a = torch.rand(2,3,28,28)

dim为4的张量经常用来表示图片。从左往右，第一个数字表示有几张图片，第二个数字表示rgb的第几个通道，比如1表示灰色图片，3表示彩色图片。第三、第四分别表示图片的长和宽。

例如100张MNIST数据集的灰度图(通道数为1，如果是RGB图像通道数就是3)，每张图高28像素，宽28像素，那么这个Tensor的shape=[100, 1, 28, 28]，也就是一个batch的数据维度：[batch_size, channel, height, width]。

![image-20201108135153302](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/hazne6m8CrWsVFl.png)![image-20201108135206069](https://i.loli.net/2020/11/08/Q8iL69lxgAzmfRT.png)

###  额外知识

torch.numel()   :    得到tensor数据的具体大小。

torch.dim()    :   和length(a.shape)   方法一样，返回的数据表示tensor张量的维度大小。

![image-20201108140109173](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108140109173.png)

## 创建tensor

### 导入数据

从numpy导入数据

导入的数据值和数据类型不变，只是从numpy数组变为了张量。

![image-20201101142624144](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/SHexq4T85wuO9Ec.png)



从list导入数据。

torch.tensor()  根据数据生成张量，建议有数据的情况尽量使用小写的生成，有助于区分。

torch.FloatTensor()    既可以根据已有数据来生成，也可以根据给出的shape数据生成。

![image-20201108143007496](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108143007496.png)

### 创建未初始化张量

torch.empty()  ：给定shape可以生成未初始化的数据。

torch.Tensor(): 若为指定生成张量类型，则生成默认的类型，一般是FlaotTensor。

torch.FloatTensor( )  :  给定shape可以生成未初始化的浮点型数据。也可以根据具体的数据生成张量。

torch.IntTensor( )  :  给定shape可以生成未初始化的整型数据。也可以根据具体的数据生成张量。

生成的额数据是随机的，可能很大或者很小，一般不能直接用于计算，需要后续的赋值。

![image-20201115105901353](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201115105901353.png)



### 初始化张量

#### 随机生成

torch.rand()   : 初始化的每一个数据都是在从0 到1 之间随机均匀选取的。

torch.rand_like()  :  接收的是一个tensor张量，读取其shape数据，之后再用torch.rand()进行从0到1的随机均匀选取。

torch.randint(low,high,size)  :  这个方法前两个参数是取值的范围，左闭右开。第三个参数是传入一个tuple类型的size参数。 

![image-20201108143228905](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108143228905.png)



torch.randn(3,3)    :   根据正态化生成数据，N(0,1),  以0为均值，以1为方差生成数据。

torch.normal(mean=3 ,std=torch.arange(1,0,-0.1))    :  mean是生成数据的平均值，std是数据的方差，后面表示方差从1到0以步长0.1减小。也可以只填写前面两个值，默认步长为1。后面括号中的参数，需要包含浮点数，全是小数的时候会报错。

![image-20201108143333136](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201108143333136.png)

torch.randperm(n)   :  生成0到n-1 的一维张量，顺序是打散了的。

![image-20201110194905773](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110194905773.png)

#### 根据数值要求



torch.full([2,3],5)  :   表示生成一个2*3的矩阵，里面的数据全部是5。数据的类型为默认类型。

若需要生成标量，则传入中括号空值；生成一维tensor张量只需要传入1就行。

![image-20201110194028715](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110194028715.png)



torch.arange(0,10)   :   生成从0开始到但不包括10的等差数列。也可以传入一个数作为步长。

torch.range(0,10)   :  也可以实现上面函数一样的功能。但该函数之后会被删除，所以不推荐使用。

![image-20201110194130047](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110194130047.png)



torch.linspace(start, end, steps) ： 从start到end之间（两数闭区间）按照steps进行均分，之后返回steps个数这么多的等差数列。

torch.logspace(start, end, steps，base) ： 取得的是两个数的对数，在两个数之间以步数取均值。比如第三个例子是从10的0次方到10的-1次方，平均来取。base是设置对数的基数，默认值为10.

![image-20201110194337912](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110194337912.png)

torch.ones()  :  生成全是1的张量，维度由传入的数字确定，可以传入元组或者列表。

torch.zeros()  : 同上

torch.eye():   生成对角矩阵，但是传入的参数，只能是两个或者一个。更高维度的将不适用。

![image-20201110194516813](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110194516813.png)

![image-20201110194540300](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110194540300.png)



运用的例子。比如数据的第一排表示的是人，后面分别表示的是数学成绩和语文成绩，我们希望两个数据集能够同步。比如人都从第一行换到第二行。

![image-20201110194930648](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110194930648.png)

### 设置默认类型

torch.tensor()  :   里面的数据类型会给定默认的数据类型。比如整数为LongTensor类型张量，小数的为默认设置的张量类型。生成的torsor张量数据类型不会被默认类型改变。

torch.Tensor（）：无论是整数还是小数，全部设置为默认的tensor类型。生成的tensor数据类型会受到默认设置的改变。

区别一：

- `torch.Tensor（data）`是将输入的data转化`torch.FloatTensor`
- `torch.tensor(data)`:(当你未指定`dype`的类型时)将data转化为`torch.FloatTensor`、`torch.LongTensor`、`torch.DoubleTensor`等类型，转化类型依据于data的类型或者`dtype`的值

torch.set_default_tensor_type(torch.DoubleTensor)     使用该方法可以设置默认类型。

![image-20201110195516251](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110195516251.png)

![image-20201110195538602](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201110195538602.png)

## 参数解析

使用dir可以查看里面有哪些工具，

![image-20201115112755836](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201115112755836.png)

使用help()可以查看如何使用工具

![image-20201115112817009](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201115112817009.png)

```
创建一个未被初始化数值的tensor,tensor的大小是由size确定

size: 定义tensor的shape ，这里可以是一个list 也可以是一个tuple

out: 根据之前已有张量，则根据其数据复制给新的张量。之后将该数据重新复制给改变量。如果之前没有改张量，则相当于将该张量赋值。

dtype:（可选）我不设置值 默认值就是torch.set_default_tensor_type制定的值，如果需要设置那就是torch.dtype的那几个。作用是指定返回tensor的数据类型

layout:(可选)值为 torch.layout。 torch.layout表示torch.Tensor内存布局的对象。有torch.strided(dense Tensors 默认)并为torch.sparse_coo(sparse COO Tensors)提供实验支持。
torch.strided代表密集张量，是最常用的内存布局。每个strided张量都会关联 一个torch.Storage，它保存着它的数据。这些张力提供了多维度， 存储的strided视图。Strides是一个整数型列表：k-th stride表示在张量的第k维从一个元素跳转到下一个元素所需的内存。

device：表现 torch.Tensor被分配的设备类型的类，其中分为’cpu’ 和 ‘cuda’两种。没有设置就使用当前设备。

requires_grad: (可选)是bool 类型的值，默认值是False 是否计算梯度

pin_memory：是否存于锁页内存
```

out参数：

![image-20201115111851018](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201115111851018.png)

layout参数：

表示张量内存布局的对象。`Strides`是一个整数型列表：`k-th stride`表示在张量的第k维从一个元素跳转到下一个元素所需的内存。

```
#12表示从最高维度的一个元素到下一个元素所需内存
#4 表示从在第二个维度中一个元素跳到下一个元素所需内存
#1  表示在第三个也就是最后一个维度红一个元素到下一个元素所需内存
```

![image-20201115121921465](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201115121921465.png)

