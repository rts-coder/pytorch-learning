# pytorch-基本运算

## basic

+、-、*、/

torch.add(a,b)、torch.sub(a,b)、torch.mul(a,b)、torch.div(a,b)

基本运算，上面的都是等效的。

上面的乘法运算表示的是相同位置的元素进行相乘。

![image-20201106215823378](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/2sncwgm96MZYRua.png)

## 矩阵相乘

这是按照矩阵的运算规则进行相乘。

有三种方式：

1、torch.mm     只适用于2d的矩阵相乘

2、torch.matmul (a,b)     适用于两个矩阵相乘

3、 @            第二种方式等价，一种简写

![image-20201106221004345](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/OWzbSAwcCeIM8qX.png)

实例：

原始张量为【4.784】，我们希望将其降维为【4,512】这样类型的数据。

w张量是pytorch的习惯写法，第一个数据是channel-out，第二个数据是channel-in。也就是结果是512，进来的是784.

![image-20201106221935639](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/zjcICLdeMFsAxwn.png)

### torch.matmul()

适用于多维张量的运算。

a = torch.rand(4,3,28,64)
b = torch.rand(4,3,64,32)

当用于这两个张量的计算时，该函数会计算最后两个维度的相乘，前两个维度不变。得到结果：torch.Size([4, 3, 28, 32])

c = torch.rand(4,1,64,32)

torch.matmul(a,c).shape

当上述a和c进行张量相乘的时候，会首先将c进行广播维度扩展，之后进行运算。

如果前面的维度数据无法扩展到相应的数据，则无法张量相乘。

![image-20201106223000735](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/gZEGJr6Pws9c1MQ.png)

## 次方计算

1、pow(input, exponent)     :将张量根据exponent参数进行次方运算。

2、**      ：次方运算

3、sqrt  :  开方运算

4、rsqrt  ：返回一个新张量，包含输入张量每个元素的平方根倒数。

![image-20201106225254459](https://i.loli.net/2020/11/06/i8cUwXHOshbILmz.png)

## 指数、对数

torch.exp（） :  指数函数

torch.log（）   ：对数函数

![image-20201107081446247](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/6LsnFAKr2JO84ha.png)

## 近似值

a.floor()			 #向下取整函数
a.ceil()				 #向上取整函数
a.trunc() 			#数据的整数部分
a.frac() 				#数据的小数部分
a.round()             #数据的四舍五入计算

![image-20201107081925868](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/8EJ51ARIPVkWdh2.png)

## clamp

实现裁剪功能。