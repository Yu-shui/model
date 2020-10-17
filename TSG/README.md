# Temporally-language-grounding



## Requirements

- Python 2.7
- Pytorch 0.4.1

### dataset

##### 在[*YouCook*](http://youcook2.eecs.umich.edu/)数据集上构造出的新数据集

文本数据集保存在TSG/data文件夹目录下，分为测试集，验证集，训练集。

视频特征保存在TSG/data/csv文件夹目录下。



## Two Models for this task

### 1. Our model

模型使用双阶段的训练，在第一阶段用Logratio损失函数训练基础模型，再再该基础上训练回归模型。

代码结构：

1.导入包：导入程序运行所需要的包

2.路径：定义数据集获取的路径以及训练所的模型保存的地址

3.GPU：测试GPU是否有效

4.功能函数：定义一众在程序运行中需要用到的功能函数如学习率调整函数adjust_learning_rate()，数据集读取函数get_dict()

5.读取数据：通过功能函数中的get_dict()读取训练集和验证集。

6.基础模型定义

​	（1）LSTM_CNN

​    （2）Log-Ratio Loss

**7.训练基础模型**

模型文件存储在TSG/data/save路径下

**8.回归模型定义**

对于提取出来的语义特征与视觉特征进行拼接，将这个拼接的向量作为回归模型的输入，回归模型损失函数分为Alignment Loss（匹配损失）、 Localization Regression loss（回归定位损失）
$$
L=L_{align}+\lambda *L_{loc}
$$


**9.训练回归模型**

模型文件存储在TSG/data/save路径下

**10.使用test集计算R@1**

评价指标：Recall@N，tIoU=m，对于一个输入的查询语句，返回N个相关联的视频帧预测时间戳，计算这些时间戳和真实值的tIoU ，如果tIoU高于m，将被视为positive。



### 2. TALL: Temporal Activity Localization via Language Query

This is the repository for our ICCV 2017 paper [*TALL: Temporal Activity Localization via Language Query*](https://arxiv.org/abs/1705.02101).

模型结构与前者类似，模型文件存储在TSG/data/save/TALL/savemodel



## Performance

| Methods | R@1, IoU0.1 | R@1, IoU0.3 | R@1, IoU0.5 | R@1, IoU0.7 |
| :-----: | :---------: | :---------: | :---------: | :---------: |
| model1  |    0.159    |    0.061    |    0.008    |    0.000    |
| model2  |    0.187    |    0.098    |    0.031    |    0.008    |
| model3  |    0.159    |    0.101    |    0.044    |    0.019    |
| model4  |    0.152    |    0.098    |    0.038    |    0.011    |
|  TALL1  |    0.106    |    0.061    |    0.030    |    0.015    |
|  TALL2  |    0.114    |    0.076    |    0.015    |    0.000    |
