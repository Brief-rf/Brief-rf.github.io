# 搭建自己的云端IDE


# 服务器搭建code server

本篇教程所用到的是[阿里云](https://www.alibabacloud.com/zh)的服务器1m带宽，2核，4g运存

## 1.拥有一个自己的服务器

![](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620181229321.png)

系统选择ubuntu最新的就行

# 2.下载对应的code server文件

[点击这里](https://github.com/cdr/code-server/releases/tag/3.4.1)查看不同版本的code server

![image-20200620184128389](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620184128389.png)

- 服务器是ubuntu系统，这里我们选择[code-server-3.4.1-linux-x86_64.tar.gz](https://github.com/cdr/code-server/releases/download/3.4.1/code-server-3.4.1-linux-x86_64.tar.gz)

- 有多种将文件下载到服务器的方法，这里我选择将文件下载到本地，然后通过sftp上传到服务器

- 关于***ssh远程连接服务器***，请自行谷歌，这里不进行讲述

**将文件下载到桌面上**

```powershell
//在连接好服务器后，输入下面的命令将文件上传到服务器的root目录下
put C:\Users\lenovo\Desktop\code-server-3.4.1-linux-x86_64.tar.gz /root/
```

**ssh连接到服务器**

```shell
#输入下面的命令解压文件
tar -xzf code-server-3.4.1-linux-x86_64.tar.gz
```

![image-20200620185239264](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620185239264.png)

```shell
#进入code-server-3.4.1-linux-x86_64文件夹下后执行下面的代码查看帮助信息
./code-server -h
```

![image-20200620185507091](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620185507091.png)

```shell
#直接输入指令
./code-server
#即可启动codeserver
```

启动成功后会出现下面的信息：

![](https://img-blog.csdnimg.cn/20191027145819263.png)

这个时候你在你的浏览器输入你服务器的公网ip+端口8080，回车

你会发现

![image-20200620203623149](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620203623149.png)

如何解决呢？

## 3.阿里云服务器设置

- 打开**本实例安全组**

![image-20200620203808252](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620203808252.png)

- 点击**配置规则**

![image-20200620203909885](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620203909885.png)

- 点击**手动添加**，添加一条规则，内容如红色方框中的一样

![image-20200620203947591](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620203947591.png)

接下来你在你的浏览器输入你服务器的公网ip+端口8080，回车

你会发现

![image-20200620203623149](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620203623149.png)

**<u>为什么呢？？？</u>**

**<u>code-server默认只能够监听本地地址，也就是 127.0.0.1</u>**

如果想要远程监控则需要添加一些参数

```shell
#命令如下
./code-server --host 0.0.0.0 --port 8080
# --host 监听地址
# --port 监听端口

#查看登陆密码
cat ~/.config/code-server/config.yaml
#如果你嫌密码难记可以自定义密码，下面那样的代码就可以实现
export PASSWORD="sixsixsix" && code-server --host 0.0.0.0 --port 8080
```

执行这命令后，你在你的浏览器输入你服务器的公网ip+端口8080

**你会发现，终于TMD能用了**

![image-20200620205510945](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200620205510945.png)

## 4.后台运行

当你断开ssh连接之后，你会发现你连接不上服务器了。因为终端断掉项目就终止运行了。

这里提供一个方法：screen

```shell
#开启新会话
screen -S myCodeserver   # myCodeserver可以随便命名，执行后你会进入一个新的窗口
cd code-server           # 进入可执行文件的目录
export PASSWORD="sixsixsix" && code-server --host 0.0.0.0 --port 8080 #执行代码启动code server
```

+ ***按住ctrl+A+D 退出创建的screen***
+ ***输入指令：screen -ls，即可查看所有的screen***
+ ***想要恢复某个screen，指令为screen -r screen名***

具体想了解screen命令的[点我](https://wangchujiang.com/linux-command/c/screen.html)

## 5.结语

以上就是我服务器创建code server过程，其中踩了不少坑，希望对渴求知识的你有所帮助^_^

总结要用到的命令就是：

- ```shell
  export PASSWORD="sixsixsix" && code-server --host 0.0.0.0 --port 8080
  ```

- ```shell
  cat ~/.config/code-server/config.yaml
  ```
