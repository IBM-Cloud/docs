---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# FAQ {: #faq}

この FAQ には、{{site.data.keyword.objectstorageshort}} サービスに関する一般的な質問に対する答えがあります。
{: shortdesc}


## {{site.data.keyword.objectstorageshort}} ではどのようなアカウントおよび支払プランを利用できますか {: #account-payment}

{{site.data.keyword.objectstorageshort}} サービスでは、無料と標準の 2 つのプラン・オプションが提供されています。[料金](https://www.ibm.com/cloud-computing/bluemix/pricing/)は、選択したプランに応じて異なります。

<table>
<caption> 表 1. 無料プランと標準プランの比較</caption>
  <tr>
    <th> 無料プラン</th>
    <th> 標準プラン</th>
  </tr>
  <tr>
    <td> {{site.data.keyword.Bluemix_notm}} 組織に一度に存在できるサービス・インスタンスは 1 つのみです</td>
    <td> サービス・インスタンス数の制限なし</td>
  </tr>
  <tr>
    <td> どなたでも利用可能</td>
    <td> {{site.data.keyword.Bluemix_notm}} 有料アカウントと IBM 社内ユーザーのみ利用可能</td>
  </tr>
  <tr>
    <td> 無料</td>
    <td> 従量制課金またはサブスクリプションの支払プラン</td>
  </tr>
  <tr>
    <td> 最初の 5 GB のストレージ使用制限が含まれます</td>
    <td> ストレージの制限なし</td>
  </tr>
</table>

**注意**: {{site.data.keyword.Bluemix_notm}} トライアル・アカウントで作業するユーザーは無料プランを使用できます。トライアル期間の満了後、関連付けられている {{site.data.keyword.objectstorageshort}} サービス・インスタンスは無効になります。つまり、ストレージ・アカウントにアクセスできなくなります。30 日後、ご使用の {{site.data.keyword.Bluemix_notm}} アカウントはパージされ、すべてのデータが削除されます。データが失われないようにするために、可能な限り早急に[有料 {{site.data.keyword.Bluemix_notm}} アカウント](/docs/admin/account.html)にアップグレードしてください。

## プランの変更はどのようにして行うのですか {: #changeplan}  
ベータ版を使用して (つまり、「無料」プランに基づいて) 作成されたインスタンスは、「標準」プランにアップグレードできます。関連付けられている組織は、{{site.data.keyword.Bluemix_notm}} 有料アカウントでなければなりません。Object Storage インスタンスを持つトライアル・アカウントは、「標準」プランにアップグレードできません。また「標準」プランに基づくインスタンスは、他のプランにダウングレードできません。アップグレードを行うと、ご使用のサービス・インスタンスとお客様データが新しいプランに移行されます。

アップグレードを行うには、以下の手順を実行します。
1.	{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースで、**「プラン」**をクリックします。
2.	新しいプランとして**「標準」**を選択し、**「保存」**をクリックします。

コマンド・ライン・インターフェースを使用して[支払プランを変更する](/docs/pricing/index.html#changing)こともできます。

## {{site.data.keyword.objectstorageshort}} の使用に対する課金および請求の方法はどのようになっていますか {: #charge-bill}

{{site.data.keyword.objectstorageshort}} サービスでは、使用したものに対してのみ課金されます。サービスの使用を開始するための料金やコミットメントはありません。API 要求およびインバウンド・データ・ネットワーク・トラフィックに対する課金はありません。

{{site.data.keyword.objectstorageshort}} は、請求サイクル内のストレージ使用量に基づいて請求されます。これには、{{site.data.keyword.Bluemix_notm}} 組織内に作成したコンテナー内のすべてのオブジェクト・データが含まれます。

パブリック・ネットワーク上でオブジェクト・コンテナーからデータが読み取られるたびに、アウトバウンド・データ転送料金が適用されます。
請求サイクルで消費されたすべての帯域幅が、パブリック・アウトバウンド帯域幅として請求されます。

請求サイクルの終了時に、{{site.data.keyword.Bluemix_notm}} は、該当請求対象期間の使用量に対する料金を自動的に請求します。{{site.data.keyword.Bluemix_notm}} レポート作成を使用して、現在の請求対象期間の料金を確認できます。

## {{site.data.keyword.Bluemix_notm}} 地域とストレージ領域は同じものですか? {: #region}

{{site.data.keyword.objectstorageshort}} サービスは、ダラスとロンドンのストレージ地域をサポートします。これらのストレージ地域は、{{site.data.keyword.objectstorageshort}} サービス・インスタンスが作成される {{site.data.keyword.Bluemix_notm}} 地域 (「米国南部」や「英国」など) から独立しています。米国南部 {{site.data.keyword.Bluemix_notm}} 地域にインスタンスを作成した場合、「ダラス」または「ロンドン」のいずれかのストレージ地域に対してデータの読み取り/書き込みを行えます。
ストレージ地域のデフォルトは、ユーザーの {{site.data.keyword.Bluemix_notm}} 地域に基づいて設定されます。UI のドロップダウン・リストから別の地域を選択することにより、地域を切り替えることができます。
