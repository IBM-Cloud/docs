{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.autoscaling}} サービス入門
{: #autoscaling}

*最終更新日: 2015 年 1 月 18 日*

{{site.data.keyword.Bluemix_notm}} では、アプリケーション能力を自動的に管理できます。 {{site.data.keyword.autoscalingfull}} サービスを使用すると、
アプリケーションの計算容量を自動的に増減できます。アプリケーション・インスタンスの数は、定義する
{{site.data.keyword.autoscaling}} ポリシー
に基づき、動的に調整されます。{:shortdesc} 

## {{site.data.keyword.Bluemix_notm}} での {{site.data.keyword.autoscaling}} サービスの使用
{: #as-service}

{{site.data.keyword.autoscaling}} サービスを利用するには、次のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで*「サービスまたは API の追加」*をクリックし、次にサービス・カタログの DevOps セクションから {{site.data.keyword.autoscaling}} サービスを選択します。新しいウィンドウが表示され、 {{site.data.keyword.autoscaling}} サービスの概要が提示されます。
2. {{site.data.keyword.autoscaling}} サービスをバインドするアプリケーションを選択し、*「作成」*をクリックします。<br/>
*重要:* 1 つのアプリケーションにバインドできる {{site.data.keyword.autoscaling}} サービスは 1 つのみです。アプリケーションが既に他の {{site.data.keyword.autoscaling}} サービスにバインド済みの場合は、このステップではアプリケーションを選択しないでください。そうしないと CWSCV2004E エラーが発生します。<br/>「アプリケーションの再ステージ」ウィンドウが表示されます。
3. 追加した新しい {{site.data.keyword.autoscaling}} サービスを使用する前に、「アプリケーションの再ステージ」ウィンドウで*「再ステージ」*をクリックして、アプリケーションを再ステージします。アプリケーションの再ステージングが完了した後、アプリケーションに合わせた {{site.data.keyword.autoscaling}} サービスの構成が開始できます。
4. {{site.data.keyword.autoscaling}} をアプリケーションに合わせて構成するには、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースで、{{site.data.keyword.autoscaling}} サービスがバインドされているアプリケーションをクリックします。
5. ダッシュボードのサービス・セクションで、*「Auto-Scaling」*アイコンをクリックします。
6. アプリケーションの {{site.data.keyword.autoscaling}} ポリシーをまだ定義していない場合は、*「{{site.data.keyword.autoscaling}} ポリシーの作成 (Create Auto-Scaling Policy)」*をクリックして定義します。

これで、{{site.data.keyword.autoscaling}} ポリシーの構成、メトリック統計の表示、およびアプリケーションのスケーリング履歴の表示ができるようになりました。
<dl>
<dt>ポリシーの構成</dt>
<dd>このセクションを使用して、特定のスケーリング・アクティビティーをトリガーすべき条件を指定するスケーリング・ルールを作成または編集します。<ul>
<li> Liberty for Java™ アプリケーションの場合は、JVM ヒープ、メモリー、およびスループットのスケーリング・ルールを定義することができます。
<li> Node.js アプリケーションの場合は、メモリーのスケーリング・ルールを定義することができます。<li> 
Ruby アプリケーションの場合は、メモリーのスケーリング・ルールを定義することができます。</ul>
*注:* スケーリング・ルールは、複数のメトリック・タイプに対して複数定義することができます。ただし、{{site.data.keyword.autoscaling}} サービスはスケーリング・ポリシー間の競合を検出しません。スケーリング・ポリシーを定義する際は、必ず、複数のスケーリング・ルールがお互いに競合しないようにする必要があります。さもないと、アプリケーションがスケールインしたかと思うと、次の瞬間スケールアウトするため、総インスタンス数が変動する場合があります。<br/><br/>アプリケーションのワークロードがピーク時と空き時間で大幅に変動する場合は、期間が変わればスケーリング要件を変えて対処するようにスケーリング・スケジュールを作成することができます。動的スケーリング・ルールはスケールイン・アクションとスケールアウト・アクションをトリガーするためにスケジュールに適用したまま、そのスケジュールに指定されている Minimum Instance Count パラメーターを使用して、アプリケーション・インスタンス数のベースラインを定義してください。</dd>
<dt>メトリック統計</dt>
<dd>アプリケーションのインスタンスについてメトリック統計を表示します。
平均統計を表示して特定のインスタンスを選択すると、その統計を表示することができます。
</dd>
<dt>スケーリングの履歴</dt>
<dd>ご使用のアプリケーションのスケーリング履歴を表示します。<ul>
<li> 過去の週 :
この 1 週間のスケーリング履歴を表示します。<li> 過去の月 :
この 1 カ月のスケーリング履歴を表示します。<li> カスタム範囲:
期間を設定することができます。</ul>
*注:* 履歴レコードは、「スケーリング状況 (Scaling Status)」または「スケールイン/スケールアウト (Scaling In/Out)」を選択することで、フィルタリングできます。</dd>
</dl>


## {{site.data.keyword.autoscaling}} サービスのポリシー・フィールド
{: #policyfields}

| フィールド名  | 説明 |
|-------------|----------------------|
|*「許容最大インスタンス数 (Allowable maixmum instance
count)」* |	開始できるアプリケーション・インスタンスの最大数。
現在のアプリケーション・インスタンス数がこの値に等しい場合、 {{site.data.keyword.autoscaling}} サービスは、そのアプリケーションをそれ以上スケールアウトしません。「デフォルト最小インスタンス数」	開始できるアプリケーション・インスタンスの最小数。インスタンス数がこの値に等しい場合、 {{site.data.keyword.autoscaling}} サービスは、そのアプリケーションをそれ以上スケールインしません。 |
| *「メトリック・タイプ」*	| 	モニター可能なサポートされるメトリック・タイプ。
詳細については、表 2 を参照してください。 |
| *「スケールアウト」* | 	スケールアウト・アクションがトリガーされるしきい値、およびスケールアウト・アクションがトリガーされた時に増加されるインスタンスの数を指定します。 |
| *「スケールイン」* |	スケールイン・アクションがトリガーされるしきい値、およびスケールイン・アクションがトリガーされた時に削減するインスタンスの数を指定します。 |
| *「統計ウィンドウ」* |	受け取ったメトリック値が有効と認識される、過去の期間の長さ。メトリック値は、タイム・スタンプがこの期間内に含まれている場合のみ有効です。
Statistic Window パラメーターの単位は秒です。 |
| *「違反期間」*	| スケーリング・アクションがトリガーされる可能性がある、過去の期間の長さ。スケーリング・アクションは、収集されたメトリック値が、指定した時間より長い間、しきい値の上限を上回るかしきい値の下限を下回る場合にトリガーされます。Breach Duration パラメーターの単位は秒です。 |
| *「スケールインのクールダウン期間」* | スケールイン・アクションの発生後、Cooldown period for scaling in パラメーターで指定した期間中は、他のスケーリング要求は無視されます。このパラメーターの単位は秒です。 |
| *「スケールアウトのクールダウン期間」*	| スケールアウト・アクションの発生後、Cooldown period for scaling out パラメーターで指定した期間中は、他のスケーリング要求は無視されます。このパラメーターの単位は秒です。 |
| *「タイム・ゾーン (Time Zone)」*	| スケジュールが適用されるタイム・ゾーン。 |
| *「開始時刻 (Start Time)」*  |	反復スケジュールの開始時刻。 |
| *「終了時刻 (End Time)」*    |	反復スケジュールの終了時刻。	|
| *「反復曜日 (Repeat On)」*	|	反復スケジュールが適用される曜日。 |
| *「最小インスタンス数 (Minimum Instance Count)」* |	スケジュールで指定された期間に開始できる最小アプリケーション・インスタンス数。 |
| *「開始日時 (Start Date & Time)* |	特定日にセットアップされているスケジュールの開始日時。 |
| *「終了日時 (End Date & Time)」* |	特定日にセットアップされているスケジュールの終了日時。	|

表 1. スケーリング・ポリシーのポリシー・フィールド

| メトリック名 | 説明 | サポートされるアプリケーション・タイプ |
|-------------|----------------------| ------------------- |
| *「JVM ヒープ」* |	JVM のヒープ・メモリーの使用率。	| Liberty for Java |
| *「メモリー」*   |	メモリーの使用率。	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *「スループット」* | 1 秒当たりに処理される要求の数。| Liberty for Java |
| *「応答時間」* |	処理された要求の応答時間。	| Liberty for Java |

表 2. サポートされるメトリック名

## エラー・メッセージ
{: #errmsgs}
このセクションでは {{site.data.keyword.autoscaling}} サービスで出される警告とエラー・メッセージをリストします。
 
### CWSCV2004E 他の {{site.data.keyword.autoscaling}} サービスが既にアプリケーションにバインド済みです。
**1 つのアプリケーションにバインドできる {{site.data.keyword.autoscaling}} サービスは 1 つのみです。このエラーは、既に {{site.data.keyword.autoscaling}} サービスにバインドされているアプリケーションに、別の {{site.data.keyword.autoscaling}} サービスをバインドしようとした時に発生します。**

どの {{site.data.keyword.autoscaling}} サービスにもバインドされていない他のアプリケーションを選択して、ターゲットの
{{site.data.keyword.autoscaling}} サービスをそのアプリケーションにバインドします。その他のすべての状況でこのエラーが発生する場合は、IBM サポートにお問い合わせください。

### CWSCV6001E API サーバーは API の入力 JSON ストリングを解析できません: {0}。
**入力 JSON ストリングを解析している時に問題が発生しました。**

API の資料で入力 JSON を調べ、エラーを修正してください。

### CWSCV6002E API サーバーは API の出力 JSON ストリングを解析できません: {0}。
**入力 JSON ストリングを解析している時に問題が発生しました。**

詳細情報について、クラウド管理者にお問い合わせください。

### CWSCV6003E 入力 JSON ストリング・フォーマットのエラー: API の入力 JSON 内の {0}: {1}。
**入力 JSON ストリングを解析している時にフォーマット・エラーが検出されました。**

API の資料で入力 JSON を調べ、エラーを修正してください。

### CWSCV6004E 出力 JSON ストリング・フォーマットのエラー: API の出力 JSON 内の {0}: {1}。
**出力 JSON ストリングを解析している時にフォーマット・エラーが検出されました。**

詳細情報について、クラウド管理者にお問い合わせください。

### CWSCV6005E {0} 中、内部サーバー・エラーが発生しました。
**要求を処理している時に内部サーバー・エラーが発生しました。**

詳細情報について、クラウド管理者にお問い合わせください。

### CWSCV6006E CloudFoundry API の呼び出しが失敗しました: {0}
**CloudFoundry API を呼び出している時にエラーが発生しました。**

詳細情報について、クラウド管理者にお問い合わせください。

### CWSCV6007E アプリケーションが見つかりません: {0}
**アプリケーションが見つかりません。**

詳細情報について、アプリケーション情報を調べてください。

### CWSCV6008E アプリケーション {0} の情報を取得している時に次のエラーが発生しました: {1} 
**何らかのエラーによりアプリケーション情報の取得に失敗しました。**

詳細情報について、アプリケーション情報を調べてください。

### CWSCV6009E サービス: アプリ {1} の {0} が見つかりません。
**このアプリケーションのサービスが見つかりません。**

詳細情報について、このアプリケーションのサービス・バインディングを調べてください。

### CWSCV6010E アプリ {0} のポリシーが見つかりません
**このアプリケーションのポリシーが見つかりません。**

詳細情報について、アプリケーション構成を調べてください。

### CWSCV6011E {0} 中、内部認証に失敗しました
**内部認証に失敗しました。**

詳細情報について、クラウド管理者にお問い合わせください。


# 関連リンク
## サンプル
* [チュートリアル: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry アーキテクチャー・ラボ](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
* [IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}} の Rest API (Rest API of IBM Auto-Scaling for Bluemix)](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window}

## 一般
* [{{site.data.keyword.Bluemix_notm}}  価格設定シート](https://console.{DomainName}/pricing/){:new_window}
* [{{site.data.keyword.Bluemix_notm}} の前提条件](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}

