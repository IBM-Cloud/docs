---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

## Web アプリ
{: #openwhisk_common_use_cases_webapps}

{{site.data.keyword.openwhisk_short}} は本来はイベント・ベースのプログラミング向けに設計されたものですが、ユーザーに面するアプリケーションにとっての利点がいくつかあります。例えば、小さな Node.js スタブと組み合わせることで、比較的デバッグが容易なアプリケーションにサービスを提供するために使用できます。さらに、{{site.data.keyword.openwhisk_short}} アプリケーションは、PaaS プラットフォームでサーバー・プロセスを実行するよりもはるかに数値計算が少ないため、かなり安価でもあります。 

OpenWhisk を使用して、完全 Web アプリケーションを作成および実行できます。HTML、JavaScript、および CSS などのサイト・リソースのためにホスティングしている静的ファイルとサーバーレス API を結合するということは、完全にサーバーレスな Web アプリケーションを構築できることを意味します。ホストされた {{site.data.keyword.openwhisk_short}} 環境の運用の単純さ (というよりも、Bluemix 上でホストされているために、まったく何も運用する必要がないということ) は、Node.js Express またはその他の従来型のサーバー・ランタイムを立ち上げて運用することに比べると、大きな利点です。

{{site.data.keyword.openwhisk_short}} CLI *wsk* ツールの "--annotation web-export true" というオプションは、コードを Web ブラウザーからアクセス可能にするもので、役立つものの 1 つです。

{{site.data.keyword.openwhisk_short}} を使用して Web アプリケーションを作成する方法の例として、以下のものがあります。
- [Web Actions: Serverless Web Apps with OpenWhisk](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba)
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with OpenWhisk](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

従来型のサーバー・アーキテクチャーを使用して IoT アプリケーションを実装することは可能ではありますが、多くの場合、さまざまな異なるサービスおよびデータ・ブリッジを組み合わせるには、IoT デバイスからクラウド・ストレージおよび分析プラットフォームまでに及ぶ、ハイパフォーマンスかつ柔軟なパイプラインが必要です。特定のソリューション・アーキテクチャーを実装して微調整するにためにプログラム可能であることが必要であっても、事前構成されているブリッジにはそれが欠けていることがよくあります。多種多様なパイプラインが使用可能であり、一般に、特に IoT では、データ融合まわりの標準化がないことを考えると、パイプラインがカスタム・データ変換 (フォーマット変換、フィルタリング、増強などのため) を必要とするケースは多くあります。{{site.data.keyword.openwhisk_short}} は、そういった変換を「サーバーレス」な方法で実装するのに適した優れたツールであり、弾力性のある完全管理のクラウド・プラットフォームでカスタム・ロジックがホストされます。

IoT は、その性質上、センサーで駆動されることがよくあります。例えば、一定の気温を超えたセンサーに反応することが必要な場合に、{{site.data.keyword.openwhisk_short}} のアクションが起動されることがあります。IoT の対話は通常はステートレスであり、大きなイベント (自然災害、重大な天気現象、交通渋滞など) の場合には負荷が非常に大きくなる可能性があります。これにより、通常の作業負荷は小さいかもしれないけれども、非常に素早く拡大縮小して応答時間を予測可能なものにでき、システムに前もって警告することなく大量のイベントを処理できるようになる、弾力性に富んだシステムが必要になります。これらの要件を満たすシステムを従来型のサーバー・アーキテクチャーを使用して構築するのはとても困難です。従来型のサーバー・アーキテクチャーでは、能力不足でトラフィックのピークを処理できないか、オーバープロビジョンで非常に高価であるかのいずれかになる傾向があるためです。

OpenWhisk、NodeRed、Cognitive、およびその他のサービスを使用するサンプル IoT アプリケーションが [Serverless transformation of IoT data-in-motion with OpenWhisk](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt) にあります。

![IoT ソリューション・アーキテクチャー例](images/IoT_solution_architecture_example.png)

## API バックエンド
{: #openwhisk_common_use_cases_iot}

サーバーレス・コンピューティング・プラットフォームは、サーバーなしで API を素早く作成する方法を開発者に提供します。{{site.data.keyword.openwhisk_short}} は、アクション用の REST API の自動生成をサポートしており、任意の API 管理ツール (例えば、[IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) など) を OpenWhisk が提供する REST API に非常に簡単に接続することができます。他のユース・ケースと同様に、スケーラビリティーおよび他の QoS (Qualities of Services) に関するすべての考慮事項が当てはまります。 

[API バックエンドとしてのサーバーレスの使用](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples)に、説明と例があります。

## モバイル・バックエンド
{: #openwhisk_common_use_cases_mobile}

多くのモバイル・アプリケーションでは、サーバー・サイドのロジックが必要です。サーバー・サイド・ロジックの管理を行うよりも、デバイスまたはブラウザーで実行されるアプリに専念したいモバイル開発者にとっては、{{site.data.keyword.openwhisk_short}} をサーバー・サイドのバックエンドとして使用することは有効な解決策です。さらに、Swift のサポートが組み込まれていることにより、開発者は既に持っている iOS プログラミング・スキルを再利用できます。モバイル・アプリケーションの負荷パターンは予測不能であることが多く、ホストされる {{site.data.keyword.openwhisk_short}} ソリューション (例えば IBM Bluemix など) は、前もってリソースをプロビジョンする必要なく、どのようなワークロード需要にも実質的に対応できるよう拡大縮小できます。

## データ処理
{: #openwhisk_common_use_cases_data}

現在使用可能なデータ量に加えて、アプリケーション開発では、新規データを処理する能力と、将来的にそれに対応できる能力を必要とします。この要件には、構造化されたデータベース・レコードの処理と、構造化されていない文書、イメージ、またはビデオの処理の両方が含まれます。{{site.data.keyword.openwhisk_short}} をシステム提供フィードまたはカスタム・フィードを介して構成して、データの変更に反応するようにしたり、データのフィードが着信したときに自動的にアクションを実行するようにしたりできます。アクションをプログラムして、変更の処理、データ形式の変換、メッセージの送受信、他のアクションの起動、さまざまなデータ・ストア (SQL ベースのリレーショナル・データベース、メモリー内データ・グリッド、NoSQL データベース、ファイル、メッセージング・ブローカー、他のさまざまなシステムなど) の更新を行うようにできます。{{site.data.keyword.openwhisk_short}} のルールおよびシーケンスは、処理パイプラインの変更をプログラミングなしで、単純に構成変更を介して行うことのできる柔軟性を備えています。これにより、{{site.data.keyword.openwhisk_short}} ベースのシステムは、アジャイルで、変更要件に簡単に適応できるようになります。

## コグニティブ
{: #openwhisk_common_use_cases_cognitive}

コグニティブ・テクノロジーを {{site.data.keyword.openwhisk_short}} と効果的に結合して、強力なアプリケーションを作成することができます。例えば、IBM Alchemy API および Watson Visual Recognition を {{site.data.keyword.openwhisk_short}} と共に使用して、実際に視聴することなくビデオから有用な情報を自動的に抽出することができます。 

これを行うサンプル・アプリケーション [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) があります。このアプリケーションでは、ユーザーが Dark Vision Web アプリケーションを使用してビデオまたはイメージをアップロードすると、それが Cloudant DB に保管されます。ビデオがアップロードされると、{{site.data.keyword.openwhisk_short}} は Cloudant 変更 (トリガー) を listen することによって、その新規ビデオを検出します。{{site.data.keyword.openwhisk_short}} は、その後、ビデオ抽出アクションをトリガーします。抽出の実行中に、フレーム (イメージ) が生成されて Cloudant に保管されます。次に、それらのフレームは Watson Visual Recognition を使用して処理され、同じ Cloudant DB に結果が保管されます。結果は Dark Vision Web アプリケーションまたは iOS アプリケーションを使用して表示できます。Cloudant に加えて、オブジェクト・ストレージを使用できます。そうする場合、ビデオおよびイメージのメタデータが Cloudant に保管され、メディア・ファイルがオブジェクト・ストレージに保管されます。
