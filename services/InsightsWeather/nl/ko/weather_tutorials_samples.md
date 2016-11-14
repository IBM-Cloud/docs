---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 예:
{: #tutorials_samples}

다음의 예에서는 Insights for Weather 서비스를 사용하는 방법을 학습합니다.
{: shortdesc}

## Insights for Weather 데모
{: #insights_weather_demo}

샘플 애플리케이션을 활용하면 Insights for Weather 서비스를 사용하여 기상 데이터를 볼 수 있습니다. 애플리케이션은
[http://insights-for-weather-demo.mybluemix.net/](http://insights-for-weather-demo.mybluemix.net/)으로 이동하여 액세스가 가능합니다.
애플리케이션이 브라우저에서 열리고 사용자의 현재 위치를 앱과 공유할 것인지 묻습니다. 

샘플 애플리케이션에서 사용자의 위치에서 현재 관측된 기상 상태를 볼 수 있습니다. 

![온타리오주 오타와의 현재 관측이 표시된 기본 화면의 이미지입니다.](images/twctestapp_main_screen.jpg "온타리오주 오타와의 현재 관측이 표시된 기본 화면의 이미지입니다.")

그 다음 24시간 동안의 시간별 예보와 그 다음 10일 동안의 일별 예보를 볼 수도 있습니다.
샘플에서 이들 각 영역 위로 마우스를 이동하면 API 호출의 결과를
JSON 형식으로 볼 수 있으며, 이 결과에는 데이터 검색에 사용된 메타데이터가 포함됩니다. 

데모 애플리케이션에서 **Bluemix에 배치**를 클릭하여 애플리케이션의 복제된 버전을 작성하거나
[GitHub에서 직접 앱을 복제할 수 있습니다](https://github.com/IBM-Bluemix/insights-for-weather-demo).

## 표준 10일 예보 가져오기
{: #getting_ten_day_forecast}

애플리케이션에서 `GET` 연산을 실행하여 10일 간의 예보 데이터를 검색할 수 있습니다.
예를 들어, 다음 `GET` 요청을 사용하여 캐나다 온타리오주 오타와에 대한 10일 간의 예보를 검색할 수 있습니다. 

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/forecast/daily/10day?units=m&geocode=45.42%2C75.69&language=en-US
}
```

`username` 및 `password`는 애플리케이션과 서비스 인스턴스에서 고유합니다.
`VCAP_SERVICES` 환경 변수에서 이 정보를 찾을 수 있습니다. 

서비스는 응답을 JSON 형식으로 리턴합니다. 응답에 성공하면 상태 코드 200이 리턴됩니다. 응답에 성공하지 못하면 오류 코드가 리턴됩니다.


응답 본문에는 그 다음 10일 동안의 일별 예보 배열이 포함됩니다.
예를 들면, 메타데이터에는 다음 데이터가 포함됩니다.

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

각 일별 예보에는 지정된 요일의 24시간 기간에 적용되는 일반 정보가 포함됩니다(`dow`).
예를 들면, 일별 예보에는 다음 데이터가 포함됩니다.

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

각 일별 예보에는 지정된 요일의 야간 파트와 주간 파트가 포함됩니다.
예를 들면, 이 두 파트에는 모두 다음 예보 데이터가 포함됩니다.

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

## 표준 24시간 예보 가져오기
{: #getting_twenty_four_hour_forecast}

애플리케이션에서 `GET` 연산을 실행하여 24시간 예보 데이터를 검색할 수 있습니다.
예를 들어, 다음 `GET` 요청을 사용하여 캐나다 온타리오주 오타와의 24시간 예보를 검색할 수 있습니다. 

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/forecast/hourly/24hour?units=m&geocode=45.42%2C75.69&language=en-US
```

응답 본문에는 그 다음 24시간 동안의 시간별 예보 배열이 포함됩니다.
예를 들면, 메타데이터에는 다음 데이터가 포함됩니다.

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

각 시간별 예보에는 `num`에서 지정하는 시간에 적용되는 일반 정보가 포함됩니다. 예를 들면, 시간별 예보에는
다음 데이터가 포함됩니다.

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

## 현재 상태 가져오기
{: #current_conditions}

애플리케이션에서 `GET` 연산을 실행하여 현재 기상 상태를 검색할 수 있습니다.
예를 들어, 다음 `GET` 요청을 사용하여 캐나다 온타리오주 오타와의 현재 상태를 검색할 수 있습니다. 

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v2/observations/current?units=m&geocode=45.42%2C75.69&language=en-US
```

응답 본문에는 메타데이터와 관측된 현재 기상 데이터가 포함됩니다.
예를 들면, 메타데이터에는 다음 데이터가 포함됩니다.

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

관측 데이터에는 일반 정보 및 측정 단위에
특정한 값이 포함됩니다. 예를 들면, 측정 단위가 메트릭으로 지정된 경우
현재 상태에는 다음 데이터가 포함됩니다.

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






