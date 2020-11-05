---

typora-root-url: 笔记保存图片
typora-copy-images-to: 笔记保存图片
---

# 安装pytorch

## torch历史

PyTorch的前身是Torch这个机器学习框架（支持GPU加速运算），它使用Lua语言作为开发语言，该框架的小众性正是因为其使用这个冷门的编程语言。

- 2016年，Facebook在Torch7的基础上重新开发了一个深度学习框架，这就是2016年10月发布的PyTorch 0.1，它使用THNN作为后端。
- 2018年12月，发布PyTorch 1.0正式版，它使用CAFFE2作为后端，以弥补PyTorch在工业部署上的不足。

截至到2020.10.27，已经开发到了Pytorch1.7版本

![image-20201104201107147](/image-20201104201107147.png)

![image-20201031194456180](/image-20201031194456180.png)

框架优势

![image-20201031194748579](/image-20201031194748579.png)





参考链接：https://blog.csdn.net/weixin_43012220/article/details/83786637

**一、系统与环境说明**

在开始用Pytorch进行深度学习之前，要先准备好基本的软硬件环境。下面我分别从操作系统、GPU环境等方面简单说一下最基本的Pytorch运行环境。

**1、操作系统**

目前Pytorch支持的操作系统有Windows、Linux、MacOS。那么究竟使用哪一种操作系统呢？

*如果您只是简单的使用Pytorch，不需要CUDA编程或者使用高度定制化的操作。那么**任意一种操作系统**都可以。*

*如果您需要高度定制化的操作，比如说定义一个CUDA函数，那么个人建议使用**Linux或者Mac。***



如果您已经装了Windows并且不想卸载重装系统，那么您可以安装一个双系统。安装双系统前切记切记要把系统备份做好，因为手滑格式化硬盘的惨剧也不再少数。

**2、CPU与GPU**

GPU

