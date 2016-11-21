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

您可以使用 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} 来检索天气数据。可以测试 API 操作并立即查看结果，以帮助您更快地构建应用程序。
{: shortdesc}

从参考文档中，单击**列出操作**可查看每个操作的详细信息。指定参数并单击**试试看！**时，系统可能会要求您提供凭证。必须提供 `VCAP_SERVICES` 环境变量中的用户名和密码。通过打开应用程序并单击目录中的**环境变量**，可以找到这些信息。

**注：**每个区域都是独立的。不能将在一个区域中为您供应的服务凭证用于向另一个区域中的服务进行认证。
未输入正确的凭证将导致响应主体中显示*未授权*消息。

使用 REST API，可以通过提供经度和纬度坐标表示地理位置来检索天气数据。可以使用以下 API。

|**API**                                  |**描述**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |根据您所提供的格式，返回某个地理位置未来 48 小时的每小时天气预测。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。每小时天气预测数据最多可以包含每个位置 48 小时的天气预测。对于某个位置，在收到新数据后，必须废弃先前所有每小时天气预测。|
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |根据您所提供的格式，返回某个地理位置 3、5、7 或 10 天的每天天气预测。要检索的天数以 `3day`、`5day`、`7day` 或 `10day` 的格式指定。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。每一个每天天气预测都可以包含白天天气预测、晚上天气预测和 24 小时天气预测。这些分段在 JSON 响应中是不同的对象。 每天天气预测中的白天天气预测数据在当地时间下午 3:00 后不再可用。在当地时间下午 3:00，您的应用程序不会再显示白天天气预测。|
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|根据您所提供的格式，返回某个地理位置 3、5、7 或 10 天的 6 小时每天天气预测。要检索的天数以 `3day`、`5day`、`7day` 或 `10day` 的格式指定。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。每一个每天天气预测都可以包含早晨、下午、晚上和过夜天气预测。这些分段在 JSON 响应中是不同的对象。|
|`GET /v1/{geocode or location ID}/observations.json`              |返回某个地理位置的最新天气状况。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。这些最近的观察数据会保留在数据库中，特定报告站的观察数据最多保留 10 分钟，每个观察站的观察数据最多保留 24 小时。最近的观察数据会基于观察数据的日期/时间戳记，通过先进/先出方法持续更新并进行替换（使用最新的观察数据来循环数据，并将最早的观察数据移至归档存储器）。|
|`GET /v1/{geocode or location ID}/observations/timeseries.json`   |返回某个地理位置的最新观察数据以及从当前日期和时间开始一直到过去 24 小时的观察数据。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{locationId}`。天气观察数据是从部署在世界各地的物理设备以及最新天气观察 数据中收集而来的。|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |返回国家气象局 (NWS)、加拿大环境部和欧洲 MeteoAlarm 发布的天气监测、警告、预警和公告，包括 49 种语言的事件描述、国家或地区名和警报标题的翻译。您可以提供 `geocode/{latitude}/{longitude}`、`country/{countrycode}`、`country/{countrycode}/state/{statecode}`/ 或 `country/{countrycode}/area/{areaid}`。|
|`GET /v1/alert/{detail_key}/details.json`                         |返回国家气象局 (NWS)、加拿大环境部和欧洲 MeteoAlarm 发布的天气监测、警告、预警和公告。详细信息包括政府气象部门就指定区域发布的警报的深入信息，包括 49 种语言的事件描述、国家或地区名和警报标题的翻译。|
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |返回来自国家气象局观察站的每天年历信息（仅限美国），时间跨度为 10 到 30 年或更长。该信息由国家气象数据中心 (NCDC) 收集和提供。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{PostalLocationId}`。|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |返回来自国家气象局观察站的每月年历信息（仅限美国），时间跨度为 10 到 30 年或更长。该信息由国家气象数据中心 (NCDC) 收集和提供。您可以提供 `geocode/{latitude}/{longitude}` 或 `location/{PostalLocationId}`。|
|`GET /v3/location/{search or point}`                                  |提供查找位置名或地理位置代码（经度和纬度）的能力，用于检索匹配请求的位置集。定位服务支持按城市名或邮政编码搜索。|
*表 1. {{site.data.keyword.weather_short}} API 摘要*

