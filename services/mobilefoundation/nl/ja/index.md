---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Mobile Foundation の概要
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}} は {{site.data.keyword.mfp_full}} 環境 (この環境からエンタープライズ・モバイル・アプリの開発、テスト、操作が可能です) のセットアップを迅速に処理します。
{{site.data.keyword.mobilefoundation_short}} は、「開発者」と「プロフェッショナル 1 アプリケーション」の 2 つの異なるサービス・プランで利用可能です。
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> 「プロフェッショナル 1 アプリケーション」プランを使用して、Android、iOS、Windows、モバイル Web などの、サポートされるいずれかまたはすべての作動プラットフォームで構築された単一アプリケーションを管理できます。「開発者」プランは、開発とテストに最適です。<!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan -->



## 「Mobile Foundation: 開発者」プランの概要
{: #gettingstartedtemplate_dev}

「{{site.data.keyword.mobilefoundation_short}}: 開発者」のインスタンスの作成後に、数回クリックするだけでモバイル・チャネルの作成を開始できます。

*	デフォルト構成を使用して {{site.data.keyword.mobilefirst_notm}} サーバー・インスタンスを作成するには、**「基本サーバーの始動」**をクリックします。
		

  `基本サーバー・インスタンスには、単一のノードと 1 GB のメモリーが含まれています。`

* トポロジー、セキュリティー、およびその他のサーバー構成について拡張構成を使用して {{site.data.keyword.mobilefirst_notm}} サーバー・インスタンスを作成するには、**「拡張構成を使用したサーバーの始動 (Start Server with Advanced Configuration)」**をクリックします。詳しくは、[拡張構成のセットアップ](c_using_mfs_p1.html#using_mfs_advanced_p1)を参照してください。

## 「Mobile Foundation: プロフェッショナル 1 アプリケーション」プランの概要
{: #gettingstartedtemplate_prof}

「{{site.data.keyword.mobilefoundation_short}}: プロフェッショナル 1 アプリケーション」サービスのインスタンスの作成後に、以下のステップを実行することでモバイル・チャネルの作成を開始できます。

1.  {{site.data.keyword.Bluemix_notm}} 上の既存の「{{site.data.keyword.dashdbshort}} for Transactions」サービスに接続します。

    1.  {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する {{site.data.keyword.Bluemix_notm}} `組織`を選択します。

    + 選択された`組織`で使用可能なスペースのリストから、{{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する、{{site.data.keyword.Bluemix_notm}} の`スペース`を選択します。

    + 既存の {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスに接続するための {{site.data.keyword.dashdbshort_notm}} `サービス名` および `資格情報` を選択します。

    + **「接続のテスト」**をクリックして、選択された「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービス・インスタンスへの接続をテストします。

    + **「追加」**をクリックした後、選択した「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービスについて確認を求めるポップアップ・ウィンドウで**「続行」**をクリックします。このアクションにより、構成された {{site.data.keyword.dashdbshort_notm}} データベース・サービス・インスタンスで必要な表が作成されます。

    **注:** {{site.data.keyword.dashdbshort_notm}} 接続を {{site.data.keyword.mobilefoundation_short}} インスタンスに追加した後は、それを変更することはできません。

2.  サーバーを作成して始動します。

    * デフォルト構成を使用して {{site.data.keyword.mobilefirst_notm}} サーバー・インスタンスを作成するには、**「基本サーバーの始動」**をクリックします。
		

      `基本サーバー・インスタンスには、単一のノードと 1 GB のメモリーが含まれています。`

    * トポロジー、セキュリティー、およびその他のサーバー構成について拡張構成を使用して {{site.data.keyword.mobilefirst_notm}} サーバー・インスタンスを作成するには、**「拡張構成を使用したサーバーの始動 (Start Server with Advanced Configuration)」**をクリックします。詳しくは、[拡張構成のセットアップ](c_using_mfs_p2.html#using_mfs_advanced_p2)を参照してください。

## 「Mobile Foundation: 開発者専門」プランの概要
{: #gettingstartedtemplate_devpro}

「{{site.data.keyword.mobilefoundation_short}}: 開発者専門」サービスのインスタンスの作成後に、以下のステップを実行することでモバイル・チャネルの作成を開始できます。

  1.  {{site.data.keyword.Bluemix_notm}} 上の既存の「{{site.data.keyword.dashdbshort}} for Transactions」サービスに接続します。

      1.  {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する {{site.data.keyword.Bluemix_notm}} `組織`を選択します。

      + 選択された`組織`で使用可能なスペースのリストから、{{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する、{{site.data.keyword.Bluemix_notm}} の`スペース`を選択します。

      + 既存の {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスに接続するための {{site.data.keyword.dashdbshort_notm}} `サービス名` および `資格情報` を選択します。

      + **「接続のテスト」**をクリックして、選択された「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービス・インスタンスへの接続をテストします。

      + **「追加」**をクリックした後、選択した「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービスについて確認を求めるポップアップ・ウィンドウで**「続行」**をクリックします。このアクションにより、構成された {{site.data.keyword.dashdbshort_notm}} データベース・サービス・インスタンスで必要な表が作成されます。

      **注:** {{site.data.keyword.dashdbshort_notm}} 接続を {{site.data.keyword.mobilefoundation_short}} インスタンスに追加した後は、それを変更することはできません。

  2.  サーバーを作成して始動します。

      * デフォルト構成を使用して {{site.data.keyword.mobilefirst_notm}} サーバー・インスタンスを作成するには、**「基本サーバーの始動」**をクリックします。
		

      * この選択により、以下の設定で {{site.data.keyword.mfserver_long_notm}} がプロビジョンされます。

          - 1 GB のメモリーを備えた単一ノード。開発アクティビティー、中程度のテスト・アクティビティー、および小規模な実動ワークロードには、このサイズで十分です。

          -	`ユーザー名`と`パスワード`は、自動的に生成されます。サーバーの稼働中にこれらにアクセスできます。

      * トポロジー、セキュリティー、およびその他のサーバー構成について拡張構成を使用して {{site.data.keyword.mobilefirst_notm}} サーバー・インスタンスを作成するには、**「拡張構成を使用したサーバーの始動 (Start Server with Advanced Configuration)」**をクリックします。詳しくは、[拡張構成のセットアップ](c_using_mfs_p3.html#using_mfs_advanced_p3)を参照してください。

## 「Mobile Foundation: 容量当たりのプロフェッショナル」プランの概要
{: #gettingstartedtemplate_profper}

「{{site.data.keyword.mobilefoundation_short}}: 容量当たりのプロフェッショナル」サービスのインスタンスの作成後に、以下のステップを実行することでモバイル・チャネルの作成を開始できます。

  1.  {{site.data.keyword.Bluemix_notm}} 上の既存の「{{site.data.keyword.dashdbshort}} for Transactions」サービスに接続します。

      1.  {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する {{site.data.keyword.Bluemix_notm}} `組織`を選択します。

      + 選択された`組織`で使用可能なスペースのリストから、{{site.data.keyword.dashdbshort_notm}} サービス・インスタンスが存在する、{{site.data.keyword.Bluemix_notm}} の`スペース`を選択します。

      + 既存の {{site.data.keyword.dashdbshort_notm}} サービス・インスタンスに接続するための {{site.data.keyword.dashdbshort_notm}} `サービス名` および `資格情報` を選択します。

      + **「接続のテスト」**をクリックして、選択された「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービス・インスタンスへの接続をテストします。

      + **「追加」**をクリックした後、選択した「{{site.data.keyword.dashdbshort_notm}} for Transactions」サービスについて確認を求めるポップアップ・ウィンドウで**「続行」**をクリックします。このアクションにより、構成された {{site.data.keyword.dashdbshort_notm}} データベース・サービス・インスタンスで必要な表が作成されます。

      **注:** {{site.data.keyword.dashdbshort_notm}} 接続を {{site.data.keyword.mobilefoundation_short}} インスタンスに追加した後は、それを変更することはできません。

  2.  サーバーを作成して始動します。

      * デフォルト構成を使用して {{site.data.keyword.mobilefirst_notm}} サーバー・インスタンスを作成するには、**「基本サーバーの始動」**をクリックします。
		

      * この選択により、以下の設定で {{site.data.keyword.mfserver_long_notm}} がプロビジョンされます。
          -  2 個のノード (それぞれ 1 GB のメモリーを装備)。開発アクティビティー、中程度のテスト・アクティビティー、および小規模な実動ワークロードには、このサイズが適しています。

          -	`ユーザー名`と`パスワード`は、自動的に生成されます。サーバーの稼働中にこれらにアクセスできます。

      * トポロジー、セキュリティー、およびその他のサーバー構成について拡張構成を使用して {{site.data.keyword.mobilefirst_notm}} サーバー・インスタンスを作成するには、**「拡張構成を使用したサーバーの始動 (Start Server with Advanced Configuration)」**をクリックします。詳しくは、[拡張構成のセットアップ](c_using_mfs_p4.html#using_mfs_advanced_p4)を参照してください。

{{site.data.keyword.mobilefoundation_short}} の使用を開始する方法について詳しくは、[Using the Mobile Foundation service to set up MobileFirst Server<!-- on IBM Containers--> ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/){: new_window}を参照してください。

##  既知の制限
{: #knownlimitations_mfp}

* {{site.data.keyword.mobilefoundation_short}} サービス UI は、番号を表示するためにユーザーが選択したロケール特定パターンを使用しません。


# 関連リンク
{: #rellinks  notoc}

## 関連リンク
{: #general notoc}

*	[IBM MobileFirst Platform Foundation V8.0.0 製品資料![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobilefirstplatform.ibmcloud.com){: new_window}
