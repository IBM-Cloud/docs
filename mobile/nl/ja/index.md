# モバイル・アプリの作成
{: #mobile}
*最終更新日: 2016 年 1 月 28 日* 

{{site.data.keyword.Bluemix}} モバイル・サービスを使用すると、事前構築されて管理されているスケーラブルなクラウド・サービスを、IT 関与に依存することなくモバイル・アプリケーションに組み込むことができます。バックエンド・インフラストラクチャーの管理の複雑さを意識することなく、モバイル・アプリの作成に集中することができます。


<table><caption>表 1. MobileFirst&trade; Services Starter ボイラープレート</caption>
<tr>
	<td>モバイル・サービスはそれぞれ独立して使用できます。一緒に使用することで最大の利点を得ることもできます。始めに、{{site.data.keyword.mobilefirstbp}} Starter を使用してアプリを作成します。このボイラープレートで以下を行います。<ul>
			<li>テンプレート・アプリケーションを使用して Node.js ランタイムを作成する。このアプリケーションを使用して、RESTful API や静的ファイルなどのサーバー・サイド機能を提供することができます。<!-- You can read more about operating this application in the Developing Mobile Backend section.--> </li>
			<li>
各 {{site.data.keyword.Bluemix_notm}} モバイル・サービスのインスタンスをプロビジョンし、そのサービスを Node.js アプリケーションにバインドする。
</li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Bluemix モバイル・サービス" width="500"> {{site.data.keyword.mobilefirstbp}} Starter ボイラープレート</td>
</tr>
</table>

{{site.data.keyword.mobilefirstbp}} Starter ボイラープレートを使用してアプリを作成したら、各サービスの HelloWorld サンプルを入手したり、ご使用の既存のアプリを装備して {{site.data.keyword.Bluemix_notm}} サービスの使用を開始したりすることができます。


## サービスの概要
{: #services-overview}
{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter ボイラープレートを使用してすべての {{site.data.keyword.Bluemix_notm}} モバイル・サービスを一緒に使用することも、{{site.data.keyword.Bluemix_notm}} カタログから個々のサービスを使用することもできます。以下の図は、{{site.data.keyword.Bluemix_notm}} モバイル・サービスの全コンポーネントの概略を示しています。

![{{site.data.keyword.Bluemix_notm}} モバイル・サービスのアーキテクチャー](images/bms_architecture.jpg)

<table>
<caption>表 2. {{site.data.keyword.Bluemix_notm}} とエンタープライズ・システム</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>エンタープライズ・システム</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js ランタイム・アイコン"><b>Node.js</b> <br/> テンプレート・アプリをホストする Node.js ランタイムは、{{site.data.keyword.mobilefirstbp}} Starter ボイラープレートの一部として提供されます。このテンプレート・アプリケーションを使用して、RESTful API や静的ファイルなどのサーバー・サイド機能を提供することができます。
<br/>例えば、カスタム・ロジック処理のために Node.js アプリケーションを拡張したり、既存の社内インフラストラクチャー内の REST API に接続したりすることができます。{{site.data.keyword.Bluemix_notm}} で作成する各アプリには固有の アプリ ID が付きます。モバイル・アプリは SDK でこの ID を使用して、そのアプリケーションに関連付けられたサービスにアクセスします。アプリ ID は、課金やロギングなど、一般的な機能のコンテキストとして、プラットフォームが使用します。このアプリケーションの操作については、『モバイル・バックエンドの開発 (Developing Mobile Backend)』のセクションに詳しい説明があります。</td>
<td valign="top"><b>情報プロバイダー</b> <br/>{{site.data.keyword.Bluemix_notm}} でホストされる Node.js ランタイムを使用して、以下のどの情報プロバイダーにでも接続できます。
<ul>
	<li>エンタープライズ・バックエンド</li>
	<li>データベース</li>
	<li>ホストされた別のサード・パーティー・サービス</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} サービス・アイコン"> <b>{{site.data.keyword.amashort}}</b><br/>{{site.data.keyword.amafull}} サービスを使用して、{{site.data.keyword.Bluemix_notm}} でホストされる Node.js アプリケーションおよび Java for Liberty アプリケーションを保護します。{{site.data.keyword.amashort}} SDK を使用してモバイル・アプリを装備することによって、Node.js または {{site.data.keyword.Bluemix_notm}} モバイル・サービスにアクセスするユーザーにログインを要求することができます。{{site.data.keyword.amashort}} は、セキュリティー機能に加えて、分析データの収集機能も提供するので、モバイル・アプリケーションのパフォーマンスをモニターし、クライアント・ログと使用統計を収集することができます。</td>
<td valign="top"><b>ユーザー ID プロバイダー</b> <br/>以下の ID プロバイダーを使用できます。<ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="プッシュ通知サービス・アイコン"> <b>{{site.data.keyword.mobilepushshort}}</b><br/>{{site.data.keyword.mobilepushfull}} サービスは、iOS プラットフォームおよび Android プラットフォームをターゲットとしたモバイル・プッシュ通知を送信および管理するための統合プラットフォームを提供します。このサービスは、アプリケーション・ユーザーと各ユーザーのデバイスとのマッピング、およびデバイス・プラットフォームを管理し、デバイスへのプッシュ通知のディスパッチを処理します。このサービスを使用して、ブロードキャスト、ユニキャスト (ユーザー ID、デバイス ID に基づく) およびタグ (またはトピック) をプッシュ通知に基づいてモバイル・アプリケーション・ユーザーに送信することができます。</td>
<td valign="top"><b>プッシュ・サービス・プロバイダー</b><ul><li>Apple プッシュ通知サービス</li><li>Google Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant サービス・アイコン"><b>Cloudant NoSQLDB</b><br/> Cloudant は NoSQL の Database as a Service (DBaaS) です。これは積み上げ方式で構築してグローバルに拡大され、ノンストップで稼働し、JSON、フル・テキスト、地理情報などの多種多様なデータ・タイプを処理します。</td>
<td>Cloudant.com</td>
</tr>
</table>
