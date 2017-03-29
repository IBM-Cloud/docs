---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Weather 패키지 사용
{: #openwhisk_catalog_weather}

`/whisk.system/weather` 패키지는 Weather Company Data for IBM Bluemix API를 호출하는 편리한 방법을 제공합니다. 

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | 패키지 | username, password | Weather Company Data for IBM Bluemix API의 서비스  |
| `/whisk.system/weather/forecast` | 조치 | latitude, longitude, timePeriod | 지정된 기간에 대한 예보|

`username` 값과 `password` 값을 사용하여 패키지 바인딩을 작성하도록 권장합니다. 이 방법을 사용하면 패키지에서 조치를 호출할 때마다 신임 정보를 지정할 필요가 없습니다. 

## 위치에 대한 날씨 예보 가져오기
{: #openwhisk_catalog_weather_forecast}

`/whisk.system/weather/forecast` 조치는 The Weather Company에서 API를 호출하여 위치에 대한 날씨 예보를 리턴합니다. 매개변수는 다음과 같습니다.

- `username`: 예보 API를 호출할 자격이 있는 Weather Company Data for IBM Bluemix의 사용자 이름입니다. 
- `password`: 예보 API를 호출할 자격이 있는 Weather Company Data for IBM Bluemix의 비밀번호입니다. 
- `latitude`: 위치의 위도 좌표입니다.
- `longitude`: 위치의 경도 좌표입니다.
- `timePeriod`: 예보에 대한 기간입니다. 유효한 옵션은 다음과 같습니다. '10day' - (기본값) 일별로 10일 예보를 리턴함, '48hour' - 시별로 2일 예보를 리턴함, 'current' - 현재 날씨 상태를 리턴함, 'timeseries' - 현재 관측 및 현재 날짜 및 시간으로부터 최대 24시간의 지난 관측을 모두 리턴함. 


다음은 패키지 바인딩을 작성한 후 10일 간의 예보를 가져오는 예입니다. 

1. 사용자의 API 키를 사용하여 패키지 바인딩을 작성하십시오.
  
  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}
  
2. 패키지 바인딩에서 `forecast` 조치를 호출하여 날씨 예보를 가져오십시오.
  
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
  
