# 全连接网络


**keras全连接层实例**

<!--more-->

## 全连接网络

### 1.1 Sequential模型

#### 1.1.1 Binary classification

```python
from keras.layers import Dense, Dropout
from keras.models import Sequential
from keras.utils import to_categorical
import numpy as np
# 生成numpy数据
datas = np.random.random((1000,100))
labels = np.random.randint(2, size=(1000,1))


def myNet(input_dim=100, class_num=1):
    model = Sequential()
    model.add(Dense(32, activation='relu', input_dim=input_dim))
    model.add(Dropout(0.5))
    model.add(Dense(class_num, activation='sigmoid'))
    return model

model = myNet()
model.summary()
model.compile(loss='binary_crossentropy',
              optimizer='rmsprop',
              metrics=['accuracy'])
model.fit(datas, labels, batch_size=8, epochs=50)
```

#### 1.1.2 Categorical classification

```python
from keras.layers import Dense, Dropout
from keras.models import Sequential
from keras.utils import to_categorical
import numpy as np
# 生成numpy数据
datas = np.random.random((1000,100))
labels = np.random.randint(10, size=(1000,1))
# one-hot 编码
labels = to_categorical(labels, num_classes=10)

def myNet(input_dim=100, class_num=10):
    model = Sequential()
    model.add(Dense(32, activation='relu', input_dim=input_dim))
    model.add(Dropout(0.5))
    model.add(Dense(class_num, activation='softmax'))
    return model

model = myNet()
model.summary()
model.compile(loss='categorical_crossentropy',
              optimizer='rmsprop',
              metrics=['accuracy'])
model.fit(datas, labels, batch_size=8, epochs=50)
```

### 1.2 Functional模型

#### 1.2.1 Binary classification

```python
from keras.layers import Dense, Dropout, Input
from keras.models import Model
from keras.utils import to_categorical
import numpy as np

# 生成numpy数据
datas = np.random.random((1000,100))
labels = np.random.randint(10, size=(1000,1))

def myNet(input_dim=100, class_num=1):
    inputs = Input(shape=(input_dim,))
    x = Dense(64, activation='relu')(inputs)
    x = Dropout(0.5)(x)
    x = Dense(32, activation='relu')(x)
    x = Dropout(0.5)(x)
    prediction = Dense(class_num, activation='sigmoid')(x)
    model = Model(inputs=inputs, outputs=prediction)

    return model

model = myNet()
model.summary()
model.compile(loss='binary_crossentropy',
              optimizer='rmsprop',
              metrics=['accuracy'])
model.fit(datas, labels, batch_size=8, epochs=50)
```

#### 1.2.2 Categorical classification

```python
from keras.layers import Dense, Dropout, Input
from keras.models import Model
from keras.utils import to_categorical
import numpy as np

# 生成numpy数据
datas = np.random.random((1000,100))
labels = np.random.randint(10, size=(1000,1))
# one-hot 编码
labels = to_categorical(labels, num_classes=10)

def myNet(input_dim=100, class_num=10):
    inputs = Input(shape=(input_dim,))
    x = Dense(64, activation='relu')(inputs)
    x = Dropout(0.5)(x)
    x = Dense(32, activation='relu')(x)
    x = Dropout(0.5)(x)
    prediction = Dense(class_num, activation='softmax')(x)
    model = Model(inputs=inputs, outputs=prediction)

    return model

model = myNet()
model.summary()
model.compile(loss='categorical_crossentropy',
              optimizer='rmsprop',
              metrics=['accuracy'])
model.fit(datas, labels, batch_size=8, epochs=50)
```

简单的数据验证：

```python
x_test = np.random.random(size=(20, 100, 100, 3))
y_test = np.random.randint(10, size=(20, 1))

# Returns the loss value & metrics values for the model in test mode
loss, accuracy = model.valuate(x_test, y_test)
print("损失值：", loss)
print("准确率：", accuracy)
```

简单的数据预测：

```python
# Generates output predictions for the input samples.
x_test = np.random.random(size=(20, 100, 100, 3))
y_pred = model.predict(X_test,batch_size = 1)
print(y_pred)
```


