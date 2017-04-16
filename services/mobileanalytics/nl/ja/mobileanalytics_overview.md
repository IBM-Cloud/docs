---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} について  
{: aboutmobileanalytics}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} サービスは、モバイル・アプリケーション開発者とアプリケーション所有者に、主なアプリケーションの使用量とパフォーマンスに関する洞察を提供します。{{site.data.keyword.mobileanalytics_short}} を使用すると、アプリケーション所有者と開発者はユーザー側で何が実行されているのかを理解できます。また、その洞察を使用して、ユーザーにぴったりの素晴らしいアプリケーションを作成し、おびただしい数のモバイル・アプリケーションの中で差別化することができます。 

{: #overview}  
このサービスには {{site.data.keyword.mobileanalytics_short}} コンソールが含まれています。これを使用して、開発者とアプリケーション所有者は、モバイル・アプリケーションのパフォーマンスの監視、使用量の統計の確認、デバイス・ログの検索を実行することができます。{{site.data.keyword.mobileanalytics_short}} では、iOS 8+ (Swift のみ) および Android 4+ 用のクライアント SDK が提供されています。

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

{{site.data.keyword.mobileanalytics_short}} サービスを使用して、以下のことが可能です:
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>洞察を即時に獲得します</dt>
		<dd>リアルタイムでパフォーマンスおよび使用量のメトリックがわかります。</dd>
	<dt>短時間で実装します</dt>
		<dd>{{site.data.keyword.Bluemix}} でサービス・インスタンスを作成し、SDK をプロジェクトに追加し、2 行のコードをアプリケーションに貼り付ければ、数多くの定義済みメトリックを収集する準備が整います。</dd>
	<dt>目的の任意のデータを収集します</dt>
		<dd>アプリにカスタム・イベントを装備し、ユーザーがアプリとどのように対話しているかを発見し、購入を追跡し、アプリのアクティビティーをモニターします。  
</dd>
<dt>すべてのアプリケーションのメトリックが一覧できます。</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} コンソールには、<!-- both -->すぐに使用できるグラフ<!--and custom-->が用意されているため、クエリーを作成する必要はありません。</dd>
<dt>重要なものにフォーカスします</dt>
	<dd>時間、アダプター、アプリケーション、アプリケーション・バージョン、OS、OS バージョン、またはデバイス・モデルでメトリックをフィルター操作します。</dd>
<dt>問題を迅速に発見します</dt>
	<dd>異常終了の状況を監視します。重大なメトリックにアラート・トリガーを設定し、アラートを任意の REST エンドポイントに経路指定します。</dd>
<dt>根本原因のトラブルシューティング</dt>
	<dd>カスタム・ロギングをアプリケーションで使用して自動的にログをアップロードし、コンソールから検索します。異常終了イベントについて詳しく調べ、スタック・トレースを確認します。</dd>
</dl>
 

