# Keras


**keras学习笔记（二）**

<!--more-->

# 快速开始函数式（Functional）模型

我们起初将Functional一词译作泛型，想要表达该类模型能够表达任意张量映射的含义，但表达的不是很精确，在Keras2里我们将这个词改译为“函数式"，对函数式编程有所了解的同学应能够快速get到该类模型想要表达的含义。函数式模型称作Functional，但它的类名是Model,因此我们有时候也用Model来代表函数式模型。

# 第一个模型：全连接网络

## ```Sequential```当然是实现全连接网络的最好方式，但我们从简单的全连接网络开始，有助于我们学习这部分的内容。在开始前,有几个概念需要澄清:

- 层对象接受张量为参数,返回一个张量。
- 输入是张量，输出也是张量的一个框架就是一个模型，通过 Nodel定义。
- 这样的模型可以被像Keras的Sequential一样被训练

```python
from keras.layers import Input. Dense
from keras.models import Model
# This returns a tensor
inputs = Input(shape=(784,))
# a Layer instance is caLLabLe on a tensor~ and returns a tensor
x = Dense(64, activation= 'relu')(inputs)
x = Dense(64, activatlon= 'relu' )(x)
predictions = Dense(10, activation= 'softmax' )(x)
# This creates a modeL that incLudes
# the Input Layer and three Dense Layer
model = Model(inputs=inputs, outputs=predlctions)
model.compile(optimizer= 'rmsprop',
	loss= 'categorical_crossentropy' ,
	metrics=['accuracy'])
model.fit(data. labels) # starts training 
```

##  所有的模型都是可调用的,就像层一样

利用函数式模型的接口，我们可以很容易的重用已经训练好的模型:你可以把模型当作一个层一样，通过提供一个tensor来调用它。注意当你调用一个模型时，你不仅仅重用了它的结构，也重用了它的权重。

```python
x = Input(shape=(784,))
y = model(x)
```

## 多输入和多输出模型

使用函数式模型的一个典型场景是搭建多输入、多输出的模型。

![](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20201220104756400.png)

让我们用函数式模型来实现这个框图

```python
import keras
from keras.layers import Input, Embedding, LSTM, Dense
from keras.models import Model

main_input = Input(shape=(100,), dtype='int32', name='main_input')
x = Embedding(output_dim=512, input_dim=10000, input_length=100)(main_input)
lstm_out = LSTM(32)(x)
auxiliary_output = Dense(1, activation='relu', name='auxiliary_output')(lstm_out)
auxiliary_input = Input(shape=(5,), name='aux_input')
x = keras.layers.concatenate([lstm_out, auxiliary_input])

x = Dense(64, activation='relu')(x)
x = Dense(64, activation='relu')(x)
x = Dense(64, activation='relu')(x)

main_output = Dense(1, activation='sigmoid', name='main_output')(x)

model = Model(inputs=[main_input, auxiliary_input], outputs=[main_output, auxiliary_output])
```

模型定义完毕，下一步编译模型。我们给额外的损失赋0.2的权重。我们可以通过关键字参数```loss_weights```或 ```loss``` 来为不同的输出设置不同的损失函数或权值。这两个参数均可为```Python```的列表或字典。这里我们给loss传递单个损失函数，这个损失函数会被应用于所有输出上。

```python
model.compile(optimizer='rmsprop',loss='binary_crossentropy',loss_weights=[1., 0.2])

model.fit([headline_data, additional_data], [labels, labels], epochs=50, batch_size=32)
```

因为我们输入和输出是被命名过的（在定义时传递了"name”参数)，我们也可以用下面的方式编译和训练模型:

```python
model.compile(optimizer='rmsprop',
             loss={'main_output':'binary_crossentropy', 'aux_output':'binary_crossentropy'},
             loss_weights={'main_output':1., 'aux_output':0.2})
model.fit({'main_input':headline_data, 'aux_input':additional_data},
         {'main_output':labels, 'aux_output':labels},
         epochs=50, batch_size=32)
```

## 共享层

另一个使用函数式模型的场合是使用共享曾的时候。

```python
import keras
from keras.layers import Input, Dense, LSTM
from keras.models import Model

tweet_a = Input(shape=(140,256))
tweet_b = Input(shape=(140,256))
```

**若要对不同的输入共享同一层，就初始化该层一次，然后多次调用它**

```python
shared_lstm = LSTM(64)
encoded_a = shared_lstm(tweet_a)
encoded_b = shared_lstm(tweet_b)

merged_vector = keras.layers.concatenate([encoded_a, encoded_b], axis=-1)

predictions = Dense(1, activation='sigmoid')(merged_vector)
model = Model(inputs=[tweet_a, tweet_b], outputs=predictions)
model.compile(optimizer='rmsprop',
             loss='binary_crossentropy',
             metrics=['accuracy'])
model.fit([data_a, data_b], predictions, epochs=10)
```

