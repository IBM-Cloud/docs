---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IBM UrbanCode Deploy サーバーを Delivery Insights に接続する
{: #connect_ucd}

IBM UrbanCode Deploy サーバーからのデータを Delivery Insights で表示するには、そのサーバー上にパッチをインストールした後、そのサーバーを DevOps Connect に接続する必要があります。
{:shortdesc}

## 始めに

- [前提条件](uc_insights_prereqs.html) (DevOps Connect のインスタンスのセットアップなどがあります) を参照してください。

- IBM UrbanCode Deploy サーバーは、バージョン 6.2 以降でなければなりません。


## 手順

1. IBM UrbanCode Deploy サーバーにパッチをインストールします。
IBM UrbanCode Deploy のすべてのバージョンに、DevOps Connect と通信するためのパッチが必要です。
 
  1. 使用しているバージョンの IBM UrbanCode Deploy に該当する適切なパッチをダウンロードします。
そのためには、以下のページを表示して適切なパッチをダウンロードします。[http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. ファイルを解凍します。
それには、サーバーに追加する必要のある 1 つ以上のパッチ・ファイルが含まれています。


  1. サーバーを停止します。
[サーバーの開始と停止](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html)を参照してください。


  1. パッチ・ファイルを <code><em>application_data</em>/patches</code> フォルダーに入れます (<code><em>application_data</em></code> はサーバー・アプリケーション・データ・フォルダー)。
デフォルト・アプリケーション・データ・フォルダーは、`/opt/ibm-ucd/server/appdata` (Linux の場合)、および `C:&#xa5;Program Files&#xa5;ibm-ucd&#xa5;server&#xa5;appdata` (Windows の場合) です。
高可用性システムでは、アプリケーション・データ・フォルダーは常に各サーバーからアクセス可能な共有ネットワーク・ドライブ上にあります。


  1. オプション: サーバーが停止している間、このサーバーからのデータ・インポートのパフォーマンスを上げるために、以下の SQL コマンドをデータベースに対して実行します。
  
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time); 
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
`MyUCDDatabase` には、実際のデータベースの名前を使用します。
<!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. サーバーを起動します。
 

    **注:** 待ち時間は、IBM UrbanCode Deploy サーバーの通常の起動時間よりも長いことがあります。
いつまでたってもサーバーが始動しない場合、または正しく動作しない場合は、パッチ・ファイルを削除してからサーバーを始動してください。
パッチ・ファイルは、サーバーに対して永続的な影響があるわけではありません。


1. IBM UrbanCode Deploy の一部のバージョンでは、サーバーが DevOps Connect に接続するために付加的なパッチが必要です。
6.2 から 6.2.1.2 までのバージョンの IBM UrbanCode Deploy を使用している場合は、以下の付加的なパッチをサーバーにインストールする必要があります。

  1. パッチをダウンロードします:  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar)。

  1. サーバーを停止します。

  1. パッチ・ファイルを <code><em>application_data</em>/patches</code> フォルダーに入れます。

  1. サーバーを起動します。


1. DevOps Connect と IBM UrbanCode Deploy サーバーの間の統合を作成します。
  
  **重要:** 統合を初めて実行する際、DevOps Connect は過去 90 日間のデータを取り出します。
デプロイメント・データが大量にある場合、このプロセスに長い時間がかかることがあります。
90 日間未満のデータを取り出すようにするには、[『トラブルシューティング』](uc_insights_connect_ucd.html#troubleshooting)を参照してください。

  1. IBM UrbanCode Deploy で、認証トークンを作成します。
[トークン](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html)を参照してください。

  1. DevOps Connect で、**「統合」**をクリックしてから、**「新規追加」**をクリックします。

  1. 統合の名前と説明を指定します。
DevOps Connect の場所のデフォルトは `https://hostname:8443/` です (`hostname` は DevOps Connect のホストであるシステムのホスト名)。

  1. **「統合タイプ」**リストから、 **「IBM UrbanCode Deploy for Cloud のレポート (IBM UrbanCode Deploy for Cloud Reporting)」**を選択します。

  1. **「サーバー URI」**フィールドに、IBM UrbanCode Deploy サーバーのパブリック URL を入力します。例えば、`https://my_UCD.example.com:8447` など。

  1. **「認証トークン」**フィールドに、IBM UrbanCode Deploy によって生成された認証トークンを入力するか貼り付けます。

  1. **「管理ユーザー」**フィールドに、DevOps Connect インターフェースへのアクセス権を付与する IBMid のコンマ区切りリストを入力します。

  1. オプション: 即時統合を実行するには、**「統合の実行」**をクリックします。
デフォルトでは、1 分ごとに統合が実行されます。

  1. **「保存」**をクリックします。

  ![DevOps Connect での統合のセットアップ](images/uc_insights_dc_integration.gif)

これで、データが Delivery Insights と同期されます。
この段階で、このデータに基づくレポートを作成し、表示することができます。


## トラブルシューティング
{: #troubleshooting}

多くのアプリケーションやコンポーネント・プロセスの要求が IBM UrbanCode Deploy サーバー・データベースに保管されている場合、取得プロセス中にエラーが発生する場合があります。
以下のテキストのようなメッセージが、サーバー出力ログに記録されます。


`ORA-01652: 表スペース TEMP で一時セグメントを 128 拡張できませんでした`

この動作を回避するには、プラグインの `plugin.properties` ファイルを編集して、何日分のデータを取り出すかを示す日数を削減します。`plugin.properties` ファイルは、DevOps Connect のインストール先コンピューター上の `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` ディレクトリーにあります。
以下の行を編集し、番号記号 (#) を削除して日数を減らしてください。


`#numDaysToRetrieve=90`

例えば、過去 30 日のデータのみ取り出すには、この行を下記のテキストに変更します。


`numDaysToRetrieve=30`

ファイルを保存し、統合を再び実行します。
サーバー・ログを調べて、エラーがもう発生しなくなっていることを確認してください。

