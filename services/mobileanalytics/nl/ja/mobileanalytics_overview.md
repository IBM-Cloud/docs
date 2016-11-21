---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# {{site.data.keyword.mobileanalytics_short}} について  
{: aboutmobileanalytics}
最終更新日: 2016 年 8 月 29 日
{: .last-updated}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} サービスは、モバイル・アプリ開発者およびアプリ所有者に、主なアプリの使用量とパフォーマンスに関する洞察を提供します。{{site.data.keyword.mobileanalytics_short}} を使用すると、アプリ所有者および開発者はユーザー側で何が行われているのかを理解できます。また、その洞察を使用して、ユーザーにぴったりの素晴らしいアプリを作成し、おびただしい数のモバイル・アプリの中で差別化することができます。 

{: #overview}  
このサービスには {{site.data.keyword.mobileanalytics_short}} コンソールが含まれています。これを使用して、開発者とアプリ所有者は、モバイル・アプリケーションのパフォーマンスの監視、使用量の統計の確認、デバイス・ログの検索を行うことができます。{{site.data.keyword.mobileanalytics_short}} では、iOS 8+ (Swift のみ) および Android 4+ 用のクライアント SDK が提供されています。

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
		<dd>{{site.data.keyword.Bluemix}} でサービス・インスタンスを作成し、SDK をプロジェクトに追加し、2 行のコードをアプリに貼り付ければ、数多くの定義済みメトリックを収集する準備が整います。</dd>
	<!--<dt>Collect any data you want</dt>-->
		<!--<dd>Instrument apps with custom events, discover how users are interacting with your app, track purchases, and monitor app activity.  
</dd>-->
<dt>すべてのアプリのメトリックが一目でわかります</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} コンソールには、<!-- both -->すぐに使用できるグラフ<!--and custom-->が用意されているため、クエリーを作成する必要はありません。</dd>
<dt>重要なものにフォーカスします</dt>
	<dd>時間、アダプター、アプリ、アプリ・バージョン、OS、OS バージョン、またはデバイス・モデルでメトリックをフィルター操作します。</dd>
<dt>問題を迅速に発見します</dt>
	<dd>異常終了の状況を監視します。重大なメトリックにアラート・トリガーを設定し、アラートを任意の REST エンドポイントに経路指定します。</dd>
<dt>根本原因のトラブルシューティング</dt>
	<dd>カスタム・ロギングをアプリで使用して自動的にログをアップロードし、コンソールから検索します。異常終了イベントについて詳しく調べ、スタック・トレースを確認します。</dd>
</dl>
 

