# 通过shell命令启动活动

# 通过shell命令启动活动

+ 所用工具：mt管理器 钉钉

+ 闲着无聊，研究了一点关于am start命令目的为了启动某一项活动达到定时完成任务的目的

+ 具体参数：am start -n 包名/活动名
+ 通过mt管理器找到应用程序即可找到包名，通过mt管理器的Activity记录就能找到活动名

![](https://brief.wodemo.net/entry/528880/20200226/a83c531b169f27c9fb1395f48c0189da/Screenshot_20200213-094708.jpg)

![](https://i.loli.net/2020/02/26/RBAIvwMpig1XoEL.jpg)

+ 找到包名和活动名后打开mt管理器输入命令

  ```shell
  am start -n com.alibaba.android.rimet/com.alibaba.lightapp.runtime.activity.CommonWebViewActivity
  ```

  回车出现了一些错误“url不能为空”

![](https://i.loli.net/2020/02/26/QOxdY1UiupKDNob.jpg)

+ 通过网上搜索了解到am start传递网址的方法

+ 具体参数：am start -d url链接

+ 于是我准备通过抓包抓取钉钉的url链接，抓了一大堆网址试了几个不行，就懒得分析了。然后我又在钉钉里面找，找到了

![](https://i.loli.net/2020/02/26/lD7L1thUqyXM9zw.jpg)

+ 然后开始测试：输入命令

  ```shell
  am start -n com.alibaba.android.rimet/com.alibaba.lightapp.runtime.activity.CommonWebViewActivity -d https://landray.dingtalkapps.com/alid/app/report/home.html?corpid=ding114699f0a46bc4ac5d6980865&id=16ea1f906f2baa17d6a42ba896f3&skip=1&dd_from=qrcode&dd_progress=false&sourcefrom=immsg#/createRepor
  ```

  

+ 可以了，如果还想更加完善一点可以写个shell函数通过inputtap命令来模拟点击、inputswipe来模拟滑动，这里我就不详细讲解了
