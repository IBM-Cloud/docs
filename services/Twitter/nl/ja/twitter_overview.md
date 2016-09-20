---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.twittershort}} について
{: #about_twitter}

*最終更新日: 2016 年 5 月 13 日*
{: .last-updated}

{{site.data.keyword.twitterfull}} を使用して、 Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} または [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} ストリームの Twitter の内容を {{site.data.keyword.Bluemix}} アプリケーションに組み込みます。
{:shortdesc}

Content Store がリアルタイムで更新および索引付けされることにより、検索が動的かつ高速になります。このサービスは、[IBM ソーシャル・メディア分析](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}の高度な自然言語処理アルゴリズムに基づく、複数の言語での感情その他の洞察によって、ツイートに拡張情報を提供します。Twitter データ・ストリームのリアルタイムでの処理が完全にサポートされており、充実したクエリーのパラメーターとキーワードのセットを使用して構成することが可能です。{{site.data.keyword.twittershort}} には、検索をカスタマイズして、ツイートおよび拡張情報を JSON 形式で返すことを可能にする、RESTful API が含まれます。
			返されたツイートは、Twitter データの [Gnip アクティビティー・ストリーム](http://support.gnip.com/sources/twitter/data_format.html){: new_window}形式に準拠しています。

{{site.data.keyword.twittershort}} サービスは Twitter Decahose および PowerTrack のストリームをリアルタイムで分析し、それぞれのツイートの作成者に、次のような拡張情報を提供します。
* 性別
* 永住地 (国、州、および市区町村によって定義)

ツイートの内容についての、次のような拡張情報も利用可能です。

* 感情 (英語、ドイツ語、フランス語、スペイン語のツイートの「肯定」、「否定」、「両面感情」、または「中間」の感情)
* ツイートに含まれる肯定/否定の感情を表す言葉 (英語、ドイツ語、フランス語、スペイン語のツイート)

{{site.data.keyword.twittershort}} の検索結果を検証するため、サービスは、特定のツイートが Twitter でまだアクセス可能かどうかを確認する REST API メソッドを提供します。 

## フィードバックとサポート 
{: #feedback_support}

{{site.data.keyword.twitterfull}} チームは
		皆様からのご意見をお待ちしております。

このサービスに関して何か問題がある場合は、IBM [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} フォーラムにアクセスしてください。以前に送信された質問への回答を検索するか、新たに質問を追加してください。
**insights-twitter** タグと **bluemix** タグを含めると、応答時間が向上します。

ご質問が developerWorks Answers で対処されていない場合は、質問を [Stack Overflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} に投稿し、質問に **twitter** と **bluemix** のタグを付けてください。

[Bluemix プラットフォーム](https://developer.ibm.com/bluemix/support/#status){: new.window}の状況を表示すること、および[サポート・チケットをオープン](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}することもできます。詳細については、[『トラブルシューティング』](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}を参照してください。
