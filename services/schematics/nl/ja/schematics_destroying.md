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

# 一時的な環境内のリソースの破棄
{: #destroying}

{{site.data.keyword.bplong}} を使用して、リソースを破棄できます。リソースを破棄すると、環境とそれに関連付けたリソースがすべて破棄されます。  
{:shortdesc}

**警告**: リソースを破棄した場合、その操作を元に戻すことはできません。リソースを破棄することは、実稼働環境ではお勧めできませんが、テストや QA などの一時的な環境には便利です。

リソースを破棄する前に、以下のガイドラインを念頭に置いてください。 
* リソースに対する送信トラフィックがないことを確認する。
* 必要なデータがすべてバックアップされていることを確認する。 


## GUI によるリソースの破棄
{: #gui}

{{site.data.keyword.bpshort}} ダッシュボードを使用して、一時的な環境を開始したり、破棄したりできます。
{:shortdesc}

1. **「{{site.data.keyword.bpshort}}」**ダッシュボードで、**「環境」**タブを選択します。

2. 削除する特定の環境の行を選択します。 

3. オプション・メニューで、**「リソースの破棄 (Destroy resources)」**または**「環境の削除 (Delete environment)」**を選択します。削除操作と破棄操作は、どちらも元に戻せません。どちらのオプションを選択するか決めるときには、アクティブなリソースの有無を考慮してください。
  * アクティブなリソースを停止して削除する場合は、**「リソースの破棄 (Destroy resources)」**を選択します。破棄する前にプランを実行して、その環境に関連付けられているリソースを削除してよいか確認することをお勧めします。
  * {{site.data.keyword.bpshort}} サービスから環境構成を削除する場合は、**「環境の削除 (Delete environment)」**を選択します。このオプションは、通常、環境がデプロイされておらず、アクティブなリソースがない場合に使用します。アクティブなリソースがある場合にこのオプションを選択すると、{{site.data.keyword.bpshort}} サービスで環境に対する変更を追跡することもデプロイすることもできなくなります。それらのアクティブなリソースは、それぞれのサービス・ダッシュボードから個別に管理する必要があります。
  
  表示されたプロンプトに従って、選択内容を確認します。 


## CLI によるリソースの破棄
{: #cli}

{{site.data.keyword.bpshort}} CLI を使用して、一時的な環境を開始したり、破棄したりできます。
{:shortdesc}

1. `destroy` コマンドを実行して、環境とリソースを破棄します。

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
```
  {: codeblock}
  
2. オプション: サービスから構成を削除する場合は、`delete` コマンドを実行します。

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
```
  {: codeblock}


## API によるリソースの破棄
{: #api}

{{site.data.keyword.bpshort}} API を使用して、一時的な環境を開始したり、破棄したりできます。
{:shortdesc}

1. `PUT v1/environments/<environment_ID>/destroy` 呼び出しを実行して、リソースを破棄します。

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. オプション: {{site.data.keyword.bpshort}} サービスから構成を削除する場合は、`DELETE v1/environments/<environment_ID>` 呼び出しを実行します。

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
