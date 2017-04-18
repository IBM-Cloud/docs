---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.twittershort}} について
{: #about_twitter}

{{site.data.keyword.twitterfull}} を使用して、Twitter [Decahose](http://support.gnip.com/gnip2.0/){: new_window} または
[PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} ストリームの Twitter の内容を {{site.data.keyword.Bluemix}} ア
プリケーションに組み込みます。
{:shortdesc}

Content Store がリアルタイムで更新および索引付けされることにより、検索が動的かつ高速になります。このサービスは、[IBM ソーシャル・メディア分析](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}の高度な自然言語処理アルゴリズムに基づく、複数の言語での感情その他の洞察によって、ツイートに拡張情報を提供します。Twitter データ・ストリームのリアルタイムでの処理が完全にサポートされており、充実したクエリーのパラメーターとキーワードのセットを使用して構成することが可能です。{{site.data.keyword.twittershort}} には、検索をカスタマイズして、ツイートおよび拡張情報を JSON 形式で返すことを可能にする、RESTful API が含まれます。
			返されたツイートは、Twitter データの [Gnip アクティビティー・ストリーム](http://support.gnip.com/){: new_window}形式に準拠しています。

{{site.data.keyword.twittershort}} サービスは Twitter Decahose および PowerTrack のストリームをリアルタイムで分析し、それぞれのツイートの作成者に、次のような拡張情報を提供します。
* 性別
* 永住地 (国、州、および市区町村によって定義)

ツイートの内容についての、次のような拡張情報も利用可能です。

* 感情 (英語、ドイツ語、フランス語、スペイン語のツイートの「肯定」、「否定」、「両面感情」、または「中間」の感情)
* ツイートに含まれる肯定/否定の感情を表す言葉 (英語、ドイツ語、フランス語、スペイン語のツイート)

{{site.data.keyword.twittershort}} の検索結果を検証するため、サービスは、特定のツイートが Twitter でまだアクセス可能かどうかを確認する REST API メソッドを提供します。 

## フィードバックとサポート 
{: #feedback_support}

問題や質問がある場合は、フォーラムを通じて情報を検索するか質問することで、ヘルプをご利用できます。サポート・チケットをオープンすることもできます。

フォーラムを使用して質問する場合は、IBM Bluemix 開発チームの目に留まるように質問にタグを付けてください。 
* {{site.data.keyword.twittershort}} を使用するアプリの開発やデプロイメントについて技術的な質問がある場合は、質問を Stack Overflow に投稿し、質問に
**bluemix** と
**twitter** のタグを付けてください。 
* サービスおよびその開始方法についての質問は、[developerWorks dW
Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window} のフォーラムを使用してください。insights-twitter タグと bluemix タグを含めてください。

フォーラムの使用について詳しくは、『[ヘルプの取得
](https://new-console.ng.bluemix.net/docs/support/index.html#getting-help){: new.window}』を参照してください。 

IBM サポート・チケットのオープンやサポート・レベルおよびチケットの重大度については、
『[サポートへのお問い合わせ](https://new-console.ng.bluemix.net/docs/support/index.html#contacting-support){: new.window}』を参照してください。
