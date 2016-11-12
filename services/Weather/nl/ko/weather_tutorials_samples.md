---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 예:
{: #tutorials_samples}

다음 예제와 함께 {{site.data.keyword.weather_short}} 서비스를 사용하는 방법을 학습합니다.
{: shortdesc}

## {{site.data.keyword.weather_short}} 데모
{: #insights_weather_demo}

[{{site.data.keyword.weather_short}} 데모 앱](http://weather-company-data-demo.{APPDomain}){: new_window}을 시도하여 {{site.data.keyword.weather_short}}
서비스와 함께 날씨 데이터를 검색하는 방법을 학습할 수 있습니다.
애플리케이션이 브라우저에서 열리고 사용자의 현재 위치를 애플리케이션과 공유할지 여부를 묻습니다.

데모 애플리케이션에서, 사용자 위치의 날씨에 대해 현재 관측된 상태를 볼 수 있습니다.

![온타리오주 오타와의 현재 관측이 표시된 기본 화면의 이미지입니다.](images/twctestapp_main_screen.jpg "온타리오주 오타와의 현재 관측이 표시된 기본 화면의 이미지입니다.")

또한 그 다음 48시간 동안의 시간별 예보와 그 다음 10일 동안의 일별 예보를 볼 수 있습니다.
일별 예보에 주간 파트 및 야간 파트가 표시됩니다.
데모 애플리케이션에서 이러한 영역을 각각 클릭하는 경우 JSON 형식으로 API 호출의 결과를 볼 수 있으며,
이는 데이터를 검색하는 데 사용된 메타데이터가 포함됩니다.

데모 애플리케이션에서, **Bluemix에 배치**를 클릭하여 애플리케이션의 복제된 버전을 작성하거나
[GitHub에서 직접 애플리케이션 복제](https://github.com/IBM-Bluemix/weather-company-data-demo)를 수행하십시오.

## 시간별 예보 가져오기
{: #getting_twenty_four_hour_forecast}

애플리케이션에서 `GET` 연산을 실행하여 48시간 시간별 예보 데이터를 검색할 수 있습니다.

`username` 및 `password`는 애플리케이션과 서비스 인스턴스에서 고유합니다.
`VCAP_SERVICES` 환경 변수에서 이 정보를 찾을 수 있습니다. 

서비스는 응답을 JSON 형식으로 리턴합니다. 응답에 성공하면 상태 코드 200이 리턴됩니다. 응답에 성공하지 못하면 오류 코드가 리턴됩니다.


예를 들어, 다음 `GET` 요청을 사용하여
캐나다 온타리오주 오타와의 위도 및 경도 좌표에 대해 48시간 시간별 예보를 검색할 수 있습니다.

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/forecast/hourly/48hour.json?units=m&language=en-US
```
또한 애플리케이션에서 `GET` 연산을 실행하여 48시간 시간별 예보 데이터에서
우편번호를 검색할 수 있습니다.

**참고**: 지원되는 국가 코드 미국(US),
영국(GB), 프랑스(FR), 독일(DE) 또는 이탈리아(IT)의 우편번호만 제공할 수 있습니다.

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/location/97229%3A4%3AUS/forecast/hourly/48hour.json?units=m&language=en-US
```

응답 본문에는 그 다음 각 48시간마다 시간별 예보의 배열 및 메타데이터가
포함됩니다. 예를 들면, 메타데이터에는 다음 데이터가 포함됩니다.

```
{
  "metadata": {
    "language": "en-US",
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

각 시간별 예보에는 `num`에서 지정하는 시간에 적용되는 일반 정보가 포함됩니다. 예를 들면, 시간별 예보에는
다음 데이터가 포함됩니다.

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

## 일별 예보 가져오기
{: #getting_ten_day_forecast}

애플리케이션에서 `GET` 연산을 실행하여 10일 간의 예보 데이터를 검색할 수 있습니다.
예를 들어, 다음 `GET` 요청을 사용하여 캐나다 온타리오주 오타와에 대한 10일 간의 예보를 검색할 수 있습니다. 

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/forecast/daily/10day.json?units=m&language=en-US
```

응답 본문에는 그 다음 10일 동안의 일별 예보 배열이 포함됩니다.
예를 들면, 메타데이터에는 다음 데이터가 포함됩니다.

```
{
  "metadata": {
    "language": "en-US",
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

각 일별 예보에는 지정된 요일의 24시간 기간에 적용되는 일반 정보가 포함됩니다(`dow`).
예를 들면, 일별 예보에는 다음 데이터가 포함됩니다.

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

각 일별 예보에는 지정된 요일의 야간 파트와 주간 파트가 포함됩니다.
예를 들면, 이 두 파트에는 모두 다음 예보 데이터가 포함됩니다.

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

## 현재 상태 가져오기
{: #current_conditions}

애플리케이션에서 `GET` 연산을 실행하여 현재 기상 상태를 검색할 수 있습니다.
예를 들어, 다음 `GET` 요청을 사용하여 캐나다 온타리오주 오타와의 현재 상태를 검색할 수 있습니다. 

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/observations.json?units=m&language=en-US
```

응답 본문에는 메타데이터와 관측된 현재 기상 데이터가 포함됩니다.
예를 들면, 메타데이터에는 다음 데이터가 포함됩니다.

```
{
  "metadata": {
    "language": "en-US",
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

관측 데이터에는 일반 정보 및 측정 단위에
특정한 값이 포함됩니다. 예를 들면, 측정 단위가 메트릭으로 지정된 경우
현재 상태에는 다음 데이터가 포함됩니다.

```
"observation": {
    "key": "36821",
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

## 경보 가져오기
{: #getting_alerts}

애플리케이션에서 `GET` 연산을 실행하여 현재 기상 경보 헤드라인을 검색할 수 있습니다.
예를 들어, 다음 `GET` 요청을 사용하여 미국 캘리포니아주 샌 버너디노의 기상 경보 헤드라인을 검색할 수 있습니다.

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/34.12/-117.30/alerts.json?language=en-US
```

응답 본문에는 메타데이터 및 현재 기상 경보 헤드라인이 포함됩니다.
예를 들면, 메타데이터에는 다음 데이터가 포함됩니다.

```
{
  "metadata": {
    "language": "en-US",
    "transaction_id": "1467042764309:-1516467294",
    "version": "1",
    "longitude": "-117.30",
    "latitude": "34.12",
    "expire_time_gmt": 1467042824,
    "status_code": 200
  },
}
```

경보 헤드라인 데이터에 일반 정보 및 키가 포함되어
기상 경보 세부사항을 검색합니다. 예를 들어, 경보 헤드라인 데이터에는 다음 데이터가 포함될 수 있습니다.

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

경보 헤드라인 응답 본문의 키를 사용하여 기상 경보 세부사항을 찾을 수 있습니다.
예를 들어, 다음 `GET` 요청을 사용하여
이전 예제에 있는 미국 캘리포니아주 샌 버너디노의 기상 경보 헤드라인에 해당하는
기상 경보 세부사항을 검색할 수 있습니다.

```
https://twcservice.mybluemix.net:443/api/weather/v1/alert/cf63821f-9521-3f27-92ec-e1562ccd469b/details.json?language=en-US
```

응답 본문에서는 다음 메타데이터 및 정보를 제공합니다.

```
{
  "metadata": {
    "language": "en-US",
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

## 연감 데이터 가져오기
{: #getting_almanac_data}

애플리케이션에서 `GET` 연산을 실행하여 일별 또는 월별 연감 데이터를 검색할 수 있습니다.
예를 들어, 다음 `GET` 요청을 사용하여 미국 조지아주 애틀란타의 일별 연감 정보를 검색할 수 있습니다.

```
https://twcservice.mybluemix.net:443/api/weather/v1/geocode/33.40/-83.42/almanac/daily.json?units=e&start=0112&end=0115
```

응답 본문에서는 다음 메타데이터 및 정보를 제공합니다.

```
{
  "metadata": {
    "language": "en-US",
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

## 위치 서비스 사용
{: #using_location_services}

### 구/군/시 이름별 요청
구/군/시의 위치 정보를 요청하려면
구/군/시 이름 및 구/군/시의 `locationType` 등 하나 이상의 조회 매개변수를 제공해야 합니다. 또한
`countryCode` 및 `adminDistrictCode`를 제공하여
검색될 수 있는 고유한 위치의 수를 줄일 수 있습니다.

예를 들어, 다음 요청에서는 미국 조지아주 애틀란타의 위치 정보를 검색합니다.

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/search?query=Atlanta&locationType=city&countryCode=US&adminDistrictCode=GA&language=en-US
```

응답 본문에는 위치 정보 및 메타데이터가 포함됩니다.
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

### 지오코드별 요청
지오코드의 위치 세트를 요청하려면 유효한 위도 및 경도 쌍을 제공해야 합니다.

예를 들어, 다음 요청에서는 미국 조지아주 애틀란타의 지오 좌표에 대한 위치 정보를 검색합니다.

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/point?geocode=34.53%2C-84.50&language=en-US
```

### 우편번호별 요청
우편번호별로 위치 세트를 요청하려면 우편 키를 제공해야 하며, 이는
&lt;우편번호&gt;:&lt;국가 코드&gt;의 컴포지트입니다.

예를 들어, 다음 요청에서는 미국 조지아주 애틀란타의 우편번호에 대한 위치 정보를 검색합니다.

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/point?postalKey=30339%3AUS&language=en-US
```