## 层“节点”的概念

无论何时，当你在某个输入上调用时，你就创建了一个新的张量（即该层的输入），同时你也在为这个层增加一个“（计算）节点”。这个节点将输入张量映射为输出张量。当你多次调用该层时,这个层就有了多个节点,其下标分别为0，1，2...

如果层只与一个输入相连时，会出现问题

```python
a = Input(shape=(140, 256))
b = Input(shape=(140, 256))

lstm = LSTM(32)
encoded_a = lstm(a)
encoded_b = lstm(b)

lstm.output
```

上面这段代码会报错。

## 更多的例子

- inception模型

```python
from keras.layers import Conv2D, MaxPooling2D, Input
from keras.models import Model
input_img = Input(shape=(256,256,3))

tower_1 = Conv2D(64, (1,1), padding='same', activation='relu')(input_img)
tower_1 = COnv2D(64, (3,3), padding='same', activation='relu')(tower_1)

tower_2 = Conv2D(64, (1,1), padding='same', activation='relu')(input_img)
tower_2 = Conv2D(64, (5,5), padding='same', activation='relu')(tower_2)

tower_3 = MaxPooling2D((3,3), strides=(1,1), padding='same')(input_img)
tower_3 = Conv2D(64, (1,1), padding='same', activation='relu')(tower_3)

output = keras.layers.concatenate([tower_1, tower_2, tower_3], axis=-1)
model = Model(input_img,output)

model.summary()
```

上述代码执行结果：

```
Model: "model_1"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
input_1 (InputLayer)         (None, 32)                0         
_________________________________________________________________
dense_1 (Dense)              (None, 32)                1056      
=================================================================
Total params: 1,056
Trainable params: 0
Non-trainable params: 1,056
_________________________________________________________________
```

- 卷积层的残差连接

残差网络的详细信息参考文章Deep Residual Learning for Image Recognition

```python
from keras.layers import Conv2D, Input

# input tensor for a 3-channel 256x256 image
x = Input(shape=(256,256,3))
y = Conv2D(3, (3,3), padding='same')(x)
z = keras.layers.add([x,y])
```

- 共享视觉模型

该模型在两个输入上重用了图像处理的模型，用来判别两个MINIST数字是否是相同的数字

```python
from keras.layers import Conv2D, MaxPooling2D, Input, Flatten
from keras.models import Model

# first, define the vision modules
digit_input = Input(shape=(27,27,1))
x = Conv2D(64, (3,3))(digit_input)
x = Conv2D(64, (3,3))(x)
x = MaxPooling2D((2,2))(x)
out = Flatten()(x)

vision_model = Model(digit_input, out)

digit_a = Input(shape=(27,27,1))
digit_b = Input(shape=(27,27,1))

out_a = vision_model(digit_a)
out_b = vision_model(digit_b)

concatenated = keras.layers.concatenate([out_a, out_b])
out = Dense(1, activation='sigmoid')(concatenated)
classification_model = Model([digit_a, digit_b], out)
```

## 关于Keraas模型

Keras有两种类型的模型，序贯模型（Sequential）和函数时模型（Model），函数式模型应用更为广泛，序贯模型时函数式模型的一种特殊情况。

两类模型有一些方法时相同的：

- ```model.summary()```：打印出模型概况
- ```model.get_config()```：返回包含模型配置信息的Python字典。模型也可以从它的config信息中重构回去

```python
config = model.get_config()
model = Model.from_config(config)
# or, for Sequential
model = Sequential.from_config(config)
```

- ```model.get_layer()```：依据层名或下标获得层对象
- ```model.get_weights()```：返回模型权重张量的列表，类型为numpy array
- ```model.set_weights()```：从numpy array里将权重载入给模型，要求数组具有与`model.get_weights()`相同的形状
- `model.to_json()`：返回代表模型的JSON字符串，仅包含网络结构，不包含权值。可以从JSON字符串中重构原模型：

```python
from models import model_from_json
json_string = model.to_json()
model = model_from_json(json_string)
```

- `model.to_yaml()`：与`model.to_json()`类似

- ```model.save_weights(filepath)```：将模型权重保持到指定的路径，文件类型时HDF5，后缀名是.h5
- ```model.load_weights(filepath, by_name=False)```：从HDF5文件中加载权重到当前模型中，默认情况下模型的结构不变。如果想将权重载入不同的模型（有些层相同），则设置```by_name=True```，只有名字匹配的层才开载入权重










