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

# {{site.data.keyword.contdelivery_short}} のトラブルシュティング
{: #ts_cd}

{{site.data.keyword.contdelivery_full}} の使用に関するトラブルシュティングのための一般的な質問に対する回答を示します。
{:shortdesc}


## GitHub で許可できない
{: #cannot_authorize_github}

ユザが GitHub で許可されていません。
{:shortdesc}

GitHub アカウントにアクセスできるように {{site.data.keyword.Bluemix_notm}} を許可していない場合、以下の問題が発生する可能性があります。
{: tsSymptoms}

 * GitHub ツル統合をツルチェンに追加しようとしたときに、ツル統合が追加されない。
 * 変更を GitHub リポジトリまたは GitHub Enterprise リポジトリにプッシュしたときに、パイプラインが自動的に実行されない。

{{site.data.keyword.Bluemix_notm}} が GitHub へのアクセスを許可されていません。  
{: tsCauses}
 
ツルチェン作成時に GitHub ツル統合を構成している場合、以下の手順を実行します。
{: tsResolve}
 
  1. 「構成可能な統合 (Configurable Integrations)」セクションで**「GitHub」**をクリックします。 
  1. {{site.data.keyword.Bluemix_notm}} Public でツルチェンを作成していて、 {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していなければ、**「認可 (Authorize)」** をクリックして GitHub Web サイトに移動します。 
  1. アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワドを入力していない場合は、確認のために GitHub パスワドの入力を求められることがあります。
  
既にツルチェンが存在している場合は、GitHub ツル統合の構成を更新します。

 1. DevOps ダッシュボドの**「ツルチェン」**ペジで、ツルチェンをクリックしてその「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、その後で**「概要」**をクリックします。
 1. GitHub カドで、メニュをクリックし、**「構成」**をクリックします。
 1. {{site.data.keyword.Bluemix_notm}} が GitHub にアクセスすることを許可するよう構成設定を更新します。**「認可 (Authorize)」**をクリックして GitHub Web サイトに移動します。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワドを入力していない場合は、確認のために GitHub パスワドの入力を求められることがあります。
 1. 設定の更新が完了したら、**「統合の保存」**をクリックします。


## ツル統合が構成されない
{: #tool_integration_error}

ツルチェン用にツル統合を構成した後、そのツル統合のツル・カドに `Setup failed` エラが表示されます。
{:shortdesc}

ツル統合を構成した後、ツルチェンの「概要」ペジに、そのツル統合のツル・カドが表示され、セットアップが失敗したことが通知されます。
{: tsSymptoms}

 ![Setup failed エラ](images/tool_setup_failed.png)
 
ツル統合を追加すると、ツルチェンはそのツル統合によって表されるツルと通信して、必要なリソスのプロビジョンを行い、それらをツルチェンと関連付けます。このセットアップ処理中にエラが発生した場合、または、ツルチェンとツルとの間の通信が正常に完了しない場合、ツル統合はエラ状態になります。
{: tsCauses}

次のようにして、ツル統合を再構成します。
{: tsResolve}

1. ツル・カドで `Setup failed` メッセジの上に移動し、**「再構成 (Reconfigure)」**をクリックします。

 ![「再構成」ボタン](images/tool_reconfigure.png)
 
1. 有効な構成パラメタを使用していることを確認します。無効な構成が原因でエラが起こった場合、例えば `The integration could not be set up. Check the settings and try again. Reason: Invalid api_key:fakeKey` のようなエラ・メッセジが表示されます。ツル統合の設定を更新し、**「統合の保存」**をクリックします。
1. 通信の問題が原因でエラが起こった場合、**「統合の保存」**をクリックして再試行します。
