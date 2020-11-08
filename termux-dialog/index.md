# Termux-api之termux-dialog

#### **官方的命令讲解**

```shell
Usage: 
    termux-dialog widget [options] 
    Get user input w/ different widgets! 
    Default: text 
        -h, help Show this help 
        -l, list List all widgets and their options 
        -t, title Set title of input dialog (optional)
```

#### **翻译后**

```shell
#使用:
    termux-dialog widget [options]
    #获取用户输入的widget或者不同的widget
    #默认：文本
        -h, #展示这条帮助信息
        -l, #列出所有的widget和它们对应的options
        -t, #设置dialog的标题（非必须）
```

#### termux-dialog -l 讲解

```shell
Supported widgets: 
    confirm - Show confirmation dialog #显示确认信息
        [-i hint] text hint (optional) #需要提示的回答的文字
        [-t title] set title of dialog (optional) 
    checkbox - Select multiple values using checkboxes #使用复选框选择多个值
        [-v ",,,"] comma delim values to use (required) #使用逗号间隔
        [-t title] set title of dialog (optional) 
    counter - Pick a number in specified range #选择指定范围内的数字
        [-r min,max,start] comma delim of (3) numbers to use (optional) #使用3个数字确定范围
        [-t title] set title of dialog (optional) 
    date - Pick a date #选择一个日期
        [-t title] set title of dialog (optional) 
        [-d "dd-MM-yyyy k:m:s"] SimpleDateFormat Pattern for date widget output (optional) #设置输出格式
    radio - Pick a single value from radio buttons #从单选按钮中选择一个值
        [-v ",,,"] comma delim values to use (required) #使用逗号间隔
        [-t title] set title of dialog (optional) 
    sheet - Pick a value from sliding bottom sheet #从滑动底部表中选择一个值
    	[-v ",,,"] comma delim values to use (required) #使用逗号间隔
    	[-t title] set title of dialog (optional) 
    spinner - Pick a single value from a dropdown spinner #从下拉菜单中选择一个值
    	[-v ",,,"] comma delim values to use (required) 
    	[-t title] set title of dialog (optional) 
    speech - Obtain speech using device microphone #使用设备麦克风获取语音（可理解为文字转语音）
    	[-i hint] text hint (optional) #设置提示的文字
    	[-t title] set title of dialog (optional) 
    text - Input text (default if no widget specified) #输入文本
    	[-i hint] text hint (optional) #需要提示的文字
    	[-m] multiple lines instead of single (optional)* #多行文本内容 
    	[-n] enter input as numbers (optional)* #输入类型为数字
    	[-p] enter input as password (optional) #输入类型为密码
    	[-t title] set title of dialog (optional)  
```

#### 示例：

##### 1.confirm

```shell
termux-dialog confirm -i "Choose Yes or No" -t "Do you copy?"
```

![termux-dialog1](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog1.bmp)

```json
//选择yes
{
  "code": 0,
  "text": "yes",
  "index": 2
}
```

```json
//选择no
{
  "code": 0,
  "text": "no",
  "index": 2
}
```

##### 2.checkbox

```shell
termux-dialog checkbox -v "草莓,菠萝,香蕉,榴莲" -t "你喜欢吃哪些水果？"
```

![trmux-dialog2](https://gitee.com//Brief-rf/BlogImages/raw/master/img/trmux-dialog2.bmp)

```json
//仅选择香蕉
{
  "code": -1,
  "text": "[香蕉]",
  "index": 2,
  "values": [
    {
      "index": 2,
      "text": "香蕉"
    }
  ]
}
```

```json
//选择全部
{
  "code": -1,
  "text": "[草莓, 菠萝, 香蕉, 榴莲]",
  "index": 2,
  "values": [
    {
      "index": 0,
      "text": "草莓"
    },
    {
      "index": 1,
      "text": "菠萝"
    },
    {
      "index": 2,
      "text": "香蕉"
    },
    {
      "index": 3,
      "text": "榴莲"
    }
  ]
}
```

##### 3.counter

```shell
termux-dialog counter -r 1,120,18 -t "How old are you?"
```

![termux-dialog3](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog3.bmp)

```json
//选择19
{
  "code": -1,
  "text": "19",
  "index": 2
}
```

##### 4.date

```shell
termux-dialog date -t "2020年国庆日期：" -d "yyyy-MM-dd"
```

![termux-dialog4](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog4.bmp)

```json
//日期选择为2020年10月1日
{
  "code": -1,
  "text": "2020-10-01",
  "index": 2
}
```

##### 5.radio

```shell
termux-dialog radio -v "男生,女生" -t "你喜欢男生还是女生？"
```

![termux-dialog5](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog5.bmp)

```json
//选择女生
{
  "code": -1,
  "text": "女生",
  "index": 1
}
```

##### 6.sheet

```shell
termux-dialog sheet -v "月球,地球,火星" -t "你来自哪里？"
```

![termux-dialog6](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog6.bmp)

```json
//选择地球
{
  "code": 0,
  "text": "地球",
  "index": 1
}
```

##### 7.spinner

```shell
termux-dialog spinner -v "语文,综合,英语,数学" -t "高考第三门考什么？"
```

![termux-dialog7](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog7.bmp)

```json
//选择综合
{
  "code": -1,
  "text": "综合",
  "index": 1
}
```

##### 8.speech

```shell
termux-dialog speech -i "你叫什么名字呀？" -t "What is your name?"
```

![termux-dialog8](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog8.bmp)

```json
{
  "code": 0,
  "text": "布里啾啾底部里都", 
  "index": 1
}

```

##### 9.text

```shell
termux-dialog text -i "你的qq号码：" -t "提示信息" -n
```

![termux-dialog91](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog91.jpg)

```json
//输入我的qq号
{
  "code": -1,
  "text": "1053651085",
  "index": 1
}
```

```shell
termux-dialog text -i "你的qq密码：" -t "提示信息" -p
```

![termux-dialog92](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog92.jpg)

```json
{
  "code": -1,
  "text": "shazicaihuiqushi",
  "index": 1
}
```

```shell
termux-dialog text -i "写一篇10亿字的读后感：" -t "提示信息" -m
```

![termux-dialog93](https://gitee.com//Brief-rf/BlogImages/raw/master/img/termux-dialog93.jpg)

```json
{
  "code": -1,
  "text": "你\n在\n想\n屁\n吃",
  "index": 1
}
```

#### ***提取文本内容***

如果你不用jq来提取json字符转中text后面的内容，那么下面的一串代码将会帮助到你

```shell
#适用于大多情况
#弹出对话框，并将对话框的内容作为shell命令执行
termux-dialog -t "Enter shell command"|awk -F'"' '$2=/text/{print $4}'|bash
```




