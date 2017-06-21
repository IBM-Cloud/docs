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

# 入门
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} 服务可以帮助应用程序了解简短文本的语言，并对如何处理这些文本进行预测。分类器通过示例数据进行学习，然后可以返回培训分类器时未包含的文本的信息。
{:shortdesc}

您可以在不到 15 分钟的时间内创建并培训 {{site.data.keyword.nlclassifiershort}}。

## 第 1 步：登录、创建服务并获取凭证

如果已经知道用于 {{site.data.keyword.nlclassifiershort}} 服务实例的凭证，请跳过此步骤。
{: tip}

1.  转至 [{{site.data.keyword.nlclassifiershort}} 服务](https://console.{DomainName}/catalog/services/natural-language-classifier/)，然后注册免费帐户或登录到您的 {{site.data.keyword.Bluemix_notm}} 帐户。
1.  登录后，在 {{site.data.keyword.nlclassifiershort}} 页面的**服务名称**字段中，输入 `Classifier-tutorial` 以标识此服务实例，然后单击**创建**。
1.  复制凭证：
    1.  单击**服务凭证**。
    2.  单击“服务凭证”部分中的**查看凭证**。
    3.  复制 `username` 和 `password` 值。

## 第 2 步：创建并培训分类器
分类器通过示例学习后，才能返回以前从未处理过的文本的信息。示例数据指的是“训练数据”。创建分类器时，上传训练数据。

1.  下载样本 <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code>。这是[演示 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://natural-language-classifier-demo.mybluemix.net){:new_window} 中使用的相同培训数据。

	该文件为 CSV 格式，包含两列。第一列是文本输入。第二列是该文本的类：temperature 或 condition。查看该文件可看到相应的条目。
2.  发出以下 curl 命令以调用 `POST /classifiers/` 方法；此方法将上传培训数据，并创建分类器：
    -   将 `{username}` 和 `{password}` 替换为上一阶段中复制的服务凭证。
    -   将 training\_data 的位置修改为指向 `weather_data_train.csv` 文件的保存位置。

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	响应包含新的分类器标识和状态。例如：

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

	培训将立即开始，并且必须在培训完成后，您才能查询分类器。
3.  定期检查培训状态，直到看到状态 `Available`。使用此样本数据，培训大约需要 6 分钟：
	- 发出 `GET /classifiers/{classifier_id}` 调用可检索分类器的状态。在以下示例中，将 `{username}`、`{password}` 和 `{classifier_id}` 替换为您的信息：

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## 第 3 步：对文本分类
现在，分类器已经过培训，可以对其进行查询。

1.  对一些与天气相关的问题分类，以查看新培训的分类器如何响应。下面是示例调用。将 `{username}`、`{password}` 和 `{classifier_id}` 替换为您的信息：

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	API 返回的响应包含分类器具有最高置信度的类的名称。其他“类/置信度”对按置信度降序列出：

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

	置信度值表示为百分比，值越大表示置信度越高。响应最多包含 10 个类。

	如果培训数据中的类少于 10 个，那么所有置信度值的和为 100%。在此样本培训数据中，只定义了两个类，所以只能返回两个类。
2.  查看问题的顶级类，以了解分类器是如何对其进行预测的。

	下面是其他一些可分类的样本问题：

	-   Is it hot outside?
	-   Will it be windy?
	-   Will we see some sun?
	-   What is the expected high for today?
	-   Will it be foggy tomorrow morning?

	其中一个样本问题包含未对分类器进行培训的词语（“foggy”）。您无须执行额外工作来识别这些“缺少”的词语，分类器对于这些词语就能获得不错的分数。请尝试使用包含培训数据中没有的词（例如，“sleet”或“storm”）的其他问题。

已完成！您已在 {{site.data.keyword.nlclassifiershort}} 服务中创建、培训和查询了分类器。

## 删除教程分类器

您可能会希望从教程中删除此分类器，以便可以使用自己的培训数据创建分类器以供自己使用。要删除分类器，请调用 `DELETE /classifiers/{classifier_id}` 方法。

如前所述，将以下命令中的 `{username}`、`{password}` 和 `{classifier_id}` 替换为您的信息。

```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

 对该命令的响应为空 JSON 对象。

## 后续操作
您已基本掌握了如何使用 {{site.data.keyword.nlclassifiershort}}。现在更深入地学习：
- 学习如何[使用自己的数据](/docs/natural-language-classifier/using-your-data.html)来培训分类器。
- 阅读 [API 参考 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window} 中有关该 API 的信息。
- 在 [API Explorer ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window} 中与该 API 交互。
- 查看 [Node.js 入门模板应用程序](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window}以获取示例 Web 应用程序。
