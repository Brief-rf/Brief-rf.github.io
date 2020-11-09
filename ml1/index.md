# 机器学习知识总结

**笔记-科研**

<!--more-->

## 1.Softmax

实际神经网络最后的输出层的类别是没有意义的，是给出的标签赋予了其意义，softmax之前的分类每一个类都有一个数值，训练过程中经过softmax后将其转化位概率，挑选出最大的概率与正确的标签比较，从而进行神经网络训练，在实战测试中继续给出预测的概率，onehot后给出类别

## 2.Dropout

随机断开神经网络连接，减少每次训练时实际参与计算的模型的参数量，但是在模型实战测试时，Dropout会恢复所有的连接，保证模型测试时获得最好的性能。

![Dropout ](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200814215324381.png "Dropout")

![Dropout](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200814215339727.png "DropoutInfo")

![Dropout](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200814215349134.png "DropoutImg")

## 3.BatchNorm层

简单来说就是将输**入的数据**进行映射，使得数据分布相近，并且分布在较小范围内

![BN](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200814210649048.png "BN")




