# pytorch-合并和切割

## 合并（Merge)

### cat

cat(tensors, dim=0)   :   将多个张量合并起来，tesor是传入的张量，这些张量除了在需要合并的维度上不同外，其他维度上都必需要相同。dim 是指需要合并的维度。

![image-20201106195613711](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/AEDedgwC8vmo9yz.png)

下面是一些示例：![image-20201106200839789](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/2hi8gtCLPkb7Vf1.png)

### stack

stack(tensors, dim=0)  :  不同与cat，该函数会在dim维度上新建一个维度。同时，需要传入的tensor的维度信息也一样。

适用场景：cat相当于同一个班级的两个老师各自统计了一部分学生，然后合并起来。stack相当于两个班级的老师各自将自己班级的学生成绩统计了，但是需要分开来合并，表示是不同班级的。

![image-20201106201208381](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/o7yBD4TvZmfIuPM.png)

## 切割(split)

### length

split(tensor, split_size_or_sections, dim=0)    :    

- tesnor：input，待分输入
- split_size_or_sections：需要切分的大小(int or list )
- dim：切分维度

当split_size_or_sections为**int**时，则范围为（n/2,n-1),n为相应维度的数字。会自动根据所给数字给划分为两个部分。

![image-20201106211252718](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/c6jW81KTsRvuwx5.png)

当split_size_or_sections 为**list**时，那么tensor结构会一共切分成len(list)这么多的小块，每个小块中的大小按照list中的大小决定，其中list中的数字总和应等于该维度的大小，否则会报错（注意这里与split_size_or_sections为int时的情况不同）。

这个list里面的数字只能有两个。超过两个会报错

![image-20201106211849004](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/SKdvm6GgjRMqpXH.png)



### num

chunk(input, chunks, dim=0)  :  返回的数量为指定轴的元素个数除chunks。如果指定轴的元素个数被chunks除不尽，那么最后一块的元素个数变少。

似乎只能将chunks设置为2，返回两个新的张量。

![image-20201106212609436](https://cdn.jsdelivr.net/gh/rts-coder/pytorch-learning/img/x1TQ5dMEcNAXw7C.png)