---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# クラウド・ネイティブ・プロジェクトの構築
{: #web-mobile}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} [プロジェクト](projects.html)の概念を通じて、クラウド・ネイティブ・アプリを管理できます。プロジェクトを作成するには、[{{site.data.keyword.dev_console}}](devex.html) を使用するか、{{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} CLI のために [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) を使用することができます。{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} は、クラウド・ネイティブ・アプリケーション開発者に必要な最も一般的なサービス機能を、その開発者用に最適化された単一のエクスペリエンスに結合します。

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} を使用して、クラウド・ネイティブ・アプリケーション開発者は、さまざまな[パターン・タイプ](patterns.html)および[スターター](starters.html)からプロジェクトを作成し、{{site.data.keyword.Bluemix_notm}} 向けに最適化された主要サービスを作成してプロジェクトに接続し、機能するコードを SDK と共に迅速にダウンロードすることができます。それらの SDK には機能の資格情報や依存関係が完全に組み込まれているため、数分のうちに実行することが可能です。アプリケーションが実行中で、機能のセットアップおよび構成を完了したら、プロジェクトに戻って、アプリケーション・ユーザーとの関わりをモニターおよび管理することができます。また、{{site.data.keyword.dev_console}} でサービスを構成および管理することも可能です。

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## プロジェクト
{: #projects}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} は、アプリのユーザー・インターフェース、データ、およびサービスを結合して 1 つの完全な*プロジェクト* にします。プロジェクトを作成することによって、アプリのすべての必要なパーツおよび追加された機能が {{site.data.keyword.Bluemix_notm}} サーバー上で保守されます。サービスがプロジェクトに構成されている場合に、アプリ・コードや、必要な資格情報および初期化指定子をダウンロードできます。**「プロジェクト」**を選択すると、すべてのプロジェクトを表示できます。  

**「プロジェクト」**ページで単一プロジェクトを選択すると、それに関する追加情報を表示できます。これにより、プロジェクトの構成済みの使用可能なサービスを示した**「プロジェクト概要」**ページが表示されます。サービスは分離した機能であり、アプリの機能を拡充します。サービスは個別に追加されるため、必要なサービス (プッシュ・サービス、認証サービス、データおよびストレージ、またはその他のサービス) を追加できます。**「プロジェクト概要」**ページでサービスをプロジェクトに追加し、手順に従ってサービスを構成すると、サービスは自動的にアプリに関連付けられます。「プロジェクト概要」ページについて詳しくは、[「プロジェクト概要」ページ](project_overview_page.html)を参照してください。

プロジェクトを作成するには、[パターン](patterns.html)を選択し、その後に[スターター](starters.html)を選択する必要があります。


### プロジェクト概要ページ
{: #project_overview}

**「プロジェクト」**ページでプロジェクトを選択して「プロジェクト概要」ページを開くことにより、単一の {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} プロジェクトを表示および処理することができます。
{: shortdesc}

**「プロジェクト概要」**ページには、選択したプロジェクトで構成されている、または構成が可能な各機能のタイルが表示されています。このタイルには、機能のタイプと、垂直に並んだ 3 つのドットが付いた*「アクション」* ボタンが表示されています。使用可能または構成済みの可能性のある機能の例としては、{{site.data.keyword.mobilepushshort}}、Analytics (分析)、または Data and Storage (データおよびストレージ) があります。互換性のある機能は、プロジェクトのタイプおよびその地域で利用可能な機能によって異なるため、すべての機能がすべてのプロジェクトに関連付けできるわけではありません。 

機能のタイプがまだプロジェクトに関連付けられていない場合は、タイルに**「作成」**ボタンが表示されます。アクション・ボタンのオプションは、サービスのインスタンスを作成すること、または機能がまだ関連付けられていない場合に既存のサービス・インスタンスを追加することです。**「既存の追加 (Add Existing)」**を選択すると、スペース内にあるそのタイプのサービス・インスタンスのリストが表示されます。

機能が既にこのプロジェクトに関連付けられている場合、関連付けられているサービス・インスタンスの名前が、タイル上の機能タイプの後に表示されます。これにより、{{site.data.keyword.dev_console}} 上でどのサービス・インスタンスがこのプロジェクトに関連しているかを見つけるのが容易になります。機能が既にプロジェクトに関連付けられている場合、アクション・ボタンで使用可能なアクションは** 「表示」**と **「削除」**です。サービス・インスタンスを削除しても、このプロジェクトへの関連付けが削除されるだけで、{{site.data.keyword.dev_console}} からサービス・インスタンスが削除されるわけではありません。サービス・インスタンスを削除するには、**「Web およびモバイル (Web and Mobile)」>「サービス」**ページをクリックし、サービス・インスタンスを表示して削除します。

プロジェクトのコードをダウンロードするには、**「コード」**タイルで**「コードの取得 (Get the Code)」**を選択します。コードのダウンロードについて詳しくは、[コードの取得](get_code.html)を参照してください。


### 新しいスターターを使用するためのプロジェクトの更新
{: #update-starter}

1. **「プロジェクト」**または**「プロジェクト概要」**ページから、**「オーバーフロー・メニュー (Overflow Menu)」**アイコンをクリックして**「スターターの更新 (Update Starter)」**を選択します。

2. 新しいスターターを選択して、**「更新」**をクリックします。

3. **「プロジェクト概要 (Project Overview)」**ページで**「コードの取得 (Get the Code)」**をクリックして、言語を選択します。

   代替方法として、**「コード」**ページで以下をクリックすることもできます。


### 新しい言語を生成するためのプロジェクトの更新
{: #update-language}

1. **「プロジェクト」**または**「プロジェクト概要」**ページから、**「オーバーフロー・メニュー (Overflow Menu)」**アイコンをクリックして**「スターターの更新 (Update Starter)」**を選択します。

2. 新しい言語を選択して**「更新」**をクリックします。

3. **「プロジェクト概要 (Project Overview)」**ページで**「コードの取得 (Get the Code)」**をクリックして、言語を選択します。


## パターン・タイプ
{: #patterns}

クラウド・ネイティブ・パターンは、整合性、拡張性、信頼性のあるアプリケーション・トポロジーにするための実証された設計になっています。プロジェクトの作成時に、各種パターン・タイプが提示され、その中から選択することができます。プロジェクトに取り込みたいパターン・タイプと機能を選択するだけです。プロジェクト設定を定義すると、スターター・プロジェクトが生成されます。それを編集、実行、またはデバッグし、ローカルまたは {{site.data.keyword.Bluemix}} にデプロイできます。


### Web アプリ
{: #web}

Web プロジェクトでは、HTML、JavaScript、スタイルシートなどの Web コンテンツを処理する機能を Web サーバーに追加します。

以下の Web スターターが使用可能です。

* ベーシック Web: 静的 `index.html` ファイル、デフォルトおよび空のスタイルシート、JavaScript ファイルを処理します。
* Webpack: ECMAScript 6 (ES6) ソース・ファイルが `src/client` 内にあって、ブラウザーで使用するために縮小と変換が行われるように WebPack でコンパイルされるプロジェクトを作成します。
* Webpack + React: ユーザー・インターフェースをビルドするためのリッチ・フレームワーク。ソース・ファイルは `src/client/app` 内にあり、WebPack でコンパイルされて、パブリック・ディレクトリーで処理されます。


### モバイル・アプリ
{: #mobile}

モバイル・アプリ・パターンを利用して、{{site.data.keyword.mobilepushshort}}、{{site.data.keyword.mobileanalytics_short}}、
{{site.data.keyword.appid_short}}、その他のバックエンド・サービスに直接接続するモバイル・アプリを構築できます。プロジェクトは、sdkGen (BFF など) やマイクロサービスでも追加可能です。

{{site.data.keyword.watson}} Conversation、{{site.data.keyword.visualrecognitionshort}}、{{site.data.keyword.openwhisk_short}}、その他のスターターのリストから選択できます。

モバイル・アプリは、Swift、Android、または Cordova で生成できます。


### Backend for Frontend (BFF)
{: #bff}

Backend for Frontend パターン (通常 BFF と呼ばれる) は、ユーザー・インタラクションの要件に一致する形式でビジネス・データおよびサービスを公開することに重点を置く上で役立ちます。クラウド・ソリューションへのユーザー・ジャーニーを最適化するには、モバイル・アプリケーション用の別のユーザー・ジャーニーと、Web アプリケーション用のよりリッチで詳細なジャーニーが必要な可能性があります。[{{site.data.keyword.conversationfull}} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/watson/developercloud/conversation.html) サービスのような音声制御デバイスの導入により、ユーザーとのインタラクションは音声で制御される可能性があります。このデジタル・チャネルには、これらの音声インテント・ベースのインタラクションを管理するための、非常に異なる BFF が必要になります。

{{site.data.keyword.Bluemix_notm}} では、BFF を定義するための Polyglot プログラミング・アプローチを使用して BFF を作成することができます。Node.js、Swift、または Java を使用すること、および Cloud Foundry、Container サービス、またはサーバーレスのいずれかを使用してクラウド・ネイティブ・パターンでそれらを実行することを IBM は推奨しています。

BFF は、データ・パーシスタンスおよびキャッシング用のサービスとの統合、および {{site.data.keyword.ibmwatson}}、{{site.data.keyword.iot_short_notm}}、{{site.data.keyword.weather_short}} のような高価値サービス、および {{site.data.keyword.sparks}} のようなデータ分析との統合を管理します。

BFF は、最も一般的には REST パターンを使用して API を公開しますが、{{site.data.keyword.messagehub}} を使用してメッセージング・アーキテクチャーから BFF が機能するように設計することができます。

BFF ベーシック・スターターは、Node.js または Swift で使用可能です。


### マイクロサービス
{: #microservice}

マイクロサービス・プロジェクトは、基本ヘルス・エンドポイント、REST API などのバックエンド・マイクロサービスを構築するための基盤を提供します。生成されるプロジェクトには、マイクロサービス自体と、接続されたクラウド・サービスの両方に必要なすべての依存関係が含まれます。

マイクロサービス・ベーシック・スターターは、Java で使用可能です。

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### 言語
{: #languages notoc}

サポートされる言語は、以下のとおりです。

   * [Java ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java には、エンタープライズ規模のアプリケーションを構築するための実証された機能があります。しかし、Java 8 の新機能では、Liberty のような軽量のランタイムと Spring Boot のようなフレームワークと組み合わせて、Java をマイクロサービスの構築にも最適なものにしています。


#### Node.js
{: #node notoc}

Node.js は、イベント・ドリブンの非ブロッキング入出力モデルを使用し、軽量化と効率化を図った JavaScript ランタイムで、Web アプリケーション、Backend for Frontends (BFF) パターン、およびマイクロサービスのスループットと拡張性に優れています。Node.js のパッケージ・エコシステムである npm により、非常に数多くのオープン・ソース・モジュールにアクセス可能になり、アプリケーション開発を加速する幅広い機能が提供されます。


#### Swift
{: #swift notoc}

Swift は、2014 年に Apple によって作成された最新のプログラミング言語です。Objective C の使用に置き換わるものとして設計され、2015 年 12 月にオープン・ソース化されました。今日では、x86、ARM、または Z アーキテクチャーを使用した Linux および macOS のオペレーティング・システムで、iOS、macOS、Web サービス、およびシステム・ソフトウェアを構築するために使用されます。スクリプト言語のように記述しますが、コンパイルされるとオーバーヘッドが少なく C のようなハイパフォーマンスを実現し、クラウド・ランタイムに理想的です。Java で見られる強力で静的なタイプのシステムを使用しながら、JavaScript で見られる機能スタイルおよび非同期ルーチンを使用しています。非常に高性能で、ソースは LLVM コンパイラー・ツールチェーンを使用してネイティブ・コードにコンパイルされ、C で記述された外部システム・ライブラリーを簡単に利用できます。


## スターター
{: #starters}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} で、各パターン・タイプに対応したさまざまなスターターから選択することができます。

スターターは、主要な {{site.data.keyword.Bluemix_notm}} と高価値サービスとの統合を示すことに焦点を当てた、実動準備の完了したスターター・コードになるように最適化されています。各スターターが 1 つのサービスに焦点を合わせていて、コードへのサービス SDK の統合を示します。場合によっては、スターターは、シンプルなユーザー・エクスペリエンスを提供してサービス・データの統合やユーザーとの対話を特長とします。プロジェクト用に Authentication (認証)、Data (データ)、およびその他の機能を構成すると決めた場合、各スターターはそれらの機能を有効にするように構成されます。
