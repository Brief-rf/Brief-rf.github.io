# 损失函数


**keras学习笔记（四）**

<!--more-->

目标函数，或称损失函数，是编译一个模型必须的两个参数之一：

```python
model.compile(loss='mean_squared_error', optimizer='sgd')
```

可以通过传递预定义目标函数名字指定目标函数，也可以传递一个Tensorflow的符号函数作为目标函数，该函数对每个数据点应该只返回一个标量值，并以下列两个参数为参数：

- y_true：真实的数据标签，Tensorflow张量
- y_pred：预测值，与y_true相同shape的Tensorflow张量

真实的优化目标函数实在各个数据点得到的损失函数值之和的均值

## 自定义损失函数例子

原文链接：https://kexue.fm/archives/4493

```python
from keras.layers import Input,Embedding,LSTM,Dense
from keras.models import Model
from keras import backend as K

word_size = 128
nb_features = 10000
nb_classes = 10
encode_size = 64

input = Input(shape=(None,))
embedded = Embedding(nb_features,word_size)(input)
encoder = LSTM(encode_size)(embedded)
predict = Dense(nb_classes, activation='softmax')(encoder)

def mycrossentropy(y_true, y_pred, e=0.1):
    loss1 = K.categorical_crossentropy(y_true, y_pred)
    loss2 = K.categorical_crossentropy(K.ones_like(y_pred)/nb_classes, y_pred)
    return (1-e)*loss1 + e*loss2

model = Model(inputs=input, outputs=predict)
model.compile(optimizer='adam', loss=mycrossentropy)
```