## メトリックおよびイベントの使用
{: #usingmetrics}

**定義済みメトリック**を使用して、以下のような疑問に答えることができます:

* 新規ユーザーは何人いるか?  
* アプリケーションをアクティブに使用している人は何人いるのか?  
* ユーザーはどのくらいの頻度でアプリケーションを使用しているのか? 
* ユーザーはどんな時刻にアプリケーションを使用しているのか?  
* ユーザーに好まれているデバイス・モデルは何か? 
* レガシー・オペレーティング・システムのサポートをいつ廃止すべきか? 
* パフォーマンスの問題が発生しているアプリケーションはどれか?  

独自の**カスタム・イベント**を追加することにより、以下のような疑問に答えることができます。 

* 最も使用されているフィーチャーと最も使用されていないフィーチャーは何か?  
* ユーザーはアプリのどこから入ってどこで終わらせているか?  
* ユーザーが最もよく表示するアクティビティーは何か?  
* ユーザーはアプリのワークフロー (例えば変換ファネル) を終了しているか?   

クライアント・サイドのログと使用データは自動的に収集され、要求に応じて Mobile Analytics サービスに送信されます。開発者と管理者は、{{site.data.keyword.mobileanalytics_short}} サービス・ダッシュボードを使用して、クライアント SDK によって収集されたデータを見ることができます。

## データ可視化
{: data-visualization}

分析サービスによって収集されたすべてのデータを、{{site.data.keyword.mobileanalytics_short}} ダッシュボードで視覚化できます。このダッシュボードは、{{site.data.keyword.Bluemix_notm}} ダッシュボードで IBM {{site.data.keyword.mobileanalytics_short}} サービス・タイル・インスタンスをクリックすることによってアクセスできます。<!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.--> モバイル分析の概要ビューに加えて、クライアント・ログや取り込まれたクライアント異常終了データに対してロー検索を行う機能も、分析フィーチャーに組み込まれています。さらに、{{site.data.keyword.mobileanalytics_short}} サービスに送り込まれるクライアント API ファンクション・コールで明示的に提供される追加データに対するロー検索機能も含まれます。 

## {{site.data.keyword.mobileanalytics_short}} に関するよくある質問 
{: #faq}

<dl>
	<dt>{{site.data.keyword.mobileanalytics_full}} とは</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} は、モバイル・アプリケーションのパフォーマンスや使用状況についてのリアルタイムの洞察や履歴に基づく洞察を提供するサービスです。{{site.data.keyword.mobileanalytics_short}} を使用すると、アプリケーション開発者やアプリケーション所有者は、アクティブ・ユーザー、セッション、モバイル・プラットフォーム、アプリケーションの異常終了の傾向をモニターしてデータ主導型の決定を下すことができます。選択したメトリックに対するアラートを設定し、アラートがトリガーされた場合にはプッシュ・サービスや内部メッセージング・サービスなどの REST エンドポイントにメッセージを送信するように構成できます。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} でできることは何ですか?</dt>
		<dd>モバイル・アプリケーション・プロダクト・マネージャーは、自分のアプリケーションを使用している人数 (ユーザー・メトリック) や、それがいつ使用されているのか (セッション・メトリック) を知ることができます。この情報は時系列で表示され、リアルタイムで更新されるので、アプリケーションに加えた変更の影響を調べることができます。特定のアプリケーション・バージョンまたはオペレーティング・システムをフィルタリングして参照し、廃止や優先事項に関する決定を下すことができます。</dd>
		<dd>モバイル・アプリケーション・マーケティング担当者は、ユーザー・メトリックとセッション・メトリックを使用して経時変化を観察し、イベント日に関連付けることで、顧客のエンゲージメントをモニターし、顧客離れに対処し、モバイル・アプリケーション・マーケティング活動の有効性を評価することができます。</dd>
		<dd>モバイル・アプリケーション開発者は、ユーザーの不満が募り、アプリケーションの評判に傷が付く前に、異常終了メトリックを使用することにより、モバイル・アプリケーションのパフォーマンスの問題を検出して解決できます。異常終了の回数と発生率の両方を分析コンソールからモニターできます。また、最も多くのユーザーに影響を与えている異常終了を優先することができます。指定したしきい値を異常終了数が超過した場合に通知を送信したり自動化されたアクションを実行したりするようにアラートを設定できます。また、異常終了の事象ごとにドリルダウンしてデバイス・ログやアプリケーション・スタック・トレースを参照してトラブルシューティングすることができます。</dd>
	<dt>Mobile Analytics を使用するにはデータ・アナリストのスキルが必要ですか?</dt>
		<dd>いいえ、{{site.data.keyword.mobileanalytics_short}} には、ビジネス関係者やアプリケーション開発者用に、すぐに使用できる分析コンソールが用意されています。クエリー・スキルは不要です。</dd>
	<dt>分析データに対してカスタム・クエリーを実行できますか?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} ではカスタム・クエリーは使用できませんが、将来この機能を使用できるように検討中です。</dd>
	<dt>どのようにしてアプリケーションを {{site.data.keyword.mobileanalytics_short}} に接続するのですか?</dt>
		<dd>[iOS または Android の場合はオープン・ソース SDK をダウンロード](install-client-sdk.html)し、他のプラットフォームの場合は {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/) を使用します。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} はどの Bluemix 地域で使用できますか?</dt>
		<dd>現在のところ、Mobile Analytics は米国南部と英国で利用可能です。他の地域で使用可能にすることも計画中ですが、その時期は未定です。</dd>
	<dt>このサービスのコストを教えてください。</dt>
		<dd>各月に収集される最初の 1 億イベントは無料です。その後のイベントについては、100 万イベントごとに $1 の費用がかかります。</dd>
	<dt>イベントとは何ですか?</dt>
		<dd>現時点で、報告されイベントには、アプリケーション・セッションの開始、アプリケーション・セッションの終了 (アプリケーション・クラッシュを含む)、アラート通知、ログ・エントリーが含まれます。</dd>
	<dt>1 カ月あたりのサービスのコストをどのように見積もることができますか?</dt>
		<dd>価格設定はクライアント・アカウントごとにサービスに送信されたイベントの数に応じて異なるため、価格を見積もるということは、イベント数を見積もるということです。  
