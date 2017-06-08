---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.contdelivery_short}} のトラブルシューティング
{: #ts_cd}

{{site.data.keyword.contdelivery_full}} の使用に関するトラブルシューティングのための一般的な質問に対する回答を示します。
{:shortdesc}


## GitHub で許可できない
{: #cannot_authorize_github}

ユーザーが GitHub で許可されていません。
{:shortdesc}

GitHub アカウントにアクセスできるように {{site.data.keyword.Bluemix_notm}} を許可していない場合、以下の問題が発生する可能性があります。
{: tsSymptoms}

 * GitHub ツール統合をツールチェーンに追加しようとしたときに、ツール統合が追加されない。
 * 変更を GitHub リポジトリーまたは GitHub Enterprise リポジトリーにプッシュしたときに、パイプラインが自動的に実行されない。

{{site.data.keyword.Bluemix_notm}} が GitHub へのアクセスを許可されていません。  
{: tsCauses}
 
ツールチェーン作成時に GitHub ツール統合を構成している場合、以下の手順を実行します。
{: tsResolve}
 
  1. 「構成可能な統合 (Configurable Integrations)」セクションで**「GitHub」**をクリックします。 
  1. {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを作成していて、 {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していなければ、**「認可 (Authorize)」** をクリックして GitHub Web サイトに移動します。 
  1. アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケーションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワードを入力していない場合は、確認のために GitHub パスワードの入力を求められることがあります。
  
既にツールチェーンが存在している場合は、GitHub ツール統合の構成を更新します。

 1. DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックしてその「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、その後で**「概要」**をクリックします。
 1. GitHub カードで、メニューをクリックし、**「構成」**をクリックします。
 1. {{site.data.keyword.Bluemix_notm}} が GitHub にアクセスすることを許可するよう構成設定を更新します。**「認可 (Authorize)」**をクリックして GitHub Web サイトに移動します。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケーションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワードを入力していない場合は、確認のために GitHub パスワードの入力を求められることがあります。
 1. 設定の更新が完了したら、**「統合の保存」**をクリックします。


## ツール統合が構成されない
{: #tool_integration_error}

ツールチェーン用にツール統合を構成した後、そのツール統合のツール・カードに `Setup failed` エラーが表示されます。
{:shortdesc}

ツール統合を構成した後、ツールチェーンの「概要」ページに、そのツール統合のツール・カードが表示され、セットアップが失敗したことが通知されます。
{: tsSymptoms}

 ![Setup failed エラー](images/tool_setup_failed.png)
 
ツール統合を追加すると、ツールチェーンはそのツール統合によって表されるツールと通信して、必要なリソースのプロビジョンを行い、それらをツールチェーンと関連付けます。このセットアップ処理中にエラーが発生した場合、または、ツールチェーンとツールとの間の通信が正常に完了しない場合、ツール統合はエラー状態になります。
{: tsCauses}

次のようにして、ツール統合を再構成します。
{: tsResolve}

1. ツール・カードで `Setup failed` メッセージの上に移動し、**「再構成 (Reconfigure)」**をクリックします。

 ![「再構成」ボタン](images/tool_reconfigure.png)
 
1. 有効な構成パラメーターを使用していることを確認します。無効な構成が原因でエラーが起こった場合、例えば `The integration could not be set up. Check the settings and try again. Reason: Invalid api_key:fakeKey` のようなエラー・メッセージが表示されます。ツール統合の設定を更新し、**「統合の保存」**をクリックします。
1. 通信の問題が原因でエラーが起こった場合、**「統合の保存」**をクリックして再試行します。
