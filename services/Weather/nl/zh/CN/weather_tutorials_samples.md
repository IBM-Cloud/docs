---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 示例
{: #tutorials_samples}

通过以下示例了解如何使用 {{site.data.keyword.weather_short}} 服务。
{: shortdesc}

## {{site.data.keyword.weather_short}} 演示
{: #insights_weather_demo}

您可以通过尝试使用 [{{site.data.keyword.weather_short}} 演示应用程序](http://weather-company-data-demo.{APPDomain}){: new_window}来确定如何通过 {{site.data.keyword.weather_short}} 服务检索天气数据。
应用程序会在浏览器中打开，并询问您是否要与将您的当前位置与该应用程序共享。

在演示应用程序中，可以查看观察到的您所在位置的最新天气状况。

![包含安大略省渥太华最新观察数据的主屏幕图像。](images/twctestapp_main_screen.jpg "包含安大略省渥太华最新观察数据的主屏幕图像。")

您还可以查看未来 48 小时的每小时天气预测以及未来 10 天的每天天气预测。每天天气预报显示白天天气和夜间天气。
如果在演示应用程序中单击各个区域，可以查看 JSON 格式的 API 调用结果，包括用于检索数据的元数据。

在演示应用程序中，单击**部署到 Bluemix** 以创建应用程序的克隆版本，或者[直接从 GitHub 克隆应用程序](https://github.com/IBM-Bluemix/weather-company-data-demo)。

## 获取每小时天气预测
{: #getting_twenty_four_hour_forecast}

您可以在应用程序中发出 `GET` 操作来检索 48 小时的天气预测数据。

`username` 和 `password` 对于您的应用程序和服务实例是唯一的。您可以在 `VCAP_SERVICES` 环境变量中找到这些信息。

服务将返回 JSON 格式的响应。如果响应成功，将返回状态码 200。如果响应失败，将返回错误代码。

例如，可以使用以下 `GET` 请求来检索加拿大安大略省渥太华经度和纬度坐标 48 小时的天气预测：

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/forecast/hourly/48hour.json?units=m&language=en-US
```
您还可以在应用程序中发出 `GET` 操作来检索邮政编码的 48 小时天气预测数据。**注**：您仅可以提供受支持国家或地区代码美国 (US)、英国 (GB)、法国 (FR)、德国 (DE) 或意大利 (IT) 的邮政编码。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/location/97229%3A4%3AUS/forecast/hourly/48hour.json?units=m&language=en-US
```

响应主体包含元数据和大量未来 48 小时每小时的天气预测。例如，元数据可能包含以下数据：

```
{
  "metadata": {"language": "en-US",
    "transaction_id": "1467041322756:187065199",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1467041562,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

每小时天气预测包含适用于 `num` 所指定的小时的常规信息。例如，每小时天气预测可能包含以下数据：

```
   {
      "class": "fod_short_range_hourly",
      "expire_time_gmt": 1467041922,
      "fcst_valid": 1467043200,
      "fcst_valid_local": "2016-06-27T22:00:00+0600",
      "num": 1,
      "day_ind": "N",
      "temp": 21,
      "dewpt": 12,
      "hi": 21,
      "wc": 21,
      "feels_like": 21,
      "icon_extd": 2900,
      "wxman": "wx1600",
      "icon_code": 29,
      "dow": "Monday",
      "phrase_12char": "P Cloudy",
      "phrase_22char": "Partly Cloudy",
      "phrase_32char": "Partly Cloudy",
      "subphrase_pt1": "Partly",
      "subphrase_pt2": "Cloudy",
      "subphrase_pt3": "",
      "pop": 0,
      "precip_type": "rain",
      "qpf": 0,
      "snow_qpf": 0,
      "rh": 56,
      "wspd": 11,
      "wdir": 291,
      "wdir_cardinal": "WNW",
      "gust": null,
      "clds": 31,
      "vis": 16,
      "mslp": 1008.73,
      "uv_index_raw": 0,
      "uv_index": 0,
      "uv_warning": 0,
      "uv_desc": "Low",
      "golf_index": null,
      "golf_category": "",
      "severity": 1
    },
```

## 获取每天天气预测
{: #getting_ten_day_forecast}

您可以在应用程序中发出 `GET` 操作来检索 10 天的天气预测数据。例如，可以使用以下 `GET` 请求来检索加拿大安大略省渥太华 10 天的天气预测：

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/forecast/daily/10day.json?units=m&language=en-US
```

响应主体包含元数据和大量未来 10 天每天的天气预测。例如，元数据可能包含以下数据：

```
{
  "metadata": {"language": "en-US",
    "transaction_id": "1467041740847:-1868497945",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1467043540,
    "status_code": 200
  },
  "forecasts": [
  ]
}
```

每天天气预测包含适用于一周指定天 (`dow`) 的 24 小时时间段的常规信息。例如，每天天气预测可能包含以下数据：

```
"class": "fod_long_range_daily",
      "expire_time_gmt": 1467043540,
      "fcst_valid": 1467075600,
      "fcst_valid_local": "2016-06-28T07:00:00+0600",
      "num": 2,
      "max_temp": 29,
      "min_temp": 18,
      "torcon": null,
      "stormcon": null,
      "blurb": null,
      "blurb_author": null,
      "lunar_phase_day": 22,
      "dow": "Tuesday",
      "lunar_phase": "Last Quarter",
      "lunar_phase_code": "LQ",
      "sunrise": "2016-06-28T05:11:23+0600",
      "sunset": "2016-06-28T20:49:39+0600",
      "moonrise": "2016-06-28T00:56:48+0600",
      "moonset": "2016-06-28T13:39:37+0600",
      "qualifier_code": null,
      "qualifier": null,
      "narrative": "Mainly sunny. Highs 28 to 30C and lows 17 to 19C.",
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

每天天气预测包含一周指定天的日段和夜段。例如，这两个部分可能包含以下天气预测数据：

```
"night": {
        "fcst_valid": 1467118800,
        "fcst_valid_local": "2016-06-28T19:00:00+0600",
        "day_ind": "N",
        "thunder_enum": 0,
        "daypart_name": "Tomorrow night",
        "long_daypart_name": "Tuesday night",
        "alt_daypart_name": "Tuesday night",
        "thunder_enum_phrase": "No thunder",
        "num": 3,
        "temp": 18,
        "hi": 26,
        "wc": 18,
        "pop": 0,
        "icon_extd": 3100,
        "icon_code": 31,
        "wxman": "wx1500",
        "phrase_12char": "Clear",
        "phrase_22char": "Clear",
        "phrase_32char": "Clear",
        "subphrase_pt1": "Clear",
        "subphrase_pt2": "",
        "subphrase_pt3": "",
        "precip_type": "rain",
        "rh": 43,
        "wspd": 15,
        "wdir": 55,
        "wdir_cardinal": "NE",
        "clds": 2,
        "pop_phrase": "",
        "temp_phrase": "Low 18C.",
        "accumulation_phrase": "",
        "wind_phrase": "Winds NE at 10 to 15 km/h.",
        "shortcast": "Clear",
        "narrative": "A mostly clear sky. Low 18C. Winds NE at 10 to 15 km/h.",
        "qpf": 0,
        "snow_qpf": 0,
        "snow_range": "",
        "snow_phrase": "",
        "snow_code": "",
        "vocal_key": "D4:DA09:X3200320043:S320043:TL18:W02R02",
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

## 获取最新天气状况
{: #current_conditions}

您可以在应用程序中发出 `GET` 操作来检索最新天气状况。例如，可以使用以下 `GET` 请求来检索加拿大安大略省渥太华的最新天气状况：

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/observations.json?units=m&language=en-US
```

响应主体包含元数据和观察到的最新天气数据。例如，元数据可能包含以下数据：

```
{
  "metadata": {"language": "en-US",
    "transaction_id": "1467042290443:151881483",
    "version": "1",
    "latitude": 45.42,
    "longitude": 75.69,
    "units": "m",
    "expire_time_gmt": 1467051300,
    "status_code": 200
  },
  "observation": {
  }
}
```

观察数据包含常规信息以及特定于度量单位的值。例如，如果度量单位指定为度量标准，那么最新天气状况可能包含以下数据：

```
"observation": {"key": "36821",
    "class": "observation",
    "expire_time_gmt": 1467051300,
    "obs_id": "36821",
    "obs_name": "Bakanas",
    "valid_time_gmt": 1467039600,
    "day_ind": "N",
    "temp": 21,
    "wx_icon": 27,
    "icon_extd": 2700,
    "wx_phrase": "Mostly Cloudy",
    "pressure_tend": 1,
    "pressure_desc": "Rising",
    "dewPt": 17,
    "heat_index": 21,
    "rh": 74,
    "pressure": 965.2,
    "vis": 50,
    "wc": 21,
    "wdir": 270,
    "wdir_cardinal": "W",
    "gust": null,
    "wspd": 4,
    "max_temp": -4,
    "min_temp": null,
    "precip_total": null,
    "precip_hrly": null,
    "snow_hrly": null,
    "uv_desc": "Low",
    "feels_like": 21,
    "uv_index": 0,
    "qualifier": null,
    "qualifier_svrty": null,
    "blunt_phrase": null,
    "terse_phrase": null,
    "clds": 75
  }
```

## 获取警报
{: #getting_alerts}

您可以在应用程序中发出 `GET` 操作来检索最新天气警报标题。例如，可以使用以下 `GET` 请求来检索美国加利福尼亚州圣伯纳迪诺的天气警报标题：

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/34.12/-117.30/alerts.json?language=en-US
```

响应主体包含元数据和最新天气警报标题。例如，元数据可能包含以下数据：

```
{
  "metadata": {"language": "en-US",
    "transaction_id": "1467042764309:-1516467294",
    "version": "1",
    "longitude": "-117.30",
    "latitude": "34.12",
    "expire_time_gmt": 1467042824,
    "status_code": 200
  },
}
```

警报标题数据包含常规信息和用于检索天气警报详细信息的密钥。
例如，警报标题数据可能包含以下数据：

```
"alerts": [
    {
      "key": "cf63821f-9521-3f27-92ec-e1562ccd469b",
      "class": "bulletin",
      "msg_type_cd": 2,
      "msg_type": "Update",
      "pil": "NPW",
      "phenomena": "HT",
      "significance": "Y",
      "etn": "0003",
      "office_cd": "KSGX",
      "office_name": "San Diego",
      "office_st_cd": "CA",
      "office_cntry_cd": "US",
      "event_desc": "Heat Advisory",
      "severity_cd": 3,
      "severity": "Moderate",
      "categories": [
        {
          "category": "Met",
          "category_cd": 2
        }
      ],
      "response_types": [
        {
          "response_type": "Execute",
          "response_type_cd": 4
        }
      ],
      "urgency": "Expected",
      "urgency_cd": 2,
      "certainty": "Likely",
      "certainty_cd": 2,
      "effective_dt_tm_local": null,
      "effective_dt_tm_tz_abbrv": null,
      "expire_dt_tm_local": "2016-06-29T20:00:00-07:00",
      "expire_dt_tm_tz_abbrv": "PDT",
      "expire_time_gmt": 1467255600,
      "onset_dt_tm_local": null,
      "onset_dt_tm_tz_abbrv": null,
      "flood": null,
      "area_type": "Z",
      "lat": 33.48,
      "lon": -117.29,
      "area_id": "CAZ048",
      "area_name": "San Bernardino and Riverside County Valleys",
      "st_cd": "CA",
      "st_name": "California",
      "cntry_cd": "US",
      "cntry_name": "UNITED STATES OF AMERICA",
      "headline_text": "Heat Advisory until 8PM PDT WED",
      "detail_key": "cf63821f-9521-3f27-92ec-e1562ccd469b",
      "source": "National Weather Service",
      "disclaimer": null,
      "issue_dt_tm_local": "2016-06-27T04:38:50-07:00",
      "issue_dt_tm_tz_abbrv": "PDT",
      "identifier": "e234b6f889bf9a91c5d9f309db63eaa0",
      "proc_dt_tm_local": "2016-06-27T04:38:58-07:00",
      "proc_dt_tm_tz_abbrv": "PDT"
    }
  ]
```

来自警报标题响应主体的密钥可用于查找天气警报详细信息。
例如，可以使用以下 `GET` 请求来检索对应于上一个示例中美国加利福尼亚州圣伯纳迪诺的天气警报标题的天气警报详细信息：

```
https://twcservice.mybluemix.net:443/api/weather/v1/alert/cf63821f-9521-3f27-92ec-e1562ccd469b/details.json?language=en-US
```

响应主体提供以下元数据和信息：

```
{
  "metadata": {"language": "en-US",
    "transaction_id": "1467043225642:-1066997140",
    "version": "1",
    "alert_id": "cf63821f-9521-3f27-92ec-e1562ccd469b",
    "expire_time_gmt": 1467043285,
    "status_code": 200
  },
  "alertDetail": {
    "key": "cf63821f-9521-3f27-92ec-e1562ccd469b",
    "class": "bulletin",
    "msg_type_cd": 2,
    "msg_type": "Update",
    "pil": "NPW",
    "phenomena": "HT",
    "significance": "Y",
    "etn": "0003",
    "office_cd": "KSGX",
    "office_name": "San Diego",
    "office_st_cd": "CA",
    "office_cntry_cd": "US",
    "event_desc": "Heat Advisory",
    "severity_cd": 3,
    "severity": "Moderate",
    "categories": [
      {
        "category": "Met",
        "category_cd": 2
      }
    ],
    "response_types": [
      {
        "response_type": "Execute",
        "response_type_cd": 4
      }
    ],
    "urgency": "Expected",
    "urgency_cd": 2,
    "certainty": "Likely",
    "certainty_cd": 2,
    "effective_dt_tm_local": null,
    "effective_dt_tm_tz_abbrv": null,
    "expire_dt_tm_local": "2016-06-29T20:00:00-07:00",
    "expire_dt_tm_tz_abbrv": "PDT",
    "expire_time_gmt": 1467255600,
    "onset_dt_tm_local": null,
    "onset_dt_tm_tz_abbrv": null,
    "flood": null,
    "area_type": "Z",
    "lat": 33.48,
    "lon": -117.29,
    "area_id": "CAZ048",
    "area_name": "San Bernardino and Riverside County Valleys",
    "st_cd": "CA",
    "st_name": "California",
    "cntry_cd": "US",
    "cntry_name": "UNITED STATES OF AMERICA",
    "headline_text": "Heat Advisory until 8PM PDT WED",
    "source": "National Weather Service",
    "disclaimer": null,
    "issue_dt_tm_local": "2016-06-27T04:38:50-07:00",
    "issue_dt_tm_tz_abbrv": "PDT",
    "identifier": "e234b6f889bf9a91c5d9f309db63eaa0",
    "proc_dt_tm_local": "2016-06-27T04:38:58-07:00",
    "proc_dt_tm_tz_abbrv": "PDT",
    "texts": [
      {
        "language_cd": "en-US",
        "description": ".HIGH PRESSURE ALOFT WILL REMAIN IN PLACE THROUGH TUESDAY...THEN\nSLOWLY WEAKEN INTO NEXT WEEKEND. THIS WILL MAKE FOR VERY HOT\nAFTERNOONS IN THE MOUNTAINS...DESERTS...AND INLAND EMPIRE THROUGH\nWEDNESDAY. THE PEAK OF THE HEAT IS EXPECTED TUESDAY.* TEMPERATURE...MID AND HIGH CLOUDS WILL KEEP HIGH TEMPERATURES\n  TODAY SLIGHTLY LESS HOT THAN SUNDAY...THEN WARMING FOR TUESDAY\n  WITH HIGH TEMPERATURES 108 TO 114 IN THE LOWER DESERTS...100 TO\n  106 IN THE UPPER DESERTS...AND 98 TO 105 IN THE INLAND EMPIRE.\n\n* IMPACTS...HEAT ILLNESS POSSIBLE FOR THOSE PEOPLE MOST AT \n  RISK...INCLUDING CHILDREN...THE ELDERLY...AND THOSE WITH \n  CHRONIC ILLNESS. PETS ARE ALSO VULNERABLE TO HEAT ILLNESS.",
        "instruction": "TO REDUCE RISK DURING OUTDOOR WORK THE OCCUPATIONAL SAFETY AND\nHEALTH ADMINISTRATION RECOMMENDS SCHEDULING FREQUENT REST BREAKS\nIN SHADED OR AIR CONDITIONED ENVIRONMENTS. ANYONE OVERCOME BY\nHEAT SHOULD BE MOVED TO A COOL AND SHADED LOCATION.   HEAT STROKE\nIS AN EMERGENCY - CALL 9 1 1.\n\nTAKE EXTRA PRECAUTIONS IF YOU WORK OR SPEND TIME OUTSIDE. WHEN\nPOSSIBLE... RESCHEDULE STRENUOUS ACTIVITIES TO EARLY MORNING OR\nEVENING.  KNOW THE SIGNS AND SYMPTOMS OF HEAT EXHAUSTION AND HEAT\nSTROKE.  WEAR LIGHT WEIGHT AND LOOSE FITTING CLOTHING WHEN\nPOSSIBLE AND DRINK PLENTY OF WATER.\n\n",
        "overview": null
      }
    ],
    "polygon": null
  }
}
```

## 获取年历数据
{: #getting_almanac_data}

您可以在应用程序中发出 `GET` 操作来检索每天或每月的年历数据。例如，可以使用以下 `GET` 请求来检索美国乔治亚州亚特兰大的每天年历信息：

```
https://twcservice.mybluemix.net:443/api/weather/v1/geocode/33.40/-83.42/almanac/daily.json?units=e&start=0112&end=0115
```

响应主体提供以下元数据和信息：

```
{
  "metadata": {"language": "en-US",
    "transaction_id": "1467044012413:-416805755",
    "version": "1",
    "latitude": 33.4,
    "longitude": -83.42,
    "units": "e",
    "expire_time_gmt": 1466157922,
    "status_code": 200
  },
  "almanac_summaries": [
    {
      "class": "almanac",
      "station_id": "095988",
      "station_name": "MONTICELLO",
      "almanac_dt": "0112",
      "interval": "D",
      "avg_hi": 56,
      "avg_lo": 28,
      "record_hi": 71,
      "record_hi_yr": 1974,
      "record_lo": 0,
      "record_lo_yr": 1982,
      "mean_temp": 42,
      "avg_precip": 0.13,
      "avg_snow": 0.1,
      "record_period": 30
    },
    {
      "class": "almanac",
      "station_id": "095988",
      "station_name": "MONTICELLO",
      "almanac_dt": "0113",
      "interval": "D",
      "avg_hi": 56,
      "avg_lo": 28,
      "record_hi": 72,
      "record_hi_yr": 1972,
      "record_lo": 13,
      "record_lo_yr": 1981,
      "mean_temp": 42,
      "avg_precip": 0.12,
      "avg_snow": 0,
      "record_period": 30
    },
    {
      "class": "almanac",
      "station_id": "095988",
      "station_name": "MONTICELLO",
      "almanac_dt": "0114",
      "interval": "D",
      "avg_hi": 56,
      "avg_lo": 28,
      "record_hi": 71,
      "record_hi_yr": 2000,
      "record_lo": 14,
      "record_lo_yr": 1956,
      "mean_temp": 42,
      "avg_precip": 0.13,
      "avg_snow": 0,
      "record_period": 30
    },
    {
      "class": "almanac",
      "station_id": "095988",
      "station_name": "MONTICELLO",
      "almanac_dt": "0115",
      "interval": "D",
      "avg_hi": 56,
      "avg_lo": 28,
      "record_hi": 75,
      "record_hi_yr": 1953,
      "record_lo": 11,
      "record_lo_yr": 1964,
      "mean_temp": 42,
      "avg_precip": 0.12,
      "avg_snow": 0,
      "record_period": 30
    }
  ]
}

```

## 使用定位服务
{: #using_location_services}

### 按城市名请求
要请求城市的位置信息，您必须至少提供一个查询参数，如城市名和城市的 `locationType`。您还可以提供 `countryCode` 和 `adminDistrictCode`，以减少可检索的唯一位置数。


例如，以下请求可检索美国乔治亚州亚特兰大的位置信息。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/search?query=Atlanta&locationType=city&countryCode=US&adminDistrictCode=GA&language=en-US
```

响应主体包含位置信息和元数据。
```
{
  "location": [
    {
      "address": "Atlanta, Georgia, United States",
      "adminDistrict": "Georgia",
      "adminDistrictCode": "GA",
      "city": "Atlanta",
      "longitude": -84.3902,
      "postalCode": "30303",
      "latitude": 33.7491,
      "country": "United States",
      "countryCode": "US"
    }
  ],
  "metadata": {
    "transaction_id": null,
    "format": "json",
    "adminDistrictCode": "GA",
    "total_cache_time_secs": 10800,
    "language": "en-US",
    "generated_time": 1467044888246,
    "locationType": "city",
    "status_code": 200,
    "version": "v3",
    "query": "Atlanta",
    "countryCode": "US"
  }
}
```

### 按地理位置代码请求
要请求地理位置代码的位置集，您必须提供有效的经度和纬度对。

例如，以下请求可检索美国乔治亚州亚特兰大的地理坐标位置信息。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/point?geocode=34.53%2C-84.50&language=en-US
```

### 按邮政编码请求
要按邮政编码请求位置集，您必须提供邮政索引码，其由 &lt;邮政编码&gt;:&lt;国家或地区代码&gt; 组成。

例如，以下请求可检索美国乔治亚州亚特兰大的邮政编码位置信息。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/point?postalKey=30339%3AUS&language=en-US
```
