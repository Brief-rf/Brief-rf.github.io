# Markdown软件推荐

# Markdown写作软件推荐

## 1.WIN

### Typora

自从电脑开始写markdown笔记的时候我就开始用Typora了，刚开始用的时候还没有图片自动上传功能，几天之后软甲更新了，来看一下[官方文档](http://support.typora.io/Upload-Image/)吧！

刚开始我用的是Picgo app，但是用过几次后发现不稳定，所以我开始使用picgo-core通过gitee搭建自己的图床，在网上找了一些解决办法，然后配置测试，最终完成。下面讲解一下具体配置方法：

打开文件>偏好设置>图像，找到上传服务，选择picgo-core(command line)，首次需要下载。

![image-20200304093105330](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200304093105330.png)

打开命令提示符开始安装picgo

```powershell
npm install picgo -g
```

前提是你的电脑安装了[nodejs](https://nodejs.org/)才可以。

![image-20200304093713541](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200304093713541.png)

安装后输入：

```powershell
picgo -h
```

查看命令帮助

![image-20200304093806597](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200304093806597.png)

### 安装gitee插件

```powershell
picgo install gitee #安装gitee插件命令
picgo use #通过方向键选择gitee
```

选择gitee插件好后，打开配置文件

输入

```powershell
.picgo\config.json
```

![image-20200304094509297](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200304094509297.png)

配置信息填写如下：

```json
{
  "PICGO_ENV": "GUI",
  "needReload": false,
  "settings": {
    "showUpdateTip": true,
    "server": {
      "port": 36679,
      "host": "127.0.0.1",
      "enable": true
    },
    "shortKey": {
      "picgo:upload": {
        "enable": true,
        "key": "CommandOrControl+Shift+P",
        "name": "upload",
        "label": "快捷上传"
      }
    },
    "pasteStyle": "markdown"
  },
  "picBed": {
    "current": "gitee",
    "smms": true,
    "gitee": {
      "message": null,
      "owner": "gitee的账户名字",
      "path": "仓库中存放图片的文件夹",
      "repo": "仓库名字",
      "token": "你gitee的token",
      "url": "https://gitee.com/"
    }
  },
  "picgoPlugins": {
    "picgo-plugin-gitee": true
  },
  "debug": true
}
```

可以直接复制粘贴到你的配置文件中，然后保存关闭即可。

**注意** ，用typora测试图片上传的时候不要重复测试，因为第一次测试成功后你的仓库中已经有了测试的图片，再次测试会导致出错的，可以在typora里直接粘贴图片进行上传测试。

## 2.Android

安卓上推荐的软件是[MarkdownQ](https://www.coolapk.com/apk/com.dabai.markdownq)，软件可以在酷安里面找到

打开软件可以直接插入图片，从相册选择图片，链接选择类型为网络链接，这样你的图片会自动上传到smms图床上面

![123](https://gitee.com//Brief-rf/BlogImages/raw/master/img/123.jpg)

注意，由于软件内部smms的api已经过期了，需要把原来的api替换掉

新的api为

```
https://sm.ms/api/v2/upload/
```

下面是我替换好的

![1233](https://gitee.com//Brief-rf/BlogImages/raw/master/img/1233.jpg)

然后保存重新打包apk签名就可以安装使用了^_^
