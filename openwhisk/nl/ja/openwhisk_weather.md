---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Weather パッケージの使用
{: #openwhisk_catalog_weather}

`/whisk.system/weather` パッケージは、Weather Company Data for IBM Bluemix API を呼び出すのに便利な方法を提供します。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | パッケージ | username、password | Weather Company Data for IBM Bluemix API からのサービス  |
| `/whisk.system/weather/forecast` | アクション | latitude、longitude、timePeriod | 指定された時間枠の予測|

`username` と `password` の値を使用して、パッケージ・バインディングを作成することをお勧めします。この方法を使用すると、パッケージ内のアクションを起動するたびに資格情報を指定する必要はありません。

## 場所を指定した天気予報の取得
{: #openwhisk_catalog_weather_forecast}

`/whisk.system/weather/forecast` アクション
は、The Weather Company から API を呼び出して、場所を指定した天気予報を返します。パラメーターは次のとおりです。


- `username`: 予測 API を起動する権限を与えられた Weather Company Data for IBM Bluemix のユーザー名。
- `password`: 予測 API を起動する権限を与えられた Weather Company Data for IBM Bluemix のパスワード。
- `latitude`: 場所の経度の座標。
- `longitude`: 場所の緯度の座標。
- `timePeriod`: 予測の時間枠。有効なオプションは、デフォルトの「10 日間」(毎日の予測を 10 日間返す)、「48 時間」(毎時の予測を 2 日間返す)、「現在」(現在の天気状況を返す)、「時系列」(現在の日時から、現在の観測と過去 24 時間までの観測の両方を返す) です。


以下は、パッケージ・バインディングを作成してから 10 日間の予測を取得する例です。

1. API キーを使用してパッケージ・バインディングを作成します。
  
  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}
  
2. パッケージ・バインディングの `forecast` アクションを起動して、天気予報を取得します。
  
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
  
