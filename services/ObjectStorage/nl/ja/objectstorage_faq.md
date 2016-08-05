{:new_window: target="_blank"}

# よくある質問 {: #faq} 

*最終更新日: 2016 年 7 月 18 日*
{: .last-updated}


## 選択したプランによって料金はどのように異なりますか? {: #plan-price}
料金は、選択したプランに応じて異なります。価格設定について詳しくは、[IBM Bluemix 料金シート](https://console.ng.bluemix.net/pricing/){: new_window}を参照するか、詳細な見積もりのための[カリキュレーター](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window}をご利用ください。


## {{site.data.keyword.objectstorageshort}} に使用できるアカウントと支払いプランは何ですか? {: #account-payment}
{{site.data.keyword.objectstorageshort}} サービスには、プランに関する選択肢が複数あります。一般出荷可能日のリリース時点で提供されるのは、「標準」と「無料」の 2 つのプランです。「標準」プランは、{{site.data.keyword.Bluemix_notm}} 有料アカウント (「従量制課金」または「サブスクリプション」のいずれか) および IBM 社内ユーザーにのみ使用可能です。「標準」プランには、アカウントごとに、ストレージ使用に関して最初の 5 GB のクレジット無料枠が含まれています。

引き続きアクティブな「無料」アカウントは「無料」プランを使用できます。このプランでは、1 つの {{site.data.keyword.Bluemix_notm}} 組織に 1 つのみのインスタンスの存在が許可されます。{{site.data.keyword.Bluemix_notm}} 試用の有効期限が切れた後は、関連付けられた {{site.data.keyword.objectstorageshort}} サービス・インスタンスは使用不可になります。つまり、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースでもコマンド・ラインでもストレージ・アカウントにアクセスできなくなります。30 日の猶予期間の後、{{site.data.keyword.Bluemix_notm}} アカウントは消去され、すべてのデータが削除されます。データが失われるのを回避するため、できるだけ早く {{site.data.keyword.Bluemix_notm}} 有料アカウントにアップグレードすることをお勧めします。アカウントをアップグレードするには、ユーザー管理メニューをクリックして**「アカウント」**を選択します。そうすると、アップグレード・プロセスについての指示が表示されます。

## 自分のプランを変更するには? {: #changeplan}  
ベータ版または「無料」プランで作成されたインスタンスは、「標準」プランにアップグレード可能です。関連付けられた組織が {{site.data.keyword.Bluemix_notm}} 有料アカウントである必要があります。{{site.data.keyword.objectstorageshort}} インスタンスを持つ無料アカウントを「標準」プランにアップグレードすることはできません。また、「標準」プランのインスタンスを他のプランにダウングレードすることもできません。アップグレード時に、サービス・インスタンスおよびお客様のデータは新しいプランに移行されます。

プランをアップグレードするには、以下のようにします。
1.	{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースで**「プラン」**をクリックします。
2.	新規プランとして**「標準」**を選択し、**「保存」**をクリックします。

コマンド・ライン・インターフェースを使用して支払いプランを変更することもできます。詳しくは、[プラン変更方法 (How to change your plan) ](../../pricing/index.html#changing)を参照してください。


## {{site.data.keyword.objectstorageshort}} を使用すると課金と請求はどのように行われますか? {: #charge-bill}

{{site.data.keyword.objectstorageshort}} サービスで課金対象になるのは、お客様が使用しているもののみです。最低料金もないしセットアップ料金もかかりません。このサービスをそのまま継続使用しなければならないというコミットメントもありません。API 要求にもインバウンド・データのネットワーク・トラフィックにも料金はかかりません。

{{site.data.keyword.objectstorageshort}} でお客様が使用した分については、請求サイクル内のストレージ使用量に基づいて請求を行います。これには、お客様が自分の {{site.data.keyword.Bluemix_notm}} 組織アカウントの下で作成した、コンテナー内のオブジェクト・データがすべて含まれます。 

ご使用のオブジェクト・コンテナーの中に、パブリック・ネットワークを介してデータが読み出されているものがあれば、常にアウトバウンド・データ転送料金がかかります。パブリック・アウトバウンド帯域幅は、請求サイクルで消費されたすべての帯域幅について請求が行われます。

{{site.data.keyword.objectstorageshort}} 料金の課金要素は以下のとおりです。
* ストレージ使用  - $0.04 (1 カ月 1GB あたり)
* パブリック・アウトバウンド・データ転送  - $0.09 (1 カ月 1GB あたり) 

請求サイクルの終わりに、当該請求期間の使用量に対して、{{site.data.keyword.Bluemix_notm}} から自動的に請求を行います。お客様は、{{site.data.keyword.Bluemix_notm}} のレポート作成機能を使用して、当該請求期間にかかった料金を詳しく調べることができます。

ロンドンおよびダラス向けに発表した標準サービス・プランは同一料金になっています。

## {{site.data.keyword.objectstorageshort}} では、データのレプリケーションはどのように行われているのですか? {: #replication}
{{site.data.keyword.objectstorageshort}} サービスでは、お客様のデータのレプリカを 3 つ保持します。これらのレプリカは、複数のストレージ・ノードに渡って複製されています。詳しくは、[OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window} の資料を参照してください。

