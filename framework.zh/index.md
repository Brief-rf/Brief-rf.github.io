# 制作自己的jar并用shell调用

# 推送第三方jar至/system/framework

## 1.工具

* 安卓手机
* AIDE软件
* MT管理器
* Termux软件

## 2.教程

* 打开AIDE，创建一个java项目。我命名为TestShell

![Screenshot_20200313-132524](https://gitee.com//Brief-rf/BlogImages/raw/master/img/Screenshot_20200313-132524.jpg)

* 项目新建后会自动生成Main.Java，因为仅供测试，便不再做改动，直接点击右上角的运行按钮编译运行，控制台会打印“hellow world”和让你输入数字。

![Screenshot_20200313-133009](https://gitee.com//Brief-rf/BlogImages/raw/master/img/Screenshot_20200313-133009.jpg)

* 用MT文件管理器打开项目所在文件夹，进入TestShell/bin/release/dex/,会有下图中的目录和文件，classes.dex.zip和oat/arm64/目录下的classes.dex.odex、classes.dex.vdex的这三个文件就是所需要的。

![Screenshot_20200313-133112](https://gitee.com//Brief-rf/BlogImages/raw/master/img/Screenshot_20200313-133112.jpg)

* 将classes.dex.zip重命名为TS.jar,用re管理器复制到/system/framework下，修改权限为644 ；将classes.dex.odex、classes.dex.vdex分别改名为TS.odex和TS.vdex,复制到/system/framework/oat/arm64目录下，该权限为644

![Screenshot_20200313-133241](https://gitee.com//Brief-rf/BlogImages/raw/master/img/Screenshot_20200313-133241.jpg)

![Screenshot_20200313-133546](https://gitee.com//Brief-rf/BlogImages/raw/master/img/Screenshot_20200313-133546.jpg)

* 新建脚本，命名为ts ，脚本内容如下：

```shell
#!/system/bin/sh
base=/system 
export CLASSPATH=$base/framework/TS.jar
 
exec app_process $base/bin Main "$@"
```

* 将脚本复制到/system/bin下，修改权限为755。

![Screenshot_20200313-134029](https://gitee.com//Brief-rf/BlogImages/raw/master/img/Screenshot_20200313-134029.jpg)

* 打开终端模拟器，以root权限或系统用户权限运行runtest命令。

![Screenshot_20200313-134152](https://gitee.com//Brief-rf/BlogImages/raw/master/img/Screenshot_20200313-134152.jpg)


