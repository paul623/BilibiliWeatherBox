# 网络天气时钟小电视

本项目来自 [Network Weather Clock](https://gitee.com/taijichuangke/bilibili_weather_clock)

## 已知问题

目前三日预告解析失败，自己手动获取没问题，目前不知道哪里出错了。

由于我使用的是不带开发板的esp8266所以不太好调试，待解决。

和风天气我升级了个人开发者后就获取失败了，很奇怪。

[2021.08.01]另外这个版本我把定位固定了，根据ip定位很容易定位错

## 更换展示的源

源项目提供了展示bilibili的粉丝数，这个你可以改，我在项目中做的是知乎订阅者展示。

到HeFeng.cpp中的fans函数里配置一下就好，这个就不赘述了。

安利一下这个网站：https://substats.spencerwoo.com/#sponsoring

几乎支持了市面上大部分的粉丝数查看，但貌似有访问限制

所以我把更新频率改到了60分钟/次

毕竟暂也不用这么关心这些数据（没这么多人关注）

## 接线和备忘录

绿黄紫黑

SDC IO2

SDA IO0

| 绿色 | GND  |      |
| ---- | ---- | ---- |
| 黄色 | VCC  |      |
| 紫色 | SCL  | IO2  |
| 黑色 | SDA  | IO0  |

## ESP8266 TTL

刷固件的时候 ,注意IO0要接地

## 值得注意的地方

由于我是使用的esp8266开发板，所以端口不一样

连接的时候

```c
const int SDA_PIN = 0;  //引脚连接（原芯片GPIO0 口，对应显示屏的D0口，开发板上的D4口）
const int SDC_PIN = 2;  //（原芯片GPIO2 口，对应显示屏的D1口，开发板上的D3口）
```



oled显示屏购买

注意要买四引脚的（IIS连接！！！）

我比较坑买了七引脚的（中景园那款），而且默认连接方式是SPI，需要将电阻R3移动到R1上，并短接R8

下面引脚连接方式

```
    GND          地
    VCC          3.3V或者5V
    CLK（D0）   接D4
    DIN（D1）   接D3
    RES 		接高
    D/C         接地
    CS          接地
```



arduino ide for esp的教程

http://www.taichi-maker.com/homepage/esp8266-nodemcu-iot/iot-c/nodemcu-arduino-ide/

## 说明

原作者教程写的已经非常详细了！该库只是备份用，如有侵权请立刻联系我，我会删除该库。

新玩具+1
