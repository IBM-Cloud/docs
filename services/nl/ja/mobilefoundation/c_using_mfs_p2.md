---

copyright:
  years: 2016

---

#	「プロフェッショナル 1 アプリケーション」プランの使用
{: #using_mobilefoundation_p2}

*最終更新日: 2016 年 6 月 15 日*
{: .last-updated}

「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの作成後、以下の手順を読んでサービスを開始してください。

## 前提条件
{: #prerequisites_p2}

{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスを構成する前に、以下の項目を考慮してください。
* 「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」は「{{site.data.keyword.dashdbshort_notm}}: エンタープライズ・トランザクション (OLTPをサポート)」{{site.data.keyword.Bluemix_notm}} プランでのみサポートされます。

* {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスとその資格情報を使用可能な状態にしないと、{{site.data.keyword.mobilefoundation_short}} サービス・インスタンスの設定を構成できません。

**注意**: {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスは {{site.data.keyword.Bluemix_notm}} の `組織` 内の任意の `スペース` に存在することができます。{{site.data.keyword.dashdbshort_notm}} サービスが存在するスペース以外の {{site.data.keyword.Bluemix_notm}} `スペース` に {{site.data.keyword.mobilefoundation_short}} サービスをデプロイする場合は、{{site.data.keyword.dashdbshort_notm}} サービスにアクセスする権限があることを確認してください。


## データベース接続の追加
{: #configure_dashdb_p2}

###  最初の手順
{: #firststeps_p2}

「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの作成後、{{site.data.keyword.mfp_full_notm}} V8.0 のライセンス条項に同意して始めます。

### {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスへの接続のセットアップ
{: #connect_dashdb_p2}

「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの作成後、*「概要」* ページが表示されます。ここで「{{site.data.keyword.dashdbshort_notm}}: エンタープライズ・トランザクション」サービス・インスタンスの接続情報を指定する必要があります。

1.  現在の `組織` で使用可能なスペースのリストから、{{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する {{site.data.keyword.Bluemix_notm}} `スペース` を選択します。

+ 既存の {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスに接続するための {{site.data.keyword.dashdbshort_notm}} `サービス名` および `資格情報` を選択します。

+  指定された「{{site.data.keyword.dashdbshort_notm}}:  エンタープライズ・トランザクション」サービス・インスタンスへの接続をテストします。

+  **「続行」**をクリックします。このアクションにより、構成された {{site.data.keyword.dashdbshort_notm}} データベース・サービス・インスタンスで必要な表が作成されます。

**注意**: {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスで使用するように構成された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスを変更することはできません。ただし、同じ {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスを複数の {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスで使用することは可能です。これは、各 {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスが選択された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンス内に独自のスキーマを作成するためです。

* 数秒で `概要` ページにアクセスでき、ここで {{site.data.keyword.mobilefoundation_short}} サービスを使い始める上で役立つチュートリアルやビデオが提供されます。

## {{site.data.keyword.mobilefirst}} サーバーの始動
{: #start_mobilefoundation_p2}

* {{site.data.keyword.mfserver_short_notm}} をデフォルト設定で始動するには、**「基本サーバーの始動」**をクリックしてください。

* この選択により、以下の設定で {{site.data.keyword.mfserver_long_notm}} がプロビジョンされます。
    -  1 GB のメモリーおよび 64 GB のストレージ。開発アクティビティーと中程度のテスト・アクティビティーには、このサイズで十分です。

    -	`ユーザー名` と `パスワード` は自動的に生成されます。サーバーの稼働中にこれらにアクセスできます。

サーバーのプロビジョン・プロセスが始動します。このプロセスには約 10 分かかり、メッセージ・ウィンドウにはこの操作の進行が示されます。完了すると、以下のことを確認できるダッシュボードが表示されます。

  -	実行中のサーバーの状況 (状態、サイズ、ストレージ)。

  -	自動的に作成されたサーバーの経路。この経路を使用して、公衆インターネットからモバイル・サーバーに到達します。モバイル・アプリは、この経路を使用してサーバーにアクセスします。

  -	{{site.data.keyword.mfp_oc_short_notm}} にアクセスするための個人の`ユーザー名` と `パスワード`。`パスワード` は非表示です。表示するには**「パスワードの表示」**をクリックします。

*	**「コンソールの起動」**をクリックして {{site.data.keyword.mfp_oc_short_notm}} を開きます。


このコンソールはコンテナー内で実行されます。このコンソールを使用して、モバイル・アプリとモバイル・デバイスの管理、モバイル・バックエンドとしてのサーバーの使用、プッシュ通知の送信などを行えます。

## {{site.data.keyword.mobilefirst}} サーバーの再作成
{: #recreate_mobilefoundation_p2}

*	**「再作成」**をクリックしてサーバーを再作成します。

* このアクションにより、ご使用の既存サーバーが停止し、削除されます。新しいサーバー・インスタンスが作成されます。このアクションは、完了するまでに数分かかります。

**注意**: アプリおよびアダプターに関する情報を含め、前のサーバー・インスタンスのデータはすべて、構成された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンス内に保持されます。このデータは、サーバーの再作成後も使用可能です。

##	拡張構成のセットアップ
{: #using_mfs_advanced_p2}

拡張設定またはカスタム設定を使用してサーバーを作成するには、`「概要」` ページの**「拡張構成を使用したサーバーの始動 (Start Server with Advanced Configuration)」**を使用します。また、**「構成 (Configuration)」**タブをクリックして、サーバー構成をカスタマイズするためにサーバー設定を更新することもできます。{{site.data.keyword.mobilefoundation_short}} では、拡張設定にアクセスできます。

*	**「トポロジー (Topology)」**タブから、コンテナーのサイズを選択できます。開発と簡単なテストにはデフォルトの 1 GB のサーバーで十分です。
  - ニーズに応じて、ご使用のサーバーに合ったサイズを選択してください。

  - **「ノード (Nodes)」**は作成されたノード数を表示します。
      - {{site.data.keyword.IBM_notm}} コンテナー・グループ内で必要なノードの最小数と最大数を構成できます。コンテナー・グループは、高可用性とスケーラビリティーを提供します。

      - ここでノード数を構成することで、{{site.data.keyword.mobilefirst}} サーバー・ファームを作成できます。

詳しくは、[{{site.data.keyword.mobilefoundation_long}} の資料](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}を参照してください。
