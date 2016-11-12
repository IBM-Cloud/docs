---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 例
{: #tutorials_samples}

以下の例を用いて、{{site.data.keyword.weather_short}} サービスの使用方法を説明します。
{: shortdesc}

## {{site.data.keyword.weather_short}} デモ
{: #insights_weather_demo}

[{{site.data.keyword.weather_short}} デモ・アプリケーション](http://weather-company-data-demo.{APPDomain}){: new_window}を試すことで、{{site.data.keyword.weather_short}} サービスを使用した気象データの取得方法を習得できます。
ご使用のブラウザーでアプリケーションが開き、ユーザーの現在の位置をアプリケーションと共有するかどうかを尋ねられます。

デモ・アプリケーションでは、現在の位置の気象についての、現在の観測された状態を表示できます。

![オンタリオ州オタワの現在の観測を示すメインスクリーンの画像。](images/twctestapp_main_screen.jpg "オンタリオ州オタワの現在の観測を示すメインスクリーンの画像。")

次の 48 時間についての毎時の予報および次の 10 日間についての毎日の予報を表示することもできます。毎日の予報では、夜間部分と日中部分が表示されます。
デモ・アプリケーション内でこれらの各領域をクリックすると、API 呼び出しの結果が JSON 形式で表示されます。これには、データを取得するために使用されたメタデータが含まれています。

デモ・アプリケーションで、**「Bluemix にデプロイ」**をクリックして、アプリケーションの複製版を作成するか、[GitHub から直接、アプリケーションを複製します](https://github.com/IBM-Bluemix/weather-company-data-demo)。

## 毎時の予報の取得
{: #getting_twenty_four_hour_forecast}

アプリケーションで `GET` 命令を発行して、48 時間の毎時の予報データを取得できます。

`username` と `password` は、アプリケーションとサービス・インスタンスごとに固有です。この情報は、`VCAP_SERVICES` 環境変数で確認できます。

サービスは、応答を JSON 形式で戻します。応答が正常である場合は、状況コード 200 が返されます。応答が正常ではない場合は、エラー・コードが返されます。

例えば、次の `GET` 要求を使用して、オンタリオ州オタワ (カナダ) の緯度と経度に関する 48 時間の毎時の予報を取得できます。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/forecast/hourly/48hour.json?units=m&language=en-US
```
アプリケーションで `GET` 命令を発行して、郵便番号の地域について 48 時間の毎時の予報データを取得することもできます。

**注**: 郵便番号を指定できるのは、サポートされる国別コードの米国 (US)、英国 (GB)、フランス (FR)、ドイツ (DE)、またはイタリア (IT) の場合のみです。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/location/97229%3A4%3AUS/forecast/hourly/48hour.json?units=m&language=en-US
```

応答の本文には、メタデータおよび今後 48 時間の毎時の予報の配列が含まれています。例えば、メタデータには、以下のようなデータが含まれている可能性があります。

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

毎時の予報にはそれぞれ、`num` で指定された時間に適用される一般情報が含まれています。例えば、毎時の予報には、以下のようなデータが含まれている可能性があります。

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

## 毎日の予報の取得
{: #getting_ten_day_forecast}

アプリケーションで `GET` 命令を発行して、10 日間の予報データを取得できます。
例えば、次の `GET` 要求を使用して、オンタリオ州オタワ (カナダ) の 10 日間の予報を取得できます。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/forecast/daily/10day.json?units=m&language=en-US
```

応答の本文には、メタデータおよび今後 10 日間の毎日の予報の配列が含まれています。例えば、メタデータには、以下のようなデータが含まれている可能性があります。

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

毎日の予報にはそれぞれ、指定された曜日 (`dow`) の 24 時間に適用される一般情報が含まれています。
例えば、毎日の予報には、以下のようなデータが含まれている可能性があります。

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

毎日の予報にはそれぞれ、指定された曜日の夜の部分と昼の部分が含まれています。
例えば、この両方の部分に、以下のような予報データが含まれている可能性があります。

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

## 現在の条件の取得
{: #current_conditions}

アプリケーションで `GET` 命令を発行して、現在の気象条件を取得できます。
例えば、次の `GET` 要求を使用して、オンタリオ州オタワ (カナダ) の現在の気象条件を取得できます。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/45.42/75.69/observations.json?units=m&language=en-US
```

応答の本文には、メタデータおよび現在の観測気象データが含まれています。例えば、メタデータには、以下のようなデータが含まれている可能性があります。

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

観測データには、一般情報および計測単位に固有の値が含まれています。
例えば、計測単位にメートル系が指定されている場合、現在の条件には、以下のようなデータが含まれている可能性があります。

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

## アラートの取得
{: #getting_alerts}

アプリケーションで `GET` 命令を発行して、現在の気象アラート・ヘッドラインを取得できます。
例えば、次の `GET` 要求を使用して、カリフォルニア州サンバーナーディーノ (米国) の気象アラート・ヘッドラインを取得できます。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v1/geocode/34.12/-117.30/alerts.json?language=en-US
```

応答の本文には、メタデータおよび現在の気象アラート・ヘッドラインが含まれています。例えば、メタデータには、以下のようなデータが含まれている可能性があります。

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

アラート・ヘッドライン・データには、一般的な情報、および気象アラート詳細を取得するためのキーが含まれています。例えば、アラート・ヘッドライン・データには、以下のようなデータが含まれている可能性があります。

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

アラート・ヘッドラインの応答本体のキーを使用して、気象アラート詳細を検索できます。
例えば、次の `GET` 要求を使用して、前の例のカリフォルニア州サンバーナーディーノ (米国) の気象アラート・ヘッドラインに対応する気象アラート詳細を取得できます。

```
https://twcservice.mybluemix.net:443/api/weather/v1/alert/cf63821f-9521-3f27-92ec-e1562ccd469b/details.json?language=en-US
```

応答本体は、以下のようなメタデータおよび情報を提供します。

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

## アルマナック・データの取得
{: #getting_almanac_data}

アプリケーションで `GET` 命令を発行して、日ごとまたは月ごとのアルマナック・データを取得できます。
例えば、次の `GET` 要求を使用して、ジョージア州アトランタ (米国) の日ごとのアルマナック情報を取得できます。

```
https://twcservice.mybluemix.net:443/api/weather/v1/geocode/33.40/-83.42/almanac/daily.json?units=e&start=0112&end=0115
```

応答本体は、以下のようなメタデータおよび情報を提供します。

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

## ロケーション・サービスの使用
{: #using_location_services}

### 市区町村による要求
市区町村のロケーション情報を要求するには、少なくとも 1 つの照会パラメーター (市区町村名など) と市区町村の `locationType` を指定する必要があります。`countryCode` や `adminDistrictCode` を指定して、取得できる固有の場所の数を削減することもできます。

例えば、次の要求は、ジョージア州アトランタ (米国) のロケーション情報を取得します。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/search?query=Atlanta&locationType=city&countryCode=US&adminDistrictCode=GA&language=en-US
```

応答本体には、ロケーション情報およびメタデータが含まれています。
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

### ジオコードによる要求
特定のジオコードの一連の場所を要求するには、有効な緯度と経度のペアを指定する必要があります。

例えば、次の要求は、ジョージア州アトランタ (米国) の地理座標のロケーション情報を取得します。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/point?geocode=34.53%2C-84.50&language=en-US
```

### 郵便番号による要求
郵便番号によって一連の場所を要求するには、郵便キー (&lt;郵便番号&gt;:&lt;国別コード&gt; から成る合成ストリング) を指定する必要があります。

例えば、次の要求は、ジョージア州アトランタ (米国) 内の郵便番号に関するロケーション情報を取得します。

```
GET https://<username>:<password>@twcservice.mybluemix.net:443/api/weather/v3/location/point?postalKey=30339%3AUS&language=en-US
```
