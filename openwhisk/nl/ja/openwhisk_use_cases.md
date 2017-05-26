---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} の一般的なユース・ケース
{: #openwhisk_common_use_cases}

{{site.data.keyword.openwhisk_short}} が提供する実行モデルは、さまざまなユース・ケースをサポートします。以下のセクションで、典型的な例を示します。
サーバーレス・アーキテクチャーについての詳しい解説、ユース・ケース例、賛否両論の議論、および実装最良事例については、優れた [Mike Roberts article on Martin Fowler's blog](https://martinfowler.com/articles/serverless.html) をお読みください。
{: shortdesc}

## マイクロサービス
{: #openwhisk_common_use_cases_microservices}

マイクロサービス・ベースのソリューションは、その利点にもかかわらず、主流のクラウド・テクノロジーを使用して構築するのは依然として難しく、複雑なツールチェーンの制御やビルド・パイプラインと運用パイプラインの分離が必要とされることも少なくありません。
インフラストラクチャーやオペレーションの複雑さ (耐障害性、ロード・バランシング、自動スケーリング、およびロギング) に対処するために多大な時間を費やしている機動的な小さなチームでは特に、合理化された付加価値のあるコードを、固有の問題を解決するのに最適な、既に知っている好きなプログラミング言語で開発できる方法が望まれています。

{{site.data.keyword.openwhisk_short}} のモジュラー性と本質的な拡張容易性は、小さなロジック断片をアクションに実装するのに理想的です。{{site.data.keyword.openwhisk_short}} アクションは互いに独立しており、{{site.data.keyword.openwhisk_short}} でサポートされている多くの言語を使用して実装可能であり、さまざまなバックエンド・システムにアクセスします。各アクションは独立してデプロイおよび管理でき、他のアクションとは無関係にスケーリングされます。アクション間の接続性は、{{site.data.keyword.openwhisk_short}} によって、ルール、シーケンス、および命名規則の形で提供されています。これは、マイクロサービスをベースにするアプリケーションにとって、よい前兆です。

{{site.data.keyword.openwhisk_short}} が支持されているもう 1 つの重要な根拠は、災害復旧構成でのシステムのコストです。マイクロサービスを PaaS または CaaS で使用する場合と {{site.data.keyword.openwhisk_short}} で使用する場合を比較してみましょう。コンテナーまたは CloudFoundry ランタイムを使用する 10 個のマイクロサービスがあると仮定します。つまり、1 つのアベイラビリティー・ゾーン (AZ) 内に連続的に実行されている支払請求可能なプロセスが 10 個あります。それらのマイクロサービスを 2 つの AZ に渡って実行する場合は 20 個のプロセス、それぞれ 2 つのゾーンがある 2 つの地域に渡って実行する場合は 40 個のプロセスになります。{{site.data.keyword.openwhisk_short}} でマイクロサービスを実行して同じことを行う場合、増分費用をまったく支払う必要なしに、望むだけの数の AZ および地域にわたってマイクロサービスを実行できます。

[Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/) は、{{site.data.keyword.openwhisk_short}} と CloudFoundry を活用して Twelve-Factor スタイルのアプリケーションを作成する、エンタープライズ・グレードのサンプル・アプリケーションです。これは、ERP システムを実行する環境をシミュレートすることを目的とした、スマートなサプライ・チェーン・マネジメント・ソリューションです。アプリケーションを使用してこの ERP システムを強化し、サプライ・チェーン・マネージャーの可視性と俊敏性を向上させます。

## Web アプリ
{: #openwhisk_common_use_cases_webapps}

{{site.data.keyword.openwhisk_short}} は、そのイベント・ドリブン特性により、ユーザー向けアプリケーションにいくつかの利点を提供するのに対して、ユーザーのブラウザーからの HTTP 要求はイベントとしての役目を果たします。{{site.data.keyword.openwhisk_short}} アプリケーションは計算能力を使用し、ユーザー要求にサービス提供しているときにのみ料金が請求されます。アイドル・スタンバイや待機モードのようなものはありません。これにより、ほとんどの時間をユーザー要求の着信を待つだけに費やしている可能性があり、その「スリープ」時間のすべてを請求対象とする従来型のコンテナーや CloudFoundry アプリケーションに比べて、{{site.data.keyword.openwhisk_short}} は大幅にコストが安くなります。 

{{site.data.keyword.openwhisk_short}} を使用して、完全 Web アプリケーションを作成および実行できます。HTML、JavaScript、および CSS などのサイト・リソースのためにホスティングしている静的ファイルとサーバーレス API を結合するということは、完全にサーバーレスな Web アプリケーションを構築できることを意味します。ホストされた {{site.data.keyword.openwhisk_short}} 環境の運用の単純さ (というよりも、Bluemix 上でホストされているために、まったく何も運用する必要がないということ) は、Node.js Express またはその他の従来型のサーバー・ランタイムを立ち上げて運用することに比べると、大きな利点です。

{{site.data.keyword.openwhisk_short}} を使用して Web アプリケーションを作成する方法の例として、以下のものがあります。
- [Web Actions: Serverless Web Apps with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba)
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

IoT は、その性質上、センサーで駆動されることがよくあります。例えば、一定の気温を超えたセンサーに反応することが必要な場合に、{{site.data.keyword.openwhisk_short}} のアクションが起動されることがあります。IoT の対話は通常はステートレスであり、大きなイベント (自然災害、重大な天気現象、交通渋滞など) の場合には負荷が非常に大きくなる可能性があります。これにより、通常の作業負荷は小さいかもしれないけれども、非常に素早く拡大縮小して応答時間を予測可能なものにでき、システムに前もって警告することなく大量のイベントを処理できるようになる、弾力性に富んだシステムが必要になります。これらの要件を満たすシステムを従来型のサーバー・アーキテクチャーを使用して構築するのはとても困難です。従来型のサーバー・アーキテクチャーでは、能力不足でトラフィックのピークを処理できないか、オーバープロビジョンで非常に高価であるかのいずれかになる傾向があるためです。

従来型のサーバー・アーキテクチャーを使用して IoT アプリケーションを実装することは可能ではありますが、多くの場合、さまざまな異なるサービスおよびデータ・ブリッジを組み合わせるには、IoT デバイスからクラウド・ストレージおよび分析プラットフォームまでに及ぶ、ハイパフォーマンスかつ柔軟なパイプラインが必要です。特定のソリューション・アーキテクチャーを実装して微調整するにためにプログラム可能であることが必要であっても、事前構成されているブリッジにはそれが欠けていることがよくあります。多種多様なパイプラインが使用可能であり、一般に、特に IoT では、データ融合まわりの標準化がないことを考えると、パイプラインがカスタム・データ変換 (フォーマット変換、フィルタリング、増強などのため) を必要とするケースは多くあります。{{site.data.keyword.openwhisk_short}} は、そういった変換を「サーバーレス」な方法で実装するのに適した優れたツールであり、弾力性のある完全管理のクラウド・プラットフォームでカスタム・ロジックがホストされます。

{{site.data.keyword.openwhisk_short}}、NodeRed、Cognitive、およびその他のサービスを使用するサンプル IoT アプリケーションが [Serverless transformation of IoT data-in-motion with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt) にあります。

![IoT ソリューション・アーキテクチャー例](images/IoT_solution_architecture_example.png)

## API バックエンド
{: #openwhisk_common_use_cases_iot}

サーバーレス・コンピューティング・プラットフォームは、サーバーなしで API を素早く作成する方法を開発者に提供します。{{site.data.keyword.openwhisk_short}} は、アクション用の REST API の自動生成をサポートします。{{site.data.keyword.openwhisk_short}} の[試験的フィーチャー](./apigateway.md)を使用すると、{{site.data.keyword.openwhisk_short}} API ゲートウェイを介して、アクションの許可 API キーなしで、POST 以外の HTTP メソッドを使用してアクションを起動することができます。この機能は、API を外部利用者に公開するだけでなく、マイクロサービス・アプリケーションの作成にも役立ちます。

また、{{site.data.keyword.openwhisk_short}} アクションは任意の API 管理ツール (例えば、[IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) など) に接続できます。他のユース・ケースと同様に、スケーラビリティーおよび他の QoS (Qualities of Services) に関するすべての考慮事項が当てはまります。 

[Emoting](https://github.com/l2fprod/openwhisk-emoting) は、REST API を介して {{site.data.keyword.openwhisk_short}} アクションを使用するサンプル・アプリです。

[API バックエンドとしてのサーバーレスの使用](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples)に、説明と例があります。

## モバイル・バックエンド
{: #openwhisk_common_use_cases_mobile}

多くのモバイル・アプリケーションでは、サーバー・サイドのロジックが必要です。モバイル開発者のほとんどがサーバー・サイド・ロジックの管理経験に乏しく、デバイス上で実行されるアプリに専念できるようにしたい場合は、{{site.data.keyword.openwhisk_short}} をサーバー・サイドのバックエンドとして使用することが良い解決策になります。また、サーバー・サイド Swift のサポートが組み込まれていることにより、開発者は既に持っている iOS プログラミング・スキルを再利用できます。モバイル・アプリケーションの負荷パターンは予測不能であることが多く、ホストされる {{site.data.keyword.openwhisk_short}} ソリューション (例えば IBM Bluemix など) は、前もってリソースをプロビジョンする必要なく、どのようなワークロード需要にも実質的に対応できるよう拡大縮小できます。

[Skylink](https://github.com/IBM-Bluemix/skylink) は、{{site.data.keyword.openwhisk_short}}、IBM Cloudant、IBM Watson、および Alchemy Vision を活用した、ほぼリアルタイムでのイメージ分析により、無人航空機を iPad を介して IBM Cloud に接続できるようにする、サンプル・アプリケーションです。

[BluePic](https://github.com/IBM-Swift/BluePic) は、写真を撮影して他の BluePic ユーザーと共有できるようにする、写真および画像共有アプリケーションです。 このアプリケーションは、{{site.data.keyword.openwhisk_short}}、Cloudant、イメージ・データ用のオブジェクト・ストレージを使用して、モバイル iOS 10 アプリケーション内で、Swift で作成された Kitura ベースのサーバー・アプリケーションを活用する方法を示します。AlchemyAPI も {{site.data.keyword.openwhisk_short}} シーケンス内で使用され、イメージを分析し、イメージの内容に基づいてテキスト・タグを抽出して、プッシュ通知をユーザーに送信します。

## データ処理
{: #openwhisk_common_use_cases_data}

現在使用可能なデータ量に加えて、アプリケーション開発では、新規データを処理する能力と、将来的にそれに対応できる能力を必要とします。この要件には、構造化されたデータベース・レコードの処理と、構造化されていない文書、イメージ、またはビデオの処理の両方が含まれます。{{site.data.keyword.openwhisk_short}} をシステム提供フィードまたはカスタム・フィードを介して構成して、データの変更に反応するようにしたり、データのフィードが着信したときに自動的にアクションを実行するようにしたりできます。アクションをプログラムして、変更の処理、データ形式の変換、メッセージの送受信、他のアクションの起動、さまざまなデータ・ストア (SQL ベースのリレーショナル・データベース、メモリー内データ・グリッド、NoSQL データベース、ファイル、メッセージング・ブローカー、他のさまざまなシステムなど) の更新を行うようにできます。{{site.data.keyword.openwhisk_short}} のルールおよびシーケンスは、処理パイプラインの変更をプログラミングなしで、単純に構成変更を介して行うことのできる柔軟性を備えています。これにより、{{site.data.keyword.openwhisk_short}} ベースのシステムは、アジャイルで、変更要件に簡単に適応できるようになります。

[OpenChecks](https://github.com/krook/openchecks) プロジェクトは、光学式文字認識を使用して銀行口座への小切手の預金を処理するための {{site.data.keyword.openwhisk_short}} の使用方法を示す、PoC (概念検証) です。これは現在、パブリック Bluemix {{site.data.keyword.openwhisk_short}} サービス上に構築されており、Cloudant および SoftLayer オブジェクト・ストレージに依存します。オンプレミスで、CouchDB および OpenStack Swift を使用できます。その他のストレージ・サービスには、FileNet や Cleversafe があります。Tesseract が OCR ライブラリーを提供します。
## コグニティブ
{: #openwhisk_common_use_cases_cognitive}

コグニティブ・テクノロジーを {{site.data.keyword.openwhisk_short}} と効果的に結合して、強力なアプリケーションを作成することができます。例えば、IBM Alchemy API および Watson Visual Recognition を {{site.data.keyword.openwhisk_short}} と共に使用して、実際に視聴することなくビデオから有用な情報を自動的に抽出することができます。これは、前に説明した[データ処理](#data-processing)ユース・ケースの「コグニティブ」拡張にすぎません。{{site.data.keyword.openwhisk_short}} のもう 1 つの上手な使い方は、コグニティブ・サービスと組み合わせて Bot 関数を実装することです。 

これを行うサンプル・アプリケーション [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) があります。このアプリケーションでは、ユーザーが Dark Vision Web アプリケーションを使用してビデオまたはイメージをアップロードすると、それが Cloudant DB に保管されます。ビデオがアップロードされると、{{site.data.keyword.openwhisk_short}} は Cloudant 変更 (トリガー) を listen することによって、その新規ビデオを検出します。{{site.data.keyword.openwhisk_short}} は、その後、ビデオ抽出アクションをトリガーします。抽出の実行中に、フレーム (イメージ) が生成されて Cloudant に保管されます。次に、それらのフレームは Watson Visual Recognition を使用して処理され、同じ Cloudant DB に結果が保管されます。結果は Dark Vision Web アプリケーションまたは iOS アプリケーションを使用して表示できます。Cloudant に加えて、オブジェクト・ストレージを使用できます。そうする場合、ビデオおよびイメージのメタデータが Cloudant に保管され、メディア・ファイルがオブジェクト・ストレージに保管されます。

Slack チャネルへのトーンおよび POST を分析するための {{site.data.keyword.openwhisk_short}}、IBM Mobile Analytics、Watson を示す[サンプル iOS Swift アプリケーション](https://github.com/gconan/BluemixMobileServicesDemoApp)はここにあります。

## Kafka または Message Hub を使用したイベント処理 

{{site.data.keyword.openwhisk_short}} は、Kafka、IBM Message Hub サービス (Kafka ベース)、およびその他のメッセージング・システムと組み合わせて使用するのに最適です。これらのシステムにはイベント・ドリブン特性があるので、メッセージを処理し、それらのメッセージにビジネス・ロジックを適用するためにイベント・ドリブン・ランタイムが必要です。これはまさに {{site.data.keyword.openwhisk_short}} がそのフィード、トリガー、アクションなどで提供するものです。Kafka と Message Hub は、多くの場合、予測不能な非常に大量のワークロードに使用されるため、これらのメッセージのコンシューマーは瞬時に拡張できる必要があります。この点でも {{site.data.keyword.openwhisk_short}} は最適です。{{site.data.keyword.openwhisk_short}} には、[openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka) パッケージで提供される、組み込みのメッセージ・コンシュームおよびメッセージ・パブリッシュの機能があります。

{{site.data.keyword.openwhisk_short}}、Message Hub、および Kafka を使用して[イベント処理シナリオを実装するサンプル・アプリケーション](https://github.com/IBM/openwhisk-data-processing-message-hub)はここにあります。
