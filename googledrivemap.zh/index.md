# GoogleDrive映射到本地

# GoogleTeamDrive映射到本地

## 1.工具安装工具

[rclone](https://rclone.org/downloads/)和[winsfp](https://github.com/billziss-gh/winfsp/releases)（Windows使用rclone必要插件）

## 2.配置工具

进入rclone所在文件夹，shift+鼠标右键在当前目录打开powershell（当然你也可以添加到你的环境变量里面，这里就不做演示了。）

输入命令：

```powershell
cmd
rclone.exe config
```

开始配置rclone

![image-20200308151338865](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200308151338865.png)

按n添加新配置，并为其命名(此处命名为GoogleDrive)

![image-20200308151441611](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200308151441611.png)

选择13，然后回车

![image-20200308151523358](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200308151523358.png)

到这里选择1

![image-20200308151606551](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200308151606551.png)

这里第一次直接回车，然后后面的选择n

然后会让你登陆你的谷歌账号登陆然后选择GoogleTeam就行了。

![image-20200308151848815](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200308151848815.png)

到这里我选择2

![image-20200308152003292](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200308152003292.png)

到这里基本上就可以了，输入y

![image-20200308152103480](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200308152103480.png)

输入q，然后会回车退出

## 3.挂载到本地

```powershell
rclone.exe mount Brief:/ j: —-vfs-cache-mode off
```

其中“Brief”是之前命名的网盘配置；“:/”代表挂载网盘根目录，你也可以“:/foldername/”来挂载网盘中的某个文件夹。—-vfs-cache-mode用来指定本地缓存，这里用“off”将其关闭，以测试网络传输真是速度。平时可以使用“writes”来启用缓存。配置完成后效果如下。

![image-20200308152404873](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200308152404873.png)

然后你就可以操作你的网盘了

**注：1PB=2(10) TB=1024TB**
