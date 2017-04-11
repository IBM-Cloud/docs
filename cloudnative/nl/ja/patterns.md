---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# パターン・タイプ
{: #patterns}

クラウド・ネイティブ・パターンは、整合性、拡張性、信頼性のあるアプリケーション・トポロジーにするための実証された設計になっています。プロジェクトの作成時に、各種パターン・タイプが提示され、その中から選択することができます。プロジェクトに取り込みたいパターン・タイプと機能を選択するだけです。プロジェクト設定を定義すると、スターター・プロジェクトが生成されます。それを編集、実行、またはデバッグし、ローカルまたは {{site.data.keyword.Bluemix}} にデプロイできます。

## Web アプリ
{: #web}

Web プロジェクトでは、HTML、JavaScript、スタイルシートなどの Web コンテンツを処理する機能を Web サーバーに追加します。

以下の Web スターターが使用可能です。

* ベーシック Web: 静的 `index.html` ファイル、デフォルトおよび空のスタイルシート、JavaScript ファイルを処理します。
* Webpack: ECMAScript 6 (ES6) ソース・ファイルが `src/client` 内にあって、ブラウザーで使用するために縮小と変換が行われるように WebPack でコンパイルされるプロジェクトを作成します。
* Webpack + React: ユーザー・インターフェースをビルドするためのリッチ・フレームワーク。ソース・ファイルは `src/client/app` 内にあり、WebPack でコンパイルされて、パブリック・ディレクトリーで処理されます。


## モバイル・アプリ
{: #mobile}

モバイル・アプリ・パターンを利用して、{{site.data.keyword.mobilepushshort}}、{{site.data.keyword.mobileanalytics_short}}、
{{site.data.keyword.appid_short}}、その他のバックエンド・サービスに直接接続するモバイル・アプリを構築できます。プロジェクトは、sdkGen (BFF など) やマイクロサービスでも追加可能です。

{{site.data.keyword.watson}} Conversation、{{site.data.keyword.visualrecognitionshort}}、{{site.data.keyword.openwhisk_short}}、その他のスターターのリストから選択できます。

モバイル・アプリは、Swift、Android、または Cordova で生成できます。


## Backend for Frontend (BFF)
{: #bff}

Backend for Frontend パターン (通常 BFF と呼ばれる) は、ユーザー・インタラクションの要件に一致する形式でビジネス・データおよびサービスを公開することに重点を置く上で役立ちます。クラウド・ソリューションへのユーザー・ジャーニーを最適化するには、モバイル・アプリケーション用の別のユーザー・ジャーニーと、Web アプリケーション用のよりリッチで詳細なジャーニーが必要な可能性があります。[{{site.data.keyword.conversationfull}} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/conversation.html) サービスのような音声制御デバイスの導入により、ユーザーとのインタラクションは音声で制御される可能性があります。このデジタル・チャネルには、これらの音声インテント・ベースのインタラクションを管理するための、非常に異なる BFF が必要になります。

{{site.data.keyword.Bluemix_notm}} では、BFF を定義するための Polyglot プログラミング・アプローチを使用して BFF を作成することができます。Node.js、Swift、または Java を使用すること、および Cloud Foundry、Container サービス、またはサーバーレスのいずれかを使用してクラウド・ネイティブ・パターンでそれらを実行することを IBM は推奨しています。

BFF は、データ・パーシスタンスおよびキャッシング用のサービスとの統合、および {{site.data.keyword.ibmwatson}}、{{site.data.keyword.iot_short_notm}}、{{site.data.keyword.weather_short}} のような高価値サービス、および {{site.data.keyword.sparks}} のようなデータ分析との統合を管理します。

BFF は、最も一般的には REST パターンを使用して API を公開しますが、{{site.data.keyword.messagehub}} を使用してメッセージング・アーキテクチャーから BFF が機能するように設計することができます。

BFF ベーシック・スターターは、Node.js または Swift で使用可能です。


## マイクロサービス
{: #microservice}

マイクロサービス・プロジェクトは、基本ヘルス・エンドポイント、REST API などのバックエンド・マイクロサービスを構築するための基盤を提供します。生成されるプロジェクトには、マイクロサービス自体と、接続されたクラウド・サービスの両方に必要なすべての依存関係が含まれます。

マイクロサービス・ベーシック・スターターは、Java で使用可能です。

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## 言語
{: #languages notoc}

サポートされる言語は、以下のとおりです。

   * [Java ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java には、エンタープライズ規模のアプリケーションを構築するための実証された機能があります。しかし、Java 8 の新機能では、Liberty のような軽量のランタイムと Spring Boot のようなフレームワークと組み合わせて、Java をマイクロサービスの構築にも最適なものにしています。


### Node.js
{: #node notoc}

Node.js は、イベント・ドリブンの非ブロッキング入出力モデルを使用し、軽量化と効率化を図った JavaScript ランタイムで、Web アプリケーション、Backend for Frontends (BFF) パターン、およびマイクロサービスのスループットと拡張性に優れています。Node.js のパッケージ・エコシステムである npm により、非常に数多くのオープン・ソース・モジュールにアクセス可能になり、アプリケーション開発を加速する幅広い機能が提供されます。


### Swift
{: #swift notoc}

Swift は、2014 年に Apple によって作成された最新のプログラミング言語です。Objective C の使用に置き換わるものとして設計され、2015 年 12 月にオープン・ソース化されました。今日では、x86、ARM、または Z アーキテクチャーを使用した Linux および macOS のオペレーティング・システムで、iOS、macOS、Web サービス、およびシステム・ソフトウェアを構築するために使用されます。スクリプト言語のように記述しますが、コンパイルされるとオーバーヘッドが少なく C のようなハイパフォーマンスを実現し、クラウド・ランタイムに理想的です。Java で見られる強力で静的なタイプのシステムを使用しながら、JavaScript で見られる機能スタイルおよび非同期ルーチンを使用しています。非常に高性能で、ソースは LLVM コンパイラー・ツールチェーンを使用してネイティブ・コードにコンパイルされ、C で記述された外部システム・ライブラリーを簡単に利用できます。
