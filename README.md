作者：于天源  YoneyY

## 短时预报

调用接口：http://aliv8.data.moji.com/whapi/json/aliweather/shortforecast

*请求方式：*POST

*返回类型：*JSON

传参

| 名称  | 类型   | 是否必须 | 描述                        |
| ----- | ------ | -------- | --------------------------- |
| lat   | STRING | 必选     | 纬度                        |
| lon   | STRING | 必选     | 经度                        |
| token | STRING | 可选     | 请求token（默认参数，必填） |

正常返回

```json
{
  "code": 0,
  "data": {
    "city": {
      "cityId": 284609,
      "counname": "中国",
      "name": "东城区",
      "pname": "北京市"
    },
    "sfc": {
      "banner": "您的位置，未来一小时不会下雨",
      "percent": [
        {
          "desc": "无雨",
          "icon": -1,
          "percent": 0
        },
        {
          "desc": "无雨",
          "icon": -1,
          "percent": 0
        },
          {
          "desc": "无雨",
          "icon": -1,
          "percent": 0
        }
      ],
      "sfCondition": 30,
      "timestamp": 1472740023000,
      "useLbs": 0
    }
  },
  "msg": "success",
  "rc": {
    "c": 0,
    "p": "success"
  }
}
```

## 未来15天天气

*调用地址：*http://aliv8.data.moji.com/whapi/json/aliweather/forecast15days

*请求方式：*POST

*返回类型：*JSON

传参

| 名称  | 类型   | 是否必须 | 描述                        |
| ----- | ------ | -------- | --------------------------- |
| lat   | STRING | 必选     | 纬度                        |
| lon   | STRING | 必选     | 经度                        |
| token | STRING | 可选     | 请求token（默认参数，必填） |

```json
{
  "code": 0,
  "data": {
    "city": {
      "cityId": 284609,
      "counname": "中国",
      "name": "东城区",
      "pname": "北京市"
    },
    "forecast": [
      {
        "conditionDay": "多云",
        "conditionIdDay": "1",
        "conditionIdNight": "31",
        "conditionNight": "多云",
        "moonphase": "WaningCrescent",
        "moonrise": "2016-08-31 04:19:00",
        "moonset": "2016-08-31 18:07:00",
        "predictDate": "2016-08-31",
        "sunrise": "2016-08-31 05:41:00",
        "sunset": "2016-08-31 18:47:00",
        "tempDay": "34",
        "tempNight": "18",
        "updatetime": "2016-08-31 23:07:06",
        "windDirDay": "北风",
        "windDirNight": "西北风",
        "windLevelDay": "3",
        "windLevelNight": "3",
        "windSpeedDay": "5.0",
        "windSpeedNight": "5.0"
      }
    ]
  },
  "msg": "success",
  "rc": {
    "c": 0,
    "p": "success"
  }
}
```

## 天气预报24小时

*调用地址：*http://aliv8.data.moji.com/whapi/json/aliweather/forecast24hours

*请求方式：*POST

*返回类型：*JSON

传参

| 名称  | 类型   | 是否必须 | 描述                        |
| ----- | ------ | -------- | --------------------------- |
| lat   | STRING | 必选     | 纬度                        |
| lon   | STRING | 必选     | 经度                        |
| token | STRING | 可选     | 请求token（默认参数，必填） |

```json
{
  "code": 0,
  "data": {
    "city": {
      "cityId": 284609,
      "counname": "中国",
      "name": "东城区",
      "pname": "北京市"
    },
    "hourly": [
      {
        "condition": "阴",
        "date": "2016-09-01",
        "hour": "20",
        "humidity": "51",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "21",
        "temp": "23",
        "uvi": "0",
        "windDir": "N",
        "windSpeed": "12"
      },
      {
        "condition": "阴",
        "date": "2016-09-01",
        "hour": "21",
        "humidity": "56",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "21",
        "temp": "22",
        "uvi": "0",
        "windDir": "NNW",
        "windSpeed": "11"
      },
      {
        "condition": "阴",
        "date": "2016-09-01",
        "hour": "22",
        "humidity": "60",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "20",
        "temp": "22",
        "uvi": "0",
        "windDir": "NNW",
        "windSpeed": "11"
      },
      {
        "condition": "阴",
        "date": "2016-09-01",
        "hour": "23",
        "humidity": "62",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "19",
        "temp": "21",
        "uvi": "0",
        "windDir": "NW",
        "windSpeed": "9"
      },
      {
        "condition": "阴",
        "date": "2016-09-02",
        "hour": "0",
        "humidity": "62",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "19",
        "temp": "21",
        "uvi": "0",
        "windDir": "NW",
        "windSpeed": "9"
      },
      {
        "condition": "阴",
        "date": "2016-09-02",
        "hour": "1",
        "humidity": "63",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "19",
        "temp": "21",
        "uvi": "0",
        "windDir": "NW",
        "windSpeed": "9"
      },
      {
        "condition": "阴",
        "date": "2016-09-02",
        "hour": "2",
        "humidity": "66",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "19",
        "temp": "20",
        "uvi": "0",
        "windDir": "NW",
        "windSpeed": "9"
      },
      {
        "condition": "阴",
        "date": "2016-09-02",
        "hour": "3",
        "humidity": "68",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "18",
        "temp": "19",
        "uvi": "0",
        "windDir": "NNW",
        "windSpeed": "9"
      },
      {
        "condition": "阴",
        "date": "2016-09-02",
        "hour": "4",
        "humidity": "68",
        "iconDay": "2",
        "iconNight": "2",
        "pressure": "0",
        "realFeel": "18",
        "temp": "19",
        "uvi": "0",
        "windDir": "NNW",
        "windSpeed": "9"
      }
    ]
  },
  "msg": "success",
  "rc": {
    "c": 0,
    "p": "success"
  }
}
```



## 天气实况

*调用地址：*http://aliv8.data.moji.com/whapi/json/aliweather/condition

*请求方式：*POST

*返回类型：*JSON

传参

| 名称  | 类型   | 是否必须 | 描述                        |
| ----- | ------ | -------- | --------------------------- |
| lat   | STRING | 必选     | 纬度                        |
| lon   | STRING | 必选     | 经度                        |
| token | STRING | 可选     | 请求token（默认参数，必填） |

```json
{
  "code": 0,
  "data": {
    "city": {
      "cityId": 284609,
      "counname": "中国",
      "name": "东城区",
      "pname": "北京市"
    },
    "condition": {
      "condition": "晴",
      "conditionId": "5",
      "humidity": "42",
      "icon": "30",
      "pressure": "999",
      "realFeel": "18",
      "sunRise": "2016-09-01 05:42:00",
      "sunSet": "2016-09-01 18:45:00",
      "temp": "24",
      "tips": "冷热适宜，感觉很舒适。",
      "updatetime": "2016-09-01 22:03:00",
      "uvi": "0",
      "windDir": "东北风",
      "windLevel": "2",
      "windSpeed": "2.45"
    }
  },
  "msg": "success",
  "rc": {
    "c": 0,
    "p": "success"
  }
}
```



![weather](https://github.com/YoneyY/vue-weather-demo/blob/master/weather.png?raw=true)



