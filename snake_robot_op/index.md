# 关于蛇形机器人使用说明


## 1.准备工作

机器人通过wifi进行数据传输包括视频画面和传感器数据

- 树莓派上电
- 默认情况下树莓派开机后会自动连接Brie名称的wifi
- 查看树莓派ip地址（在terminal中 输入```ifconfig```回车 即可查看）

至此，准备工作完成

## 2.启动服务

无论何种方法，只要能将树莓派路径```~/sessions.sh```执行即可启动所有所需服务

所需服务：

假设树莓派IP地址为```192.168.43.7```

- 控制活动 ```Address:192.168.43.7:8001```
- 信息检测 ```Address:192.168.43.7:8686```
- 视频输出 ```Address:http://192.168.43.7:8080/?action=stream```

## 3.详细说明

在linux系统中想要执行多个命令或者在后台执行一些命令的话可以使用```nohup```或```screen```，本机器人采用的是```screen```方案。

在路径```~/sessions.sh```文件，内容写的是分别启动三个screen，名称分别为 ```camera | info | control```

| 名称    | 代码                                                         |
| :-------: | :------------------------------------------------------------: |
| camera  | ```cd /home/pi/webCam/Pan-Tilt_HAT_code/RaspberryPi/web_Python/mjpg-streamer/mjpg-streamer-experimental/ && sudo ./start.sh``` |
| info    | ```/usr/bin/python3 -u /home/pi/code/infoCode/DTH11_run.py``` |
| control | ```/usr/bin/python3 -u /home/pi/code/runCode/web_Python/main.py``` |

## 4.注意事项

1. 每次树莓派断开网连接后需要重新运行脚本来启动服务，并结合好树莓派的地址，否则将打不开网页！
2. 如果可以的话建议使用5GHz的WIFI，可使延迟做到很低，使用2.4GHz的WIFI画面可能卡顿。


