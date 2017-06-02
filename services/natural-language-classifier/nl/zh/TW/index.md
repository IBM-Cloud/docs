---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:download: .download}
{:tip: .tip}

# 開始使用
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} 服務可協助您的應用程式瞭解簡短文字的語言，並預測如何處理它們。分類器會先瞭解您的範例資料，接著可以傳回未對其進行訓練之文字的資訊。
{:shortdesc}

您可以在不超過 15 分鐘的時間內建立及訓練 {{site.data.keyword.nlclassifiershort}}。

## 步驟 1：登入、建立服務，並取得認證

如果您已知道 {{site.data.keyword.nlclassifiershort}} 服務實例的認證，請跳過此步驟。
{: tip}

1.  移至 [{{site.data.keyword.nlclassifiershort}} 服務](https://console.{DomainName}/catalog/services/natural-language-classifier/)，並註冊免費帳戶或登入 {{site.data.keyword.Bluemix_notm}} 帳戶。
1.  登入之後，請在 {{site.data.keyword.nlclassifiershort}} 頁面的**服務名稱**欄位中鍵入 `Classifier-tutorial` 來識別服務的這個實例，然後按一下**建立**。
1.  複製認證：
    1.  按一下**服務認證**。
    2.  按一下「服務認證」區段中的**檢視認證**。
    3.  複製 `username` 及 `password` 值。

## 步驟 2：建立及訓練分類器
分類器要先瞭解範例，才能傳回以前未看過之文字的資訊。範例資料稱為「訓練資料」。當您建立分類器時，即可上傳訓練資料。

1.  下載範例 <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code>。這是[展示 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://natural-language-classifier-demo.mybluemix.net){:new_window} 中所用的相同訓練資料。

	此檔案的格式為 CSV 且內含兩個直欄。第一個直欄是文字輸入。第二個直欄是該文字的類別：溫度或狀況。請檢視檔案來查看項目。
2.  發出下列 curl 指令來呼叫 `POST /classifiers/` 方法，以上傳訓練資料，以及建立分類器：
    -   將 `{username}` 及 `{password}` 取代為您在前一個階段中所複製的服務認證。
    -   修改 training\_data 的位置，以指向您儲存 `weather_data_train.csv` 檔案的位置。

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	回應包括新的分類器 ID 及狀態。例如：

	```
	{
	  "name": "TutorialClassifier",
	  "language": "en",
	  "status": "Training",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/10D41B-nlc-1",
	  "classifier_id": "10D41B-nlc-1",
	  "created": "2015-05-28T18:01:57.393Z",
	  "status_description": "The classifier instance is in its training phase, not yet ready to accept classify requests"
	}
	```
	{: screen}

	訓練會立即開始，而且必須先完成，您才能查詢分類器。
3.  除非您看到`可用`狀態，否則請定期檢查訓練狀態。使用這個範例資料，訓練大約需要 6 分鐘：
	- 發出 `GET /classifiers/{classifier_id}` 呼叫，以擷取分類器的狀態。在下列範例中，請將 `{username}`、`{password}` 及 `{classifier_id}` 取代為您的資訊：

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## 步驟 3：分類文字
現在，已訓練過分類器，您可以對其進行查詢。

1.  分類一些天氣相關問題，以檢閱新訓練分類器的回應方式。以下是範例呼叫。請將 `{username}`、`{password}` 及 `{classifier_id}` 取代為您的資訊：

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	API 會傳回一個回應，其中包括分類器具有最高信任之類別的名稱。其他類別/信任配對則會依遞減信任順序列出：

	```
	{
	  "classifier_id": "10D41B-nlc-1",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1",
	  "text": "How hot will it be today?",
	  "top_class": "temperature",
	  "classes": [
	    {
	      "class_name": "temperature",
	      "confidence": 0.9998201258549781
	    },
	    {
	      "class_name": "conditions",
	      "confidence": 0.00017987414502176904
	    }
	  ]
	}
	```
	{: screen}

	信任值以百分比呈現，值越高，代表越受信任。回應最多包括 10 個類別。

	如果您訓練資料中的類別少於 10 個，則所有信任值的總和為 100%。 在此範例訓練資料中，只定義兩個類別，因此只會傳回兩個類別。
2.  檢閱問題的頂端類別，以查看分類器如何預測它們。

	以下是要分類的一些其他範例問題：

	-   Is it hot outside?（外面是否很熱？）
	-   Will it be windy?（會刮風嗎？）
	-   Will we see some sun?（會看到一些陽光嗎？）
	-   What is the expected high for today?（今天的預期最高溫度為何？）
	-   Will it be foggy tomorrow morning?（明早是否起霧？）

	其中一個範例問題包括分類器未受過訓練的術語 ("foggy")。分類器可以對這些「遺漏」術語進行良好評分，而您不需要執行額外工作即可識別它們。請嘗試其他問題，而這些問題包括不在訓練資料中的單字（例如，"sleet" 或 "storm"）。

已完成！您已在 {{site.data.keyword.nlclassifiershort}} 服務中建立、訓練及查詢分類器。

## 刪除指導教學分類器

因此，您可以使用專屬訓練資料來建立專用分類器，而且可能會想要從指導教學刪除此分類器。若要刪除分類器，請呼叫 `DELETE /classifiers/{classifier_id}` 方法。

如前所述，請將下列指令中的 `{username}`、`{password}` 及 `{classifier_id}` 取代為您的資訊。

```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

此指令的回應是空 JSON 物件。

## 下一步
您對如何使用 {{site.data.keyword.nlclassifiershort}} 有基本瞭解。現在，請更深入地探討：
- 瞭解如何[使用自己的資料](/docs/natural-language-classifier/using-your-data.html)來訓練分類器。
- 在 [API 參考資料 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window} 中閱讀 API。
- 在 [API 瀏覽器 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window} 中，與 API 互動。
- 查看範例 Web 應用程式的 [Node.js 入門範本應用程式](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window}。
