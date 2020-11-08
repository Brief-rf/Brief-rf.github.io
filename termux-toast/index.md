# Termux-api之termux-toast

#### **官方的命令讲解**

```shell
Usage: 
    termux-toast [-b bgcolor] [-c color] [-g gravity] [-s] [text] 
    Show text in a Toast (a transient popup). 
    The text to show is either supplied as arguments or read from stdin if no arguments are given. 
     -h show this help 
     -b set background color (default: gray) 
     -c set text color (default: white) 
     -g set position of toast: [top, middle, or bottom] (default: middle) 
     -s only show the toast for a short while NOTE: color can be a standard name (i.e. red) or 6 / 8 digit hex value (i.e. "#FF0000" or "#FFFF0000") where order is (AA)RRGGBB. Invalid color will revert to default value
```

#### **翻译后:**

```shell
#使用：
    termux-toast [-b bgcolor] [-c color] [-g gravity] [-s] [text] 
    #在Toast中显示文本（瞬态弹出窗口）
    #要显示的文本要么作为参数提供，要么在未提供参数的情况下从标准输入读取。
     -h #展示这条帮助信息
     -b #设置背景颜色（默认：灰色） 
     -c #设置文本颜色（默认：白色） 
     -g #设置弹窗的位置【顶部，中部或者底部】（默认：中部） 
     -s #仅显示片刻吐司注意：颜色可以是标准名称（例如：红色、6/8位十六进制值）。无效的颜色将恢复为默认值
```

#### 示例：

##### 1.低级弹窗

```shell
#弹出Brief
termux-toast Brief #如果要弹出的信息中有空格，则需要加引号，否则空格后面的内容会被当作参数传递。
```

![termux-toast1](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-toast1.jpg)

##### 2.中级弹窗

```shell
#弹出Helo Brief
termux-toast -b yellow -c red -g bottom -s "Hello Brief"
    # -b yellow 设置背景颜色为黄色
    # -c red 设置文本颜色为红色
    # -g bottom 设置弹窗位置为底部
    # -s 显示时间比不加 -s 短一点点
```

![termux-toast2](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-toast2.jpg)

##### 3.高级弹窗

```shell
#弹出变量内容
num=520
termux-toast -b yellow -c red -g middle -s $num
termux-toast -b yellow -c red -g middle -s $RANDOM #随机弹出一串数字
```

![termux-toast3](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-toast3.jpg)

![termux-toast4](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-toast4.jpg)
