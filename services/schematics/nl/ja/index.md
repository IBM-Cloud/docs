---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.bpfull_notm}} (ベータ) 概説
{: #gettingstarted}

{{site.data.keyword.bplong}} は、クラウドのインフラストラクチャーを単一ユニットとして定義してデプロイすることができる自動化ツールです。これを使用すると、任意の数の環境でクラウドのリソース定義を再利用できます。
{:shortdesc}

{{site.data.keyword.bpshort}} は (HashiCorp の) Terraform を使用してインフラストラクチャーをコード化します。インフラストラクチャーのコンポーネントは個々のリソース (物理ハードウェアからユーザー・アカウントに至るあらゆるもの) に細分化されます。高位のリソースと低位のリソースを抽象化することによって、ソフトウェアを扱うかのようにインフラストラクチャーをコードとして扱うことができます。 

{{site.data.keyword.bpshort}} を使用する場合は、環境の構成を宣言構文で記述します。実動環境に 10 の {{site.data.keyword.virtualmachinesshort}} を含めるなど、環境の概要を記述します。このサービスは、その構成と Terraform で以前作成した内容を比較して、必要に応じてリソースを追加したり削除したりします。

{{site.data.keyword.bpshort}} は、インフラストラクチャーについての信頼できる唯一のソースを提供する DevOps コラボレーション・ツールです。環境構成をソース・コントロールに格納して、コード・レビュー、インフラストラクチャーのバージョン管理、コミット履歴による変更の追跡、変更の取り消しをチームで簡単に行うことができます。

{{site.data.keyword.bpshort}} は、{{site.data.keyword.Bluemix_notm}} アカウント内のすべてのユーザーに自動的に提供されます。


## 構成の作成
{: #configuration}

構成を作成するときには、環境を構成するクラウド・リソースをコード化します。
{:shortdesc}


{{site.data.keyword.bpshort}} でサンプル構成を試したい場合は、次の手順を実行してください。このサンプルでは、{{site.data.keyword.BluSoftlayer}} で使用する SSH 鍵をプロビジョンできます。 

**注:** このサンプル構成には、{{site.data.keyword.BluSoftlayer}} アカウントが必要です。アカウントを既に持っている場合には [{{site.data.keyword.Bluemix_notm}} アカウントと SoftLayer アカウントのリンク方法に関する資料](../../pricing/linking_accounts.html#unifyingaccounts)を参照してください。そうでない場合は、[アカウントを登録する](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)ことができます。

1. SSH 鍵ペアをローカルに生成します。
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> でサンプル構成をフォークします。 

  このサンプル構成に含まれているさまざまなタイプのブロックを例として次に示します。完全な構成は、GitHub リポジトリーの `main.tf` ファイルで確認できます。
  
  * provider ブロックでは、{{site.data.keyword.IBM_notm}} Cloud プロバイダーとログインの資格情報をセットアップします。

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * resource ブロックでは、インフラストラクチャーのコンポーネントを定義します。このサンプルの場合には SSH 鍵です。
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * variable ブロックでは変数を定義します。このサンプルの場合、変数は {{site.data.keyword.bpshort}} GUI で入力できます。
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * output ブロックでは、構成を使用して環境が作成され、リソース (SSH 鍵) が作成された後に Terraform 出力に表示される内容を定義します。
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
これで、構成から環境を作成できます。 

{:codeblock}

## 環境の作成
{: #environment}

環境を作成するときには、サービスに構成を参照させ、サービスが最新のコード変更を抽出できるようにします。
{:shortdesc}

サンプル構成を使用して、以下の手順を実行して環境を作成します。

1. メニューで、「**サービス**」、「**{{site.data.keyword.bpshort}}**」の順に選択します。{{site.data.keyword.bpshort}} ダッシュボードが表示されます。

2. 左側のナビゲーション・メニューで、「**環境**」を選択し、「**環境の作成 (Create Environment)**」をクリックして構成に関するプロパティーを記述します。環境を作成するということは、{{site.data.keyword.bpshort}} によるクラウド・リソースのプロビジョン方法と更新方法を定義することです。リソースはまだ作成されません。

3. 環境の詳細を入力します。このサンプル構成には、以下の表にリストする値が必要です。

  <table summary="サンプル構成を環境ソースとして使用するために必要な値。">
  <caption>表 1. サンプル構成を環境ソースとして使用するために必要な値。
  </caption>
  <thead>
  <th colspan="1">設定</th>
  <th colspan="1">説明</th>
  </thead>
  <tbody>
  <tr>
  <td>ソース・コントロール URL</td>
  <td>サンプル構成のフォーク操作を行った GitHub の URL を入力します。</td>
  </tr>
  <tr>
  <td>名前</td>
  <td>環境に割り当てる固有の名前を入力します。</td>
  </tr>
  <td>Terraform バージョン</td>
  <td>互換性のある Terraform バージョンが環境に対して実行されるようにするため、Terraform のバージョンを入力します。このサンプル構成の場合は、バージョン <code>0.9.1</code> を使用してください。</td>
  </tr>
  <tr>
  <td>変数</td>
  <td>サービスで変数を定義することも、<code>.tf</code> ファイルにある環境変数をオーバーライドすることもできます。ロック・アイコンをクリックすると、機密性の高い変数をマスクできます。変数をマスクした場合、隠された値は環境の詳細ページで他のユーザーに表示されなくなります。
  <p>
  <p>サンプル構成を使用するためには、次の変数と値を追加します。
  <ul>
  <li><code>ibmid</code> - 完全な {{site.data.keyword.ibmid}} を値として入力します。</li>
  <li><code>ibmidpw</code> - {{site.data.keyword.ibmid}} に関連付けられているパスワードを入力し、ロック・アイコンをクリックして値をマスクします。</li>
  <li><code>slaccountnum</code> - {{site.data.keyword.BluSoftlayer}} アカウント番号を入力します。
   <li><code>datacenter</code> - SSH 鍵リソースのデプロイ先のデータ・センターを入力します。使用可能なすべての値のリストについては、<a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">readme ファイル <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。</li> 
   <li><code>public_key</code> - 公開 SSH 鍵を入力します。公開鍵をクリップボードにコピーするには、<code>pbcopy < ~/.ssh/id_rsa.pub</code> コマンドを実行します。
   <li><code>key_label</code> - 固有の名前を使用して鍵を指定します。
   <li><code>key_note</code> - オプション: SSH 鍵に関するテキスト説明を追加します。</ul></td>
   </tr></tbody></table>

4. 環境の詳細を入力し終えたら、「**作成**」をクリックします。新たに作成された環境が表示されます。 
5. 環境のデプロイ時にプロビジョンまたは削除されるリソースをプレビューするには、「**プラン**」をクリックします。 
6. プランのログを表示し、出力にエラーがないか確認します。 
7. 環境をデプロイする準備が整ったら、「**適用**」をクリックします。適用ログをモニターし、鍵が正常にデプロイされたかどうか確認できます。デプロイが正常に行われた場合は、出力の最後のあたりに次の行が表示されます。

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  また、SSH 鍵を [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys) で確認することもできます。
8. オプション: SSH 鍵を削除し、環境も {{site.data.keyword.Bluemix_notm}} から削除する場合は、アクション・メニューから「**リソースの破棄 (Destroy resources)**」を選択します。

### 次の作業
{: #next}

* プログラムを使用して環境をデプロイする方法について理解を深めるために、[CLI または API について調べます](schematics_deploying.html)。
* 独自の構成を最初から作成する場合は、<a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud リソース <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> について調べます。{{site.data.keyword.IBM_notm}} Cloud リソースは、Terraform プラグイン・プロバイダーとして利用できます。
