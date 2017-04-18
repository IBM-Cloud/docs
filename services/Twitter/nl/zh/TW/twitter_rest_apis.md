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

{{site.data.keyword.twittershort}} 服務包含 RESTful API，來搜尋及耗用 Twitter 內容。[查詢語言](twitter_rest_apis.html#querylanguage){: new.window}表格列出服務 API 所支援的查詢詞彙。我們提供了範例，示範如何建構查詢。
{:shortdesc}

## REST API 文件 {: #rest_api}
REST API 文件是使用 Swagger 所建置，而後者可讓您測試 API 作業以及立即檢視結果，以協助您更快速地建置應用程式。下列是目前可用的 API 作業：

* Search : 在 Decahose 或過濾的 PowerTrack 串流中尋找推文。
* Count : 根據指定的查詢，傳回推文數目。
* Check : 判定訊息清單是否符合	Twitter 原則及 Twitter 使用者。
* Tracks : 可讓「入門方案」使用者分配端點，來管理 PowerTrack 過濾器。

如需所支援 REST API 及其資源的相關資訊，請參閱 [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window} 參考資料。選取您的應用程式所在的區域。每一個地區都是獨立的；您無法使用在某個地區中佈建給您的服務認證來鑑別另一個地區中的服務。

從參考文件，按一下**清單作業**以檢視每一個作業的詳細資料。在按下**試用看看吧！**按鈕之後，您可能需要提供認證。您需要透過 **VCAP_SERVICES** 環境變數提供使用者名稱及密碼。開啟應用程式並按一下目錄中的**環境變數**，即可找到此資訊。

**附註**：若未輸入適當的認證，將會在回應主體中造成 Unauthorized 訊息。

**重要事項**：使用**試用看看吧！**特性建立的作用中追蹤將從 Twitter 收集推文，這會計入您的每月額度中。當不再需要追蹤時，請將其狀態變更為 **Inactive**，或是乾脆刪除追蹤。


## 查詢語言 {: #querylanguage}

您可以使用 {{site.data.keyword.twittershort}} 以透過豐富的一組查詢參數來搜尋	Twitter 內容，並過濾以產生更精確的結果。

查詢中支援下列布林運算子。 

| **運算子**        | **說明**                                                                                                                   | **範例**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| term1 **AND** term2 | 傳回同時含有 term1 及 term2 的推文。兩個詞彙之間的空格視為 AND，因此可以省略運算子。 | `#ibm twitter`      |
| term1 **OR** term2  | 傳回含有 term1 或 term2 的推文。    | `#money OR revenue` |
| -term1              | 傳回不含 term1 的推文。  |`ibm -apple`  |

*表 1. 布林運算子*

運算子優先順序："-" 優先於 "AND"，"AND" 優先於 "OR"。您應該使用括弧，讓運算子優先順序更為明確。例如，`large animals` -(`giraffes` OR `bears`) 會搜尋含有 large 及 animals 詞彙的推文，但是排除含有 giraffes 及 bears 的推文。

下表列出目前支援的查詢詞彙。

| **詞彙** 	| **說明** 	| **範例** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| keyword 	| 符合主體中含有 "keyword" 的推文。搜尋不區分大小寫。 	| analytics 	|
| "完全相符的詞組" 	| 符合含有確切關鍵字序列的推文。 	| "IBM and analytics" 	|
| `#hashtag` 	| 符合具有主題標籤 *#hashtag* 的推文。 	| `#insight2015` 	|
| `bio_lang:language` 	| 符合其設定檔語言設定符合指定的語言代碼之使用者的推文。如需支援的語言清單，請參閱 `lang:`。 	| `bio_lang:en` 	|
| `bio_location:"location"` 	| 符合設定檔位置設定包含指定 `location` 參照之使用者的推文。 	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| 符合其標籤位置或位置符合指定的國碼的推文。</br>**如需支援國碼的清單，請參閱**：http://en.wikipedia.org/wiki/ISO_3166-1 	| `country_code:us` 	|
| `followers_count: lowerLimit,upperLimit` 	| 符合擁有屬於指定範圍內一些關注者的使用者推文。upperLimit 是選用的，而且兩個限制都內含。 	| `followers_count:500` 	|
| `friends_count: lowerLimit,upperLimit` 	| 符合追蹤屬於指定範圍內一些使用者的使用者推文。upperLimit 是選用的，而且兩個限制都內含。 	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| 符合具有偏好使用者名稱 *twitterHandle* 之使用者的推文。不得包含 &commat; 符號。 	| `from:alexlang11` 	|
| `has:children` 	| 符合擁有小孩的使用者推文。 	| `has:children` 	|
| `is:married` 	| 符合已婚的使用者推文。 	| `is:married` 	|
| `is:verified` 	| 符合其中由 Twitter 所驗證之作者的推文。 	| `analytics is:verified` 	|
| `lang:language-code` 	| 符合特定語言的推文。支援的語言碼清單如下：<ul><li>`ar`（阿拉伯文）</li><li>`zh`（中文）</li><li>`da`（丹麥文）</li><li>`dl`（荷蘭文）</li><li>`en`（英文）</li><li>`fi`（芬蘭文）</li><li>`fr`（法文）</li><li>`de`（德文）</li><li>`el`（希臘文）</li><li>`he`（希伯來文）</li><li>`id`（印尼文）</li><li>`it`（義大利文）</li><li>`ja`（日文）</li><li>`ko`（韓文）</li><li>`no`（挪威文）</li><li>`fa`（波斯文）</li><li>`pl`（波蘭文）</li><li>`pt`（葡萄牙文）</li><li>`ru`（俄文）</li><li>`es`（西班牙文）</li><li>`sv`（瑞典文）</li><li>`th`（泰文）</li><li>`tr`（土耳其文）</li><li>`uk`（烏克蘭文）</li></ul>    | `lang:de`（符合德文的推文） 	|
| `listed_count: lowerLimit,upperLimit` 	| 符合屬於指定範圍內 Twitter 作者清單的推文。upperLimit 是選用的，而且兩個限制都內含。 	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| 符合由其經度與緯度座標及半徑所指定的地理區域的推文。</br></br>所有座標均以十進位來代表。`longitude` 必須是介於 -180 及 +180 之間的值，而 `latitude` 必須是介於 -90 及 +90 之間的值。指定支援範圍之外的值會傳回錯誤。這些值必須輸入為浮點數；不支援整數。</br></br>周圍區域的半徑必須指定為以哩 (mi) 或 公里 (km) 為單位。 	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| 符合在 "startTime" 當時或之後張貼的推文。"endTime" 是選用的，而且兩個限制皆為內含。時間戳記必須為下列其中一種格式：</br>"yyyy-mm-dd" 或 "yyyy-mm-ddTHH:MM:SSZ" </br>  時區係根據 UTC（世界標準時間）。指定小時、分鐘及秒時，根據規定的格式，時間必須以 T 及 Z 括住，如同指定格式。 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| 符合具有特定觀感的推文。支援的值如下：</br><dl>positive</dl> <dlentry>推文所含的正面觀感詞組多於負面觀感詞組。</dlentry> </br></br><dl>negative</dl> <dlentry>推文所含的負面觀感詞組多於正面觀感詞組。</dlentry>  </br></br><dl>neutral</dl>  <dlentry>推文不包含任何觀感，或為不提供觀感偵測的語言。</dlentry> </br></br><dl>ambivalent</dl>  <dlentry>推文包含等量的正面及負面觀感詞組。</dlentry> 	| `sentiment:positive` 	|
| `statuses_count: lowerLimit,upperLimit` 	| 比對已張貼屬於指定範圍內一些狀態的使用者推文。upperLimit 是選用的，而且兩個限制都內含。 	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| 比對其設定檔設定符合指定時區之使用者的推文。 	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| 比對其設定檔設定符合指定城市之使用者的推文。 	| `time_zone:"Dublin"` 	|

*表 2. 查詢詞彙*

所有支援的查詢詞彙都可以與上述布林運算子合併使用。例如，

`ibm -apple followers_count:500`
