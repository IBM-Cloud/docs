---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 例
{: #tutorials_samples}

以下の例を用いて、Insights for Weather サービスの使用方法を説明します。
{: shortdesc}

## Insights for Weather デモ
{: #insights_weather_demo}

サンプル・アプリケーションを使用すると、Insights for Weather サービスを使用して気象データを表示することができます。
このアプリケーションには、[http://insights-for-weather-demo.mybluemix.net/](http://insights-for-weather-demo.mybluemix.net/) にナビゲートしてアクセスできます。
ご使用のブラウザーでアプリケーションが開き、ユーザーの現在の位置をアプリケーションと共有するかどうかを尋ねられます。

サンプル・アプリケーションでは、現在の位置の気象についての、現在の観測された状態を表示できます。

![オンタリオ州オタワの現在の観測を示すメインスクリーンの画像。](images/twctestapp_main_screen.jpg "オンタリオ州オタワの現在の観測を示すメインスクリーンの画像。")

次の 24 時間についての毎時の予報および次の 10 日間についての毎日の予報を表示することもできます。サンプル内でこれらの領域にマウスのポインターを合わせると、API 呼び出しの結果が JSON 形式で表示されます。これには、データを取得するために使用されたメタデータが含まれています。

デモ・アプリケーションで、**「Bluemix にデプロイ」**をクリックして、アプリケーションの複製版を作成するか、[GitHub から直接、アプリを複製します](https://github.com/IBM-Bluemix/insights-for-weather-demo)。

## 標準の 10 日間の予報の取得
{: #getting_ten_day_forecast}

アプリケーションで `GET` 命令を発行して、10 日間の予報データを取得できます。
例えば、次の `GET` 要求を使用して、オンタリオ州オタワ (カナダ) の 10 日間の予報を取得できます。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/forecast/daily/10day?units=m&geocode=45.42%2C75.69&language=en-US
}
```

`username` と `password` は、アプリケーションとサービス・インスタンスごとに固有です。この情報は、`VCAP_SERVICES` 環境変数で確認できます。

サービスは、応答を JSON 形式で戻します。応答が正常である場合は、状況コード 200 が返されます。応答が正常ではない場合は、エラー・コードが返されます。

応答の本文には、メタデータおよび今後 10 日間の毎日の予報の配列が含まれています。例えば、メタデータには、以下のようなデータが含まれている可能性があります。

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1443712484194:-1546029161",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443714284,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

毎日の予報にはそれぞれ、指定された曜日 (`dow`) の 24 時間に適用される一般情報が含まれています。
例えば、毎日の予報には、以下のようなデータが含まれている可能性があります。

```
    {
      "class": "fod_long_range_daily",
      "expire_time_gmt": 1443714284,
      "fcst_valid": 1444525200,
      "fcst_valid_local": "2015-10-11T07:00:00+0600",
      "num": 11,
      "max_temp": 14,
      "min_temp": 4,
      "torcon": null,
      "stormcon": null,
      "blurb": null,
      "blurb_author": null,
      "lunar_phase_day": 28,
      "dow": "Sunday",
      "lunar_phase": "Waning Crescent",
      "lunar_phase_code": "WNC",
      "sunrise": "2015-10-11T07:07:25+0600",
      "sunset": "2015-10-11T18:19:57+0600",
      "moonrise": "2015-10-11T05:17:47+0600",
      "moonset": "2015-10-11T17:40:49+0600",
      "qualifier_code": null,
      "qualifier": null,
      "narrative": "Times of sun and clouds. Highs 13 to 15C and lows 3 to 5C.",
      "qpf": 0,
      "snow_qpf": 0,
      "snow_range": "",
      "snow_phrase": "",
      "snow_code": "",
      "night": {
      },
      "day": {
      }
    }
```

毎日の予報にはそれぞれ、指定された曜日の夜の部分と昼の部分が含まれています。
例えば、この両方の部分に、以下のような予報データが含まれている可能性があります。

```
      "night": {
        "fcst_valid": 1444568400,
        "fcst_valid_local": "2015-10-11T19:00:00+0600",
        "day_ind": "N",
        "thunder_enum": 0,
        "daypart_name": "Sunday night",
        "long_daypart_name": "Sunday night",
        "alt_daypart_name": "Sunday night",
        "thunder_enum_phrase": "No thunder",
        "num": 21,
        "temp": 4,
        "hi": 10,
        "wc": 3,
        "pop": 10,
        "icon_extd": 2900,
        "icon_code": 29,
        "wxman": "wx1650",
        "phrase_12char": "P Cloudy",
        "phrase_22char": "Partly Cloudy",
        "phrase_32char": "Partly Cloudy",
        "subphrase_pt1": "Partly",
        "subphrase_pt2": "Cloudy",
        "subphrase_pt3": "",
        "precip_type": "precip",
        "rh": 65,
        "wspd": 10,
        "wdir": 98,
        "wdir_cardinal": "E",
        "clds": 40,
        "pop_phrase": "",
        "temp_phrase": "Low 4C.",
        "accumulation_phrase": "",
        "wind_phrase": "Winds E at 10 to 15 km/h.",
        "shortcast": "Partly cloudy",
        "narrative": "A few clouds. Low 4C. Winds E at 10 to 15 km/h.",
        "qpf": 0,
        "snow_qpf": 0,
        "snow_range": "",
        "snow_phrase": "",
        "snow_code": "",
        "vocal_key": "D22:DA05:X3000300044:S300042:TL4:W04R02",
        "qualifier_code": null,
        "qualifier": null,
        "uv_index_raw": 0,
        "uv_index": 0,
        "uv_warning": 0,
        "uv_desc": "Low",
        "golf_index": null,
        "golf_category": ""
      },
```

## 標準の 24 時間の予報の取得
{: #getting_twenty_four_hour_forecast}

アプリケーションで `GET` 命令を発行して、24 時間の予報データを取得できます。
例えば、次の `GET` 要求を使用して、オンタリオ州オタワ (カナダ) の 24 時間の予報を取得できます。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/forecast/hourly/24hour?units=m&geocode=45.42%2C75.69&language=en-US
```

応答の本文には、メタデータおよび今後 24 時間の毎時の予報の配列が含まれています。例えば、メタデータには、以下のようなデータが含まれている可能性があります。

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1443722945280:-1956318185",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443723545,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

毎時の予報にはそれぞれ、`num` で指定された時間に適用される一般情報が含まれています。例えば、毎時の予報には、以下のようなデータが含まれている可能性があります。

```
    {
      "class": "fod_short_range_hourly",
      "expire_time_gmt": 1443723545,
      "fcst_valid": 1443726000,
      "fcst_valid_local": "2015-10-02T01:00:00+0600",
      "num": 1,
      "day_ind": "N",
      "temp": 12,
      "dewpt": 1,
      "hi": 12,
      "wc": 11,
      "feels_like": 11,
      "icon_extd": 3100,
      "wxman": "wx1550",
      "icon_code": 31,
      "dow": "Friday",
      "phrase_12char": "Clear",
      "phrase_22char": "Clear",
      "phrase_32char": "Clear",
      "subphrase_pt1": "Clear",
      "subphrase_pt2": "",
      "subphrase_pt3": "",
      "pop": 0,
      "precip_type": "rain",
      "qpf": 0,
      "snow_qpf": 0,
      "rh": 48,
      "wspd": 15,
      "wdir": 208,
      "wdir_cardinal": "SSW",
      "gust": null,
      "clds": 17,
      "vis": 16.1,
      "mslp": 1018.6,
      "uv_index_raw": 0,
      "uv_index": 0,
      "uv_warning": 0,
      "uv_desc": "Low",
      "golf_index": null,
      "golf_category": "",
      "severity": 1
    },
```

## 現在の条件の取得
{: #current_conditions}

アプリケーションで `GET` 命令を発行して、現在の気象条件を取得できます。
例えば、次の `GET` 要求を使用して、オンタリオ州オタワ (カナダ) の現在の気象条件を取得できます。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/observations/current?units=m&geocode=45.42%2C75.69&language=en-US
```

応答の本文には、メタデータおよび現在の観測気象データが含まれています。例えば、メタデータには、以下のようなデータが含まれている可能性があります。

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1443724606672:1993259329",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1443725206,
    "status_code": 200
  },
  "observation": {
  }
}
```

観測データには、一般情報および計測単位に固有の値が含まれています。
例えば、計測単位にメートル系が指定されている場合、現在の条件には、以下のようなデータが含まれている可能性があります。

```
  "observation": {
    "class": "observation",
    "expire_time_gmt": 1443725206,
    "obs_time": 1443724606,
    "obs_time_local": "2015-10-02T00:36:46+0600",
    "wdir": 210,
    "icon_code": 33,
    "icon_extd": 3300,
    "sunrise": "2015-10-02T06:55:47+0600",
    "sunset": "2015-10-02T18:36:42+0600",
    "day_ind": "N",
    "uv_index": 0,
    "uv_warning": 0,
    "wxman": "wx1550",
    "obs_qualifier_code": null,
    "ptend_code": 2,
    "dow": "Friday",
    "wdir_cardinal": "SSW",
    "uv_desc": "Low",
    "phrase_12char": "Fair",
    "phrase_22char": "Fair",
    "phrase_32char": "Fair",
    "ptend_desc": "Falling",
    "sky_cover": "Partly Cloudy",
    "clds": "FEW",
    "obs_qualifier_severity": null,
    "vocal_key": "OT53:OX3300",
    "metric": {
      "wspd": 13,
      "gust": null,
      "vis": 16.09,
      "mslp": 1018.7,
      "altimeter": 1018.63,
      "temp": 12,
      "dewpt": 3,
      "rh": 54,
      "wc": 11,
      "hi": 12,
      "temp_change_24hour": -16,
      "temp_max_24hour": 19,
      "temp_min_24hour": 6,
      "pchange": -1.02,
      "feels_like": 11,
      "snow_1hour": 0,
      "snow_6hour": 0,
      "snow_24hour": 0,
      "snow_mtd": null,
      "snow_season": null,
      "snow_ytd": null,
      "snow_2day": null,
      "snow_3day": null,
      "snow_7day": null,
      "ceiling": null,
      "precip_1hour": 0,
      "precip_6hour": 0,
      "precip_24hour": 0,
      "precip_mtd": null,
      "precip_ytd": null,
      "precip_2day": null,
      "precip_3day": null,
      "precip_7day": null,
      "obs_qualifier_100char": null,
      "obs_qualifier_50char": null,
      "obs_qualifier_32char": null
    }
  }
```






