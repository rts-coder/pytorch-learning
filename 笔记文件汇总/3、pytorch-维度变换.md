---
typora-root-url: 笔记保存图片
---

# pytorch—维度变换

## 改变张量形状

view和reshape：两个方法是一样的。view是0.3版本之前的，reshape方法是为了同步numpy开发的端口。

改变形状之后，要保证整个tensor的size不变。

b = a.view(4,784)、b.view(4,28,28,1)     这里理论上来说没问题，但是数据有一个维度丢失，我们需要拿到数据原先的维度信息。

![image-20201105202848141](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/IeV3H5wZ1fX97qA.png)

没有将数据的size保持住，所以会报错

![image-20201105203806541](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/2FBEan3JlPvuidj.png)

## 维度增加、减少

### unsqueeze

torch.unsqueeze(dim )：新插入一个维度，这个维度是自己定义的，数据的插入不会改变数据本身，不会增加也不会减少数据；只是说给数据增加了一个组别，这个组别的意义是我们自己去定义的。

dim是第一个维度处增加。范围和目标张量有关。[-a.dim()-1,a.dim()+1).   超过维度会报错。

里面传入参数为0和正数的时候是在这个数之前插入，如果是负数则是在这个维度之后进行数据的插入。

![image-20201105205502273](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/xnwgN572oEPOZLz.png)

以下例子反应了数据本身不会改变，只是理解数据的方式变了。

![image-20201105210442972](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/fnJ7rP5UymqF4iL.png)

案例：

通过维度变换之后可以进行其他操作。

![image-20201105210919905](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/kdrAaO3CFg4sQm9.png)

### squeeze

squeeze(input,dim)  :  如果不给参数，那么就会将能挤压的全部进行挤压。如果给出了具体的数字，那么只会在相应的维度进行挤压。

![image-20201105211447107](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/yqrCV9g6lIuK7He.png)

## 维度扩展

维度扩展是指将那个维度上的shape改变掉。

### expand

只是改变了我们的理解方式，并没有改变数据，只是一种view。不会主动复制数据，只会在有需要的时候复制数据。实现速度快，节约内存，推荐使用。

仅仅限于原来维度上的数据是1，变为之后的n才是可行的。如果原来的数据不为1，那么就不能进行操作。

如果输入的参数是-1，那么系统会默认给参数，这个用于有时候懒得去计算，让系统自己添加。这里有个bug，如果输入的参数是其他负数，生成的结果也是该负数，但是这是没有意义的。

![image-20201105213425424](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/gGi2Idc5UFavhnX.png)

repeat

实实在在的增加了数据。将原张量横向、纵向地复制。

![image-20201105214031224](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/jOoKnJ6cCwd15ry.png)

## 转置

### .t

.t  :  对矩阵进转置操作。只能对2D的矩阵进行操作，对于高维的矩阵不能进行该操作。

![image-20201105215637318](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/Y6aXO1uqeGLw89R.png)

### transpose

transpose(input, dim0, dim1) ：input是张量，后面两个参数是需要调换位置的维度。

调换维度之后会打乱原先的顺序，要是数据连续，需要使用contiguous方法来使数据连续。

![image-20201105220811342](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/NoupaIRyM6Bs2XF.png)

维度可以进行交换，但是我们需要人为记住并跟踪维度信息。否则就会出现数据的污染。

![image-20201105221547436](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/iEkSZunYvqPtw4D.png)

### permute

transpose可以进行任意两个维度的变化。但是当我们需要变化的维度较多的时候，那么我们可以使用permute方法。

同样，permute也会涉及到将内存打乱的问题，因此，我们有时候也会需要使用contiguous函数保持内存的连续。

![image-20201105222623224](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/EFSgdZQ2fmKilXp.png)

## broadcasting

官方文档：https://pytorch.org/docs/stable/notes/broadcasting.html#broadcasting-semantics

能够扩展维度。从末尾开始连续找第一个不相同的维度容量开始扩充，直到扩充成维度相同。

需要满足两个条件：

- 每个tensor至少是一维的
- 两个tensor的维数从后往前，对应的位置要么是相等的，要么其中一个是1，或者不存在

如果`x`和`y`是broadcastable的，那么结果的tensor的size按照如下的规则计算

- 如果两者的维度不一样，那么就自动增加1维（也就是unsqueeze）
- 对于结果的每个维度，它取x和y在那一维上的最大值



利用broadcast可以省略内存，减少内存消耗。

![image-20201106194431588](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/bVq7uKXapNRdWgt.png)

