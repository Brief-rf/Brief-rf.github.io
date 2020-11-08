# Android免费下载网易云VIP音乐

# Android免费下载网易云VIP音乐

这里介绍了三种方法，每种方法都有其优缺点，可以选择一种适合自己的方法使用。

## 方法一：修改手机代理

### 这种方法可以说是最简单的了，对手机没有什么要求，不需要使用什么工具，只需修改手机代理即可。

***打开wifi连接的详细设置界面***

***如图所示：***

![Screenshot_20200229-171344](https://gitee.com/Brief-rf/BlogImages/raw/master/img/Screenshot_20200229-171344.jpg)

***代理：*** 代理自动配置

***PAC网址：*** https://wy.ydlrqx.com/proxy.pac

然后点击保存，打开网易云音乐搜索想要听的歌曲就行了！

***！！！注意！！！*** 如果歌曲听完后需要将代理重新设置为无，不然无法上网！

## 方法二：安装xposed模块

### 这种方法对手机要求较高，需要手机安装有xposed框架或ed xposed框架。

安装[UnblockMusic Pro](https://www.lanzous.com/tp/i9ov06f)模块，并在框架中激活此模块。

![](https://gitee.com/Brief-rf/BlogImages/raw/master/img/qq_pic_merged_1582968176502.jpg)

***并在模块中配置好***

![](https://gitee.com/Brief-rf/BlogImages/raw/master/img/Screenshot_20200229-172201.jpg)

然后打开网易云音乐即可下载vip音乐了。

## 方法三：手机端搭建代理服务

### 此方法比前两种方法要麻烦的多，手机需要安装软件[Termux](https://www.coolapk.com/apk/com.termux)软件界面

***如图所示：***

![Screenshot_20200229-172957](https://gitee.com/Brief-rf/BlogImages/raw/master/img/Screenshot_20200229-172957.jpg)

依次输入下面的命令：

```shell
pkg undata
pkg upgrade
pkg install nodejs
git clone https://github.com/nondanee/UnblockNeteaseMusic.git
cd UnblockNeteaseMusic
node app.js
```

如图：

![](https://gitee.com/Brief-rf/BlogImages/raw/master/img/Screenshot_20200229-172957.jpg)

我的nodejs已经安装好了

![Screenshot_20200229-173333](https://gitee.com/Brief-rf/BlogImages/raw/master/img/Screenshot_20200229-173333.jpg)

![Screenshot_20200229-173547](https://gitee.com/Brief-rf/BlogImages/raw/master/img/Screenshot_20200229-173547.jpg)

然后手机上的代理服务搭建好了，接下来需要设置手机的代理

```
http://127.0.0.1:8080/proxy.pac
```

然后与方法一的配置都一样了，只不过PAC代理改为这个，剩下的这里就不再详细说了。

#### 至此，教程结束！！！


