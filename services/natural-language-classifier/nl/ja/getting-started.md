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

# 開始
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} サービスは、アプリケーションがショート・テキストの言語を理解し、それらのテキストの処理方法を予測するのに役立ちます。分類子は、サンプル・データから学習した後、トレーニングされていないテキストに関する情報を返すことができるようになります。
{:shortdesc}

{{site.data.keyword.nlclassifiershort}} は、15 分未満で作成してトレーニングできます。

## ステップ 1: ログイン、サービスの作成、および資格情報の取得

{{site.data.keyword.nlclassifiershort}} サービス・インスタンスの資格情報が既にわかっている場合は、このステップをスキップしてください。
{: tip}

1.  [{{site.data.keyword.nlclassifiershort}} サービス](https://console.{DomainName}/catalog/services/natural-language-classifier/)にアクセスして、無料アカウントに登録するか、{{site.data.keyword.Bluemix_notm}} アカウントにログインします。
1.  ログイン後に、{{site.data.keyword.nlclassifiershort}} ページで**「サービス名」** フィールドに `Classifier-tutorial` と入力してサービスのこのインスタンスを指定し、**「作成」**をクリックします。
1.  資格情報をコピーします。
    1.  **「サービス資格情報」**をクリックします。
    2.  「サービス資格情報」セクションで**「資格情報の表示」**をクリックします。
    3.  `username` 値と `password` 値をコピーします。

## ステップ 2: 分類子の作成およびトレーニング
分類子は、以前見たことのないテキストに関する情報を返す前にサンプルから学習します。それらのサンプル・データは、「トレーニング・データ」と呼ばれます。分類器を作成する際は、トレーニング・データをアップロードします。

1.  サンプルの <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code> をダウンロードします。 これは、[デモ ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](http://natural-language-classifier-demo.mybluemix.net){:new_window} で使用されるサンプルのトレーニング・データです。

	このファイルは、2 つの列から成る CSV フォーマットのファイルです。最初の列はテキスト入力です。2 番目の列は、そのテキストのクラス (temperature または condition) です。このファイルを表示して、項目を確認します。
2.  以下の curl コマンドを発行して、トレーニング・データをアップロードして分類子を作成する `POST /classifiers/` メソッドを呼び出します。
    -   `{username}` と `{password}` を、前のステージでコピーしたサービス資格情報で置き換えます。
    -   training\_data の場所を、`weather_data_train.csv` ファイルを保存した場所を指すように変更します。

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	応答には、新規分類子 ID と状況が含まれています。以下に例を示します。

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

	トレーニングが即時に開始されます。分類子を照会するには、その前にトレーニングが終了している必要があります。
3.  `Available` の状況が表示されるまで、トレーニング状況を定期的に確認してください。このサンプル・データでは、トレーニングは約 6 分かかります。
	- `GET /classifiers/{classifier_id}` 呼び出しを発行して、分類子の状況を取得します。以下の例では、`{username}`、`{password}`、および `{classifier_id}` をご自分の情報で置き換えてください。

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## ステップ 3: テキストの分類
分類子のトレーニングが終了したため、分類子を照会できます。

1.  いくつかの天気関連の質問を分類して、新たにトレーニングされた分類子がどのように応答するかを確認します。以下に、呼び出しの例を示します。`{username}`、`{password}`、および `{classifier_id}` をご自分の情報で置き換えてください。

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	API は、分類子が最も高い信頼度を持つクラスの名前を含む応答を返します。その他のクラスと信頼度のペアは、信頼度の降順でリストされます。

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

	信頼度の値はパーセンテージを表し、値が高いほど信頼度が高いことを意味します。応答には、最大 10 個のクラスが含まれます。

	トレーニング・データに含まれているクラスが 10 個より少ない場合、信頼度のすべての値の合計は 100% です。このサンプルのトレーニング・データでは、2 つのクラスのみが定義されているため、2 つのみを返すことができます。
2.  分類子が質問をどのように予測しているかを確認するには、質問の最上位クラスを参照します。

	以下に、分類する質問のその他のいくつかの例を示します。

	-   Is it hot outside?
	-   Will it be windy?
	-   Will we see some sun?
	-   What is the expected high for today?
	-   Will it be foggy tomorrow morning?

	質問の例の 1 つには、分類子がトレーニングされていない用語 (「foggy」) が含まれています。これらの「欠落」している用語を識別するために追加の作業をユーザーが行わなくても、分類子はこれらの用語で適切にスコアリングすることができます。トレーニング・データにない用語 (例えば、「sleet」や「storm」) を含むその他の質問を試してみます。

これで完了です。{{site.data.keyword.nlclassifiershort}} サービスで、分類子の作成、トレーニング、および照会を行いました。

## チュートリアル分類子の削除

独自のトレーニング・データで自分用に分類子を作成できるように、チュートリアルからこの分類子を削除することをお勧めします。分類子を削除するには、`DELETE /classifiers/{classifier_id}` メソッドを呼び出します。

前と同じように、以下のコマンドでは `{username}`、`{password}`、および `{classifier_id}` をご自分の情報で置き換えてください。

```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

このコマンドに対する応答は空の JSON オブジェクトです。

## 次の作業
{{site.data.keyword.nlclassifiershort}} の使用方法の基本を理解しました。さらに知識を深めてください。
- [独自のデータを使用](/docs/natural-language-classifier/using-your-data.html)して分類子をトレーニングする方法を学習します。
- [API リファレンス ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window} で API について確認します。
- [API Explorer ![「外部リンク」アイコン](../../icons/launch-glyph.svg "「外部リンク」アイコン")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window} で API と対話します。
- サンプルの Web アプリについては、[Node.js スターター・アプリケーション](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window}を確認してください。
