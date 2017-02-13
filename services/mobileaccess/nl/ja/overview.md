---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.amashort}} の概要
{: #mca-overview}


{{site.data.keyword.amafull}} サービスは、{{site.data.keyword.Bluemix_notm}} 上でホストされているクラウド・リソースにアクセスするモバイル・アプリケーションおよび Web アプリケーションに対する認証を提供します。

{{site.data.keyword.amashort}} サービスを使用すると、{{site.data.keyword.Bluemix_notm}} 上でホストされている Node.js アプリケーションおよび Liberty for Java&trade; アプリケーションをさまざまな認証タイプによって保護できます。モバイル・アプリケーションに {{site.data.keyword.amashort}} SDK を装備することにより、{{site.data.keyword.amashort}} サービスによって提供されている認証機能を使用することができます。{{site.data.keyword.amashort}} ダッシュボードを使用して、さまざまな認証タイプを構成し、クライアント・サイド SDK によって収集および送信されるデータを表示します。

**注**: {{site.data.keyword.amashort}} サービスの以前の名称は Advanced Mobile Access でした。

## コンポーネント
{: #components}

* **{{site.data.keyword.amashort}} ダッシュボード**: さまざまな認証タイプを構成します

* **{{site.data.keyword.amashort}} Client SDK**: {{site.data.keyword.amashort}} の機能を使用するようにモバイル・アプリケーションを装備します。サポートされるプラットフォームは、iOS 8+、Android 4+、Cordova、および Web アプリケーションです。

* **{{site.data.keyword.amashort}} Server SDK**: {{site.data.keyword.Bluemix_notm}} 上でホストされているリソースを保護します。現在サポートされているランタイムは、Node.js と Liberty for Java&trade; です。

## 認証タイプ
{: #authtypes}
モバイル・アプリでは以下の認証タイプを使用できます。

* **Facebook**: Facebook を ID プロバイダーとして使用します。ユーザーは、Facebook の資格情報を使用してモバイルまたは Web アプリにログインします。

* **Google**: Google を ID プロバイダーとして使用します。ユーザーは、Google+ の資格情報を使用してモバイルまたは Web アプリにログインします。

* **カスタム**: 独自の ID プロバイダーを作成します。ユーザーが、どのような種類の情報を収集し、検証するかを完全に制御します。

## アーキテクチャーの概要
{: #architecture}

![アーキテクチャー概要ダイアグラム](images/mca-overview.jpg)

* {{site.data.keyword.amashort}} Server SDK を使用してクラウド・リソース (Node.js アプリケーション) を保護します。

* {{site.data.keyword.amashort}} Client SDK によって提供される `Request` クラスを使用して、保護されたクラウド・リソースと通信します。

* {{site.data.keyword.amashort}} Server SDK は、無許可の要求を検出し、HTTP 401 許可チャレンジを返します。

* {{site.data.keyword.amashort}} Client SDK は、HTTP 401 許可チャレンジを検出し、{{site.data.keyword.amashort}} サービスでの認証プロセスを自動的に開始します。

* Facebook 認証、Google 認証、またはカスタム認証が試行されます。

* 認証が正常に行われると、{{site.data.keyword.amashort}} は許可トークンを返します。

* {{site.data.keyword.amashort}} Client SDK はその許可トークンを元の要求に自動的に追加し、要求をクラウド・リソースに再送します。

* {{site.data.keyword.amashort}} Server SDK は、要求からアクセス・トークンを抽出し、{{site.data.keyword.amashort}} サービスを使用してそれを検証します。

* アクセスが付与されます。モバイル・アプリケーションに応答が返されます。

## 要求フロー
{: #flow}
以下の図は、要求が Client SDK からモバイル・バックエンド・アプリケーションおよび ID プロバイダーへどのように流れていくのかを説明したものです。

![要求フロー・ダイアグラム](images/mca-sequence-overview.jpg)

* {{site.data.keyword.amashort}} SDK を使用して、{{site.data.keyword.amashort}} Server SDK によって保護されているバックエンド・リソースへ要求を出します。
* {{site.data.keyword.amashort}} Server SDK は無許可の要求を検出し、HTTP 401 と許可範囲を返します。
* {{site.data.keyword.amashort}} Client SDK は自動的に HTTP 401 を検出し、認証プロセスを開始します。
* {{site.data.keyword.amashort}} Client SDK は {{site.data.keyword.amashort}} サービスに連絡し、認証ヘッダーを送信するよう要求します。
* {{site.data.keyword.amashort}} サービスは、現在構成されている認証タイプに従って認証チャレンジを提供して、最初に認証するようクライアント・アプリに要求します。
* 認証タイプに基づいて {{site.data.keyword.amashort}} Client SDK は以下を行います。
   * Facebook 認証または Google 認証: 認証チャレンジを自動的に処理します。
   * カスタム認証: 開発者によって提供されたロジックに基づいて資格情報を取得します。
* Facebook 認証または Google 認証が構成されている場合、{{site.data.keyword.amashort}} Client SDK は、関連付けられた SDK を使用して Facebook または Google のアクセス・トークンを取得します。これらのトークンは、認証チャレンジ応答として機能します。
* カスタム認証が構成されている場合は、開発者が認証チャレンジ応答を取得し、それを {{site.data.keyword.amashort}} Client SDK に提供する必要があります。
* 認証チャレンジ応答が取得されると、{{site.data.keyword.amashort}} サービスに送信されます。
* Mobile Client Access サービスは、関連する ID プロバイダー (Facebook/Google/カスタム) で認証チャレンジ応答を検証します。
* 検証が正常に行われると、{{site.data.keyword.amashort}} サービスは許可ヘッダーを生成し、そのヘッダーを {{site.data.keyword.amashort}} Client SDK に返します。この許可ヘッダーには、アクセス許可情報を含むアクセス・トークンと、現行のユーザー、デバイス、またはアプリケーションに関する情報を含む ID トークンの、2 つのトークンが含まれています。
* この時点以降、{{site.data.keyword.amashort}} Client SDK で行われたすべての要求は、新しく入手した許可ヘッダーを含むようになります。
* {{site.data.keyword.amashort}} Client SDK は、認証フローをトリガーしたオリジナルの要求を自動的に再送します。
* {{site.data.keyword.amashort}} Server SDK は、要求から許可ヘッダーを抽出し、{{site.data.keyword.amashort}} サービスを使用してそのヘッダーを検証し、バックエンド・リソースへのアクセスを認可します。


## {{site.data.keyword.amashort}} のヘルプおよびサポートの利用
{: #gettinghelp}

{{site.data.keyword.amashort}} を使用しているときに問題や質問がある場合は、情報を検索したり、フォーラムで質問したりして、支援を得ることができます。
また、サポート・チケットを開くことができます。 

フォーラムを使用して質問する場合は、{{site.data.keyword.Bluemix_notm}} の開発チームの目に触れるように、質問にタグを付けます。

* {{site.data.keyword.amashort}} を使用したアプリの開発やデプロイについて技術的な質問がある場合は、[スタック・オーバーフロー![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://stackoverflow.com/search?q={{site.data.keyword.amashort}}+ibm-bluemix "外部リンク・アイコン"){: new_window}に質問を投稿し、質問に「ibm-bluemix」と「{{site.data.keyword.amashort}}」のタグを付けます。
* サービスおよび開始手順に関する質問については、[IBM developerWorks ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=mobile+client+access%20%2B[bluemix] "外部リンク・アイコン"){: new_window}を使用してください。

フォーラム。 

フォーラムの使用について詳しくは、[ヘルプの利用](https://www.{DomainName}/docs/support/index.html#getting-help)を参照してください。

IBM サポート・チケットのオープン、またはサポート・レベルとチケットの重大度については、[サポートへのお問い合わせ](https://www.{DomainName}/docs/support/index.html#contacting-support)を参照してください。

