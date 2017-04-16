---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 最新更新情報
{: #latest_updates}
最終更新日: 2016 年 8 月 17 日
{: .last-updated}

サービスの最新更新情報のリスト。

## 2016 年 8 月 17 日: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} の更新

* WebSphere Application Server for Bluemix のバイナリーが 8.5.5.9 から 8.5.5.10 にアップグレードされました。
* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} に影響を与える、以下を含む[いくつかのセキュリティー脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window}についての対処を行いました。
  * WebSphere Application Server および WebSphere Application Server Hypervisor Edition 管理コンソールに影響を与える Apache Struts の脆弱性。
  * SIP サービス使用時の IBM WebSphere Application Server の潜在的なサービス妨害の脆弱性。
  * WebSphere Application Server に使用される IBM HTTP Server に影響を与える可能性のあるいくつかの脆弱性。
  * IBM HTTP Server (IHS) に影響を与える可能性のある CGI アプリケーションを使用した HTTP トラフィックのリダイレクトを許可する脆弱性。この脆弱性は「HTTPOXY」と呼ばれます。
  * IBM WebSphere Application Server 内の情報開示に対する脆弱性。
  * IBM WebSphere Application Server 内でセキュリティー制限を潜在的に迂回する脆弱性 (これは Webcontainer カスタム・プロパティー HttpSessionIdReuse を使用可能にする環境でのみ発生します)。


## 2016 年 6 月 24 日: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} の更新

* 新規の *Traditional ND* または *Traditional WebSphere* インスタンスを作成するときに、お客様が V8.5 と V9.0 のどちらかを選択できる機能が追加されました。
* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} のバイナリーがアップグレードされ、WebSphere Application Server Liberty (Core プランおよび ND プラン) の新規インスタンスにはフィックスパック 16.0.0.2 がインストール済みになります。16.0.0.2 は、8.5.5.9 の後の次のフィックスパックです。16.0.0.2 以降は、これらのプランでサポートされる、使用許諾のある Liberty オプション・フィーチャーすべてがデフォルトでインストールされます。
* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} に影響を与える、以下を含む[いくつかのセキュリティー脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window}についての対処を行いました。
  * IBM WebSphere Application Server に影響を与える、Apache Standard Taglibs の XML External Entity Injection (XXE) の脆弱性。
  * WebSphere Application Server Liberty プロファイル API Discovery フィーチャーおよび Swagger の資料を使用する際のセキュリティーが予想より脆弱である可能性。
  * IBM WebSphere Application Server Liberty の管理センター内の情報開示に関する潜在的な脆弱性。
  * IBM WebSphere Application Server で HTTP 応答が分割されるという潜在的な脆弱性。
  * 2016 年 5 月 3 日に OpenSSL プロジェクトによって明らかになった OpenSSL の脆弱性。

## 2016 年 6 月 13 日: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} の更新

* WebSphere Application Server for Bluemix RESTful API を使用したアプリケーションまたはスクリプトの作成によりお客様が仮想マシン・インスタンスの構築、プロビジョン、管理、および削除を行える機能が追加されました。
* IP アドレス 10 個およびメモリー 64 GB を超えない決まった数の停止インスタンスを持つことができる機能が追加されました。停止状態の累積インスタンスについては、5 % 減額して課金されるようになりました。

## 2016 年 4 月 26 日: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} の更新

* FIPS 140-2 が有効な場合の WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} における[潜在的なセキュリティー脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window}と、Samba における複数の脆弱性 (Badlock を含む) について対処を行いました。
* 各種サービス・メンテナンスを統合しました。

## 2016 年 4 月 15 日: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} の更新

* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} のバイナリーが 8.5.5.8 から 8.5.5.9 にアップグレードされました。
* OpenID Connect (OIDC) クライアントを使用する利用者に影響を及ぼす、IBM {{site.data.keyword.Bluemix_notm}} の Liberty for Java における[クロスサイト・スクリプティング](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window}の脆弱性についての対処を行いました。
* 各種サービス・メンテナンスを統合しました。

## 2016 年 2 月 19 日: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} の更新
* メモリーを大量に使用するアプリケーションを使用するクライアントのために、より大きな仮想マシンによって環境を「適正化」するオプションを追加しました。クライアントは、所定の WebSphere Application Server コンポーネントまたは単一システムの特定のリソース・サイズを、最大 32 GB RAM 仮想マシンまで選択することができます。
* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} のバイナリーが 8.5.5.7 から 8.5.5.8 にアップグレードされました。
* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} に影響を及ぼし、一般に [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window} と呼ばれている、IBM SDK Java Technology Edition における複数の脆弱性について、対処を行いました。
* OAuth プロバイダー出力の利用者に影響を及ぼす[クロスサイト・スクリプティング](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window}の脆弱性について、対処を行いました。
* 各種サービス・メンテナンスを統合しました。

## 2015 年 12 月 11 日: WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} の更新
* 正式な製品名が、IBM Application Server on Cloud for {{site.data.keyword.Bluemix_notm}} から IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} に変更されました
* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment プランに新機能が追加されました。このプランは、2 つ以上の仮想マシンを使用する WebSphere Application Server Network Deployment セル環境で構成されています。これらの新機能により、ユーザーは高可用性、フェイルオーバー、およびスケーラビリティーに対してクラスター環境をセットアップすることができます。
* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core プランに新機能が追加されました。このプランには、Liberty プロファイル (サーバー) のグループの管理ドメインであり、2 つ以上の仮想マシンで構成される Liberty 集合の使用が含まれています
* WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} のバイナリーが 8.5.5.6 から 8.5.5.7 に更新されました
* Java オブジェクトのデシリアライゼーションの処理に関する [Apache Commons Collections の脆弱性](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window}についての対処を行いました。
* [HTTP レスポンス分割攻撃](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}を可能にする可能性のある脆弱性についての対処を行いました。
* 各種サービス・メンテナンスを統合しました。

## 2015 年 10 月 15 日: Application Server on Cloud の更新
* 次の 2 つの新しいプランが追加されました。
  * [WebSphere Application Server Traditional V9 ベータ](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* 各種サービス・メンテナンス
