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

某些 {{site.data.keyword.weather_short}} API 可以进行聚集。可以使用聚集将两个或更多原子 API 调用组合成单个 HTTP 请求。
{: shortdesc}

原子 API 调用引用用于定义聚集别名的任何 API。每个 API 用户文档在 URL 格式部分中包含聚集名称的别名（如果为聚集提供了别名）。例如，标准每天天气预测 API 的聚集别名为 `v2fcstdaily10`，此别名可作为聚集请求的一部分用于检索 10 天每天天气预测。

聚集具有以下限制：

* 完整聚集的未压缩响应总大小必须小于 1 兆字节。
* URL 的长度必须少于约 4,096 字符（包括协议、主机名、路径和查询字符串）。
* 最多可以聚集 10 个原子 API。

**注：**如果请求或响应违反上述任何限制，您都会收到错误响应以及 500 HTTP 状态码（通常为 500 或 502，但也可能会返回其他状态码）。

## 聚集 API URL
聚集 API URL 以 `/v2/aggregate/` 开头，后跟用分号分隔的别名。例如，要聚集 10 天每天天气预测 API (`v2fcstdaily10`) 以及最新观察数据 (`v2obscurrent`)，请使用以下格式：

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## 原子 API 和聚集的查询参数规则
查询参数对于所有请求都是必需的。用于聚集的查询参数的传递方式与原子 API 调用基本相同，但还有额外的几个规则。以下各部分描述了可以如何应用查询参数来构成不同的聚集。

### 指定应用于所有原子 API 的查询参数

最简单的聚集形式是将查询参数应用于所有原子 API。在这种情况下，查询参数的标准格式为 `?param1=value1&amp;param2=value2`。

以下示例将 `geocode=31.44,84.33&amp;language=en&amp;units=e` 应用于 `v2fcstdaily10` 和 `v2obscurrent` 原子 API 的请求：

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### 指定哪些原子 API 接收哪些查询参数。

如果需要指定特定原子 API 的参数，那么查询参数可以使用位置表示法 `?R1.param1=value1&amp;R2.param2=value2`。此格式将 `param1` 用于第一个原子 API，将 `param2` 用于第二个原子 API。

以下示例将 `geocode=31.44,84.33&amp;language=en&amp;units=e` 应用于 `v2fcstdaily10`，将 `geocode=44.44,50.23&amp;language=en&amp;units=e` 应用于 `v2obscurrent`。

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### 对特定原子 API 的查询参数分组

您可以将位置表示法用作以逗号分隔的格式 (`?R1,R2.param1=value1&amp;param2=value2`)，以对参数分组。
此格式将 `param1` 用于第一个和第二个原子 API，将 `param2` 用于所有原子 API。

以下示例将 `geocode=34.06,84.21&amp;language=enUS&amp;units=e` 应用于 `v2fcstdaily10` 和 `v2obscurrent`，将 `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` 应用于 `v2loc`：

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### 以多种方式请求同一资源

您可以通过多种方式请求同一资源，例如以不同的语言或使用不同的度量单位。通过此格式，原子 API 可以在请求中重复：`/v2/aggregate/v2fcstdaily10;v2fcstdaily10`，并且参数的位置表示法可用于指示用哪种方法请求哪种 API：`?R1.param1=value1&amp;R2.param1=value2`。在本例中，用户收到以不同方式设置格式或转换的同一资源。

以下示例将 `geocode=31.44,84.33&amp;language=en&amp;units=e` 应用于第一个 `v2fcstdaily10`，将 `geocode=31.44,84.33&amp;language=fr&amp;units=m` 应用于第二个 `v2fcstdaily10`：

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

以下示例将 `geocode=31.44,84.33&amp;language=en&amp;units=e` 应用于第一个 `v2fcstdaily10`，将 `geocode=33.54,85.43&amp;language=en&amp;units=e` 应用于第二个 `v2fcstdaily10`，以在多个位置中检索相同数据：

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




