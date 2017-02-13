---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# サービス
{: #services}

{{site.data.keyword.Bluemix}} 「モバイル」ダッシュボードの**「サービス」**ビューから、既存サービスを表示したり、新規サービスを作成したりできます。「モバイル」ダッシュボードでは、プロジェクトによって管理されているすべての Bluemix サービスを 1 箇所で表示できます。  

**「サービス」**ビューからサービスを削除すると、そのサービスが関連付けられているプロジェクトからそのサービスを切断することになります。そのサービスをプロジェクトに再接続したい場合は、新しいサービス・インスタンスを作成してください。

## {{site.data.keyword.Bluemix_notm}} モバイル・サービスの概要
{: #mobile_services_overview}

以下の表で、各種 {{site.data.keyword.Bluemix_notm}} モバイル・サービスを説明します。個々のサービスを {{site.data.keyword.Bluemix_notm}} カタログから使用することも、これらのサービスを統合してモバイル・プロジェクトに入れることもできます。

<table summary="この表は、{{site.data.keyword.Bluemix_notm}} モバイル・サービスについて説明し、各サービス文書へのリンクも示します">
<caption>表 1. {{site.data.keyword.Bluemix_notm}} モバイル・サービス</caption>
<th>{{site.data.keyword.Bluemix_notm}} モバイル・サービス</th>
<th>説明</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}} アイコン"><br/>{{site.data.keyword.mobileanalytics_short}}</td>
<td valign="top">{{site.data.keyword.mobileanalytics_full}} サービスを使用して、モバイル・アプリがどのように実行され、使用されているのかについての洞察を得ることができます。<br/><br/>
このサービスの操作について詳しくは、<a href="/docs/services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} 文書リンク">{{site.data.keyword.mobileanalytics_short}} 文書</a>を参照してください。
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="{{site.data.keyword.amashort}} サービスのアイコン"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">{{site.data.keyword.amafull}} サービスを使用して、モバイル・アプリにセキュリティー機能を追加します。クライアント認証プロバイダーおよび ID プロバイダーを構成して、ユーザーが既存の Google アカウントまたは Facebook アカウントを使用してアプリにログインできるようにすることができます。<br/><br/>
このサービスの操作について詳しくは、<a href="/docs/services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} 文書リンク">{{site.data.keyword.amashort}} 文書</a>を参照してください。</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} サービスのアイコン"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">{{site.data.keyword.mobilefoundation_long}} サービスを使用して、エンタープライズ・モバイル・アプリの開発、テスト、操作を行うことのできる {{site.data.keyword.mfp_full}} 環境のセットアップを迅速に行います。<br/><br/>
このサービスの操作について詳しくは、<a href="/docs/services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} 文書リンク">{{site.data.keyword.mobilefoundation_short}} 文書</a>を参照してください。</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} サービスのアイコン"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">{{site.data.keyword.mqafull}} サービスを使用して、アプリのモバイル品質サービスをディスカバーしてセットアップします。モバイル・アプリの品質メトリックの概要を表示して、開発しているアプリの問題を素早く理解することができます。これらのメトリックには、異常終了、バグ、ユーザー・フィードバック、およびユーザー評価の情報が含まれます。アプリに関するこの情報を確認することによって、特定の問題を詳しく調査するかどうかを判別できます。<br/><br/>
このサービスの操作について詳しくは、<a href="/docs/services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} 文書リンク">{{site.data.keyword.mqa}} 文書</a>を参照してください。</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} サービスのアイコン"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">{{site.data.keyword.mobilepushfull}} サービスは、複数のプラットフォームをターゲットとするモバイル・プッシュ通知と Web のプッシュ通知を送信および管理するための統合プラットフォームを提供します。
<br/><br/>
{{site.data.keyword.mobilepushshort}} は、アプリケーション・ユーザーとそれらのユーザーが使用するデバイス、デバイス・プラットフォーム、Web ブラウザーとのマッピングを管理し、プッシュ通知のディスパッチを処理します。ブロードキャスト、ユニキャスト (ユーザー ID とデバイス ID に基づく)、およびタグ (またはトピック) をプッシュ通知としてモバイル・アプリケーション・ユーザーと Web ブラウザー・アプリケーション・ユーザーに送信することができます。また、SDK および REST API を使用してクライアント・アプリケーションをさらに開発することもできます。
<br/><br/>
このサービスの操作について詳しくは、<a href="/docs/services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} の資料リンク">{{site.data.keyword.mobilepushshort}} の資料</a>をお読みください。</td>
</table>

## モバイル・サービスの統合
{: #services_integration}
既存の {{site.data.keyword.Bluemix_notm}} モバイル・サービス ({{site.data.keyword.cloudant}} など) をプロジェクトに統合することができます。


#### {{site.data.keyword.cloudant}} の統合
{: #cloudant_integration}

既存の {{site.data.keyword.cloudant}} サービスを統合するには、以下の手順を実行します。

1. {{site.data.keyword.cloudant}} サービス・インスタンスをクリックします。
2. **「起動」**をクリックします。
3. **「データベース」**ビューで、データベース名をクリックします。
4. **「API」**をクリックし、**「API キー」**の値からデータベース名までをコピーします。

   **注:** データベース名を超える内容をコピーしないでください。

5. **「許可」** > **「API キーの生成」**をクリックし、**「キー」**の値と**「パスワード」**の値をコピーします。
6. 「モバイル」ダッシュボードの**「プロジェクト」**ビューに戻ります。
7. 編集するためにプロジェクトをクリックします。
8. **「データ」** > **「+ データ・ソース」** > **「Cloudant」**をクリックし、データ・ソース名を入力し、**「追加」**をクリックします。
9. **「Cloudant 構成 (Cloudant Config)」**をクリックします。
10. 前にコピーした**「API キー」**値を**「API URL」**に入力します。
11. 前にコピーした**「キー」**値を**「ユーザー」**に入力します。
12. 前にコピーした**「パスワード」**値を**「パスワード」**に入力します。
13. **「OK」**をクリックします。
