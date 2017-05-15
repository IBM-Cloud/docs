---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Weather 套件
{: #openwhisk_catalog_weather}

`/whisk.system/weather` 套件提供一種簡便的方式來呼叫 Weather Company Data for IBM Bluemix API。

該套件包含下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | 套件 | username、password | Weather Company Data for IBM Bluemix API 的服務  |
| `/whisk.system/weather/forecast` | 動作 | latitude、longitude、timePeriod | 指定時段的預報|

建議使用 `username` 及 `password` 值來建立套件連結。如此，您就不需要每次在呼叫套件中的動作時都指定認證。

## 取得某個位置的天氣預報
{: #openwhisk_catalog_weather_forecast}

`/whisk.system/weather/forecast` 動作會從 The Weather Company 呼叫 API，以傳回某個位置的天氣預報。參數如下所示：

- `username`：獲授權呼叫預報 API 的 The Weather Company Data for IBM Bluemix 的使用者名稱。
- `password`：獲授權呼叫預報 API 的 The Weather Company Data for IBM Bluemix 的密碼。
- `latitude`：位置的緯度座標。
- `longitude`：位置的經度座標。
- `timePeriod`：預報的時段。有效選項為 '10day' -（預設值）傳回 10 天的每日預報、'48hour' - 傳回 2 天的每小時預報、'current' - 傳回目前的天氣狀況、'timeseries' - 傳回目前的觀察，以及從目前日期和時間算起，過去最多 24 小時的觀察。


下列範例說明如何建立套件連結，然後取得 10 天預報。

1. 使用 API 金鑰建立套件連結。
  
  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}
  
2. 在套件連結中呼叫 `forecast` 動作，以取得天氣預報。
  
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
  
