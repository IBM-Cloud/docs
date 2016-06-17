---

copyright:
  years: 2016

---

#	「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」の使用
{: #using_mobilefoundation_p2}


「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの作成後、以下の手順を読んでサービスを開始してください。

## 前提条件
{: #prerequisites_p2}

{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスを構成する前に、以下の項目を考慮してください。
* 「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」は「{{site.data.keyword.dashdbshort_notm}}: エンタープライズ・トランザクション (OLTPをサポート)」{{site.data.keyword.Bluemix_notm}} プランでのみサポートされます。

* {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスとその資格情報を使用可能な状態にしないと、{{site.data.keyword.mobilefoundation_short}} サービス・インスタンスの設定を構成できません。

**注意**: {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスは {{site.data.keyword.Bluemix_notm}} の*組織* 内の任意の*スペース* に存在する可能性があります。  

## 「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの構成
{: #configure_dashdb_p2}

###  最初の手順
{: #firststeps_p2}

「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの作成後、以下のステップを実行してサービスを開始してください。

* {{site.data.keyword.mfp_full_notm}} V8.0.0.0 のライセンス条項に同意します。

* {{site.data.keyword.Bluemix_notm}} の資格情報を入力します。これにより、{{site.data.keyword.Bluemix_notm}} スペースでの変更と {{site.data.keyword.mobilefirst_notm}} サーバーをホストする {{site.data.keyword.containerlong}} の作成がサービスに許可されます。


### {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスへの接続のセットアップ
{: #connect_dashdb_p2}

「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービス・インスタンスの作成後、*「概要」* ページが表示されます。ここで「{{site.data.keyword.dashdbshort_notm}}: エンタープライズ・トランザクション」サービス・インスタンスの接続情報を指定する必要があります。

* 「{{site.data.keyword.dashdbshort_notm}}: エンタープライズ・トランザクション」サービス・インスタンスが存在する {{site.data.keyword.Bluemix_notm}} の**組織**および**スペース**を指定します。
* 作成した {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが複数ある場合は、{{site.data.keyword.mobilefoundation_short}} サービス・インスタンスで使用する {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスの**サービス名**をドロップダウンから選択してください。
* 選択した {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスの**資格情報**を選択します。

* **「接続のテスト」**をクリックしてご使用の {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが使用可能かどうか確認し、**「保存」**をクリックします。

**注意**: {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスで使用するように構成されたこの {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスを変更することはできません。ただし、同じ {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスを複数の {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスで使用することは可能です。これは、各 {{site.data.keyword.mobilefoundation_short}} サービス・インスタンスが選択された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンス内に独自のスキーマを作成するためです。

* 数秒後には*「概要」* ページにアクセスでき、ここで {{site.data.keyword.mobilefoundation_short}} サービスを使い始める上で役立つチュートリアルやビデオが提供されます。

### {{site.data.keyword.mobilefirst}} サーバーの始動
{: #start_mobilefoundation_p2}

* {{site.data.keyword.mfserver_short_notm}} をデフォルト設定で始動するには、**「基本サーバーの始動」**をクリックしてください。

![基本サーバーの始動](images/start_basic_server.png "図 1. 基本サーバーの始動")
{: screen}
* この選択により、以下の設定で {{site.data.keyword.mfserver_long_notm}} がプロビジョンされます。
    -  1 GB のメモリーおよび 64 GB のストレージ。開発アクティビティーと中程度のテスト・アクティビティーには、このサイズで十分です。

    -	*ユーザー名* と*パスワード* は自動的に生成されます。サーバーの稼働中にこれらにアクセスできます。

サーバーのプロビジョン・プロセスが始動します。このプロセスには約 10 分かかり、メッセージ・ウィンドウにはこの操作の進行が示されます。完了すると、以下のことを確認できるダッシュボードが表示されます。

  -	実行中のサーバーの状況 (状態、サイズ、ストレージ)。

  -	自動的に作成されたサーバーの経路。この経路を使用して、公衆インターネットからモバイル・サーバーに到達します。モバイル・アプリは、この経路を使用してサーバーにアクセスします。

  -	{{site.data.keyword.mfp_oc_short_notm}} にアクセスするための個人の*ユーザー名* と*パスワード*。*パスワード* は非表示です。視覚化するには、小さい目のアイコンをクリックします。

*	**「コンソールの起動」**をクリックして {{site.data.keyword.mfp_oc_short_notm}} を開きます。

![コンソールの起動](images/launch_console.png "図 2. コンソールの起動")
{: screen}

このコンソールはコンテナー内で実行されます。このコンソールを使用して、モバイル・アプリとモバイル・デバイスの管理、モバイル・バックエンドとしてのサーバーの使用、プッシュ通知の送信などを行えます。

### {{site.data.keyword.mobilefirst}} サーバーの再作成
{: #recreate_mobilefoundation_p2}

*	**「再作成」**をクリックしてサーバーを再作成します。

![再作成](images/recreate.png "図 3. 再作成")
{: screen}

* このアクションにより、ご使用の既存サーバーが停止し、削除されます。新しいサーバー・インスタンスが作成されます。このアクションは、完了するまでに数分かかります。

**注意**: アプリおよびアダプターに関する情報を含め、前のサーバー・インスタンスのデータはすべて、構成された {{site.data.keyword.dashdbshort_notm}} サービス・インスタンス内に保持されます。このデータは、サービスの再作成後も使用可能です。

##	拡張構成のセットアップ
{: #using_mfs_advanced_p2}

拡張設定またはカスタム設定を使用してサーバーを作成するには、*「概要」* ページの**「拡張構成を使用したサーバーの始動 (Start Server with Advanced Configuration)」**を使用します。また、**「構成 (Configuration)」**タブをクリックして、サーバー構成をカスタマイズするためにサーバー設定を更新することもできます。{{site.data.keyword.mobilefoundation_short}} では、拡張設定にアクセスできます。

*	**「トポロジー (Topology)」**タブから、コンテナーのトポロジー・サイズを選択できます。開発と簡単なテストにはデフォルトの 1 GB のサーバーで十分ですが、ロード・テストの実行などにはより多くが必要になる可能性があります。
  - ニーズに応じて、ご使用のサーバーに合ったサイズを選択してください。

  - **「ノード (Nodes)」**は作成されたノード数を表示します。
      - {{site.data.keyword.IBM_notm}} コンテナー・グループ内で必要なノードの最小数と最大数を構成できます。コンテナー・グループは、高可用性とスケーラビリティーを提供します。

      - ここでノード数を構成することで、{{site.data.keyword.mobilefirst}} サーバー・ファームを作成できます。

詳しくは、[{{site.data.keyword.mobilefoundation_long}} の資料](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}を参照してください。
