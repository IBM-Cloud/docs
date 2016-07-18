---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# {{site.data.keyword.mobileanalytics_short}} について  
{: aboutmobileanalytics}
*最終更新日時: 2016 年 4 月 21 日*
{: .last-updated}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} サービスは、モバイル・アプリ開発者およびアプリ所有者に、主なアプリの使用量とパフォーマンスに関する洞察を提供します。{{site.data.keyword.mobileanalytics_short}} を使用すれば、アプリ所有者および開発者は「ユーザー側」で何が発生しているのかを把握することができます。また、この洞察を使用して、ユーザーに関連性の高い、おびただしい数のモバイル・アプリの中で際立つ、より良いアプリを作成することができます。 

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
	<dt>必要なすべてのデータを収集します</dt>
		<dd>アプリにカスタム・イベントを装備し、ユーザーがアプリとどのように対話しているのかを知り、購買を追跡し、アプリのアクティビティーを監視します。  
</dd>
<dt>すべてのアプリのメトリックが一目でわかります</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} コンソールには、既製グラフおよびカスタム・グラフの両方が用意されており、照会を記述する必要がありません。</dd>
<dt>重要なものにフォーカスします</dt>
	<dd>時間、アダプター、アプリ、アプリ・バージョン、OS、OS バージョン、またはデバイス・モデルでメトリックをフィルター操作します。</dd>
<dt>問題を迅速に発見します</dt>
	<dd>異常終了の状況を監視します。重大なメトリックにアラート・トリガーを設定し、アラートを任意の REST エンドポイントに経路指定します。</dd>
<dt>根本原因のトラブルシューティング</dt>
	<dd>カスタム・クライアント・ロギングをアプリで使用して、自動的にログをアップロードし、それらをコンソールから検索します。異常終了イベントについて詳しく調べ、スタック・トレースを確認します。</dd>
</dl>
 

## メトリックおよびイベントの使用
{: #usingmetrics}

**定義済みメトリック**を使用して、以下のような疑問に答えることができます:

*私の新規ユーザーは何人か?*  
*私のアプリをアクティブに使用している人は何人いるのか?*  
*ユーザーはどのくらいの頻度で私のアプリを使用しているのか?*  
*私のアプリをユーザーが使用するのは何時か?*  
*ユーザーはどのデバイス・モデルを好むのか?*  
*レガシー・オペレーション・システムのサポートをいつ廃止すべきか?*  
*パフォーマンス上の問題が発生しているのはどのアプリか?*  

独自の**カスタム・イベント**を追加することで、以下のような疑問に答えることができます:  

*利用数が一番多い機能と一番少ない機能はどれか?*  
*私のアプリにユーザーが入る場所と出る場所はどこか?*  
*ユーザーが最も多く見ているアクティビティーは何か?*  
*ユーザーはアプリ内でワークフローを完了しているか? (例えばコンバージョン・ファネル)*  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

># 関連リンク{:class="linklist"}
<!-->## チュートリアルおよびサンプル {:id="samples"}-->
<!-->* [Link1](https://github.com/)-->
>
># 関連リンク{:class="linklist"}
>## 関連リンク{:id="general"}
## SDK
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core )  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  
>
>{:elementKind="article" id="rellinks"}
