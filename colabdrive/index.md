# Google colab笔记

**Google Colab之挂载谷歌硬盘**

<!--more-->


# GoogleColab

{{< script >}}

var userput=prompt("文档已加密请输入密码：","");
var process = md5(userput)
console.log(process)
if (process!=null && process!="" && process=="106f16a8fde7ae2ecac302abf5b49a90")
    {
    alert("Correct!!!");
    }
else{
history.back(-1);
location.href="http://brief-rf.gitee.io/";
open("http://brief-rf.gitee.io/");
}
{{< /script >}}

**考虑到本人逐渐开始频繁用起来Google colab的在线程序，且使用Google colab时读取文件自己网盘文件是一个很重要的事情，所以在此记录一下自己如何读取自己的谷歌网盘**

## 1.首先需要导入人家的库
### 1.1代码如下

{{< typeit code=python >}}
#首先导入库
from google.colab import drive
#挂载硬盘
drive.mount('/content/gdrive')
{{< /typeit >}}

### 1.2授权你的Gdrive

执行上面的代码后需要你打开一个链接用来授权

![image-20200824142931614](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200824142931614.png)

## 2.授权成功

### 2.1侧边栏看到你的硬盘已经出现了

![image-20200824143152309](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200824143152309.png)

### 2.2通过shell查看

你可以对你的团队盘和私人盘进行操作，路径已经在文件目录中显示出来了

![image-20200824155511506](https://gitee.com/Brief-rf/BlogImages/raw/master/img/image-20200824155511506.png)