<p>
課金価格は、{{site.data.keyword.mobileanalytics_short}} に接続したすべてのアプリケーションからのイベント数の合計になります。特定のアプリケーションのイベントの数は、アプリケーション内に実装した装備の度合い、ユーザーの数、また、ユーザーがどれほどアクティブかに応じて異なります。   
</p>
<p>
使用量を見積もるには、次の式を使用します。
各アプリの月ごとのイベント数 = (1 日のユーザー数)(1 日のユーザーごとのセッション数)(月の日数)(セッションごとのイベント数)
</p>
<p>
セッションごとのイベント数は、開発者がアプリケーションで構成したネットワーク呼び出し、カスタム分析、ログ・キャプチャー、アラート定義に応じて 2 から数百まで大きく変動する可能性があります。</p>
	<dt>分析データの保持期間を教えてください。</dt>
		<dd>データは少なくとも 30 日間保持されます。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} コンソールにデータが表示されるまでどれくらいかかりますか?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} コンソールのデータは、ほぼリアルタイムです。つまり実際のイベントから数秒以内に表示されます。</dd>
	<dt>{{site.data.keyword.mobileanalytics_full}} と MobileFirst Platform Foundation のモバイル分析にはどんな違いがありますか?</dt>
		<dd>これらの 2 つのコンソールのユーザーやセッションはよく似ていますが、MobileFirst Platform Foundation の分析のほうには、クライアントがオンプレミスで独自の分析クラスターを管理できるように、追加のメトリックや設定が含まれています。また、MobileFirst Platform Foundation 分析コンソールでは、アダプターやアダプター・プロシージャー用のメトリックを細分化できます。一方、{{site.data.keyword.mobileanalytics_short}} サービスでは、これらのメトリックはネットワーク要求のグラフや表に統合されています。</dd>
	<dt>MobileFirst Platform Foundation をオンプレミスで使用してアプリを開発していますが、独自の分析クラスターをホストしたくありません。代わりに、{{site.data.keyword.mobileanalytics_full}} を使用できますか?</dt>
		<dd>はい。選択肢がいくつかあります。MobileFirst Platform Foundation 7.x または 8.0 を使用していて、アプリを MobileFirst Platform SDK で装備している場合は、分析データを {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} にレポートするように MobileFirst サーバーを構成できます。詳しくは、[Configuring Mobile Analytics and Mobile Foundation Bluemix services ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/ "外部リンク・アイコン"){: new_window} のブログ投稿を参照してください。また、{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} SDK を使用してアプリを計装し、{{site.data.keyword.mobileanalytics_short}} サービスに直接レポートすることもできます。</dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# 関連リンク
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "外部リンク・アイコン"){: new_window} 
* [iOS SDK ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core "外部リンク・アイコン"){: new_window}

<!-- {:elementKind="article" id="rellinks"} -->
