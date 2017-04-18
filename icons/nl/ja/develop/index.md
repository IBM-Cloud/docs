---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

# アプリの開発 
{: #develop-apps-IDS}

*最終更新日: 2015 年 12 月 7 日*  

統合開発環境 (IDE) またはテキスト・エディターを使用するか、{{site.data.keyword.jazzhub}} を使用することによって、アプリケーションを開発できます。
{: shortdesc}

## Bluemix DevOps Services によるアプリケーションの開発
{: #dev_ops}

{{site.data.keyword.jazzhub_short}} を使用して、クラウド内でアプリケーションの開発、トラッキング、プランを行い、その後、それを {{site.data.keyword.Bluemix_notm}} にデプロイすることができます。ソース・コードからアプリケーション実行までを数分で行うことができます。  

{{site.data.keyword.jazzhub_short}} では、{{site.data.keyword.trackplan}} と {{site.data.keyword.deliverypipeline}} という 2 つのサービスが提供されています。{{site.data.keyword.trackplan}} サービスは、迅速な計画立案に使用されます。{{site.data.keyword.deliverypipeline}} サービスは、ビルドおよびデプロイメントを自動化します。これらのサービスは {{site.data.keyword.Bluemix_notm}} カタログにあります。それらの使用方法について詳しくは、『[Track & Plan 概説](../services/TrackPlan/index.html#gettingstartedtemplate)』および『[Delivery Pipeline 概説](../services/DeliveryPipeline/index.html#getstartwithCD)』を参照してください。 

{{site.data.keyword.jazzhub_short}} では、ソース管理用の Git ホスティングと、コードの編集、管理、デプロイを行うことのできる Web IDE も提供されています。アプリの「概要」ページの右上隅にある**「Git の追加」**リンクをクリックすることによってアプリ内で Git ホスティングを使用可能にします。その後、**「コードの編集」**をクリックして、Web IDE でアプリのコードを編集できます。Web IDE シェルから、コンテンツ・アシストを利用して cf コマンドを実行できます。例えば、次のコマンドを入力することによって、すべての Cloud Foundry コマンドのリストを取得できます。  
```
help cfo
```
{:pre}
