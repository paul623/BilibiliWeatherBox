# 网络天气时钟小电视

本项目来自 [Network Weather Clock](https://gitee.com/taijichuangke/bilibili_weather_clock)





### 测试

2022年4月15日

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

| 绿色  | GND |     |
| --- | --- | --- |
| 黄色  | VCC |     |
| 紫色  | SCL | IO2 |
| 黑色  | SDA | IO0 |

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
    RES         接高
    D/C         接地
    CS          接地
```

arduino ide for esp的教程

http://www.taichi-maker.com/homepage/esp8266-nodemcu-iot/iot-c/nodemcu-arduino-ide/

## 说明

原作者教程写的已经非常详细了！该库只是备份用，如有侵权请立刻联系我，我会删除该库。

新玩具+1

## 迁移施工

### 实时天气预报

S6

```JSON
{
    "HeWeather6":[
        {
            "basic":{
                "cid":"CN101191306",
                "location":"Sucheng",
                "parent_city":"Suqian",
                "admin_area":"Jiangsu",
                "cnty":"China",
                "lat":"33.937725",
                "lon":"118.278984",
                "tz":"+8.00"
            },
            "update":{
                "loc":"2021-08-01 22:42",
                "utc":"2021-08-01 14:42"
            },
            "status":"ok",
            "now":{
                "cloud":"76",
                "cond_code":"104",
                "cond_txt":"Overcast",
                "fl":"31",
                "hum":"84",
                "pcpn":"0.0",
                "pres":"997",
                "tmp":"28",
                "vis":"6",
                "wind_deg":"90",
                "wind_dir":"E",
                "wind_sc":"2",
                "wind_spd":"9"
            }
        }
    ]
}
```

V7

```JSON
{
    "code":"200",
    "updateTime":"2021-08-01T22:42+08:00",
    "fxLink":"http://hfx.link/1tux1",
    "now":{
        "obsTime":"2021-08-01T22:28+08:00",
        "temp":"28",
        "feelsLike":"31",
        "icon":"154",
        "text":"Overcast",
        "wind360":"90",
        "windDir":"E",
        "windScale":"2",
        "windSpeed":"9",
        "humidity":"84",
        "precip":"0.0",
        "pressure":"997",
        "vis":"6",
        "cloud":"76",
        "dew":"26"
    },
    "refer":{
        "sources":[
            "Weather China"
        ],
        "license":[
            "no commercial use"
        ]
    }
}

```

三日预报

```json
{
    "code":"200",
    "updateTime":"2021-08-01T22:35+08:00",
    "fxLink":"http://hfx.link/1tux1",
    "daily":[
        {
            "fxDate":"2021-08-01",
            "sunrise":"05:18",
            "sunset":"19:08",
            "moonrise":"23:58",
            "moonset":"14:02",
            "moonPhase":"Waning crescent",
            "tempMax":"33",
            "tempMin":"25",
            "iconDay":"101",
            "textDay":"Cloudy",
            "iconNight":"305",
            "textNight":"Light Rain",
            "wind360Day":"148",
            "windDirDay":"SE",
            "windScaleDay":"1-2",
            "windSpeedDay":"7",
            "wind360Night":"45",
            "windDirNight":"NE",
            "windScaleNight":"1-2",
            "windSpeedNight":"3",
            "humidity":"93",
            "precip":"0.0",
            "pressure":"998",
            "vis":"23",
            "cloud":"16",
            "uvIndex":"11"
        },
        {
            "fxDate":"2021-08-02",
            "sunrise":"05:19",
            "sunset":"19:08",
            "moonrise":"00:00",
            "moonset":"14:02",
            "moonPhase":"Waning crescent",
            "tempMax":"30",
            "tempMin":"25",
            "iconDay":"305",
            "textDay":"Light Rain",
            "iconNight":"101",
            "textNight":"Cloudy",
            "wind360Day":"45",
            "windDirDay":"NE",
            "windScaleDay":"1-2",
            "windSpeedDay":"3",
            "wind360Night":"45",
            "windDirNight":"NE",
            "windScaleNight":"1-2",
            "windSpeedNight":"3",
            "humidity":"95",
            "precip":"4.7",
            "pressure":"1002",
            "vis":"24",
            "cloud":"78",
            "uvIndex":"6"
        },
        {
            "fxDate":"2021-08-03",
            "sunrise":"05:19",
            "sunset":"19:07",
            "moonrise":"00:31",
            "moonset":"14:59",
            "moonPhase":"Waning crescent",
            "tempMax":"31",
            "tempMin":"26",
            "iconDay":"101",
            "textDay":"Cloudy",
            "iconNight":"101",
            "textNight":"Cloudy",
            "wind360Day":"45",
            "windDirDay":"NE",
            "windScaleDay":"1-2",
            "windSpeedDay":"3",
            "wind360Night":"90",
            "windDirNight":"E",
            "windScaleNight":"1-2",
            "windSpeedNight":"3",
            "humidity":"96",
            "precip":"0.0",
            "pressure":"1003",
            "vis":"24",
            "cloud":"7",
            "uvIndex":"10"
        }
    ],
    "refer":{
        "sources":[
            "Weather China"
        ],
        "license":[
            "no commercial use"
        ]
    }
}


```

```c++
void HeFeng::fans(HeFengCurrentData *data, String id) {  //获取粉丝数
  std::unique_ptr<BearSSL::WiFiClientSecure>client(new BearSSL::WiFiClientSecure);
  client->setInsecure();
  HTTPClient https;
  //String url = "https://api.bilibili.com/x/relation/stat?vmid=" + id;
  //https://api.spencerwoo.com/substats/?source=zhihu&queryKey=
  String url = "https://api.spencerwoo.com/substats?source=coolapk&queryKey=" + id;
  Serial.print("[HTTPS] begin...zhihu\n");
  if (https.begin(*client, url)) {  // HTTPS
    // start connection and send HTTP header
    int httpCode = https.GET();
    // httpCode will be negative on error
    if (httpCode > 0) {
      // HTTP header has been send and Server response header has been handled
      Serial.printf("[HTTPS] GET... code: %d\n", httpCode);

      if (httpCode == HTTP_CODE_OK || httpCode == HTTP_CODE_MOVED_PERMANENTLY) {
        String payload = https.getString();
        Serial.println(payload);
        DynamicJsonDocument  jsonBuffer(2048);
        deserializeJson(jsonBuffer, payload);
        JsonObject root = jsonBuffer.as<JsonObject>();

        //String follower = root["data"]["follower"];
        //totalSubs
        String follower = root["data"]["totalSubs"];
        data->follower = follower;
      }
    } else {
      Serial.printf("[HTTPS] GET... failed, error: %s\n", https.errorToString(httpCode).c_str());
      data->follower = "-1";
    }

    https.end();
  } else {
    Serial.printf("[HTTPS] Unable to connect\n");
    data->follower = "-1";
  }
}
```