图形处理器（英语：Graphics Processing Unit，缩写：GPU），又称显示核心、视觉处理器、显示芯片，是一种专门在[个人电脑](https://baike.baidu.com/item/个人电脑/3688503)、[工作站](https://baike.baidu.com/item/工作站/217955)、游戏机和一些[移动设备](https://baike.baidu.com/item/移动设备/9157757)（如[平板电脑](https://baike.baidu.com/item/平板电脑/1348389)、[智能手机](https://baike.baidu.com/item/智能手机/94396)等）上做图像和图形相关运算工作的[微处理器](https://baike.baidu.com/item/微处理器/104320)。



如果您想深入学习Pytorch，那么一块GPU是少不了的。没有GPU许多实验都无法迅速完成。如果没有GPU，就请使用CPU吧！把数据集缩小，过把瘾总是可以的。

一些朋友也许会问，那么能不能用带GPU的笔记本搞深度学习呢？当然可以！只要程序运行的时间不是太长，用带GPU的笔记本也能完成任务。游戏都能玩，程序还跑不了吗？不过如果有条件，我建议还是买一台台式机，再根据经济条件配一块显卡（二手的显卡其实也能用）。毕竟笔记本散热差，而且笔记本上的显卡很多时候是被阉割过的，性能比较差。当然，如果只是用于学习目的，一个笔记本电脑已经足够了。

GPU也有许多型号，如果要用Pytorch请准备1050以及以上的显卡。10系列以下的显卡上是运行不了最新版本的Pytorch的。

## 1、安装anaconda

anaconda  包含了大量的packge。

使用虚拟环境安装可以方便的适用于需要不同版本的开发，各个环境之间相互独立，可随意切换。

找到个人版本的anaconda

网址：https://www.anaconda.com/products/individual

![image-20201030131152451](/image-20201030131152451.png)

下载相应版本的安装包

![image-20201030131252724](/image-20201030131252724.png)

之后点击安装包进行安装

![image-20201030131627782](/image-20201030131627782.png)

需要选择安装路径，后面的都选择默认就行

![image-20201030131715483](/image-20201030131715483.png)

跳过安装visual studio  code

![image-20201030131807597](/image-20201030131807597.png)

点击完成

![image-20201030131841388](/image-20201030131841388.png)

检验安装是否成功：找到anaconda  prompt  

![image-20201030131942913](/image-20201030131942913.png)

看到有base字样则说明安装成功

![image-20201030132030744](/image-20201030132030744.png)



## 2 安装驱动和CUDA环境

GPU 显卡主要起到加速的作用，有没有显卡对于学习没有影响

检查电脑是否有GPU

打开任务管理器![image-20201019101137908](/image-20201019101137908.png)

点击性能

![image-20201019105713134](/image-20201019105713134.png)

若有，则需安装CUDA和CUDNN







## 3  通过pip安装pytorch

没有GPU，直接进到官网

去官网看看，官网（https://pytorch.org/），点击install

![image-20201018145429553](/image-20201018145429553.png)



选择与自己相匹配的版本，这里显示是我安装的选择

![image-20201019213313233](/image-20201019213313233.png)

win+r  调出终端

![image-20201019213413552](/image-20201019213413552.png)



输入cmd

![image-20201019213427750](/image-20201019213427750.png)

将pytorch官网上的命令复制到终端

出现错误

![image-20201019213605373](/image-20201019213605373.png)

之后直接连接不了

![image-20201020162242454](/image-20201020162242454.png)



查看自己python版本，将下列命令输入到cmd中，可以看到我的版本是python3.8

python --version

![image-20201020165737645](/image-20201020165737645.png)











将复制好的地址贴到浏览器地址框，并回车[访问](https://download.pytorch.org/whl/torch_stable.html)，可以看到一整个网页的超链接；

![image-20201020165259396](/image-20201020165259396.png)

电脑上有时候访问不了。用手机浏览器可以打开，下载再传到电脑

![image-20201020165427952](/image-20201020165427952.png)

使用Ctrl+F或F3调出查找框，并按如下规则找到需要的torch和torchvision（可以按第2步里官网推荐的版本）；

这里可以和官网上的代码进行一个对比，找出你想要下载的文件

```
pip install torch==1.6.0+cpu torchvision==0.7.0+cpu -f https://download.pytorch.org/whl/torch_stable.html
```

![image-20201020165452699](/image-20201020165452699.png)

下载的文件，我放到了在D盘下新建的文件夹

![image-20201020185128795](/image-20201020185128795.png)





安装.whl包

先win+r，输入cmd进入命令端口，优先输入python -m pip install --upgrade pip对pip进行更新。

![image-20201020170550224](/image-20201020170550224.png)





之后使用以下命令进行安装

pip install 下载路径\***torch-***-cp**-cp**-win_amd64.whl
pip install 下载路径\***torchvision-***-cp**-cp**-win_amd64.whl

![image-20201020171139803](/image-20201020171139803.png)

![image-20201020185151300](/image-20201020185151300.png)



验证安装

使用win+R打开运行，输入`cmd`然后回车，来到命令控制符界面。
输入`pip list`找找有没有如下两个项目和对应的版本号，有即为安装成功。

![image-20201020185245160](/image-20201020185245160.png)

下面是进入python环境运行pytorch

![image-20201020185947332](/image-20201020185947332.png)





## 4、通过conda安装

1、安装anaconda

2、在开始栏点击打开“Anaconda”-->"Anaconda Prompt",得到一个命令行窗口anaconda  prompt

3、输入python，查看python版本，可见我的python是3.83版本的，然后输入exit（）退出

![image-20201030132858635](/image-20201030132858635.png)

4、用以下命令创建环境，并命名为pytorch

-n  是为这个环境命名

```
conda create -n pytorch python=3.8
```

出现conda的“Solving environment: failed”问题。这里是因为输入的python版本为3.83.

![image-20201030133646263](/image-20201030133646263.png)

将3.83替换为3.8，这里conda会自动找3.4中最新的版本下载，运行成功。

![image-20201030134711069](/image-20201030134711069.png)

下面的是安装的路径

![image-20201030160326013](/image-20201030160326013.png)

接下来说这个环境需要安装这些包，我们输入y，表示yes

![image-20201030134758300](/image-20201030134758300.png)

接下来字体自动变大，这里提示下列命令可以激活这个环境

![image-20201030135026916](/image-20201030135026916.png)

当我们使用命令~conda activate pytorch~之后，可以看到他的环境配置变成了pytorch，使用pip  list  查看里面有哪些包。里面并没有pytorch，接下来就是pytorch的conda安装。

![image-20201030135325313](/image-20201030135325313.png)

5、打开pytorch官网，往下翻可以看到安装配置

如果电脑有cuda，可以在任务管理器中，查看性能中GPU，看到cuda的型号下面是GPU型号例子![image-20201030140040759](/image-20201030140040759.png)

下面是我的安装配置，因为没有显卡，所以我选择的none

![image-20201030140321068](/image-20201030140321068.png)

将安装的代码复制下来到anaconda prompt中。记得要是之前的pytorch环境

```
conda install pytorch torchvision torchaudio cpuonly -c pytorch
```

![image-20201030140447887](/image-20201030140447887.png)

有很多包需要下载，它会询问你是否要安装，输入y，回车下载。

![image-20201030140551662](/image-20201030140551662.png)

出现condahttperror错误：

可能因为anaconda版本原因有些库安装失败，下面的代码可以帮助更新： conda update -n base -c defaults conda，更新后重新安装还是不行。

![image-20201030153853585](/image-20201030153853585.png)

出现上面的错误后。首先将anaconda的官方源切换为清华源。

(1)win+r再输入cmd。在cmd中输入下面内容：

```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/mro/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/numba/label/dev/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/win-64/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/win-64/
conda config --set show_channel_urls yes
```

(2)在anaconda  prompt中输入conda  update  --all

对conda进行更新，之后再走一遍前面的流程，可以在anaconda安装的地方找到envs文件夹将之前失败的环境删除。







## 5  设置环境

### conda大环境的编译器

在file中选择new project

![image-20201020193150172](/image-20201020193150172.png)

选项点击省略号

![image-20201020194032535](/image-20201020194032535.png)

设置anaconda的python环境

![image-20201020194156379](/image-20201020194156379.png)

路径可以在cmd中输入  where  python，可以查看python环境的路径

![image-20201020194317980](/image-20201020194317980.png)

设置好存储路径

![image-20201020195105674](/image-20201020195105674.png)



### conda虚拟环境编译器

创建一个新项目，选择保存的地址

![image-20201030210827124](/image-20201030210827124.png)

之后设置anaconda虚拟环境的编译器，选择三个省略点

![image-20201030210910490](/image-20201030210910490.png)

选择conda environment  ，之后点击省略号，寻找到之前创建好的环境中的python解释器。

![image-20201030211027136](/image-20201030211027136.png)

设置好之后的样式，点击creat

![image-20201030211227686](/image-20201030211227686.png)

创建项目成功

![image-20201030211622173](/image-20201030211622173.png)

在file中找到setting，里面可以查看安装的pytorch包

![image-20201030211734837](/image-20201030211734837.png)



### 写程序

#### place one

创建一个python文件

![image-20201030211841514](/image-20201030211841514.png)

设置相应的python解释器

（1）第一种方法

![image-20201030212006895](/image-20201030212006895.png)

添加python解释器

![image-20201030212107985](/image-20201030212107985.png)

选择脚本运行位置，其他的系统以及设置好了，点击ok

![image-20201030212140799](/image-20201030212140799.png)

点击绿色三角运行。在pycharm中按shift+回车  会跳到下一行的行首。

![image-20201030212342258](/image-20201030212342258.png)

（2）第二种方法

鼠标右键点击或者快捷键ctrl+shift+F10

![image-20201030212433701](/image-20201030212433701.png)



#### place two

在控制台输入代码执行

![image-20201030212628393](/image-20201030212628393.png)

和ipython类似

![image-20201030212701933](/image-20201030212701933.png)



pycharm两种方法的比较：

1、如果理解代码是以块为整体运行的话，第一种方法中，python文件的块是所有行的代码；第二种方法，是以每一行或者多行为块运行的，方便排除错误或者主要用于查看单行的作用。

2、第一种方法比较整洁，第二种发生错误的时候代码可读性查。

3、在jupyter中时以任意行为块运行的。

![image-20201030214323722](/image-20201030214323722.png)



