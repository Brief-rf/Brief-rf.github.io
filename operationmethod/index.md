# 获取树莓派摄像头画面

**简单使用教程**

<!--more-->

主要有三个阶段：

1. 树莓派与手机或者电脑在同WiFi下
2. 连接树莓派
3. 执行树莓派上面的代码
4. 手机或者电脑接收视频画面

## 1.树莓派连接WiFi

通过键盘和鼠标，控制树莓派从而连接WiFi，连接成功之后**记住树莓派的ip地址(我这里是 192.168.0.123)，后面要用到**，然后手机也连接同一个WiFi

## 2.设备连接树莓派

**手机或者电脑控制树莓派有两种方法。设备与树莓派连接前提是要在同一个WiFi下，且要知道树莓派的IP地址**

### 2.1 ssh连接

```shell
#手机或者电脑在终端输入下面的命令    这里树莓派的ip地址是192.168.0.123
ssh pi@192.168.0.123
#第一次连接可能会让你输入yes或者no 输入yes然后回车就行
#然后就会让你输入密码。 密码是2053
pi@raspberrypi:~ $         #出现这个就说明连接成功了
```

![电脑连接树莓派](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926205046460.png "电脑连接树莓派")

#### 2.1.1然后执行命令：

```shell
bash /home/pi/Desktop/start.sh
```

#### 2.1.2出现下面这个就说明代码执行成功

![ssh操作](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926210636199.png "ssh操作")

### 2.2 VNC连接

#### 2.2.1 手机上或者电脑上安装vnc客户端

将树莓派的IP地址填写在如下图的地址栏，然后回车。连接需要输入用户名和密码

```shell
#用户名:pi
#密码:2053
```

![电脑vnc](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926205849511.png "电脑vnc")

#### 2.2.2 连接成功后的界面

![vnc](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926205956222.png "vnc")

之后你就可以通过鼠标或者键盘操作树莓派了

#### 2.2.3打开桌面上web_Python文件夹

如下图：

![操作](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926210410052.png "操作")

#### 2.2.4出现下面这种情况就说明代码执行成功

![vnc success](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926210456685.png "vnc success")

## 3.图像获取

确保是手机或者电脑与树莓派在同一个wifi下

### 3.1获取视频流

http://192.168.0.123:8080/?action=stream 

![stream](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926204922914.png "stream")

### 3.2 控制+视频

在电脑浏览器地址栏输入下面的网址：

http://192.168.0.123:8001/

![control&video](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926204848627.png "control&video")



### 3.3 获取图片

在电脑浏览器地址栏输入下面的网址：

http://192.168.0.123:8080/?action=snapshot

![pic](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926204938647.png "pic")

### 3.4更多控制参数

http://192.168.0.123:8080/java.html

![detail](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200926212211980.png "detail")









