---

copyright:
  years: 2016
lastupdated: "2016-06-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# API 聚集
{: #api_aggregation}

部分 {{site.data.keyword.weather_short}} API 可予以聚集。您可以使用聚集，將兩個以上的基本 API 呼叫合併為單一 HTTP 要求。
{: shortdesc}

基本 API 呼叫會參照任何定義用於聚集之別名的 API。如果 API 可用於聚集，則每個 API 使用者文件在 URL 格式區段都包含用於聚集的別名。例如，標準每日預測 API 具有用於聚集的別名 `v2fcstdaily10`，其可用來擷取 10 天的每日預測作為聚集要求的一部分。

聚集具有下列限制：

* 完整聚集的未壓縮回應大小總計必須小於 1 MB。
* URL 的長度必須小於大約 4,096 個字元（包括通訊協定、主機名稱、路徑及查詢字串）。
* 您最多可以聚集 10 個基本 API。

**附註：**如果您的要求或回應違反任一限制，則會收到一則含有 500 HTTP 狀態碼（一般是 500 或 502，然而可能傳回其他狀態碼）的錯誤回應。

## 聚集 API URL
聚集 API URL 以 `/v2/aggregate/` 為開頭，後面接著以分號區隔的別名。例如，若要聚集 10 天的每日預測 API (`v2fcstdaily10`) 及目前觀測資料 (`v2obscurrent`)，請使用下列格式：

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## 基本 API 及聚集的查詢參數規則
所有要求都需要查詢參數。用於聚集的查詢參數，其遞送方式與利用一些額外規則用於基本 API 呼叫的查詢參數相同。下列各節說明如何套用它們來構成不同的聚集。

### 指定套用到所有基本 API 的查詢參數

聚集的最簡單方式是將查詢參數套用到所有基本 API。在此情況下，查詢參數具有標準格式 `?param1=value1&amp;param2=value2`。

下列範例會將 `geocode=31.44,84.33&amp;language=en&amp;units=e` 套用到 `v2fcstdaily10` 的要求及 `v2obscurrent` 基本 API：

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### 指定哪些基本 API 接收哪些查詢參數

如果您需要指定特定基本 API 的參數，則查詢參數可以使用位置表示法 `?R1.param1=value1&amp;R2.param2=value2`。這個格式使用 `param1` 代表第一個基本 API，並使用 `param2` 代表第二個基本 API。

下列範例會將 `geocode=31.44,84.33&amp;language=en&amp;units=e` 套用到 `v2fcstdaily10`，並將 `geocode=44.44,50.23&amp;language=en&amp;units=e` 套用到 `v2obscurrent`。

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### 將特定基本 API 的查詢參數分組

您可以使用位置表示法作為 `?R1,R2.param1=value1&amp;param2=value2` 的逗點區隔格式，來將參數分組。
這個格式使用 `param1` 代表第一個及第二個基本 API，並使用 `param2` 代表所有基本 API。

下列範例會將 `geocode=34.06,84.21&amp;language=enUS&amp;units=e` 套用到 `v2fcstdaily10` 及 `v2obscurrent`。它會將 `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` 套用到 `v2loc`：

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### 以多種方式要求相同資源

您可以多種方式要求相同資源，例如使用不同語言或利用不同度量單位。利用這個格式，基本 API 可以在要求中重複使用：`/v2/aggregate/v2fcstdaily10;v2fcstdaily10`，而參數的位置表示法可以用來指出以何種方式要求哪個 API：`?R1.param1=value1&amp;R2.param1=value2`。在此情況下，使用者會收到以不同方式格式化或翻譯的相同資源。


下列範例會將 `geocode=31.44,84.33&amp;language=en&amp;units=e` 套用到第一個 `v2fcstdaily10`，並將 `geocode=31.44,84.33&amp;language=fr&amp;units=m` 套用到第二個 `v2fcstdaily10`：

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

下列範例會將 `geocode=31.44,84.33&amp;language=en&amp;units=e` 套用到第一個 `v2fcstdaily10`，並將 `geocode=33.54,85.43&amp;language=en&amp;units=e` 套用到第二個 `v2fcstdaily10` 來擷取相同資料的多個位置：

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




