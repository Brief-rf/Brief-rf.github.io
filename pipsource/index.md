# pip换源

**知识-笔记**

<!--more-->
## 1.国内源：

+ 清华：https://pypi.tuna.tsinghua.edu.cn/simple
+ 阿里云：https://mirrors.aliyun.com/pypi/simple/
+ 中国科技大学：https://pypi.mirrors.ustc.edu.cn/simple/
+ 华中理工大学：https://pypi.hustunique.com/
+ 山东理工大学：https://pypi.sdutlinux.org/
+ 豆瓣：https://pypi.douban.com/simple/

{{< admonition warning "注意" True >}}
新版ubuntu要求使用https源，要注意。
{{< /admonition >}}

## 2.临时使用

可以在使用pip的时候加参数`-i https://pypi.tuna.tsinghua.edu.cn/simple`
 例如：`pip install -i https://mirrors.aliyun.com/pypi/simple/ tensorflow`，这样就会从阿里云这边去安装库。

## 3.永久使用

在Linux下, 修改 `~/.pip/pip.conf` (没有就创建一个文件夹及文件。文件夹要加“.”，表示是隐藏文件夹)

内容如下：

```python
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host=mirrors.aliyun.com
```

windows下，直接在user目录中创建一个pip目录，再新建文件pip.ini。（例如：C:\Users\Administrator\pip\pip.ini）内容同上。
