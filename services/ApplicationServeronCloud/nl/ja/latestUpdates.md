---

copyright:
  years: 2015, 2016
lastupdated: "2017-04-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 最新更新情報
{: #latest_updates}

サービスの最新更新情報のリスト。

## 2017 年 3 月 15 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* 各種サービス・メンテナンスを統合しました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のバイナリーがアップグレードされ、従来の WebSphere Application Server の新しいインスタンスにフィックスパック 8.5.5.11 や 9.0.0.3 がインストールされるようになりました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} では、以下のような[いくつかのセキュリティー脆弱性](https://www-01.ibm.com/support/docview.wss?uid=swg22000587){: new_window}に対処しました。
  * 機密性への影響はなく、保全性に対する高い影響があり、可用性への影響はない、Libraries コンポーネントに関連する未指定の脆弱性。
  * 不明な攻撃ベクトルを使用して、リモート・アタッカーが機密情報を取得することで、機密性に高い影響を与えることにつながる可能性のある、Libraries コンポーネントに関連する未指定の脆弱性。
  * 不明な攻撃ベクトルを使用して、リモート・アタッカーがサービス妨害を引き起こすことによって、可用性を低くする影響を引き起こす可能性のある、Libraries コンポーネントに関連する未指定の脆弱性。
  * SSL/TLS プロトコルの一部として使用される DES/3DES 暗号で発生するエラーに起因し、リモート・アタッカーが機密情報を取得する可能性のある、OpenSSL の脆弱性。
  * ユーザーが Web UI に任意の JavaScript コードを埋め込むことができるため、信頼されたセッション内で資格情報の漏えいにつながる恐れのある、機能を故意に変更できるという脆弱性。
  * ユーザー入力の不適切な検証によって引き起こされる、Apache HTTPD から HTTP 応答の分割アタックに存在する脆弱性。
  * PAC チェックサム処理の失敗により、リモートで認証されたアタッカーがシステム上で高い権限を得る可能性のある、Samba 内の脆弱性。
  * Kerberos 認証使用時にチケット許可チケット (TGT、Ticket Granting Ticket) を他のサービスに転送することにより、リモートで認証されたアタッカーがシステム上で高い権限を得る可能性のある、Samba 内の脆弱性。
  * ndr_pull_dnsp_name() 関数の整数ラップ・フローが原因で生じるヒープ・ベースのバッファー・オーバーフローに対する、Samba 内の脆弱性。


## 2017 年 2 月 10 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* 各種サービス・メンテナンスを統合しました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のバイナリーがアップグレードされ、従来の WebSphere Application Server の新しいインスタンスにフィックスパック 8.5.5.11 や 9.0.0.2 がインストールされるようになりました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のバイナリーがアップグレードされ、WebSphere Application Server Liberty (Core および ND Plans) の新しいインスタンスにフィックスパック 16.0.0.4 がインストールされるようになりました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} では、以下のような[いくつかのセキュリティー脆弱性](https://www-01.ibm.com/support/docview.wss?uid=swg21997657){: new_window}に対処しました。
  * 信頼できないソースからのシリアライズド・オブジェクトを実行し、リソースの消費を引き起こすことによる、サービス妨害の脆弱性。
  * リモート・アタッカーが機密情報を取得する可能性がある、不正な SOAP 要求の使用。


## 2016 年 12 月 16 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* 各種サービス・メンテナンスを統合しました。
* IBM SDK Java Technology Edition では、WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} に影響を与える、以下のような[いくつかのセキュリティー脆弱性](https://www-01.ibm.com/support/docview.wss?uid=swg21995995){: new_window}に対処しました。
  * 機密性、保全性、および可用性に対して高い影響がある、Hotspot コンポーネントに関連する、Oracle Java SE および Java SE Embedded にある未指定の脆弱性。
  * 不明な攻撃ベクトルを使用して、リモート・アタッカーが機密情報を取得する可能性があり、その結果、機密性に高い影響を与える、Networking コンポーネントに関連する Oracle Java SE および Java SE Embedded にある未指定の脆弱性。
  *  ユーザーが Web UI に任意の JavaScript コードを埋め込むことができるため、信頼されたセッション内で資格情報の漏えいにつながる恐れのある、機能を故意に変更できるという、IBM WebSphere Application Server でのクロスサイト・スクリプトの脆弱性。


## 2016 年 11 月 8 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* お客様が WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} VM 用の[パブリック IP](networkEnvironment.html#networkEnvironment) アドレスを要求できる機能を追加しました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} に影響を与える、以下を含む[いくつかのセキュリティー脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window}についての対処を行いました。
  * リモート・アタッカーが信頼できないソースからシリアライズド・オブジェクトを使用して任意の Java コードを実行できる恐れのある、IBM WebSphere Application Server の脆弱性。
  * TS_OBJ_print_bio 機能での領域外メモリー参照に起因する、サービス妨害の脆弱性。特別に作成したタイム・スタンプ・ファイルを使用してリモート・アタッカーがこの脆弱性を悪用し、アプリケーションを異常終了させる恐れがあります。
  * SSL/TLS プロトコルの一部として使用される 64 ビットのブロック暗号の Triple-DES で発生するエラーに起因し、リモート・アタッカーが機密情報を取得できる危険性のある、OpenSSL の潜在的な脆弱性。SSL/TLS サーバーとクライアント間の暗号化されたトラフィックを大量に取り込むことで、中間攻撃を行う能力を持つリモート・アタッカーがこの脆弱性を悪用し、非暗号化テキストのデータを復旧して機密情報を入手できる危険性があります。この脆弱性は SWEET32 Birthday アタックとしても知られています。

  * OpenSSL には、サービス妨害に対する脆弱性があります。再ネゴシエーションを繰り返し要求することで、認証されたリモート・アタッカーが過大な OCSP 状況確認要求を送信し、使用可能なメモリー・リソースをすべて消費してしまう危険性があります。
  * OpenSSL には、MDC2_Update 機能における整数オーバーフローに起因する、サービス妨害に対する脆弱性があります。不明の攻撃ベクトルを使用することで、リモート・アタッカーがこの脆弱性を悪用して領域外メモリーへの書き出しをトリガーし、アプリケーションを異常終了させる恐れがあります。
  * 特定の操作に対する非定時間 codepath のフォローを許可する DSA 実装で発生するエラーに起因し、リモート・アタッカーが機密情報を取得できる危険性のある、OpenSSL の潜在的な脆弱性。アタッカーがキャッシュ・タイミング攻撃を使用してこの脆弱性を悪用し、DSA 秘密鍵を復旧する恐れがあります。
  * OpenSSL には、証明書の構文解析時のメッセージ長チェックの欠落に起因する、サービス妨害に対する脆弱性があります。認証済みのリモート・アタッカーがこの脆弱性を悪用して領域外メモリー参照をトリガーし、サービス妨害を引き起こす可能性があります。


## 2016 年 9 月 19 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のバイナリーがアップグレードされ、WebSphere Application Server Liberty (Core プランおよび ND プラン) の新規インスタンスにはフィックスパック 16.0.0.3 がインストール済みになります。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} に影響を与える、以下を含む[いくつかのセキュリティー脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window}についての対処を行いました。
  * リモート・アタッカーがフィッシング攻撃を実行できる恐れのある、IBM WebSphere Application Server Liberty の脆弱性。
  * OpenID Connect クライアントでのクロスサイト・スクリプティングに対する、IBM WebSphere Application Server Liberty の脆弱性。
  * デフォルトのエラー・ページが存在しない場合に例外が適切に取り扱われないことに起因し、リモート・アタッカーが機密情報を取得できる危険性のある、IBM WebSphere Application Server Liberty における潜在的な脆弱性。
  * Apache Commons FileUpload コンポーネントでのエラーに起因する、サービス妨害に対する Apache Tomcat の脆弱性。
  * 特定の条件で応答が不適切に取り扱われることに起因し、リモート・アタッカーが機密情報を取得できる危険性のある、IBM WebSphere Application Server および IBM WebSphere Application Server Liberty の脆弱性。
  * 機密性への影響はなく、保全性の影響は少なく、可用性のない、ネットワーキング・コンポーネントに関連する未指定の脆弱性。

## 2016 年 8 月 17 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* WebSphere Application Server in Bluemix のバイナリーが 8.5.5.9 から 8.5.5.10 にアップグレードされました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} に影響を与える、以下を含む[いくつかのセキュリティー脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window}についての対処を行いました。
  * WebSphere Application Server および WebSphere Application Server Hypervisor Edition 管理コンソールに影響を与える Apache Struts の脆弱性。
  * SIP サービス使用時の IBM WebSphere Application Server の潜在的なサービス妨害の脆弱性。
  * WebSphere Application Server に使用される IBM HTTP Server に影響を与える可能性のあるいくつかの脆弱性。
  * IBM HTTP Server (IHS) に影響を与える可能性のある CGI アプリケーションを使用した HTTP トラフィックのリダイレクトを許可する脆弱性。この脆弱性は「HTTPOXY」と呼ばれます。
  * IBM WebSphere Application Server 内の情報開示に対する脆弱性。
  * IBM WebSphere Application Server 内でセキュリティー制限を潜在的に迂回する脆弱性 (これは Webcontainer カスタム・プロパティー HttpSessionIdReuse を使用可能にする環境でのみ発生します)。


## 2016 年 6 月 24 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* 新規の *Traditional ND* または *Traditional WebSphere* インスタンスを作成するときに、お客様が V8.5 と V9.0 のどちらかを選択できる機能が追加されました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のバイナリーがアップグレードされ、WebSphere Application Server Liberty (Core プランおよび ND プラン) の新規インスタンスにはフィックスパック 16.0.0.2 がインストール済みになります。16.0.0.2 は、8.5.5.9 の後の次のフィックスパックです。16.0.0.2 以降は、これらのプランでサポートされる、使用許諾のある Liberty オプション・フィーチャーすべてがデフォルトでインストールされます。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} に影響を与える、以下を含む[いくつかのセキュリティー脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window}についての対処を行いました。
  * IBM WebSphere Application Server に影響を与える、Apache Standard Taglibs の XML External Entity Injection (XXE) の脆弱性。
  * WebSphere Application Server Liberty プロファイル API Discovery フィーチャーおよび Swagger の資料を使用する際のセキュリティーが予想より脆弱である可能性。
  * IBM WebSphere Application Server Liberty の管理センター内の情報開示に関する潜在的な脆弱性。
  * IBM WebSphere Application Server で HTTP 応答が分割されるという潜在的な脆弱性。
  * 2016 年 5 月 3 日に OpenSSL プロジェクトによって明らかになった OpenSSL の脆弱性。

## 2016 年 6 月 13 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* WebSphere Application Server in Bluemix RESTful API を使用したアプリケーションまたはスクリプトの作成によりお客様が仮想マシン・インスタンスの構築、プロビジョン、管理、および削除を行える機能が追加されました。
* IP アドレス 10 個およびメモリー 64 GB を超えない決まった数の停止インスタンスを持つことができる機能が追加されました。停止状態の累積インスタンスについては、5 % 減額して課金されるようになりました。

## 2016 年 4 月 26 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* FIPS 140-2 が有効な場合の WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} における[潜在的なセキュリティー脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window}と、Samba における複数の脆弱性 (Badlock を含む) について対処を行いました。
* 各種サービス・メンテナンスを統合しました。

## 2016 年 4 月 15 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新

* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のバイナリーが 8.5.5.8 から 8.5.5.9 にアップグレードされました。
* OpenID Connect (OIDC) クライアントを使用する利用者に影響を及ぼす、IBM {{site.data.keyword.Bluemix_notm}} の Liberty for Java における[クロスサイト・スクリプティング](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window}の脆弱性についての対処を行いました。
* 各種サービス・メンテナンスを統合しました。

## 2016 年 2 月 19 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新
* メモリーを大量に使用するアプリケーションを使用するクライアントのために、より大きな仮想マシンによって環境を「適正化」するオプションを追加しました。クライアントは、所定の WebSphere Application Server コンポーネントまたは単一システムの特定のリソース・サイズを、最大 32 GB RAM 仮想マシンまで選択することができます。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のバイナリーが 8.5.5.7 から 8.5.5.8 にアップグレードされました。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} に影響を及ぼし、一般に [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window} と呼ばれている、IBM SDK Java Technology Edition における複数の脆弱性について、対処を行いました。
* OAuth プロバイダー出力の利用者に影響を及ぼす[クロスサイト・スクリプティング](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window}の脆弱性について、対処を行いました。
* 各種サービス・メンテナンスを統合しました。

