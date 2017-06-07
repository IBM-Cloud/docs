---



copyright:

  years: 2015，2017

lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cloud Foundry アプリの作成

{{site.data.keyword.Bluemix}} では、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースでアプリを作成することができます。アプリが作成された後、アプリの開発、トラッキング、計画、およびデプロイのために、その UI を引き続き使用するか、cf コマンド・ライン・インターフェースを使用するか、もしくは {{site.data.keyword.jazzhub_title}} を使用するよう選択できます。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} でアプリを作成する際は、スターターから始めます。*スターター* は、特定のビルドパックで構成された事前定義サービスおよびアプリケーション・コードを含むテンプレートです。スターターには、ボイラープレートとランタイムの 2 つのタイプがあります。

*ボイラープレート*は、アプリケーションとその関連するランタイム環境、および特定のドメイン用の事前定義サービスのためのコンテナーです。例えば、Mobile Cloud ボイラープレートには Node.js ランタイムのほか、Mobile Data サービス、Mobile Application Security サービス、および Push サービスが含まれています。また、これらのサービスにアクセスするモバイル・アプリの開発を始めるための SDK とサンプル・アプリケーションも含まれています。

*ランタイム* は、アプリケーションの実行に使用するリソースのセットです。{{site.data.keyword.Bluemix_notm}} は、さまざまなタイプのアプリケーションのコンテナーとして、ランタイム環境を提供します。
ランタイム環境はビルドパックとして {{site.data.keyword.Bluemix_notm}} に統合され、使用できるよう自動的に構成されます。保守の必要性はほとんどないか、まったくありません。

アプリケーションの作成を始めるには、以下の手順に従ってください。
  1. {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースのダッシュボードに移動します。
  2. **「アプリの作成」**をクリックします。
  3. **「Web」**をクリックし、指示に従ってスターターを選択し、名前を指定し、コーディング方法を選択します。
  4. 指示を実行し終えたら、**「アプリの概要の表示」**をクリックします。ダッシュボードにアプリの概要が表示されます。
  5. {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースでは、アプリの「概要」で**「サービスまたは API の追加」**をクリックすることによって、サービスをアプリに追加できます。カタログを表示してサービスを選択するか、あるいは、カタログを最後までスクロールして**「{{site.data.keyword.Bluemix_notm}} Experimental Services」**をクリックし、試験的サービスを表示します。あるいは cf コマンド・ライン・インターフェースを使用することもできます。『アプリの処理のオプション』を参照してください。
  6. アプリの「概要」ページで、「継続的デリバリー」カードまでスクロールし、**「有効化」**をクリックします。アプリのソースは、Bluemix 上でホストされる「Git Repos and Issue Tracking」内のリポジトリーに保存されます。そのリポジトリーおよび配信のパイプラインを使用してアプリを開発してデプロイする、オープン・ツールチェーンも作成されます。Continuous Delivery サービスについて詳しくは、『<a href="https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started">Getting started with Continuous Delivery</a>』を参照してください。

**注:** アプリにバインドしたサービスが異常終了すると、アプリは実行を停止するか、エラーを起こす可能性があります。{{site.data.keyword.Bluemix_notm}} では、それらの問題から復旧するためにアプリを自動的に再始動することはありません。
障害、例外、および接続障害を発見して復旧するようアプリをコーディングすることを検討してください。詳しくは、トラブルシューティングのトピック『アプリが自動的に再始動されない』を参照してください。

## アプリの処理のオプション

アプリの作成後、引き続きサービスをアプリに追加し、アプリのビルドとデプロイを行うには、以下のようにいくつかのオプションがあります。

<dl><dt>cf コマンド・ライン・インターフェース</dt>
<dd>cf コマンド・ライン・インターフェースを使用して、アプリケーションの更新、サービス・インスタンスの作成、またはアプリケーションへのサービスのバインドを行います。また、cloud-cli コマンド・ライン・インターフェースを使用して、サービス・オファリングの作成、更新、および削除を行うこともできます。</dd>
<dt>{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェース</dt>
<dd>{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用して、アプリケーションをビルドします。これには、ビジネス上の問題を解決するためにサービスおよびランタイムを選出して組み合わせる作業も含まれます。</dd>
<dt>{{site.data.keyword.contdelivery_full}}</dt>
<dd>{{site.data.keyword.contdelivery_short}} を使用して、ビルド、単体テスト、デプロイメントなどを自動化します。機能豊富な Web ベース IDE により、コードの編集およびプッシュを行います。開発、デプロイメント、および運用の作業をサポートするツール統合を実現するツールチェーンを作成します。Continuous Delivery サービスには、Delivery Pipeline、Eclipse Orion Web IDE、および Git Repos and Issue Tracking が含まれています。詳しくは、『<a href="https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started">Getting started with Continuous Delivery</a>』を参照してください。
</dd>
</dl>

## ヒント

Web アプリのデプロイ時には、以下のヒントを使用してください。

<dl><dt>永続性</dt>
<dd>アプリケーション用にローカル・ストレージを指定しないでください。1 つのインスタンスのみが実行中である場合でも、アプリケーションの各インスタンスはいつでも再始動されたり別の仮想マシンに移動されたりする可能性があります (通常、これはロード・バランシングのために行われます)。ローカル・ストレージに保管されたデータは、アプリケーションが移動または削除されると消去されます。永続的な保管のためには、{{site.data.keyword.Bluemix_notm}} データ・ストア・サービスのいずれかを使用してください。</dd>
<dt>リソースの制限</dt>
<dd>トライアル・アカウントで使用可能なリソースの数量に関する制限を把握しておいてください。制限は以下のとおりです。
<table style="width:100%">
<caption>表 1. トライアル・アカウントの {{site.data.keyword.Bluemix_notm}} リソース制限</caption>
  <th>リソース・タイプ</th>	<th>数量の制限</th>
<tr><td>すべてのアプリでの使用サービス数</td> <td>10</td>
<tr><td>すべてのアプリでの使用メモリー</td> <td>	2 G</td>
<tr><td>経路の数</td> <td>500</td>
</table>
</dd></dl>
