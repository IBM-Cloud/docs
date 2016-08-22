---

copyright:
  years: 2016

---
{:new_window: target="_blank"}

# 「モバイル」ダッシュボードからのモバイル・プロジェクトの作成
{: #mobile}
*最終更新日: 2016 年 7 月 18 日*
{: .last-updated}

{{site.data.keyword.Bluemix}} モバイル・サービスを使用すると、事前構築されて管理されているスケーラブルなクラウド・サービスを、IT 関与に依存することなくモバイル・アプリケーションに組み込むことができます。バックエンド・インフラストラクチャーの管理の複雑さを意識することなく、モバイル・アプリの作成に集中することができます。


「モバイル」ダッシュボードは、{{site.data.keyword.Bluemix_notm}} での 1 つの統合された作業環境を提供します。このダッシュボードから、新規モバイル・プロジェクトを簡単に作成できます。**「プロジェクト」**ビューを使用して、所有するすべてのプロジェクトを 1 箇所で管理できます。**「サービス」**ビューには、既存のモバイル・サービス・インスタンスが表示されます。

「モバイル」ダッシュボードを表示するには、{{site.data.keyword.Bluemix_notm}} ホームから**「モバイル」**カテゴリーをクリックします。
<img src="images/mobile_dashboard.jpg" alt="{{site.data.keyword.Bluemix_notm}} ホーム">

開始するには、「モバイル」ダッシュボードの**「プロジェクト」**ビューから**「新規プロジェクト」**をクリックします。

## {{site.data.keyword.Bluemix_notm}} モバイル・サービスの概要
{: #mobile_services_overview}

以下の表に、使用可能な {{site.data.keyword.Bluemix_notm}} モバイル・サービスを示します。個々のサービスを {{site.data.keyword.Bluemix_notm}} カタログから使用することも、これらのサービスを統合してモバイル・プロジェクトに入れることもできます。

<table summary="この表は、{{site.data.keyword.Bluemix_notm}} モバイル・サービスについて説明し、各サービス文書へのリンクも示します">
<caption>表 1. {{site.data.keyword.Bluemix_notm}} モバイル・サービス</caption>
<th>{{site.data.keyword.Bluemix_notm}} モバイル・サービス</th>
<th>説明</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}}アイコン"><br/><b>{{site.data.keyword.mobileanalytics_short}} (試験的)</b></td>
<td valign="top">{{site.data.keyword.mobileanalytics_full}} サービスを使用して、モバイル・アプリ、モバイル・ユーザー、およびモバイル・デバイスの状態、動作、およびコンテキストを測定します。<br/><br/>
このサービスの操作について詳しくは、<a href="../services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} 文書リンク">{{site.data.keyword.mobileanalytics_short}} 文書</a>を参照してください。
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} サービスのアイコン"><br/><b>{{site.data.keyword.amashort}}</b></td>
<td valign="top">{{site.data.keyword.amafull}} サービスを使用して、モバイル・アプリにセキュリティー機能を追加します。クライアント認証プロバイダーおよび ID プロバイダーを構成して、ユーザーが既存の Google アカウントまたは Facebook アカウントを使用してアプリにログインできるようにすることができます。<br/><br/>
このサービスの操作について詳しくは、<a href="../services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} 文書リンク">{{site.data.keyword.amashort}} 文書</a>を参照してください。</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} サービスのアイコン"><br/> <b>{{site.data.keyword.mobilefoundation_short}}</b></td>
<td valign="top">{{site.data.keyword.mobilefoundation_long}} サービスを使用して、エンタープライズ・モバイル・アプリの開発、テスト、操作を行うことのできる {{site.data.keyword.mfp_full}} 環境のセットアップを迅速に行います。<br/><br/>
このサービスの操作について詳しくは、<a href="../services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} 文書リンク">{{site.data.keyword.mobilefoundation_short}} 文書</a>を参照してください。</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} サービスのアイコン"><br/><b>{{site.data.keyword.mqa}}</b></td>
<td valign="top">{{site.data.keyword.mqafull}} サービスを使用して、アプリのモバイル品質サービスをディスカバーしてセットアップします。モバイル・アプリの品質メトリックの概要を表示して、開発しているアプリの問題を素早く理解することができます。これらのメトリックには、異常終了、バグ、ユーザー・フィードバック、およびユーザー評価の情報が含まれます。アプリに関するこの情報を確認することによって、特定の問題を詳しく調査するかどうかを判別できます。<br/><br/>
このサービスの操作について詳しくは、<a href="../services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} 文書リンク">{{site.data.keyword.mqa}} 文書</a>を参照してください。</td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="プッシュ通知サービスのアイコン"><br/><b>{{site.data.keyword.mobilepushshort}}</b></td>
<td valign="top">{{site.data.keyword.mobilepushfull}} サービスを使用して、iOS プラットフォームおよび Android プラットフォームをターゲットとするモバイル・プッシュ通知を送信および管理します。このサービスは、アプリケーション・ユーザーと各ユーザーのデバイスとのマッピング、およびデバイス・プラットフォームを管理し、デバイスへのプッシュ通知のディスパッチを処理します。このサービスを使用して、ブロードキャスト、ユニキャスト (ユーザー ID、デバイス ID に基づく)、およびタグ (またはトピック) をプッシュ通知に基づいてモバイル・アプリケーション・ユーザーに送信することができます。<br/><br/>
このサービスの操作について詳しくは、<a href="../services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} 文書リンク">{{site.data.keyword.mobilepushshort}} 文書</a>を参照してください。</td>
</table>

## モバイル・サービスの統合
{: #services_integration}
既存の {{site.data.keyword.Bluemix_notm}} モバイル・サービス (例えば、{{site.data.keyword.mobilepushshort}} や {{site.data.keyword.cloudant}} など) を統合してプロジェクトに入れることができます。

#### {{site.data.keyword.mobilepushshort}} の統合
{: #push_integration}

既存の {{site.data.keyword.mobilepushshort}} サービスを統合するには、以下の手順を実行します。

1. {{site.data.keyword.mobilepushshort}} サービス・インスタンスをクリックします。
2. **「モバイル・オプション」**をクリックし、**「経路」**の値と**「アプリ GUID」**の値をコピーします。

   **注:** **「モバイル・オプション」**を表示するには、{{site.data.keyword.mobilepushshort}} サービスがアプリにバインドされている必要があります。

3. 「モバイル」ダッシュボードの**「プロジェクト」**ビューに戻ります。
4. 編集するためにプロジェクトをクリックします。
5. **「プッシュ」**をクリックし、通知を有効にします。
6. 前にコピーした**「アプリ GUID」**値を**「アプリ ID」**に入力します。
7. 前にコピーした**「経路」**値を**「アプリ経路 URL」**に入力します。

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


# 関連リンク
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Experimental)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## ブログ投稿
{: #general}
* [ブログ投稿: Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [ブログ投稿: Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [ブログ投稿: Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## チュートリアルおよびサンプル
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
