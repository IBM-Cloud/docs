---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使用 {{site.data.keyword.weather_short}} REST API
{: #rest_apis}

您可以使用 [ REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} 來擷取氣候資料。您可以測試 API 作業並立即檢視結果，以協助您更快速地建置應用程式。
{: shortdesc}

從參考文件中，按一下**清單作業**以檢視每一個作業的詳細資料。在您指定參數並按一下**試試看！**後，系統可能會要求您提供認證。您必須提供來自 `VCAP_SERVICES` 環境變數的使用者名稱及密碼。開啟應用程式並按一下目錄中的**環境變數**，即可找到此資訊。

**附註：**每個區域各自獨立。您無法將在某個區域佈建給您的服務認證，在另一個區域中用來鑑別服務。若無法輸入適當的認證，則會導致回應內文中出現*未獲授權* 訊息。

利用 REST API，您可以透過緯度及經度座標提供地理定位來擷取天氣資料。您可以使用下列 API。

|**API**                                  |**說明**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |根據您提供的格式，傳回地理定位未來 48 小時的每小時天氣預測。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。每小時預測資料可以包含每個位置的最多 48 小時預測。收到新資料時，您必須捨棄某個位置的所有先前每小時預測。|
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |根據您提供的格式，傳回地理定位 3 、 5 、 7 或 10 天的每日天氣預測。要擷取的天數以 `3day`、`5day`、`7day` 或 `10day` 格式指定。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。每日預測每個都包含白天預測、晚間預測以及 24 小時預測。這些區段是 JSON 回應中的個別物件。在當地時間下午 3:00 之後，每日預測的白天預測資料就無法再使用。在當地時間下午 3:00 時，您的應用程式不得再顯示白天預測。|
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|根據您提供的格式，傳回地理定位 3 、 5 、 7 或 10 天的每日天氣預測，並以 6 小時的期間為單位。要擷取的天數以 `3day`、`5day`、`7day` 或 `10day` 格式指定。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。每日預測每個都包含上午、下午、傍晚及徹夜預測。這些區段是 JSON 回應中的個別物件。|
|`GET /v1/{geocode or location ID}/observations.json`              |傳回某個地理定位的目前天氣狀況。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。這些最近的觀測資料會保留在資料庫中，特定報告工作站最多保留 10 分鐘的資料，而每個工作站則最多保留 24 小時的觀測資料。會根據觀測資料的日期/時間戳記，以先進/先出方法（以最新的觀測資料輪換資料，並將最舊的觀測資料移至保存儲存空間）不斷更新及取代最近的觀測資料。|
|`GET /v1/{geocode or location ID}/observations/timeseries.json`   |傳回某個地理定位從目前日期和時間開始的目前觀測資料，以及最多 24 小時的過去觀測資料。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。天氣觀測資料收集自世界各地所部署的實際裝置，以及目前天氣觀測資料。|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |傳回由 National Weather Service (NWS)、Environment Canada 及 MeteoAlarm（歐洲）所發出的天氣監視、警告、聲明及建議，並且包含 49 種語言翻譯的事件說明、國家/地區名稱及警示標題。您可以提供 `geocode/{latitude}/{longitude}`、`country/{countrycode}`、`country/{countrycode}/state/{statecode}`/ 或 `country/{countrycode}/area/{areaid}`。|
|`GET /v1/alert/{detail_key}/details.json`                         |傳回由 National Weather Service (NWS)、Environment Canada 及 MeteoAlarm（歐洲）所發出的天氣監視、警告、聲明及建議。詳細資料包括關於政府氣象單位針對指定區域所發出警示的深入資訊，並且包含 49 種語言翻譯的事件說明、國家/地區名稱及警示標題。|
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |傳回每日年鑑資訊（僅限美國），資料來源是 National Weather Service（美國國家氣象局）觀測站，時間則跨越 10 到 30 年以上。資訊由 National Climatic Data Center (NCDC) 收集和提供。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{PostalLocationId}`。|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |傳回每月年鑑資訊（僅限美國），資料來源是 National Weather Service（美國國家氣象局）觀測站，時間則跨越 10 到 30 年以上。資訊由 National Climatic Data Center (NCDC) 收集和提供。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{PostalLocationId}`。|
|`GET /v3/location/{search or point}`                                  |提供查閱位置名稱或地理編碼（經緯度）以擷取符合要求之位置集的功能。位置服務支援依城市名稱或郵遞區號來進行搜尋。|
*表 1. {{site.data.keyword.weather_short}} API 摘要*

## 每日及當天預測
{: #daily_intraday}
每日預測 API 可以包含每個位置的多天的每日預測。
每天的預測最多可包含三個不同的預測。針對任何預測日，API 可以傳回白天、夜晚和 24 小時預測。

當天預測 API 可以包含每個位置的多天的每日預測。
每天的預測都包含四個不同的 6 小時預測，分別是針對早上（上午 7 點至下午 1 點）、下午（下午 1 點至下午 7 點）、傍晚（下午 7 點至上午 1 點）以及徹夜（上午 1 點至上午 7 點）。當天預測的結構類似於每日預測。

每個區段都有日期部分號碼、星期幾名稱以及日期部分名稱。例如，下列範例顯示 API 在星期四早上產生之預測的
`num`、`dow` 和 `daypart_name` 資料欄位順序與資料值：

* 1，星期四，早上
* 2，星期四，下午
* 3，星期四，傍晚
* 4，星期四，徹夜
* 5，星期五，早上
* 6，星期五，下午
* 7，星期五，傍晚
* 8，星期五，徹夜

## 目前及時間序列觀測資料
{: #time_series}

目前狀況和時間序列天氣觀測資料提供溫度、降雨、風、氣壓、能見度、紫外線 (UV) 以及其他觀測元素的相關資訊，包括觀測站、觀測日期/時間、天氣圖示代碼和詞組。時間序列觀測資料和目前觀測資料之間的不同之處在於觀測時段，這個導致產生一個以上的觀測資料集。

目前狀況是未使用時間參數下所要求之位置的最新觀測資料。會傳回一個資料集。時間序列觀測資料包含發生的過去觀測資料，最多包括所要求位置的前 24 小時資料。

最新的觀測資料會保留在主要資料庫中，特定報告工作站最多保留 48 小時（2 天）的資料。會根據觀測資料的日期/時間戳記，以先進/先出方法（以最新的觀測資料輪換資料，並將最舊的觀測資料移至保存儲存空間）不斷更新及取代最近的觀測資料。任何工作站保留及提供的資料量可以多於 24 個個別觀測報告。觀測資料數目取決於其觀測資料類型。

## 警示標題及詳細資料
{: #alerts_levels}
警示 API 會傳回與嚴重暴風雨、龍捲風、地震及水災相關的現行天氣警示標題。這些 API 也會傳回非天氣的警示，例如兒童誘拐以及執法警告。

**附註**：這個 API 只適用於美國、加拿大及歐洲。

警示標題 API 提供 `detail_key` 屬性中的金鑰值，以存取警示詳細資料 API 中的警示詳細資料。請查詢警示標題 API 以取得
`detail_key` 值，然後使用 `detail_key` 擷取警示詳細資料 API 回應。

**附註**：您必須針對您應用程式中所顯示的任何警示資料顯示其資料來源歸屬。

歸屬詞組必須顯示下列資訊：

*發出單位：<機構名稱> - &lt;機構管理區代碼&gt;，&lt;機構國碼&gt;，&lt;來源&gt;，&lt;聲明&gt;*

例如：
* 發出單位：National Weather Service - 俾斯麥，美國
* 發出單位：Central Institute for Meteorology and Geodynamics - 奧地利，EMETNET-Meteoalarm

## 年鑑資訊
{: #almanac_details}
年鑑 API 需要位置 ID 及位置類型（城市或郵遞區號）或緯度與經度配對，以擷取特定位置的資訊。

當您在 URL 中使用 `location` 時，位置必須包含位置 ID（郵遞區號），以及位置類型和國碼。
當您在 URL 中使用 `geocode` 時，搜尋位置必須是有效的緯度與經度結合。

年鑑 API 使用參數來指定每日或每月資料、特定日期或日期範圍的資訊，以及傳回資料所用的度量單位。

日期參數是 `start` 和 `end`。`start` 參數是必要參數，但 `end` 參數則為選用性。當參數一起使用時，該組合會傳回一個範圍的資料，而不是特定月份或特定一天的資料。

用來擷取每日年鑑結果的日期格式，是四位數的數值，它代表傳回資料的月份和日期，亦即 MMDD。任何單一位數的日期都**必須**有前導零，例如 01。

擷取每月年鑑結果用的日期格式是月份，亦即 MM。任何單一位數的月份都**必須**有前導零，例如 01。任何其他格式均會導致 API 錯誤，且不會傳回任何資料。

**附註**：如果未在要求中提供日期值，則系統會傳回 404（不當要求）的狀態。API 不會提供預設值。

## URL 建構
{: #url_construction}

REST API 會使用一般 URL 結構和查詢參數來要求及過濾天氣資料。傳遞到 API 的 URL 建構如下：

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

例如：

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**屬性**     |**說明**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |管理的 URL 路徑。例如 `https://twcservice.mybluemix.net:443/api/weather`。|
|`version`         |現行反覆運算。例如 `v1`。|
|`location`        |地理編碼或位置 ID。位置群組可以是 `geocode` 或 `location`。例如，`geocode/45.4214/75.6919` 代表加拿大渥太華。如果您提供地理編碼座標，則 API 會傳回最接近的可用位置的資料。句點用來作為小數點，而逗點則用來區隔緯度值和經度值。如果提供地理編碼，則會在回應的 meta 資料中傳回實際使用的緯度值和經度值。|
|`product group`   |產品。例如 `observations` 或 `forecast`。產品子群組（例如 `historical`）為選用性。|
|`date`            |日期類型。例如 `daily` 或 `monthly`。|
|`format`          |格式。例如 `3day`、`5day`、`7day` 或 `10day`。|
|`units`           |用來傳回回應的選用單位。API 支援 English (e)、Metric (m) 及 UK-Hybrid (h) 度量單位。如果您提供度量單位但未提供值，則 API 會以對應於語言碼的度量單位傳回資料。在回應的 meta 資料的 units 參數中，會傳回預設或所要求的度量單位。|
|`language`        |用來傳回回應的語言。預設值為 en-US。在回應的 meta 資料的 language 參數中，會傳回預設或所要求的翻譯語言。|
*表 2. URL 詳細資料*

**附註**：REST API 針對國碼使用 ISO 3166 標準。如需相關資訊，請參閱
[ISO Standard Online Browsing Platform](https://www.iso.org/obp/ui/#search/code/){:new_window}。API 使用 WGS84 地理編碼座標參照系統。如需相關資訊，請參閱
[Basic Geo Vocabulary](https://www.w3.org/2003/01/geo/){:new_window}。

## 圖示代碼及影像
{: #icon_code_images}

當 {{site.data.keyword.weather_short}} REST API 在回應中傳回圖示代碼時，您可以使用此圖示代碼，以判斷在應用程式中要顯示的圖示影像。API 回應中的圖示代碼，與圖示影像的檔名之間，有一對一的關係。例如，如果 API 回應包含 `icon_code` 1，則您可以使用檔名 `01.png`，以顯示相符的圖示影像。

在您的程式碼中，您可以建立一個函數，使用 `icon_code` 來判斷圖示影像的 URL。例如：

```
function getIconURL(code) {
    return "images/weathericons/icon" + code + ".png";
}
```

下表包含可用於 {{site.data.keyword.weather_short}} REST API 的圖示代碼、說明及影像。表格指出圖示是用在預測還是觀察 API，以及圖示是可用於晚上還是白天的預測部分。

|**代碼**|**說明**|**影像**|**API 使用** |**晚上或白天**|
|----|--------------------------|------------|------------|--------------------|
| 0  | 龍捲風                  | <img src="images/00.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 晚上及白天 |
| 1  | 熱帶風暴           | <img src="images/01.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 2  | 颱風                | <img src="images/02.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 晚上及白天 |
| 3  | 強烈風暴            | <img src="images/03.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 晚上及白天 |
| 4  | 雷和冰雹         | <img src="images/04.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 5  | 陣雨到陣雪     | <img src="images/05.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 6  | 雨 / 霰             | <img src="images/06.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 7  | 雨雪混合 / 霰  | <img src="images/07.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 8  | 凍毛雨         | <img src="images/08.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 9  | 毛雨                  | <img src="images/09.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 10 | 凍雨            | <img src="images/10.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 11 | 小雨               | <img src="images/11.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 12 | 雨                     | <img src="images/12.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 13 | 零星小雪       | <img src="images/13.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 14 | 小雪               | <img src="images/14.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 15 | 高吹雪 / 低吹雪  | <img src="images/15.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 16 | 下雪                     | <img src="images/16.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 17 | 冰雹                     | <img src="images/17.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 18 | 霰                    | <img src="images/18.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 19 | 吹沙 / 沙暴 | <img src="images/19.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 20 | 有霧                    | <img src="images/20.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 21 | 霾 / 風大             | <img src="images/21.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 22 | 煙 / 風大            | <img src="images/22.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 23 | 微風                   | <img src="images/23.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 晚上及白天 |
| 24 | 吹浪 / 風大    | <img src="images/24.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 25 | 寒冷 / 冰晶    | <img src="images/25.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 26 | 陰天                   | <img src="images/26.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 27 | 多雲時陰            | <img src="images/27.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 28 | 多雲時陰            | <img src="images/28.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 白天         |
| 29 | 多雲            | <img src="images/29.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上       |
| 30 | 多雲            | <img src="images/30.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 白天         |
| 31 | 晴朗                    | <img src="images/31.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上       |
| 32 | 晴天                    | <img src="images/32.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 白天         |
| 33 | 晴 / 晴時多雲      | <img src="images/33.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上       |
| 34 | 晴 / 晴偶有雲      | <img src="images/34.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 白天         |
| 35 | 雨夾冰雹        | <img src="images/35.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 白天         |
| 36 | 炎熱                      | <img src="images/36.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 白天         |
| 37 | 局部雷雨   | <img src="images/37.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 白天         |
| 38 | 雷雨            | <img src="images/38.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 39 | 零星陣雨        | <img src="images/39.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 白天         |
| 40 | 大雨               | <img src="images/40.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 41 | 零星陣雪   | <img src="images/41.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 白天         |
| 42 | 大雪               | <img src="images/42.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
| 43 | 暴風雪                 | <img src="images/43.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 晚上及白天 |
| 44 | 無法使用 (N/A)      | <img src="images/44.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 晚上及白天 |
| 45 | 零星陣雨        | <img src="images/45.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 晚上       |
| 46 | 零星陣雪   | <img src="images/46.png " width="100" height="100" alt="圖示影像。"/>| 預測                | 晚上       |
| 47 | 零星雷雨  | <img src="images/47.png " width="100" height="100" alt="圖示影像。"/>| 預測及觀察 | 晚上及白天 |
*表 3. 圖示代碼及影像*

您可以將這組天氣圖示下載為 [PNG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_png.zip){:new_window}
或 [SVG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_svg.zip){:new_window}，然後用在應用程式裡。 

您也可以下載 [{{site.data.keyword.weather_short}} 展示應用程式](http://weather-company-data-demo.{APPDomain}){: new_window}使用的[圖示集](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}。

## 度量單位
{: #units_measure}

當您使用 REST API 時，不需要明確傳遞度量單位。這些 API 在 URL 中預設為使用與語言碼相關聯的度量單位。不過，如果您想要提供不同於預設值的度量單位，則可以傳入度量單位以置換預設值。

* 若為 en-US 或 en，預設度量單位代碼為 English/Imperial。單位代碼為 `e`。
* 若為 en-GB，預設度量單位為 Hybrid-UK。單位代碼為 `h`。
* 若為其他項目，預設度量單位為 Metric。單位代碼為 `m`。

## 語言翻譯
{: #language_translation}

REST API 翻譯了一些詞組和度量單位。當您格式化要求 URL 時，必須提供有效的語言。下列欄位已翻譯：

|**欄位**           |**說明**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |24 小時期間的敘述性預測|
|`dow`               |星期幾|
|`wind_phrase`       |說明 12 小時白天部分的風向和風速的詞組|
|`wdir_cardinal`     |以紅色標記表示的白天平均風向|
|`daypart_name`      |12 小時白天部分的名稱（不包含最初 48 小時中的白天名稱）|
|`temp_phrase`       |包含 12 小時預測期間預測到的高溫或低溫的簡短詞組|
|`shortcast`         |敘述性預測的可感測天氣縮寫部分|
|`long_daypart_name` |使用擴充格式的有效天氣預測的指定時間範圍。指定的時間範圍可以是 12 小時期間或 24 小時期間。|
|`golf_category`     |以適用於打高爾夫球之天氣狀況的詞組表示的高爾夫球指數種類|
|`phrase_nnchar`     |白天可感測天氣詞組|
|`lunar_phrase`      |月相的三個字元簡短代碼|
|`uv_desc`           |UV 指數說明，其提供與因曝露而造成皮膚傷害相關聯的風險等級來補充說明 UV 指數值|
|`wx_phrase`         |在報告站觀測到的天氣狀況文字說明。|
|`pressure_desc`     |說明過去 1 小時大氣壓力讀數變化的詞組。|
|`headline_text`     |位置事件的標題文字。|
|`event_desc`        |事件的說明。|
|`cntry_name`        |事件發生的國家/地區名稱，以大小寫混合格式提供。|
*表 4. 翻譯的回應欄位*

## 處理 API 回應中的空值或遺漏資料欄位
{: #handling_null_or_missing}

如果資料欄位因為資料無法使用而是空值，則 REST API 會傳回以 `null` 字眼標記的適當欄位，或根本不會傳回欄位。

## 處理錯誤
{: #handling_errors}

下列錯誤碼適用於所有 API：

|**錯誤** |**說明**                                    |
|----------|---------------------------------------------------|
|400       |錯誤的要求。由於語法形態異常，伺服器無法瞭解要求。這個錯誤碼是針對所有 API 實作。如果提供的任何參數無效，API 會拒絕此要求。|
|401       |未獲授權。要求需要鑑別。|
|403       |已禁止。伺服器已瞭解要求，但拒絕完成它。|
|404       |找不到。如果 API 要求中沒有必要的參數，則會傳回包含 404 錯誤碼的 MissingParameterException 錯誤。|
|500       |內部伺服器錯誤。由於伺服器遭遇到非預期的狀況，所以無法完成此要求。|
*表 5. 錯誤回應碼*

發生錯誤時的回應一律相同。可以在一個回應中傳回多個錯誤碼。例如，可能傳回的 JSON 錯誤回應如下：

```
{
  metadata: {transaction_id: "1411496413365:-1880721071"
  },
  success: false,
  errors: [
    {
      error: {
        code: "NDF-0001",
        message: "There was no data found for your product query."
      }
    }
}
```
