---

typora-root-url: 笔记保存图片
typora-copy-images-to: 笔记保存图片
---

# pytorch—索引与切片

## 索引

如果只给出tensor一个参数，则默认是从tensor张量从左往右的参数索引。

![image-20201104200851580](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201104200851580.png)



## 连续切片

切片里面的参数都是左闭右开的。  ： 两边的参数如果不写表示全取。

正向索引号是从0开始的，反向索引号是从-1开始的。

![image-20201103102249353](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201103102249353.png)

## 不连续切片

```
1、  ：  表示全部数据
2、 ：n   n:   表示从前取到n，或者取n和n之后的数据
3、 n1 ：n2    [start，end)  区间取值，左闭右开
4、n1：n2：x    [start，end，steps) 后面的数字是多少表示隔几个数取1个数据
```

![image-20201103103658798](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201103103658798.png)



## 具体索引

a.index_select(dim,index)  :  a是张量，dim是维度，你选择的是第几个数据；index是包含索引的一维张量。

 index_select(tensor, dim, index）  ： 将张量传入到函数里面进行索引，tensor代表张量。

注意：后面的index必须要是tensor类型的一维张量。

![image-20201103103658798](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201103103658798-1604491637210.png)

torch.take(input, index)  :  input  是输入的张量，index是一维张量。这个方法会将原先的所有数据进行打散，变为一维的张量。之后根据传入的第二个参数进行相当于一维的下标索引。0，2，5分表表示返回索引下标为这个数的值。

![image-20201103114032987](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201103114032987.png)



## ...索引

...   ：系统根据实际情况去推测有多少数据，然后全部取。



![image-20201103110648293](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201103110648293.png)

## mask索引

要取出所有大于0.5的数据。

masked_select(input, mask） ：input是输入的张量，mask是bool类型的张量。

该方法输出的是一个一维的张量，具体个数为符合要求数据的个数。

![image-20201103111613500](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/image-20201103111613500.png)