## メトリックおよびイベントの使用
{: #usingmetrics}

**定義済みメトリック**を使用して、以下のような疑問に答えることができます:

* 新規ユーザーは何人いるか?  
* アプリをアクティブに使用している人は何人いるのか?  
* ユーザーはどのくらいの頻度でアプリを使用しているのか? 
* ユーザーは何時にアプリを使用しているのか?  
* ユーザーに好まれているデバイス・モデルは何か? 
* レガシー・オペレーション・システムのサポートをいつ廃止すべきか? 
* パフォーマンスの問題が発生しているアプリはどれか?  

<!--By adding your own **custom events** you can answer questions like:--> 

<!--* What features are used most and least?-->  
<!--* Where are users entering and leaving my app?-->  
<!--* What activities are users viewing most? --> 
<!--* Are users completing workflows in the app (for example, conversion funnels)? -->  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

## {{site.data.keyword.mobileanalytics_short}} に関するよくある質問 
{: #faq}

<dl>
	<dt>{{site.data.keyword.mobileanalytics_full}} とは</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} は、モバイル・アプリのパフォーマンスや使用状況についてのリアルタイムの洞察および履歴に基づく洞察を提供するサービスです。{{site.data.keyword.mobileanalytics_short}} を使用すると、アプリ開発者やアプリ所有者は、アクティブ・ユーザー、セッション、モバイル・プラットフォーム、アプリの異常終了の傾向をモニターしてデータ主導型の決定を下すことができます。選択したメトリックに対するアラートを設定し、アラートがトリガーされた場合にはプッシュ・サービスや内部メッセージング・サービスなどの REST エンドポイントにメッセージを送信するように構成できます。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} ベータでできることは何ですか?</dt>
		<dd>モバイル・アプリ・プロダクト・マネージャーは、自分のアプリを使用している人数 (ユーザー・メトリック) や、アプリがいつ使用されているのか (セッション・メトリック) を知ることができます。この情報は時系列で表示され、リアルタイムで更新されるので、アプリに加えた変更の影響を調べることができます。特定のアプリ・バージョンまたはオペレーティング・システムをフィルタリングして参照し、廃止や優先事項に関する決定を下すことができます。</dd>
		<dd>モバイル・アプリ・マーケティング担当者は、ユーザー・メトリックとセッション・メトリックを使用して経時変化を観察し、イベント日に関連付けることで、顧客のエンゲージメントをモニターし、顧客離れに対処し、モバイル・アプリ・マーケティング活動の有効性を評価することができます。</dd>
		<dd>モバイル・アプリ開発者は、ユーザーの不満が募り、アプリの評判に傷が付く前に、異常終了メトリックにより、モバイル・アプリのパフォーマンスの問題を検出して解決できます。異常終了の回数と発生率の両方を分析コンソールからモニターできます。また、最も多くのユーザーに影響を与えている異常終了を優先することができます。指定したしきい値を異常終了数が超過した場合に通知を送信したり自動化されたアクションを実行したりするようにアラートを設定できます。また、異常終了の事象ごとにドリルダウンしてデバイス・ログやアプリ・スタック・トレースを参照してトラブルシューティングすることができます。</dd>
	<dt>Mobile Analytics を使用するにはデータ・アナリストのスキルが必要ですか?</dt>
		<dd>いいえ、{{site.data.keyword.mobileanalytics_short}} には、ビジネス関係者やアプリ開発者用に、すぐに使用できる分析コンソールが用意されています。クエリー・スキルは不要です。</dd>
	<dt>分析データに対してカスタム・クエリーを実行できますか?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} ベータではカスタム・クエリーは使用できませんが、将来この機能を使用できるように検討中です。</dd>
	<dt>どのようにしてアプリを {{site.data.keyword.mobileanalytics_short}} に接続するのですか?</dt>
		<dd>[iOS または Android の場合はオープン・ソース SDK をダウンロード](install-client-sdk.html)し、他のプラットフォームの場合は {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.stage1.ng.bluemix.net/analytics-service/) を使用します。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} はどの Bluemix 地域で使用できますか?</dt>
		<dd>これを執筆している時点では、Mobile Analytics は米国南部と英国で使用できます。他の地域への提供も計画されていますが、時期は未定です。</dd>
	<dt>このサービスのコストを教えてください。</dt>
		<dd>ベータ版のサービスは無償です。</dd>
	<dt>分析データの保持期間を教えてください。</dt>
		<dd>ベータ版では、データは少なくとも 30 日間保持されます。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} コンソールにデータが表示されるまでどれくらいかかりますか?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} コンソールのデータは、ほぼリアルタイムです。つまり実際のイベントから数秒以内に表示されます。</dd>
	<dt>{{site.data.keyword.mobileanalytics_full}} と MobileFirst Platform Foundation のモバイル分析にはどんな違いがありますか?</dt>
		<dd>これらの 2 つのコンソールのユーザーやセッションはよく似ていますが、MobileFirst Platform Foundation の分析のほうには、クライアントがオンプレミスで独自の分析クラスターを管理できるように、追加のメトリックや設定が含まれています。また、MobileFirst Platform Foundation 分析コンソールでは、アダプターやアダプター・プロシージャー用のメトリックを細分化できます。一方、{{site.data.keyword.mobileanalytics_short}} サービスでは、これらのメトリックは {{site.data.keyword.mobileanalytics_short}} サービス (ポスト・ベータ版) のネットワーク要求のグラフや表に統合される予定です。</dd>
	<dt>MobileFirst Platform Foundation をオンプレミスで使用してアプリを開発していますが、独自の分析クラスターをホストしたくありません。代わりに、{{site.data.keyword.mobileanalytics_full}} を使用できますか?</dt>
		<dd>はい。選択肢がいくつかあります。MobileFirst Platform Foundation 7.x または 8.0 を使用していて、アプリを MobileFirst Platform SDK で計装している場合は、分析データを {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} にレポートするように MobileFirst サーバーを構成できます。詳細については、ブログ記事[「Configuring Mobile Analytics and Mobile Foundation Bluemix services」](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/)を参照してください。また、{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} SDK を使用してアプリを計装し、{{site.data.keyword.mobileanalytics_short}} サービスに直接レポートすることもできます。</dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} を使用していますが、グラフの部分に空白文字が表示されます。なぜでしょうか? </dt>
		<dd>{{site.data.keyword.Bluemix_notm}} のクラシック・ビュー・インターフェースを使用している可能性があります。クラシック・ビューは非推奨になったため、{{site.data.keyword.mobileanalytics_short}} ベータは新しい {{site.data.keyword.Bluemix_notm}} インターフェースで実行されます。クラシック・ビューを使用している場合は、{{site.data.keyword.Bluemix_notm}} ヘッダーに「Try the new {{site.data.keyword.Bluemix_notm}}!」というリンクが表示されます。そのリンクをクリックして新規インターフェースを使用してください。</dd>
</dl>


# 関連リンク
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  

<!-- {:elementKind="article" id="rellinks"} -->
