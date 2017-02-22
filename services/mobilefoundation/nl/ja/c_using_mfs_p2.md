---

copyright:
  years: 2016, 2017
lastupdated:  "2017-01-17"

---

#	「プロフェッショナル 1 アプリケーション」プランの使用
{: #using_mobilefoundation_p2}

「プロフェッショナル 1 アプリケーション」プランでは、ユーザーは、複数のモバイル・オペレーティング・システムを備えた 1 つのモバイル・アプリケーションを作成できます。
「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの作成後、以下の手順を読んでサービスを開始してください。

## 前提条件
{: #prerequisites_p2}

{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスを構成する前に、以下の項目を考慮してください。
* 「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」は「{{site.data.keyword.dashdbshort_notm}}: エンタープライズ・トランザクション (OLTPをサポート)」{{site.data.keyword.Bluemix_notm}} プランでのみサポートされます。

* {{site.data.keyword.dashdbshort_notm}} サービス・インスタンス資格情報へのアクセスができなければ、{{site.data.keyword.mobilefoundation_short}} サービス・インスタンスの設定を構成できません。

**注**: {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスは、{{site.data.keyword.Bluemix_notm}} `組織`内のどの`スペース`にも、また、アクセスできるどの`組織`にも存在できます。{{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する`スペース`へのアクセス権限があることを確認します。


## データベース接続の追加
{: #configure_dashdb_p2}

###  最初の手順
{: #firststeps_p2}

「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスを作成した後、以下の手順に従って、始めてください。

### {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスへの接続のセットアップ
{: #connect_dashdb_p2}

「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの作成後、*「概要」*ページが表示されます。ここで、{{site.data.keyword.mobilefoundation_short}} サービス・インスタンスを接続する「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービス・インスタンスの接続情報を指定する必要があります。

**注:** 「{{site.data.keyword.dashdbshort_notm}} for Analytics: Enterprise for Transactions」サービス・インスタンスが既にある場合は、それを使用して {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスに接続するように構成できます。

既存のものがない場合は、新規の「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービス・インスタンスを作成することもできます。

以下の手順に従って、新規の「dashDB for Transactions」サービス・インスタンスを作成します。

1. *概要* ページで、**「新規サービスの作成 (Create New Service)」**セクションを選択します。

+ 高可用性の「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービス・インスタンスが必要な場合は、**「高可用性構成」**オプションで`「はい」`を選択します。

+ プランの詳細を確認し、**「作成」**をクリックします。

新規の「{{site.data.keyword.dashdbshort_notm}} for Transactions: EnterpriseForTransactions2.8.500」サービス・インスタンスが作成されます。これは、8GB RAM、2 vCPU、および 500 GB のストレージを備えた専用の {{site.data.keyword.dashdbshort_notm}} インスタンスを提供します。

以下の手順に従って、既存の {{site.data.keyword.dashdbshort_notm}} サービス・インスタンス、または先ほど作成した「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービス・インスタンスに接続します。

1. {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する {{site.data.keyword.Bluemix_notm}} `組織`を選択します。

+ 選択された`組織`で使用可能なスペースのリストから、{{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する、{{site.data.keyword.Bluemix_notm}} の`スペース`を選択します。   
**注:** {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する、リストされた`組織`と`スペース`が表示されない場合、その`組織`と`スペース`のメンバーであるかどうかを確認します。{{site.data.keyword.mobilefoundation_short}} サービスは {{site.data.keyword.dashdbshort_notm}} サービスから資格情報にアクセスするため、組織およびスペースに対して*開発者* 役割のアクセス権限を持っている必要があります。

+ 既存の {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスに接続するための {{site.data.keyword.dashdbshort_notm}} `サービス名` および `資格情報` を選択します。

+  指定された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスへの接続をテストします。

+  **「追加」**をクリックします。このアクションにより、構成された {{site.data.keyword.dashdbshort_notm}} データベース・サービス・インスタンスで必要な表が作成されます。

数秒で `概要` ページにアクセスでき、ここで {{site.data.keyword.mobilefoundation_short}} サービスを使い始める上で役立つチュートリアルやビデオが提供されます。

**注意**: {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスで使用するように構成された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスを変更することはできません。ただし、同じ {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスを複数の {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスで使用することは可能です。これは、各 {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスが選択された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンス内に独自のスキーマを作成するためです。


## {{site.data.keyword.mobilefirst}} サーバーの始動
{: #start_mobilefoundation_p2}

* {{site.data.keyword.mfserver_short_notm}} をデフォルト設定で始動するには、**「基本サーバーの始動」**をクリックしてください。

* この選択により、以下の設定で {{site.data.keyword.mfserver_long_notm}} がプロビジョンされます。
    -  1 GB のメモリー。開発アクティビティー、中程度のテスト・アクティビティー、および小規模な実動ワークロードには、このサイズで十分です。

    -	`ユーザー名` と `パスワード` は自動的に生成されます。サーバーの稼働中にこれらにアクセスできます。

サーバーのプロビジョン・プロセスが始動します。このプロセスには約 10 分かかり、メッセージ・ウィンドウにはこの操作の進行が示されます。完了すると、以下のことを確認できるダッシュボードが表示されます。

  -	実行中のサーバーの状況 (状態、サイズ)。

  -	サーバーの経路が作成されます。{{site.data.keyword.mfserver_short_notm}} に接続するには、モバイル・アプリケーションでこの経路を使用します。

  -	{{site.data.keyword.mfp_oc_short_notm}} にアクセスするための個人の`ユーザー名` と`パスワード`。`パスワード` は非表示です。表示するには**「パスワードの表示」**アイコンをクリックします。

*	**「コンソールの起動」**をクリックして {{site.data.keyword.mfp_oc_short_notm}} を開きます。


<!--This console runs inside the container.--> このコンソールを使用して、モバイル・アプリ、アダプター、およびモバイル・デバイスの管理、モバイル・バックエンドとしてのサーバーの使用、プッシュ通知の送信などを行うことができます。



##  Mobile Analytics サーバーの追加
{: #adding_analytics_server_prof}

 Mobile Analytics サーバーを {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスに追加することにより、{{site.data.keyword.mobilefirst}} サーバー上のモバイル・アプリケーションをモニターできるようになりました。

 「プロフェッショナル」プランでは、コンテナー・グループに Mobile Analytics サーバーを作成します。ユーザーは、コンテナー・グループのコンテナー・ノードの数を選択することによって、構成をカスタマイズできます。

 ユーザーはまた、ボリュームをコンテナーに接続して、データを永続化できます。一度選択されたボリュームは変更できません。20 GB は、ユーザーに使用可能なデフォルトのファイル共有スペースです。分析データを保持するためにユーザーが追加のストレージ・スペースを必要とする場合、
ユーザーは、追加ファイル共有を購入し、このファイル共有を使用してボリュームを作成する必要があります。これでユーザーは、分析サーバーをデプロイ中に、この新規ボリュームを選択できます。

 {{site.data.keyword.containerlong}} へのボリュームの追加について詳しくは、[{{site.data.keyword.Bluemix_notm}} ダッシュボードを使用してボリュームに永続データを保管する![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/docs/containers/container_volumes_ui.html "外部リンク・アイコン"){: new_window}を参照してください。

* **「Analytics の追加 (Add Analytics)」**をクリックして、Mobile Analytics サーバーを {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスに追加します。

プロビジョン・プロセスが始動します。このプロセスには約 10 分かかり、メッセージ・ウィンドウにはこの操作の進行が示されます。  

*  {{site.data.keyword.mfp_oc_short_notm}} から、MobileFirst Analytics コンソールを起動します。

* {{site.data.keyword.mfserver_short_notm}} と Mobile Analytics サーバーとの間で、シングル・サインオンが使用可能になります。Mobile Analytics サーバーは、{{site.data.keyword.mfserver_short_notm}} サーバーと同じ LTPA 鍵とユーザー資格情報で構成されます。{{site.data.keyword.mfp_oc_short_notm}} のログインに使用したのと同じ `username` と `password` を使用して、Mobile Analytics コンソールにログインできます。

MobileFirst Analytics について詳しくは、[MobileFirst Foundation Operational Analytics ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/ "外部リンク・アイコン"){: new_window}を参照してください。

**注:** {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスを削除する場合や、{{site.data.keyword.mfserver_short_notm}} を再作成しようとする場合、Mobile Analytics サーバーは削除されます。

##  Mobile Analytics サーバーの削除
{: #deleting_analytics_server_prof}

{{site.data.keyword.mobilefoundation_short}} サービス・ダッシュボードから、{{site.data.keyword.mobilefoundation_short}} サービス・インスタンスに追加された Mobile Analytics サーバーを削除できるようになりました。

* **「Analytics の削除 (Delete Analytics)」**をクリックして、{{site.data.keyword.mobilefoundation_short}} サービス・インスタンスに追加されている Mobile Analytics サーバーを削除します。

 これにより、Analytics コンテナー・グループが削除されます。Analytics コンテナーの削除プロセスには、約 10 分かかります。画面を最新表示して、更新された状況を確認できます。Analytics コンテナーが削除されると、**「Analytics の追加 (Add Analytics)」**ボタンが再び有効になります。必要であれば、これを使用して再度 Mobile Analytics サーバーを追加できます。


## {{site.data.keyword.mobilefirst}} サーバーの再作成
{: #recreate_mobilefoundation_p2}

*	**「再作成」**をクリックしてサーバーを再作成します。

* このアクションは、既存のサーバーを停止し、データを削除します。更新されたバージョンがある場合は、更新されたバージョンで新しいサーバー・インスタンスが作成されます。このアクションは、完了するまでに数分かかります。

**注**: アプリおよびアダプターに関する情報など、前のサーバー・インスタンスのデータはすべて、構成された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンス内に保持されます。このデータは、サーバーの再作成に使用されます。

##	拡張構成のセットアップ
{: #using_mfs_advanced_p2}

拡張設定またはカスタム設定を使用してサーバーを作成するには、`「概要」` ページの**「拡張構成を使用したサーバーの始動 (Start Server with Advanced Configuration)」**を使用します。また、**「構成 (Configuration)」**タブをクリックして、サーバー構成をカスタマイズするためにサーバー設定を更新することもできます。{{site.data.keyword.mobilefoundation_short}} では、拡張設定にアクセスできます。

*	**「トポロジー (Topology)」**タブから、サーバーのサイズと、必要性に基づいてインスタンスの数を選択できます。開発と簡単なテストにはデフォルトの 1 GB のサーバーで十分です。
  - ニーズに応じて、ご使用のサーバーに合ったサイズを選択してください。

  - **「ノード (Nodes)」**は作成されたノード数を表示します。

      - ここでノード数を構成することで、{{site.data.keyword.mobilefirst}} サーバー・ファームを作成できます。

詳しくは、[{{site.data.keyword.mobilefoundation_long}} documentation ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html "外部リンク・アイコン"){: new_window}を参照してください。
