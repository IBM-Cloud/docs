---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-22"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# データのバックアップ
{{site.data.keyword.cloudantfull}} データベースのレプリカを生成することにより、{{site.data.keyword.iotinsurance_full}} データのバックアップを作成することができます。
{:shortdesc}

{{site.data.keyword.iotinsurance_full}} に保管されている {{site.data.keyword.iotinsurance_short}} のデータベースは、以下の表に示されているとおりです。

*表 1: {{site.data.keyword.iotinsurance_short}} のデータベース*

データベース名| 変更の頻度| 変更の理由 | バックアップが必要 | コメント
------------- | -------------| -------------| -------------| -------------
favorites|管理|新しい管理者アクション|はい|-
Devices|管理|新しいデバイスまたはユーザーの追加または削除|はい| 変換プログラムにより、メモリー内に表が動的生成され、デバイス・プロバイダーからのデータがその表に設定されます。直接接続のゲートウェイの場合、この表にデバイスが格納されます。
hazardevents|ランダム|新しいシールド・イベントの検出|はい|-
Jscode|管理|シールド用の新しい JS コードのデプロイ|はい*| 管理者は、オプションとして、バックアップをスキップし、JS コードの新しいバージョンをデプロイすることができます。
Promotions|管理|新しいプロモーションの追加|はい|-
shieldassociations|管理|新しいユーザーまたはシールドの追加|はい|-
Shields|管理|新しいシールドの追加|はい|-
Users|管理|新しいユーザーの追加|はい|-
aggregation|-|-|いいえ|再作成可能。
aggregationschedule|-|-| いいえ|再作成可能。

{{site.data.keyword.iotinsurance_short}} のデータをバックアップするには、以下の手順を実行します。

## {{site.data.keyword.cloudant_short_notm}} インスタンスのレプリカの作成
{: #createinstance}
{{site.data.keyword.cloudant}} インスタンスのレプリカを作成するには、[{{site.data.keyword.cloudant}} のレプリケーションの手順 ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html) に従います。災害復旧が目的の場合、元の {{site.data.keyword.iotinsurance_short}} サービスとは別の場所にレプリカを作成します。例えば、元のインスタンスがダラスにある場合、レプリカをロンドンに作成することができます。

## 資格情報と URL を見つける
{: #locate_credentials}
元の {{site.data.keyword.cloudant}} のインスタンスと複製インスタンスの資格情報と URL を見つけます。
1. {{site.data.keyword.cloudant}} サービスを開きます。
2. **「サービス資格情報」**タブをクリックします。これは、サービスの名前の下にあります。
3. **「資格情報の表示」**をクリックします。
4. ユーザー名、パスワード、URL をメモします。

## 新しいレプリケーション・タスクの作成
{: #create_replication}
バックアップを作成する必要のある各データベースのレプリケーション・タスクを作成します。バックアップの必要なデータベースは、前のセクションの表 1 に示されているものです。

1. {{site.data.keyword.Bluemix_notm}} コンソールを開きます。

2. 元の {{site.data.keyword.cloudant}} サービスを開きます。

3. **「起動」**をクリックして、{{site.data.keyword.cloudant}} ダッシュボードを開きます。

4. メニューで**「レプリケーション (Replication)」**を選択します。

5. 「ソース・データベース (Source Database)」セクションに、元のデータベースの URL を入力します。各データベースの URL の形式は、https://<CloudantbaseURL>/<database_name> です。例えば、hazardevents データベースの URL は、https://<CloudantbaseURL>/hazardevents です。

6. 「ターゲット・データベース (Target Database)」セクションに、新しいデータベースの URL を入力します。

7. **重要:** **「このレプリケーションを連続にする (Make this replication continuous)」**は選択しないでください。連続レプリケーションでは、パフォーマンスが著しく低下します。

8. **「データのレプリカを生成 (Replicate Data)」**をクリックします。  

9. (オプション) 前のデータは後のレプリケーション・タスクによって上書きされるため、データを CSV ファイルにエクスポートすることを考慮してください。その手順については、[Export Cloudant JSON as CSV, RSS, or iCal ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window} を参照してください。

10. データベースごとにこれらのステップを繰り返します。

## バックアップの実行
{: #run_backup}
レプリケーション・タスクを作成した後は、いつでもバックアップを再実行できます。
1. {{site.data.keyword.Bluemix_notm}} コンソールを開きます。
2. 元の {{site.data.keyword.cloudant}} サービスを開きます。
3. **「起動」**をクリックして、{{site.data.keyword.cloudant}} ダッシュボードを開きます。
4. メニューで**「レプリケーション (Replication)」**をクリックした後、**「すべてのレプリケーション (All Replications)」**を選択します。
5. データベースをすべて選択し、各レプリケーションを再実行します。**「アクティブ・レプリケーション (Active Replications)」**をクリックすることにより、進行中のジョブの状況を確認することができます。
6. すべてのレプリケーションが完了した時点で、データを CSV フラット・ファイルにエクスポートすることができます。

## データのリストア
{: #restore_data}
複製データベースから、または保存した CSV ファイルをロードすることによりデータをリストアすることができます。
1. {{site.data.keyword.Bluemix_notm}} コンソールを開きます。
2. {{site.data.keyword.iotinsurance_short}} サービスを停止します。
3. 以下のいずれかの方法でデータを復元します。
  - CSV バックアップ・ファイルからデータをプライマリー Cloudant インスタンスに直接ロードします。
  - 複製データベースをソースとし、元のデータベースをターゲットとするレプリケーション・タスクを作成します。このタスクにより、複製データが元のデータベースに移動します。
4. 以下のスクリプトを実行して、設計文書を再作成し、参照整合性をリストアします。これらのスクリプトは、[GitHub の {{site.data.keyword.iotinsurance_short}} API サンプル・サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window} にあります。
  - iot4i-api/wearable-framework/auto-create/create.sh - このスクリプトは、{{site.data.keyword.cloudant}} 内に設計文書を再作成します。
  - iot4i-api/wearable-framework/health/check-relations - このスクリプトは、参照整合性を再確立します。例えば、このスクリプトは、シールドが削除されているがユーザーへの関連付けはまだ存在するという状況を修正します。
