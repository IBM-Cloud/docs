---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Weather 包
{: #openwhisk_catalog_weather}

通过 `/whisk.system/weather` 包，可以方便地调用 Weather Company Data for IBM Bluemix API。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | 包 | username 和 password | 来自 Weather Company Data for IBM Bluemix API 的服务  |
| `/whisk.system/weather/forecast` | 操作 | latitude、longitude、timePeriod | 指定时间段的预报|

建议使用 `username` 和 `password` 值创建包绑定。这样就无需在每次调用包中的操作时指定这些凭证。

## 获取某个位置的天气预报
{: #openwhisk_catalog_weather_forecast}

`/whisk.system/weather/forecast` 操作通过从 The Weather Company 调用 API，返回某个位置的天气预报。参数如下所示：

- `username`：The Weather Company Data for IBM Bluemix 的用户名，此用户名有权调用预测 API。
- `password`：The Weather Company Data for IBM Bluemix 的密码，此密码有权调用预测 API。
- `latitude`：位置的纬度坐标。
- `longitude`：位置的经度坐标。
- `timePeriod`：预报的时间段。有效选项为：'10day' -（缺省值）返回 10 天的每日预报，'48hour' - 返回 2 天的每小时预报，'current' - 返回当前天气状况，'timeseries' - 返回当前观察数据和过去长达 24 小时（从当前日期和时间开始）的观察数据。


以下是创建包绑定并获取 10 天天气预报的示例。

1. 使用 API 密钥创建包绑定。
  
  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}
  
2. 调用包绑定中的 `forecast` 操作来获取天气预报。
  
  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
  ```
  {: pre}
  
  ```json
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  
