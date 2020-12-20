# Keras


**keras学习笔记（一）**

<!--more-->

## 1.Sequential

> 传递一个```input_shape```的关键字参数给第一层，```input_shape```是一个**tuple**类型的数据

**编译**：在模型训练前我们需要通过```compile```来对学习过程进行配置。```compile```接受三个参数：

- 优化器**optimizer**：如```rmsprop、adagrad```，或一个```Optimizer```类的对象，详情见optimizer
- 损失函数**loss**：该参数为模型视图最小化的目标函数，它可以为预定义的损失函数名，如```categorical_crossentropy、mse```，也可以为一个损失函数，详情见losses
- 指标列表**metrics**：对分类问题，一般将该列表设置为```metrics["accuracy"]```。指标可以是一个预定义指标的名字，也可以是一个用户定制的函数。指标函数应该返回单个张量，或一个完成```metric_mane -> metric_value```映射的字典，请参考性能评估。

```python
# for a multi-class calssfication problem
model.compile(optimizer='rmsprop',
             loss='categorical_crossentropy',
             metrics=['accuracy'])
# for a binary classfication problem
model.compile(optimizer='rmsprop',
             loss='binary_crossentropy',
             metrics=['accuracy'])
# for a mean squared error regression problem
model.compile(optimizer='rmsprop',
             loss='mse')
# For custom metrics
import keras.backend as K
def mean_pred(y_true, y_pred):
    return K.mean(y_pred)
model.compile(optimizer='rmsprop',
             loss='binary_crossentropy',
             metrics=['accuracy',mean_pred])
```

**训练**：

- Keras以*Numpy数组作为输入数据和标签的数据类型*。训练模型一般使用```fit```函数，下面是一些例子

```python
# for a single-input model with 2 classes (binary classification):
model = Sequential()
model.add(Dense(32,activation='relu',input_dim=100))
model.add(Dense(1,activation='sigmod'))
model.compile(optimizer='rmsprop',
             loss='binary_crossentropy',
             metrics=['accuracy'])
# Generate numpy data
import numpy as np
data = np.random.random((1000,100))
labels = np.random.randint(2, size=(1000, 1))
# Train the model, iterating on the data in batches of 32 samples
model.fit(data, labels, epochs=10, batch_size=32)
```

```python
# for a single-input model with 10 classes (categorical classification):
model = Sequential()
model.add(Dense(32, activation='relu', input_dim=100))
model.add(Dense(10, activation='softmax'))
model.compile(optimizer='rmsprop',
             loss='categorical_crossentropy',
             metrics=['accuracy'])
# Generate numpy data
import numpy as np
data = np.random.random((1000,100))
labels = np.random.randint(10, size=(1000, 1))
one_hot_labels = keras.utils.to_categorical(labels, num_classes=10)
model.fit(data, one_hot_labels, epochs=10, batch_size=32)
```

- 基于多层感知器的softmax多分类：

```python
from keras.models import Sequential
from keras.layers import Dense, Dropout, Activation
from keras.optimizers import SGD

#Generate numpy data
import numpy as np
x_train = np.random.random((1000,20))
y_train = keras.utils.to_categorical(np.ramdom.randint(10, size=(1000, 1)), num_classes=10)
x_test = np.random.random((100, 20))
y_test = keras.utils.to_categorical(np.ramdom.randint(10, size=(100, 1)), num_classes=10)

model = Sequential()
model.add(Dense(64, activation='relu', input_dim = 20))
model.add(Dropout(0.5))
model.add(Dense(64, activation='relu'))
model.add(Dropout(0.5))
model.add(Dense(10, activation='softmax'))

sgd = SGD(lr=0.01, decay=1e-6, momentum=0.9, nesterov=True)
model.compile(optimizer=sgd,
             loss='categorical_crossentropy',
             metrics=['accuracy'])
model.fit(x_train, y_train, epochs=50, batch_size=128)
score = model.evaluate(x_test, y_test, batch_size=128)
```

- MLP的二分类：

```python
import numpy as np
from keras.layers import Dense, Dropout
from keras.models import Sequential

#Generate numpy data
x_train = np.random.random((1000, 20))
y_train = np.random.randint(2, size=(1000,1))
x_test = np.random.random((100, 20))
y_test = np.random.randint(2, size=(100, 1))

model = Sequential()
model.add(Dense(64, activation='relu', input_dim=20))
model.add(Dropout(0.5))
model.add(Dense(64, activation='relu'))
model.add(Dropout(0.5))
model.add(Dense(1, activation='sigmoid'))

model.compile(loss='binary_crossentropy',
             optimizer='rmsprop',
             metrics=['accuracy'])
model.fit(x_train,y_train, epochs = 20, batch_size=128)
loss, accuracy = model.evaluate(x_test, y_test)
print(loss, accuracy)
```

- 类似VGG的卷积神经网络：

```python
import numpy as np
from keras.layers import Dense, Flatten
from keras.models import Sequential
from kreas.layers import Conv2D, MaxPooling2D
from keras.optimizers import SGD

# Generate numpy data
x_train = np.random.random(size=(100, 100, 100, 3))
y_train = np.random.randint(10, size=(100, 1))
y_train = keras.utils.to_categorical(y_train, num_classes=10)
x_test = np.random.random(size=(20, 100, 100, 3))
y_test = np.random.randint(10, size=(20, 1))
y_test = keras.utils.to_categorical(y_test, num_classes=10)

model = Sequential()
model.add(Conv2D(32, (3,3), activation='relu', input_shape=(100,100,3)))
model.add(Conv2D(32, (3,3), activation='relu'))
model.add(MaxPooling(pool_size=(2,2)))
model.add(Dropout(0.25))

model.add(Conv2D(64, (3,3), activation='relu'))
model.add(Conv2D(64, (3,3), activation='relu'))
model.add(MaxPooling(pool_size=(2,2)))
model.add(Dropout(0.25))

model.add(Flatten())
model.add(Dense(256, activation='relu'))
model.add(Dropout(0.5))
model.add(Dense(10, activation='softmax'))

sgd = SGD(lr=0.01, decay=1e-6, momentum=0.9, nesterov=True)
model.compile(optimizer=sgd,
             loss='categorical_crossentropy')
model.fit(x_train,y_train, epochs=10, batch_size=32)
score = model.evaluate(x_test, y_test)
print(score)
```


