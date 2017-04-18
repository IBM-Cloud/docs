---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 使用 Insights for Twitter REST API
{: #rest_apis}

{{site.data.keyword.twittershort}} 服务包含 RESTful API，用于搜索和使用 Twitter 内容。[查询语言](twitter_rest_apis.html#querylanguage){: new.window}表列出服务 API 支持的查询项。提供示例以演示如何构造查询。
{:shortdesc}

## REST API 文档 {: #rest_api}
REST API 文档是使用 Swagger 构建的，支持测试 API 操作并立即查看相应结果，以帮助您更快地构建应用程序。目前提供了以下 API 操作：

* 搜索：在 Decahose 或过滤的 PowerTrack 流中查找推文。
* 计数：根据指定的查询返回推文数。
* 检查：确定是否消息列表符合 Twitter 政策和 Twitter 用户的要求。
* 跟踪：为入门套餐用户提供一种端点来管理 PowerTrack 过滤器。

有关受支持 REST API 及其资源的更多信息，请参阅 [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window} 参考。选择应用程序所在的区域。每个区域都是独立的；不能使用在一个区域中为您供应的服务凭证向其他区域中的服务进行认证。

从参考文档中，单击**列出操作**可查看每个操作的详细信息。单击**试试看！**按钮之后，系统可能会要求您提供凭证。您需要提供 **VCAP_SERVICES** 环境变量中的用户名称和密码。通过打开应用程序并单击目录中的**环境变量**，可以找到这些信息。

**注**：无法提供正确的凭证会导致在响应主体中显示“未获授权”消息。

**重要信息**：使用**试试看！**功能创建的活动跟踪会从 Twitter 收集推文，这将计入您每月的限额。不再需要跟踪时，请将其状态更改为 **Inactive**，或者只要删除跟踪即可。


## 查询语言 {: #querylanguage}

通过 {{site.data.keyword.twittershort}}，您可以使用一组丰富的查询参数和过滤器来搜索 Twitter 内容，以生成更准确的结果。

查询中支持以下布尔运算符。 

| **运算符**        | **描述**                                                                                                                   | **示例**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| term1 **AND** term2 | 返回同时包含 term1 和 term2 的推文。两个项之间的空格被视为 AND，因此可以省略该运算符。 | `#ibm twitter`      |
| term1 **OR** term2  | 返回包含 term1 或包含 term2 的推文。    | `#money OR revenue` |
| -term1              | 返回不包含 term1 的推文。  |`ibm -apple`  |

*表 1. 布尔运算符*

运算符优先级：“-”优先于“AND”，而“AND”优先于“OR”。您应该使用括号来使运算符优先级更明确。例如，`large animals` -(`giraffes` OR `bears`) 搜索包含项“large”和“animals”的推文，但不包括含有“giraffes”和“bears”的推文。

下表列出了当前支持的查询项。

| **项** 	| **描述** 	| **示例** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| 关键字 	| 与主体中包含“关键字”的推文相匹配。搜索不区分大小写。 	| analytics 	|
| “短语完全匹配” 	| 与包含精确关键字序列的推文相匹配。 	| “IBM and analytics” 	|
| `#hashtag` 	| 与具有主题标签 *#hashtag* 的推文相匹配。 	| `#insight2015` 	|
| `bio_lang:language` 	| 与其概要文件语言设置与指定语言代码相匹配的用户发布的推文相匹配。请参阅 `lang:` 以获取支持语言的列表。 	| `bio_lang:en` 	|
| `bio_location:"location"` 	| 与其概要文件语言设置包含指定 `location` 引用的用户发布的推文相匹配。 	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| 与其标记的地点或位置与指定国家或地区代码相匹配的推文相匹配。</br>**有关支持的国家或地区代码的列表，请参阅：**http://en.wikipedia.org/wiki/ISO_3166-1 	| `country_code:us` 	|
| `followers_count: lowerLimit,upperLimit` 	| 与关注者人数位于指定范围内的用户发布的推文相匹配。upperLimit 是可选的，上限值和下限值均包含在内。 	| `followers_count:500` 	|
| `friends_count: lowerLimit,upperLimit` 	| 与关注用户数位于指定范围内的用户发布的推文相匹配。upperLimit 是可选的，上限值和下限值均包含在内。 	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| 与 preferredUsername 为 *twitterHandle* 的用户发布的推文相匹配。不能包含 &commat; 符号。 	| `from:alexlang11` 	|
| `has:children` 	| 与有孩子的用户发布的推文相匹配。 	| `has:children` 	|
| `is:married` 	| 与已婚的用户发布的推文相匹配。 	| `is:married` 	|
| `is:verified` 	| 与已通过 Twitter 验证的作者发布的推文相匹配。 	| `analytics is:verified` 	|
| `lang:language-code` 	| 与特定语言的推文相匹配。支持的语言代码的列表如下：<ul><li>`ar`（阿拉伯语）</li><li>`zh`（中文）</li><li>`da`（丹麦语）</li><li>`dl`（荷兰语）</li><li>`en`（英语）</li><li>`fi`（芬兰语）</li><li>`fr`（法语）</li><li>`de`（德语）</li><li>`el`（希腊语）</li><li>`he`（希伯来语）</li><li>`id`（印度尼西亚语）</li><li>`it`（意大利语）</li><li>`ja`（日语）</li><li>`ko`（韩语）</li><li>`no`（挪威语）</li><li>`fa`（波斯语）</li><li>`pl`（波兰语）</li><li>`pt`（葡萄牙语）</li><li>`ru`（俄语）</li><li>`es`（西班牙语）</li><li>`sv`（瑞典语）</li><li>`th`（泰语）</li><li>`tr`（土耳其语）</li><li>`uk`（乌克兰语）</li></ul>    | `lang:de`（与德语推文相匹配） 	|
| `listed_count: lowerLimit,upperLimit` 	| 与 Twitter 的作者列表位于指定范围内的推文相匹配。upperLimit 是可选的，上限值和下限值均包含在内。 	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| 与自某个地理区域发布的推文相匹配，地理区域通过其经度和维度坐标及半径指定。</br></br>所有坐标均用十进制度数表示。`longitude` 必须是介于 -180 到 +180 之间的值，而 `latitude` 必须是介于 -90 到 +90 之间的值。指定超出支持范围之外的值将返回错误。输入的值必须是浮点数字；不支持整数。</br></br>周围区域的半径必须使用英里 (mi) 或公里 (km) 指定。 	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| 与在“startTime”时或在“startTime”之后发布的推文相匹配。“endTime”是可选的，上限值和下限值均包含在内。时间戳记必须为下列其中一种格式：</br>“yyyy-mm-dd”或“yyyy-mm-ddTHH:MM:SSZ”</br>  时区基于 UTC（全球标准时间）。指定小时、分钟和秒时，根据规定的格式，时间必须用“T”和“Z”括起。 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| 与具有特定观点的推文相匹配。支持的值包括：</br><dl>正面</dl> <dlentry>推文包含的正面观点短语多于负面观点短语。</dlentry> </br></br><dl>负面</dl> <dlentry>推文包含的负面观点短语多于正面观点短语。</dlentry>  </br></br><dl>中立</dl>  <dlentry>推文不包含任何观点，或者使用的是未提供观点检测的语言。</dlentry> </br></br><dl>矛盾</dl>  <dlentry>推文包含的正面和负面观点短语数量相等。</dlentry> 	| `sentiment:positive` 	|
| `statuses_count: lowerLimit,upperLimit` 	| 与已发布的状态数位于指定范围内的用户发布的推文相匹配。upperLimit 是可选的，上限值和下限值均包含在内。 	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| 与其概要文件设置与指定时区相匹配的用户发布的推文相匹配。 	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| 与其概要文件设置与指定城市相匹配的用户发布的推文相匹配。 	| `time_zone:"Dublin"` 	|
*表 2. 查询项*

所有支持的查询项都可以使用之前描述的布尔运算符进行组合。例如，

`ibm -apple followers_count:500`