## 每天和当天天气预测
{: #daily_intraday}
每天天气预测 API 可以包含每个位置多天的每天天气预测。每天的天气预测可以包含多达三个不同的天气预测。对于任何天气预测日，API 可以返回白天、夜晚和 24 小时天气预测。


当天天气预测 API 可以包含每个位置多天的每天天气预测。每天的天气预测包含四个不同的 6 小时天气预测：上午（上午 7 点到下午 1 点）、下午（下午 1 点到晚上 7 点）、夜晚（晚上 7 点到凌晨 1 点）和过夜（凌晨 1 点到上午 7 点）。
当天天气预测在结构上与每天天气预测类似。


每一段都有日段号码、星期名称和日段名称。例如，以下示例针对星期四早晨 API 生成的天气预测，显示 `num`、`dow` 和 `daypart_name` 的数据字段顺序和数据值：

* 1，星期四，早晨
* 2，星期四，下午
* 3，星期四，夜晚
* 4，星期四，过夜
* 5，星期五，早晨
* 6，星期五，下午
* 7，星期五，夜晚
* 8，星期五，过夜

## 现状和时间序列观察数据
{: #time_series}

现状和时间序列天气观察数据提供有关温度、降水、风力、气压、能见度、紫外线 (UV) 辐射以及其他相关观察元素的信息，包括观察站、观察日期/时间、天气图标代码和用语。时间序列观察数据与最新观察数据的差异在于观察数据时间段，这将生成一个或多个观察数据集。

最新天气状况是在不使用时间参数时请求的位置的最新观察数据。这将返回一个数据集。时间序列观察数据包含过去的观察数据，一直到（且包括）过去 24 小时所请求位置的观察数据。

最近的观察数据会保留在主数据库中，最多保留特定报告站的 48 小时（2 天）的观察数据。最近的观察数据会基于观察数据的日期/时间戳记，通过先进/先出方法持续更新并进行替换（使用最新的观察数据来循环数据，并将最早的观察数据移至归档存储器）。保留且可从任何观察站可用的数据量可能会超过 24 小时单个观察报告的数据量。
观察次数由观察类型确定。

## 警报标题和详细信息
{: #alerts_levels}
警报 API 会返回与严重雷暴、龙卷风、地震和洪水相关的天气警报标题。
这些 API 还会返回非天气警报，如拐卖儿童警报和执法部门警告。


**注**：仅美国、加拿大和欧洲可以使用此 API。

警报标题 API 在 `detail_key` 属性中提供密钥值，用于访问警报详细信息 API 中的警报详细信息。
查询警报标题 API，以获取 `detail_key` 值，然后使用 `detail_key`，检索警报详细信息 API 响应。

**注**：您必须显示应用程序中所显示的任何警报数据的数据源属性。

属性短语必须显示以下信息：

*< 办公室名称发出 > - &lt;办公室行政区代码&gt;、&lt;办公室国家或地区代码&gt;、&lt;来源&gt;、&lt;免责声明&gt;*

例如：
* 国家气象局发出 - 美国俾斯麦
* 中央气象和地球动力学研究所发出 - 澳大利亚 EMETNET-Meteoalarm

## 年历信息
{: #almanac_details}
年历 API 需要位置标识和位置类型（城市或邮政编码），或者经度和纬度对，来检索特定位置的信息。


当您在 URL 中使用 `location` 时，位置必须包括位置标识（邮政编码），以及位置类型和国家或地区代码。
当您在 URL 中使用 `geocode` 时，搜索位置必须是有效的经度和纬度组合。


年历 API 使用参数来指定每天或每月数据、信息的特定日期或日期范围，以及返回数据时所使用的度量单位。


日期参数为 `start` 和 `end`。`start` 参数是必需参数，而 `end` 参数为可选参数。当一起使用这两个参数时3，组合会返回日期范围而不是数据的特定月或天。


用于检索每天年历结果的日期格式为四位数字值，代表所需数据的月和天，即 MMDD。任何单一数字天都**必须**具有前置零，例如 01。

用于检索每月结果的日期格式为月，即 MM。任何单一数字月都**必须**具有前置零，例如 01。任何其他格式都会导致 API 错误，且不会返回任何数据。

**注**：如果您未在请求中提供日期值，那么系统会返回状态 404（错误的请求）。API 不会提供缺省值。

## URL 构造
{: #url_construction}

REST API 使用常用 URL 结构和查询参数来请求和过滤天气数据。传递给 API 的 URL 如下所示进行构造：

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

例如：

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**属性**     |**描述**                                    |
|------------------|---------------------------------------------------|
|`主机名`        |托管的 URL 路径。例如，`https://twcservice.mybluemix.net:443/api/weather`。|
|`版本`         |当前迭代。例如，`v1`。|
|`location`        |地理位置代码或位置标识。位置分组可以是 `geocode` 或 `location`。例如，`geocode/45.4214/75.6919` 代表加拿大渥太华。 如果提供了地理位置代码坐标，那么 API 会返回最近可用位置的数据。 句点用作十进制分隔符，逗号用于分隔经度和纬度值。如果提供了地理位置代码，那么会在响应的元数据中返回使用的实际经度和纬度值。|
|`商品组`   |产品。例如，`observations` 或 `forecast`。产品子组（例如 `historical`）是可选的。|
|`date`            |日期类型。例如，`daily` 或 `monthly`。|
|`format`          |格式。例如，`3day`、`5day`、`7day` 或 `10day`。|
|`单位`           |要返回的响应所用的单位（可选）。API 支持英制 (e)、公制 (m) 和英制混合 (h) 度量单位。如果提供了度量单位但未提供值，API 将以与语言代码对应的度量单位返回数据。响应的元数据中的“单位”参数中将返回缺省或请求的度量单位。|
|`语言`        |要返回的响应所用的语言。缺省值为 en-US。响应的元数据中的“语言”参数中将返回缺省或请求的转换语言。|
*表 2. URL 详细信息*

**注**：REST API 使用 ISO 3166 标准的国家或地区代码。有关更多信息，请参阅 [ISO 标准在线浏览平台](https://www.iso.org/obp/ui/#search/code/){:new_window}。
API 使用 WGS84 地理位置代码坐标参考系统。有关更多信息，请参阅[基本地理词汇表](https://www.w3.org/2003/01/geo/){:new_window}。

## 图标代码和图像 
{: #icon_code_images}

当 {{site.data.keyword.weather_short}} REST API 在响应中返回图标代码时，您可以使用图标代码确定在您的应用程序中显示哪个图标图像。
API 响应中的图标代码和图标图像的文件名之间存在一对一关系。
例如，如果 API 响应包括 `icon_code` 1，那么您可以使用文件名 `01.png` 显示匹配的图标图像。

在代码中，您可以创建使用 `icon_code` 的函数来确定图标图像的 URL。例如：

```
function getIconURL(code) {
    return "images/weathericons/icon" + code + ".png";
}
```

下表包含可用于 {{site.data.keyword.weather_short}} REST API 的图标代码、描述和图像。该表指示预测或观察 API 中是否使用图标，以及图标是否可用于“夜晚”或“白天”预测部分。

|**代码**|**描述**|**图像**|**API 用法** |**夜晚或白天**|
|----|--------------------------|------------|------------|--------------------|
| 0  | 龙卷风                  | <img src="images/00.png " width="100" height="100" alt="图标图像"/>| 预测                | 夜晚和白天 |
| 1  | 热带风暴           | <img src="images/01.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 2  | 飓风                | <img src="images/02.png " width="100" height="100" alt="图标图像"/>| 预测                | 夜晚和白天 |
| 3  | 强降雨            | <img src="images/03.png " width="100" height="100" alt="图标图像"/>| 预测                | 夜晚和白天 |
| 4  | 雷和冰雹         | <img src="images/04.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 5  | 雨转雨夹雪     | <img src="images/05.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 6  | 雨/雨夹雪             | <img src="images/06.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 7  | 风雪交加/雨夹雪  | <img src="images/07.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 8  | 冻毛毛雨         | <img src="images/08.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 9  | 小雨                  | <img src="images/09.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 10 | 冻雨            | <img src="images/10.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 11 | 小雨               | <img src="images/11.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 12 | 雨                     | <img src="images/12.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 13 | 零星小雪       | <img src="images/13.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 14 | 小雪               | <img src="images/14.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 15 | 飘雪  | <img src="images/15.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 16 | 雪                     | <img src="images/16.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 17 | 冰雹                     | <img src="images/17.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 18 | 雨夹雪                    | <img src="images/18.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 19 | 沙尘暴 | <img src="images/19.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 20 | 雾                    | <img src="images/20.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 21 | 霾/有风             | <img src="images/21.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 22 | 烟雾/有风            | <img src="images/22.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 23 | 微风                   | <img src="images/23.png " width="100" height="100" alt="图标图像"/>| 预测                | 夜晚和白天 |
| 24 | 雾/有风    | <img src="images/24.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 25 | 寒冷/冰晶    | <img src="images/25.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 26 | 多云                   | <img src="images/26.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 27 | 大部地区多云            | <img src="images/27.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 28 | 大部地区多云            | <img src="images/28.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 白天         |
| 29 | 部分地区多云            | <img src="images/29.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜间       |
| 30 | 部分地区多云            | <img src="images/30.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 白天         |
| 31 | 晴                    | <img src="images/31.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜间       |
| 32 | 晴天                    | <img src="images/32.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 白天         |
| 33 | 大部分时间晴      | <img src="images/33.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜间       |
| 34 | 大部分时间晴      | <img src="images/34.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 白天         |
| 35 | 雨夹冰雹        | <img src="images/35.png " width="100" height="100" alt="图标图像"/>| 预测                | 白天         |
| 36 | 热                      | <img src="images/36.png " width="100" height="100" alt="图标图像"/>| 预测                | 白天         |
| 37 | 局部雷暴   | <img src="images/37.png " width="100" height="100" alt="图标图像"/>| 预测                | 白天         |
| 38 | 雷暴            | <img src="images/38.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 39 | 零星阵雨        | <img src="images/39.png " width="100" height="100" alt="图标图像"/>| 预测                | 白天         |
| 40 | 大雨               | <img src="images/40.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 41 | 零星雨夹雪   | <img src="images/41.png " width="100" height="100" alt="图标图像"/>| 预测                | 白天         |
| 42 | 大雪               | <img src="images/42.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
| 43 | 暴风雪                 | <img src="images/43.png " width="100" height="100" alt="图标图像"/>| 预测                | 夜晚和白天 |
| 44 | 不可用（无）      | <img src="images/44.png " width="100" height="100" alt="图标图像"/>| 预测                | 夜晚和白天 |
| 45 | 零星阵雨        | <img src="images/45.png " width="100" height="100" alt="图标图像"/>| 预测                | 夜间       |
| 46 | 零星雨夹雪   | <img src="images/46.png " width="100" height="100" alt="图标图像"/>| 预测                | 夜间       |
| 47 | 零星雷暴  | <img src="images/47.png " width="100" height="100" alt="图标图像"/>| 预测和观察 | 夜晚和白天 |
*表 3. 图标代码和图像*

您可以将此天气图标集下载为 [PNG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_png.zip){:new_window} 或 [SVG](https://twcdocs.mybluemix.net/download/weather_icons_200x200_svg.zip){:new_window} 格式，并在您的应用程序中使用。 

您还可以下载 [{{site.data.keyword.weather_short}} 演示应用程序](http://weather-company-data-demo.{APPDomain}){: new_window}使用的[图标集](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}。

## 度量单位
{: #units_measure}

使用 REST API 时，无需显式传递度量单位。这些 API 缺省为与 URL 中的语言代码关联的度量单位。但是，如果要提供不同于缺省值的度量单位，那么可以传递度量单位以覆盖缺省值。

* 对于 en-US 或 en，缺省度量单位为“英制”。单位代码为 `e`。
* 对于 en-GB，缺省度量单位为“混合英制”。单位代码为 `h`。
* 对于其他语言，缺省度量单位为“公制”。单位代码为 `m`。

## 语言转换
{: #language_translation}

REST API 将转换用语和度量单位。设置请求 URL 的格式时，必须提供有效的语言。将转换以下字段：

|**字段**           |**描述**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |24 小时时间段的描述性天气预测|
|`dow`               |一周中的某天|
|`wind_phrase`       |用于描述 12 小时日段的风向和风速的用语|
|`wdir_cardinal`     |以基本表示法表示的白天平均风向|
|`daypart_name`      |12 小时日段的名称，不包括前 48 小时中的日期名称|
|`temp_phrase`       |包含 12 小时预测时间段的预测温度上限或下限的简短用语|
|`shortcast`         |描述性天气预测中缩写的感测天气部分|
|`long_daypart_name` |扩展格式的有效天气预测的指定时间范围。指定的时间范围可以为 12 小时制或 24 小时制。|
|`golf_category`     |高尔夫指数类别，用描述打高尔夫球的天气状况用语表示|
|`phrase_nnchar`     |白天感测天气用语|
|`lunar_phrase`      |三个字符构成的农历用语简短代码|
|`uv_desc`           |UV 指数描述，通过提供因曝晒使皮肤受损的关联危险级别，对 UV 指数值进行补充|
|`wx_phrase`         |在报告站中已观察天气条件的文本描述。|
|`pressure_desc`     |用于描述在过去一小时，大气压读数变化的短语。|
|`headline_text`     |位置事件的标题文本。|
|`event_desc`        |事件的描述。|
|`cntry_name`        |发生事件的国家或地区名，以混合大小写字母提供。|
*表 4. 转换的响应字段*

## 处理 API 响应中的数据字段为空或缺少数据字段的问题
{: #handling_null_or_missing}

如果由于数据不可用而导致数据字段为空，那么 REST API 会返回包含 `null` 的相应字段标签，或者根本就不返回字段。

## 处理错误
{: #handling_errors}

以下错误状态码通用于所有 API：

|**错误** |**描述**                                    |
|----------|---------------------------------------------------|
|400       |错误的请求。由于语法格式不正确，因此服务器无法识别请求。此错误代码适用于所有 API。如果提供了任何无效参数，那么 API 会拒绝该请求。|
|401       |未授权。请求需要认证。|
|403       |已禁止。服务器识别到请求，但拒绝执行该请求。|
|404       |找不到。如果必需参数在 API 请求中不存在，那么将返回 MissingParameterException 错误和 404 错误代码。|
|500       |内部服务器错误。服务器遇到意外情况，导致无法执行请求。|
*表 5. 错误响应代码*
有关错误的响应始终是相同的。在一个响应中可能会返回多个错误代码。
例如，返回的 JSON 错误响应可能如下所示：

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
