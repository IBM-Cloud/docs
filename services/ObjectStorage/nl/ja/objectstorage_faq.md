---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# FAQ {: #faq} 

*最終更新日: 2016 年 7 月 18 日*
{: .last-updated}


## 選択するプランによって料金はどのように異なりますか {: #plan-price}
料金は、選択したプランに応じて異なります。料金に関する詳しい情報は、[IBM Bluemix 料金シート](https://console.ng.bluemix.net/pricing/){: new_window}を参照するか、[計算器](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window}を使用して詳細な見積もりを行ってください。


## {{site.data.keyword.objectstorageshort}} ではどのようなアカウントおよび支払プランを利用できますか {: #account-payment}
{{site.data.keyword.objectstorageshort}} サービスには、プランに関して複数のオプションが用意されています。一般出荷版リリースの時点で、「標準」と「無料」の 2 つのプランが提供されています。「標準」プランは、{{site.data.keyword.Bluemix_notm}} 有料アカウント (「従量課金」または「サブスクリプション」向けと、IBM 社内ユーザー向けのみが利用可能です。「標準」プランには、導入時にストレージ使用量に関して、アカウント当たり 5 GB のクレジット無料枠が設けられています。

トライアル・アカウントは引き続きアクティブになっており、「無料」プランをご利用いただけます。無料プランでは、{{site.data.keyword.Bluemix_notm}} 組織内に 1 つのインスタンスのみ存在できます。{{site.data.keyword.Bluemix_notm}} のトライアル期間の満了時以降は、関連付けられている {{site.data.keyword.objectstorageshort}} サービス・インスタンスが無効になります。つまり、ストレージ・アカウントには {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースからも、コマンド・ラインからもアクセスできなくなります。30 日の猶予期間の後、ご使用の {{site.data.keyword.Bluemix_notm}} アカウントはパージされ、すべてのデータが削除されます。データが失われないようにするために、可能な限り早急に {{site.data.keyword.Bluemix_notm}} 有料アカウントにアップグレードすることをお勧めします。アカウントをアップグレードするには、ユーザー管理メニューをクリックして、**「アカウント」**を選択します。これにより、アップグレード・プロセスに関する説明が表示されます。

## プランの変更はどのようにして行うのですか {: #changeplan}  
ベータ版を使用して (つまり、「無料」プランに基づいて) 作成されたインスタンスは、「標準」プランにアップグレードできます。関連付けられている組織は、{{site.data.keyword.Bluemix_notm}} 有料アカウントでなければなりません。{{site.data.keyword.objectstorageshort}} インスタンスを含むトライアル・アカウントは、「標準」プランにアップグレードできません。また「標準」プランに基づくインスタンスは、他のプランにダウングレードできません。アップグレードを行うと、ご使用のサービス・インスタンスとお客様データが新しいプランに移行されます。

プランのアップグレードは、以下の手順で行います。
1.	{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースで、**「プラン」**をクリックします。
2.	新しいプランとして**「標準」**を選択し、**「保存」**をクリックします。

コマンド・ライン・インターフェースを使用して支払プランを変更することもできます。詳細については、[「プラン変更方法」](../../pricing/index.html#changing)を参照してください。


## {{site.data.keyword.objectstorageshort}} の使用に対する課金および請求の方法はどのようになっていますか {: #charge-bill}

{{site.data.keyword.objectstorageshort}} サービスでは、使用したものに対してのみ課金されます。サービスの使用を開始するための最小料金、セットアップ料金、またはコミットメントはありません。API 要求およびインバウンド・データ・ネットワーク・トラフィックに対する課金はありません。

{{site.data.keyword.objectstorageshort}} 使用量は、請求サイクル内のストレージ使用量に基づいて請求されます。これには、{{site.data.keyword.Bluemix_notm}} 組織アカウントの下に作成されたコンテナー内のすべてのオブジェクト・データが含まれます。 

パブリック・ネットワーク上でオブジェクト・コンテナーからデータが読み取られるたびに、アウトバウンド・データ転送料金が適用されます。パブリック・アウトバウンド帯域幅は、請求サイクル内に消費されたすべての帯域幅に対して請求が行われます。

{{site.data.keyword.objectstorageshort}} 価格設定に対するメトリック・コンポーネントは、次のとおりです。
* ストレージ使用量  - 月額、GB 当たり $0.04 (米ドル)
* パブリック・アウトバウンド・データ転送  - 月額、GB 当たり $0.09 (米ドル) 

請求サイクルの終了時に、{{site.data.keyword.Bluemix_notm}} は、現在の請求対象期間の使用量に対する料金を自動的に請求します。{{site.data.keyword.Bluemix_notm}} レポート作成を使用して、現在の請求対象期間の料金を確認できます。

ロンドンとダラスで公表されている標準サービス・プランは、同じ価格設定です。

## {{site.data.keyword.objectstorageshort}} では、データ複製はどのように行われますか {: #replication}
{{site.data.keyword.objectstorageshort}} サービスでは、お客様のデータの 3 つのコピーを維持します。それらが複数のストレージ・ノード全体に複製されます。詳細については、[OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window} 資料を参照してください。