## 2015 年 12 月 11 日: WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} の更新
* 正式な製品名が、IBM Application Server on Cloud in {{site.data.keyword.Bluemix_notm}} から IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} に変更されました
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment プランに新機能が追加されました。このプランは、2 つ以上の仮想マシンを使用する WebSphere Application Server Network Deployment セル環境で構成されています。これらの新機能により、ユーザーは高可用性、フェイルオーバー、およびスケーラビリティーに対してクラスター環境をセットアップすることができます。
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Liberty Core プランに新機能が追加されました。このプランには、Liberty プロファイル (サーバー) のグループの管理ドメインであり、2 つ以上の仮想マシンで構成される Liberty 集合の使用が含まれています
* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のバイナリーが 8.5.5.6 から 8.5.5.7 に更新されました
* Java オブジェクトのデシリアライゼーションの処理に関する [Apache Commons Collections の脆弱性](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window}についての対処を行いました。
* [HTTP レスポンス分割攻撃](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}を可能にする可能性のある脆弱性についての対処を行いました。
* 各種サービス・メンテナンスを統合しました。

## 2015 年 10 月 15 日: Application Server on Cloud の更新
* 次の 2 つの新しいプランが追加されました。
  * [WebSphere Application Server Traditional V9 ベータ](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* 各種サービス・メンテナンス
