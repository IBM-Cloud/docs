---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Dedicated
{: #dedicated}

*最終更新日: 2016 年 5 月 16 日*


{{site.data.keyword.Bluemix}} は、アプリケーションをビルド、実行、および管理するためのクラウド・ベースのオープン標準プラットフォームです。{{site.data.keyword.Bluemix_notm}} Dedicated を使用すれば、{{site.data.keyword.Bluemix_notm}}&mdash; Public 環境とお客様のネットワークの両方にセキュアに接続されたお客様の専用 SoftLayer 環境で、{{site.data.keyword.Bluemix_notm}} が持つ能力と簡潔さが得られます。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} のすべての専用デプロイメントには、追加コストなしで次の利点およびフィーチャーが含まれています。VPN、プライベート仮想ローカル・エリア・ネットワーク (VLAN)、ファイアウォール、ご使用の LDAP との接続性、既存のオンプレミス・データベースおよびアプリを利用する機能、 週 7 日 24 時間体制のオンサイト・セキュリティー、専用ハードウェア、および標準サポート。

{{site.data.keyword.Bluemix_notm}} (Dedicated) には、付属しているすべての {{site.data.keyword.Bluemix_notm}} ランタイムおよび 64 GB の計算リソース・メモリーが備わっています。

さらに、{{site.data.keyword.Bluemix_notm}} Dedicated のサービスとして使用可能な一連のサービスがあります。以下の表で、組み込みのもの、オプションで購入可能なものを確認してください。

*表 1. Dedicated のサービス*

| **タイプ **        | **名前**            | **説明** |      
|-----------------|-------------------|-------------------|
|組み込み | {{site.data.keyword.Bluemix_notm}} ランタイム | ランタイムはアプリを素早く立ち上げて実行するために使用します。マシンとオペレーティング・システムのセットアップと管理は不要です。すべての {{site.data.keyword.Bluemix_notm}} ランタイムが、{{site.data.keyword.Bluemix_notm}} Dedicated インスタンスで使用可能です。|
|組み込み | {{site.data.keyword.autoscaling}} | ポリシーに基づいて、アプリケーションの計算能力を動的に増減します。このサービスを使用することで、{{site.data.keyword.Bluemix_notm}} Dedicated 環境で使用量が無制限になります。 |
|オプション | {{site.data.keyword.apiconnect_short}} | {{site.data.keyword.apiconnect_long}} は、{{site.data.keyword.APIM}} と IBM StrongLoop を統合して単一オファリングにします。そのオファリングは、API およびマイクロサービスの作成、実行、管理、および強制を行うための包括的ソリューションを提供します。 |
|オプション | {{site.data.keyword.APIM}} | {{site.data.keyword.APIMfull}} サービスを使用して、API を構成、管理、およびソーシャル化します。API は、プロキシー URL を使用するか、HTTP データ・ソースからデータをアセンブルすることにより、リソースと一緒にインポートできます。{{site.data.keyword.APIM}} サービスを使用する利点は、API の使用方法を管理できることです。 |
|オプション | {{site.data.keyword.cloudant}} | {{site.data.keyword.cloudant}} は、常に稼働している完全管理 NoSQL JSON データ層へのアクセスを提供します。このサービスは CouchDB と互換性があり、モバイル・アプリケーション・モデルおよび Web アプリケーション・モデル用の、簡単に使用できる HTTP インターフェースでアクセスできます。 |
|オプション | {{site.data.keyword.dashdbshort}} | dashDB を使用して、地理空間情報などの特殊タイプを含む、リレーショナル・データを保管します。次に、そのデータを SQL、または予測分析とデータ・マイニング、R による分析、および Geospatial Analytics などの拡張組み込み分析を使用して分析します。 |
|オプション | {{site.data.keyword.datacshort}} | このサービスは、アプリで分散キャッシュ・シナリオをサポートするメモリー内データ・グリッドを提供します。50 GB のメモリー内キャッシュが含まれます。 |
|オプション | {{site.data.keyword.mobilepushshort}} | {{site.data.keyword.mobilepushshort}} は、iOS および Android デバイスに通知を送信するために使用できるサービスです。通知は、すべてのアプリケーション・ユーザーを宛先にするか、または、タグを使用して、特定のユーザーおよびデバイスのセットを宛先にすることができます。デバイス、タグ、およびサブスクリプションを管理できます。SDK (Software Development Kit) および Representational State Transfer (REST) アプリケーション・プログラム・インターフェース (API) を使用して、クライアント・アプリケーションをさらに開発することもできます。 |
|オプション | {{site.data.keyword.messagehub}} | {{site.data.keyword.messagehub}} は、オンプレミスとオフプレミスのテクノロジーを結合する、スケーラブルで高スループットの分散型のメッセージ・バスです。{{site.data.keyword.messagehub}} は Apache Kafka (高速でスケーラブルかつ永続的なリアルタイム・メッセージング・エンジン) をベースにしています。 |
|オプション | {{site.data.keyword.SecureGateway}} | {{site.data.keyword.SecureGateway}} サービスは、{{site.data.keyword.Bluemix_notm}} アプリケーションをオンプレミスまたはクラウド内のリモート・ロケーションに接続するための安全な方法を提供します。  |
|オプション | {{site.data.keyword.sescashort}} | 冗長性を高めるために、{{site.data.keyword.sescashort}} は、キャッシュに保管されたセッションのレプリカを提供します。これにより、ブラウンアウトまたは障害が発生した場合、クライアント・アプリケーションはキャッシュ内のセッションへのアクセスを維持できます。サービスでは、Web アプリケーションとモバイル・アプリケーションのセッション・キャッシュ・シナリオがサポートされます。 |
|オプション | {{site.data.keyword.iot_full}} | このサービスにより、アプリは、接続されたデバイス、センサー、およびゲートウェイが収集したデータと通信して、それらのデータを取り込むことができます。基本オファリングでは、100,000 個の同時接続されたデバイスまたはアプリケーションと 1.6 TB のデータ交換の容量を備えた専用環境内で {{site.data.keyword.iot_full}} の専用バージョンを実行することができます。 |

リソースおよびサービスの容量を拡大および拡張するために購入できる、オプションのコンポーネントが用意されています。販売チームに連絡して、これらのコンポーネントを購入できます。営業担当員への連絡について詳しくは、[「お問い合わせ」](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs)にアクセスしてください。サービスのプランを増やすには、カタログのサービス・タイルからプランを選択します。

*表 2. 購入用のオプション・コンポーネント*

| **名前**            | **説明** |      
|-------------------|-------------------|
|専用ランタイムの 16 GB の容量増加  | ランタイム容量を 16 GB 分追加する、ランタイム環境の拡張。 |
|Dedicated {{site.data.keyword.cloudant}} の 1.6 TB の容量増加 | 設計容量が 1.6 テラバイトの専用環境内での {{site.data.keyword.cloudantfull}} の専用バージョンの実行が組み込まれます。  |
|Dedicated {{site.data.keyword.datacshort}} および {{site.data.keyword.sescashort}} の 50 GB の容量増加 | 最大 50 GB の累積容量まで「{{site.data.keyword.datacshort}}」および「{{site.data.keyword.sescashort}}」のインスタンスをデプロイして実行することができる環境。 |
|Dedicated Direct Link 1 Gbps 容量 | 最大 1 Gbps のデータ転送用に設計され、適切に配置された SoftLayer ネットワーク・ポイントに直接接続される、専用ネットワーク・リンク。 |
|Dedicated Direct Link 10 Gbps 容量 | 最大 10 Gbps のデータ転送用に設計され、適切に配置された SoftLayer ネットワーク・ポイントに直接接続される、専用ネットワーク・リンク。 |
|Dedicated {{site.data.keyword.dashdbshort}} Enterprise 64.1 | 64 GB RAM、16 vCPU 搭載の専用サーバー上のサービス・インスタンスごとに 1 つのデータベース。標準圧縮に基づき、最大 1 TB のプリロード・データに対して推奨。  |
|Dedicated {{site.data.keyword.dashdbshort}} Enterprise 256.4 | 256 GB RAM、32 コアを搭載の専用ベアメタル・サーバー上のサービス・インスタンスごとに 1 つのデータベース。標準圧縮に基づき、最大 4 TB のプリロード・データに対して推奨。 |
|Dedicated {{site.data.keyword.dashdbshort}} Enterprise 256.12  | 256 GB RAM、32 コアを搭載の専用ベアメタル・サーバー上のサービス・インスタンスごとに 1 つのデータベース。標準圧縮に基づき、最大 12 TB のプリロード・データに対して推奨。これは、データ量が比較的多く、照会をメモリー内の速度で実行する必要のない環境に適したストレージ高密度プランです。 |
|Dedicated {{site.data.keyword.APIM}} 1000 API 呼び出し容量  | 1 秒当たり 1,000 回の API 呼び出し容量を持つ専用環境内で {{site.data.keyword.APIM}} の専用バージョンを実行できる環境。 |
|Dedicated {{site.data.keyword.APIM}} 500 回の API 呼び出しの容量増加  | 1 秒当たり 500 回の API 呼び出し容量を持つ専用環境内で IBM API Management for Bluemix の専用バージョンを実行できる環境。  |
|{{site.data.keyword.Bluemix_notm}} Dedicated コミュニティー・サービス  | コミュニティー・サービスごとに、最大合計 50 インスタンスまでコミュニティー・サービスをデプロイして実行できる環境。  |
|IBM Bluemix Dedicated Hardware Firewall – High Availability | 専用環境内の同じ VLAN 上の単一、複数、またはすべてのサーバーを保護するように構成された、冗長 1 Gbps ハードウェア・ファイアウォール。 |
|高可用性用に構成された専用 1 Gbps Vyatta VPN  | 専用環境での使用のために高可用性を実現するように構成された 1 Gbps Vyatta VPN。 |
|IBM {{site.data.keyword.Bluemix_notm}} Dedicated {{site.data.keyword.mobilepushshort}} | 1 秒当たり 300 個の要求を受け入れる能力を備えた、{{site.data.keyword.mobilepushshort}} インスタンスのデプロイメントおよび実行を許可する環境。 |
|{{site.data.keyword.iot_short}} Dedicated の増分式の拡張 | 環境の拡張。拡張される環境では、100,000 個の同時接続されたデバイスまたはアプリケーションと 0.5 TB のデータ交換の容量を備えた専用環境内で {{site.data.keyword.iot_short}} の専用バージョンを実行できます。 |


**注**: {{site.data.keyword.Bluemix_notm}} Dedicated のコンポーネントは、構成された特定の容量 (ギガバイト数や、1 秒当たりのトランザクション数など) で示される場合があります。どんな構成でも、クラウド・サービスで実際に使用される容量は、さまざまな要因によって異なるため、実際に使用される容量は、構成された容量より増減する可能性があります。


### シンジケートされたカタログ
{: #catalogdedicated}

{{site.data.keyword.Bluemix_notm}} Dedicated には、ユーザーが専用に利用可能なローカル・サービスを表示したプライベート・カタログが含まれています。また、{{site.data.keyword.Bluemix_notm}} Public から使用できる追加サービスも含まれています。

シンジケートされたカタログは、パブリック・サービスとプライベート・サービスから成るハイブリッド・アプリケーションを作成する機能を提供します。データ・プライバシーとセキュリティー基準に基づいて、ビジネスの要件に合致したパブリック・サービスを決定できます。専用環境のサービスのプライベート・インスタンスである場合、カタログ内のサービス・タイルに「Dedicated」タグが付いています。同様に、カスタム・サービスの場合は、サービス・タイルと共に「Custom」が表示されます。

*表 3. {{site.data.keyword.Bluemix_notm}} Public (地域別)* からのシンジケーションに利用可能なサービス

|サービス	|米国南部地域で利用可能	|ヨーロッパ英国地域で利用可能 |オーストラリア、シドニー地域で利用可能|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.alchemyapishort}} 		|はい	   	|はい  		|はい|
|{{site.data.keyword.alertnotificationshort}}		|はい		|はい			|はい		|
|{{site.data.keyword.appseccloudshort}}		|はい		|はい		|はい |
|{{site.data.keyword.hadoopst}}			|はい		|いいえ		|いいえ |
|{{site.data.keyword.APIM}}			|はい		|はい		|はい |
|{{site.data.keyword.rules_short}}		|はい		|はい		|はい |
|{{site.data.keyword.cloudant}}			|はい		|はい		|はい |
|{{site.data.keyword.conceptexpansionshort}}	|はい		|はい		|はい|
|{{site.data.keyword.conceptinsightsshort}}	|はい		|はい		|はい |
|{{site.data.keyword.dashdbshort}}		|はい		|はい		|はい |
|{{site.data.keyword.dataworks_short}}		|はい		|はい		|いいえ|
|{{site.data.keyword.DB2OnCloud_short}}		|はい		|はい		|はい |
|{{site.data.keyword.dialogshort}}		|はい		|はい		|はい|
|{{site.data.keyword.documentconversionshort}}	|はい		|はい		|はい|
|{{site.data.keyword.game}}			|いいえ		|いいえ		|はい |
|{{site.data.keyword.geospatialshort_Geospatial}}	|はい	|はい		|はい |
|{{site.data.keyword.GlobalizationPipeline_short}}	|はい		| はい		| はい |
|{{site.data.keyword.identitymixershort}}		|はい		|はい		|はい|
|{{site.data.keyword.twittershort}}		|はい		|はい		|はい|
|{{site.data.keyword.weather_short}}		|はい		|はい		|はい|
|{{site.data.keyword.languagetranslationshort}}	|はい		|はい		|はい |
|{{site.data.keyword.eventhubshort}}		|はい		|いいえ		|いいえ|
|{{site.data.keyword.messagehub}}		|はい		|はい		|いいえ|
|{{site.data.keyword.macm_short}}		|はい		|はい		|はい|
|{{site.data.keyword.manda}}			|はい		|はい		|はい |
|{{site.data.keyword.amashort}}			|はい		|はい		|はい |
|{{site.data.keyword.mqa}}			|はい		|はい		|はい |
|{{site.data.keyword.mql}}			|はい		|はい		|はい |
|{{site.data.keyword.nlclassifierlshort}} 	|はい 		|はい 		|はい|
|{{site.data.keyword.personalityinsightsshort}}	|はい		|はい		|はい|
|{{site.data.keyword.pm_short}}			|はい		|はい		|いいえ |
|{{site.data.keyword.presenceinsightsshort}}	|はい		|はい		|はい|
|{{site.data.keyword.mobilepush}}		|はい		|はい		|はい |
|{{site.data.keyword.questionandanswershort}}	|はい		|はい		|はい|
|{{site.data.keyword.relationshipextractionshort}}	|はい	|はい		|はい|
|{{site.data.keyword.retrieveandrankshort}}	|はい 		|はい 		|はい|
|{{site.data.keyword.runbook_short}}		|はい		|はい		|はい|
|{{site.data.keyword.SecureGateway}}		|はい		|はい		|はい |
|{{site.data.keyword.ssofull}}			|はい		|いいえ		|いいえ|
|{{site.data.keyword.speechtotextshort}}	|はい 		|はい	 	|はい|
|{{site.data.keyword.streaminganalyticsshort}}	|はい		|はい		|はい |
|{{site.data.keyword.texttospeechshort}} 	|はい 		|はい	 	|はい|
|{{site.data.keyword.toneanalyzershort}} 	|はい 		|はい 		|はい|
|{{site.data.keyword.tradeoffanalyticsshort}}	|はい		|はい		|はい|
|{{site.data.keyword.visualinsightsshort}}	|はい		|はい		|はい|
|{{site.data.keyword.visualrecognitionshort}}	|はい 		|はい	 	|はい|
|{{site.data.keyword.iot_short}}		|はい		|はい		|いいえ|
|{{site.data.keyword.workflow}}			|はい		|はい		|はい |
|{{site.data.keyword.workloadscheduler}}	|はい		|はい		|はい |

## {{site.data.keyword.Bluemix_notm}} Dedicated アーキテクチャー
{: #dedicatedarch}

{{site.data.keyword.Bluemix_notm}} Dedicated は、SoftLayer に基づいて構築されているため、最高のパフォーマンスを誇るクラウド・インフラストラクチャーを使用できます。各データ・センターは 1 週間に 7 日、1 日 24 時間のセキュリティー、および厳格な管理が施されています。お客様および IBM は、VPN トンネルおよび専用 VLAN を介して {{site.data.keyword.Bluemix_notm}} Dedicated インスタンスにアクセスします。

{{site.data.keyword.Bluemix_notm}} Dedicated は、VPN または直接のネットワーク接続によってご使用のネットワーク上に置かれます。
単一テナントのハードウェアは、世界中のどの SoftLayer データ・センターでもセットアップできます。専用プラットフォームと専用サービスの管理は {{site.data.keyword.IBM_notm}} が行うので、ユーザーはカスタム・アプリの作成に集中することができます。また、{{site.data.keyword.IBM_notm}} は、ユーザーが選択したメンテナンス期間中に専用インスタンスのすべてのメンテナンスを実行します。

![{{site.data.keyword.Bluemix_notm}} Dedicated](images/dedicated.png "{{site.data.keyword.Bluemix_notm}} Dedicated")

*図 1. {{site.data.keyword.Bluemix_notm}} Dedicated の詳細図*

インフラストラクチャー、運用、および物理的セキュリティーの観点から、{{site.data.keyword.Bluemix_notm}} Dedicated 環境のセキュリティー標準は Public {{site.data.keyword.Bluemix_notm}} のセキュリティー標準と同じです。ただし、専用 {{site.data.keyword.Bluemix_notm}} に対する開発者のアクセスは LDAP ポリシーによって制御されます。{{site.data.keyword.Bluemix_notm}} チームは、ご使用の環境の設定時にこのポリシーを構成することができます。専用環境内で、ユーザーの役割および許可を管理できます。詳しくは、『[ユーザーおよび許可の管理](../admin/index.html#oc_useradmin)』を参照してください。


##{{site.data.keyword.Bluemix_notm}} Dedicated のセットアップ
{: #setupdedicated}

{{site.data.keyword.Bluemix_notm}} Dedicated は、{{site.data.keyword.Bluemix_notm}} Public オファリングの専用バージョンを提供するように設計されています。{{site.data.keyword.Bluemix_notm}} サービスおよびランタイムを使用して、IBM でホストされている SoftLayer アカウントでコンピューティング・ニーズをサポートすることができます。

IBM は、お客様がパスワードで保護されたログインを使用して {{site.data.keyword.Bluemix_notm}} Dedicated にアクセスできるようにします。サービス、ランタイム、および関連リソースにアクセスしたり、{{site.data.keyword.Bluemix_notm}} アプリをデプロイおよび削除したりすることができます。IBM は複数の SoftLayer ロケーションを利用して、{{site.data.keyword.Bluemix_notm}} Dedicated を提供しているため、お客様に近いロケーションにある専用バージョンをご利用いただけます。

{{site.data.keyword.Bluemix_notm}} の専用バージョンをセットアップするには、以下のようにします。

<ol>
<li>IBM 指定のアカウント担当者に連絡するか、 <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a>に連絡して、開始します。</li>
<li>{{site.data.keyword.Bluemix_notm}} Dedicated インスタンスの料金について IBM と連携して決定します。毎月繰り返し発生する料金は、使用する専用サービスと、すべての {{site.data.keyword.Bluemix_notm}} のパブリック・サービスのサブスクリプションに基づきます。さらに、当該サブスクリプション契約を超えて使用したサービスに対する請求書を受け取ります。</li>
<li>{{site.data.keyword.Bluemix_notm}} Dedicated インスタンスをセットアップする各フェーズの期限を特定します。各フェーズおよび実行するタスクについては、『<a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} Dedicated の役割と責任</a>』を参照してください。</li>
<li>専用インスタンスの <a href="http://www.softlayer.com/data-centers" target="_blank">SoftLayer データ・センターのロケーション</a>を選択します。その後、専用プラットフォームおよびアカウントが作成されます。アカウントについて、専用インスタンスを稼働するために必要な役割の組織内のユーザーを特定します。割り当てる役割については、『<a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} Dedicated の役割と責任</a>』を参照してください。
</li>
<li>お客様の企業ネットワークと {{site.data.keyword.Bluemix_notm}} Dedicated インスタンス間のネットワーク接続を定義して確立します。
	<ol type="a">
	<li>IBM が、専用インスタンス用のモニターおよびセキュリティー・インフラストラクチャーをインストールします。</li>
	<li>IBM が、お客様によって選択された単一テナント専用サービスをインストールします。</li>
	<li>お客様が、IP アドレスやファイアウォールなどのネットワーク構成とエンドポイント、および {{site.data.keyword.Bluemix_notm}} と統合するための LDAP へのアクセス権限を用意します。</li>
	</ol>
</li>
<li>環境に合わせて管理チームの役割を特定し割り当てます。
	<ol type="a">
	<li>IBM が、お客様が用意した構成に基づいて、ネットワーク・アクセスおよび LDAP を構成します。お客様が指定した連絡先に、管理アクセス権限が付与されます。サポートおよび請求用の連絡先を指定する必要もあります。</li>
	<li>IBM が、専用サービスを示すために、専用環境にシンジケートされたカタログをセットアップします。シンジケートされたカタログには、{{site.data.keyword.Bluemix_notm}} Public からシンジケートされた、ユーザーが使用できる追加サービスが含まれています。データ・プライバシーとセキュリティー基準に基づいて、ビジネスの要件に合致したパブリック・サービスを決定できます。</li>
	<li>お客様が、ネットワークとファイアウォールの構成、および LDAP エンドポイントとアクセスを確認します。</li>
	</ol>
</li>
</ol>

ご使用の環境に合わせた初期デプロイメントおよび構成は、以下にリストするプロセスのようになると考えられます。各タスクを誰が担当するかについて詳しくは、『[役割および責任](../dedicated/index.html#rolesresponsibilities)』を参照してください。

<ol>
<li>専用インスタンスをホストするためにどのデータ・センターを使用するかを選択します。データ・センターのオプションついては、<a href="http://www.softlayer.com/data-centers" target="_blank">SoftLayer データ・センターのロケーション</a>を参照してください。</li>
<li>ユーザーは、デプロイメント用のドメイン・ネームと、使用する ID を指定します。{{site.data.keyword.Bluemix_notm}} インスタンスのセットアップ時に 3 つのドメインを取得します。<code>*mycompany*.*region*.bluemix.net</code> および <code>*mycompany*.*region*.mybluemix.net</code> の接頭部を選択します。そして、3 番目のドメインのフルネームはユーザーが選択します。<br />
<p>カスタム・ドメインは必要な数だけ選択できます。ただし、それらのカスタム・ドメインの証明書はユーザーの責任になります。カスタム・ドメインの作成について詳しくは、『<a href="../manageapps/updapps.html#domain">カスタム・ドメインの作成と使用</a>』を参照してください。</p></li>
<li>{{site.data.keyword.Bluemix_notm}} Public 内でユーザーの企業を表すために使用されるパブリック・アカウントの所有者を特定します。IBM はこのアカウントを使用して、シンジケートされたサービス使用量を追跡します。</li>
<li>データ・センターへのセキュア接続のタイプを選択します。SoftLayer VPN、SoftLayer Direct Link、および AT&T Net Bond の中から選択できます。</li>
<li>パブリック・インターネットからユーザーの専用環境へのアクセスがあるかどうかを決定します。</li>
<li>使用される認証のタイプを選択します。IBM ID または Active Directory から選択できます。IBM ID の使用および登録について詳しくは、<a href="https://www.ibm.com/account/profile/us?page=regfaqhelp#4">「ヘルプおよびよくある質問」</a>ページを参照してください。
</li>
<li>環境に合わせて管理チームの役割を特定し割り当てます。割り当てが必要な役割については、『<a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} Dedicated の役割と責任</a>』を参照してください。</li>
<li>IBM は、Elastic Runtime、コンソール、管理フィーチャー、およびモニタリングを含むコア・プラットフォームをデプロイします。</li>
<li>IBM は、環境へのユーザーの管理アクセスを構成します。</li>
<li>専用インスタンスの使用を開始できます。このインスタンスは、アラートに対応できるように IBM 運用チームによってモニターされています。</li>
</ol>

{{site.data.keyword.Bluemix_notm}} インスタンスがセットアップされた後は、「管理」ページを使用して {{site.data.keyword.Bluemix_notm}} インスタンスをモニターおよび管理することができます。詳しくは、『[{{site.data.keyword.Bluemix_notm}} Local および Dedicated の管理](../admin/index.html#mng)』を参照してください。アップグレードおよび保守については、『[専用インスタンスの保守](index.html#maintaindedicated)』を参照してください。

##役割および責任
{: #rolesresponsibilities}

{{site.data.keyword.Bluemix_notm}} Dedicated アカウントをセットアップする場合、インスタンスを稼働するために必要な役割を担う個人を組織内で特定します。

###役割

以下のリストでは、割り当てる顧客の役割および責任を示します。

<dl>
<dt>**調達フォーカル**</dt>
<dd>IBM 担当員と連携して、お客様の {{site.data.keyword.Bluemix_notm}} Dedicated 環境を確立します。これには、プロジェクトのあらゆる側面について作業するのに適した、組織内の個人を特定することが含まれます。この役割に割り当てられたユーザーは、プロジェクト管理の役割を担当し、パターン選択、商業協定、およびお客様のリソースへのアクセスの取り決めを監視します。調達フォーカルは、専用インスタンスをセットアップし、デプロイメントのプロセスを追跡する際の総合的連絡先になります。</dd>
<dt>**コンプライアンス責任者**</dt>
<dd>IBM 担当員と連携して、お客様のセキュリティー要件に合ったトポロジーとデプロイメントのオプションを選択します。この役割に割り当てられたユーザーは IBM コンプライアンス・コンサルタントと連携して、コンプライアンスの目標を達成するデプロイメント・パターンを決めます。</dd>
<dt>**ネットワーク専門家**</dt>
<dd>IBM 担当員と連携して、{{site.data.keyword.Bluemix_notm}} デプロイメントのネットワーク計画を決定します。この役割に割り当てられたユーザーは、IBM によって要求された必要なネットワーキング仕様をレビューし、実装計画について IBM と連携します。インストールと検証の段階が終わると、この役割に割り当てられたユーザーは、ネットワーク構成が企業標準に準拠していることを承認します。</dd>
<dt>**DevOps フォーカル**</dt>
<dd>IBM 担当員と連携して、{{site.data.keyword.Bluemix_notm}} のプラットフォーム、サービス、およびランタイムに必要な保守更新を計画して適用します。この役割を割り当てられた個人は、IBM 担当員と連携して、{{site.data.keyword.Bluemix_notm}} Dedicated インスタンスの構成も行います。</dd>
</dl>

お客様の担当者は IBM の専門家と連携して、必要なサポートが常に得られるようにします。「プレミアム」サポート層にアップグレードすると、お客様のアカウントに関して専任 Client Success Manager (CSM) と共に作業できるようになります。さまざまなサポート層について詳しくは、『[サポートへのお問い合わせ](../support/index.html#contacting-support)』を参照してください。CSM は、以下タイプのタスクを実行します。

<ul>
<li>{{site.data.keyword.Bluemix_notm}} Dedicated 環境の迅速な採用を可能にします。</li>
<li>自己完結性を高めるための有効な教育およびイネーブルメント資料を配信します。</li>
<li>お客様と、お客様が使用する {{site.data.keyword.Bluemix_notm}} 開発、サポート、およびサービスとの間の長期的な関係を深めます。</li>
</ul>

{{site.data.keyword.Bluemix_notm}} インスタンスについてお客様と連携する {{site.data.keyword.Bluemix_notm}} サポートおよび運用チームは、以下の理由でのみ、お客様の専用環境にアクセスすることがあります。

<ul>
<li>アラートに対応し、運用上の保守を実行するため</li>
<li>サポート・チケットで報告された問題の再現を試みるため</li>
</ul>

###責任

環境のセットアップから継続的な保守まで、多様なタスクの実行が必要です。以下の表は、方向付け、進行、完了の各フェーズについて、実行する必要のあるタスクとその責任者の概要を示します。

方向付けフェーズは、{{site.data.keyword.Bluemix_notm}} Dedicated 環境を確立するために使用されます。このフェーズの主な目標には、以下のものがあります。

- 金融契約を審査し、配信までのマイルストーン日付を設定します。
- {{site.data.keyword.Bluemix_notm}} プラットフォームを作成し、ランタイムおよびサービスにアクセスできるようにします。
- 企業ネットワークと {{site.data.keyword.Bluemix_notm}} 操作との間のネットワーク接続を定義して確立します。
- 管理チームの役割を特定して割り当てます。

*表 4. 方向付けフェーズのタスク*

| **タスク** | **タスクの詳細** | **責任を持つ側** |
|----------|------------------|-----------------------|
|コンプライアンス規格の設定 | 環境に必要な政府、業界、および専有企業の標準を特定します。 | お客様 |
|セキュリティーおよびコンプライアンス統合計画の作成 | セキュリティー・コンプライアンスの実現に必要なコスト、スケジュール、およびリソースなどのセキュリティーおよび統合計画を作成します。 | IBM |
|コンプライアンス計画の承認 | コンプライアンス計画を承認します。 | お客様 |
|環境のサイジングの作成 |  	高可用性と災害復旧の目標、およびプラットフォームで作成されるアプリをサポートするために必要な初期 DEA とサービス・プロビジョニングを考慮した事前定義の選択に基づいて、環境のサイジングを作成します。お客様と IBM は連携して、必要なデータベース、顧客のシンジケートされたカタログで提供するサービスなどを定義します。 | IBM とお客様の共同の責任 |
|アーキテクチャーの選択 | 高可用性および災害復旧の要件を考慮に入れた事前定義の選択に基づいて、アーキテクチャーを選択します。 | IBM |
|災害復旧目標の定義 | 環境の災害復旧の要件を定義します。 | お客様 |
|災害復旧計画の作成 | 災害復旧計画を相談して定義します。IBM は災害復旧モデルを作成してお客様と相談し、お客様はフィードバックを提供して計画を承認します。 | IBM とお客様の共同の責任 |
|バックアップおよびリカバリー計画の作成 | 頻度およびバックアップのオン/オフ・サイト分配の要件を定義したバックアップとリカバリーの計画を作成します。IBM はプラットフォーム・コンポーネント、IBM サービス、サービス・メタデータ (ユーザー役割を含む) などをバックアップします。お客様は、お客様が責任を持つアプリケーション固有のデータをバックアップします。 | IBM とお客様の共同の責任 |
|イベント検出および問題判別用ツールの特定 | {{site.data.keyword.Bluemix_notm}} プラットフォーム・レベルでイベント検出および問題判別に使用する IBM およびサード・パーティーのツールを特定します。 | IBM |
|エスカレーション計画の定義 | モニター・コンポーネントで検出されたイベントをトリアージおよび解決するためのエスカレーション計画を定義します。 | IBM |
|インフラストラクチャー、プラットフォーム、およびサポートに関する合意の承認 | 環境の金銭的条件など、サブスクリプションに関する合意を承認します。サポート・サブスクリプションを承認します。 | お客様 |
|環境の調達 | 計算リソース、ネットワーク、およびストレージを調達します。これには、{{site.data.keyword.Bluemix_notm}} をホストするためのコアおよびサービス VLAN、Data Power をホストするためのベアメタル・サービス、および SoftLayer Firewall が含まれます。VPN トンネルを可能にするインフラストラクチャーを用意します。 | お客様 |
|プラットフォーム、アプリケーション、モニター、および管理の各コンポーネントのインストール | プラットフォーム・コンポーネント (BOSH Director、クラウド・コントローラー、正常性マネージャー、メッセージング、ルーター、DEA、サービス・プロバイダーなど) およびエスカレーションや問題検出の計画で定義されているモニター・コンポーネントをインストール、構成、および検証します。 | IBM |
|セキュリティー・コンポーネントのインストールと構成 | モニタリングと報告の計画と結合しているセキュリティー・コンポーネント (IBM QRadar、資格情報ボールト、侵入防御システム、IBM BigFix、IBM Security Privileged Identity Management など) をインストールして構成します。 | IBM |
|カスタム・コンポーネントのインストールと構成 |  	{{site.data.keyword.Bluemix_notm}} 製品およびサービスの有効範囲外にあるカスタム・コンポーネントをインストールして構成します。 | お客様 |
|初期ネットワーク構成の確立 | 初期ネットワーク構成 (ファイアウォール、DataPower、Fortigate、および DNS を含む) を確立します。 | IBM |
|{{site.data.keyword.Bluemix_notm}} パイプラインの接続 | {{site.data.keyword.Bluemix_notm}} の継続的統合および継続的配信のパイプラインを IBM リポジトリーと接続します。 | IBM |
|外部ソリューション・コンポーネントのカスタマイズ | 災害復旧シナリオ用にロード・バランサーをカスタマイズします。 | お客様 |
|VPN ソリューションのインストール | 双方向の VPN ソリューションをインストールします。 | IBM |
|ログイン・サーバーの構成 | 企業 LDAP で使用するログイン・サーバーを構成します。 | IBM |
|セキュリティー、コンプライアンス、および監査管理の状況の追跡  | すべてのツールおよびプロセスが配備されて、特定したコンプライアンスが実現する時点まで状況を追跡します。 | お客様 |
|物理的インフラストラクチャーのレビュー | データ・センターを保護するセキュリティー制御の脅威および審査のためのソリューション・コンポーネントをホストする物理的プレミスをレビューします。 | お客様 |
|モニタリング・ソフトウェアの検査 | エスカレーションおよび問題判別の計画で定義したモニターおよび管理コンポーネントを検査します。 | お客様 |
|OS の検査 | オペレーティング・システム・イメージがコンプライアンス規格に合っていることを確認するための検査を行います。IBM が OS イメージにアクセスできるようにします。 | IBM とお客様の共同の責任 |

次に、進行フェーズについて説明します。進行フェーズは、お客様と IBM Cloud との進行中の協力関係を記述します。このフェーズの主な目標には、以下のものがあります。

- キャパシティーを検討し、必要な調整を行います。
- 保守およびプラットフォームの改善を検討します。
- 問題解決および根本原因分析のアクティビティーを調整します。

*表 5. 進行フェーズのタスク*

| **タスク** | **タスクの詳細** | **責任を持つ側** |
|----------|------------------|-----------------------|
|週次容量レポートのレビュー | 週次容量レポートをレビューし、必要に応じて修正アクションを実行します。 | お客様 |
|前月比予測の作成 | 容量および使用量の情報を収集し、前月比予測を作成します。 | IBM とお客様の共同の責任 |
|キャパシティー予測のレビュー | アプリの容量および予想新規デプロイメントに影響する可能性がある外部イベントに関係する容量予測をレビューします。IBM と連携して、予測をレビューし、それに従って計画します。 | IBM とお客様の共同の責任 |
|予測のレビュー | キャパシティー予測をレビューします。これはキャパシティーに影響する可能性のある外部イベントに関連します。 | お客様 |
|容量の調整 |  ニーズの変化に合わせて容量を追加または削除します。 | IBM |
|近く予定されている更新および保守の公開 | IBM コンポーネントの必要な保守に関する文書を作成します。 | IBM |
|保守の実行 | IBM と連携して、21 日の期間内の必要な保守をスケジュールします。お客様は 21 日の期間内でお客様にとって都合が悪い日付を提供し、IBM はそれに従って保守のスケジュールを組みます。 | IBM とお客様の共同の責任 |
|プロビジョニング失敗の解決 | カタログにデプロイされた顧客作成サービスでプロビジョニング失敗が発生した場合に、その失敗を修正します。 | IBM |
|ネットワークおよび IP スキャンの実行 | 日次および月次のネットワーク・スキャンおよび IP スキャンを実行します。 | IBM とお客様の共同の責任 |
|監査ログへのアクセスの提供 | すべてのセキュリティー監査ログおよび管理監査ログへのアクセスを提供します。   | IBM とお客様の共同の責任 |
|テストの実施 | 定期的な KCO (Key Controls over Operations) テストおよびサード・パーティー侵入テストを実施します。 | IBM とお客様の共同の責任 |
|状況レポート作成、監査調整、およびコンプライアンス会議  | 状況レポート作成、外部監査調整、およびコンプライアンス・レビュー状況会議での説明を実施します。 | IBM |
|雇用とビジネス・ニーズの確認 | 四半期ごとに、顧客環境にアクセスできる IBM 担当者について、雇用の確認およびビジネス・ニーズが継続していることの確認を行います。 | IBM |
|セキュリティー脆弱性の解決 | プラットフォームで報告されたセキュリティー脆弱性を解決します。 | IBM |

最終の完了ステージは、お客様と IBM {{site.data.keyword.Bluemix_notm}} 間の関係の終了を表します。このフェーズの主なタスクには、以下のものがあります。

* 金銭的合意の終了
* すべてのネットワーク接続の削除
* インフラストラクチャーのリサイクル

*表 6. 完了フェーズのタスク*

| **タスク** | **タスクの詳細** | **責任を持つ側** |
|----------|------------------|-----------------------|
|金銭的合意の終了 | 金銭的合意の契約の終了について話し合い、終了に合意します。 | IBM とお客様の共同の責任 |
|環境の廃止 | 環境へのアクセスおよび環境の資格情報をシャットダウンします。 | IBM とお客様の共同の責任 |
|お客様とのネットワーク接続の削除 | IBM とお客様環境との間のネットワーク接続を削除します。 | IBM とお客様の共同の責任 |
|インフラストラクチャーのリサイクル | お客様の環境は SoftLayer 定義のプロセスに基づいてリサイクルされます。 | IBM |

##専用インスタンスの保守
{: #maintaindedicated}

IBM は、{{site.data.keyword.Bluemix_notm}} ランタイムおよびサービスに適合していると IBM が判断した更新およびフィックスについて、保守とインストールを行います。保守期間の間はサービスが利用できない場合があります。さらに、IBM はお客様と連携して、{{site.data.keyword.Bluemix_notm}} プラットフォームの保守更新をスケジュールします。

{{site.data.keyword.Bluemix_notm}} Dedicated では、以下のタイプの保守が必要です。
<dl>
<dt>**サービスの標準保守**</dt>
<dd>サービスは、事前定義された標準保守期間を利用します。そのため、サービスが利用できなくなる場合があります。IBM はサービス保守の実施に当たり、お客様の承認を必要としませんが、お客様のサービスへの影響が最小限になるよう努めます。<br />
<br />
IBM は、「状況」ページの各保守期間で計画されている変更についてのブロードキャスト・メッセージを送信します。<br />
<br />
**重要**: 保守期間中には、一部のサービスが使用不可になる可能性があります。</dd>

<dt>**{{site.data.keyword.Bluemix_notm}} プラットフォームの標準保守**</dt>
<dd>保守の更新は、21 日の期間内でお客様と IBM の間の調整に基づいて適用されます。お客様は、事前承認済みメンテナンス時間帯および都合の悪い具体的な日時を IBM に提供し、IBM はお客様が選択した日付の間またはその近くで更新のスケジュールを組みます。
<p>
<p>スケジュールされた保守更新および保留中の保守更新を表示するには、**「管理」>「システム情報」**と進みます。事前承認済みの時間帯および適用不可日付の設定、保守更新の表示または承認について詳しくは、『<a href="../admin/index.html#oc_schedulemaintenance">保守更新</a>』を参照してください。</p></dd>
</dl>

**重要**: IBM は、必要に応じて緊急時保守を適用するためにサービスを中断する権利を留保します。IBM は、定期保守の時間を変更することがありますが、そのような変更および緊急時保守の情報についてはすべてお客様に通知いたします。

保守更新後に報告された問題がある場合、IBM による更新のロールバックを許可するのがお客様にとっての最善策である場合は、{{site.data.keyword.Bluemix_notm}} サポートに合意してください。合意した場合、IBM はその更新をロールバックして、環境を前の状態に戻します。


## インシデント対応およびサポート
{: #incidentresponse}

### お客様が検出した問題

IBM サポートおよび運用チームに知らせる必要のある問題を見つけた場合、サポートに連絡する方法はいくつかあります。サポートへの連絡方法について詳しくは、[サポートへのお問い合わせ](../support/index.html#contacting-bluemix-support-local)を参照してください。問題に応じて、お客様または IBM が問題を修正するか、または協力して問題を修正します。

### IBM が検出した重大インシデント

重大インシデントは、緊急で予期しないサービス障害であり、お客様の環境またはユーザーに影響する安定性の問題です。IBM がお客様の環境内で重大インシデントを検出した場合、それを通知するためにお客様の「**状況**」ページに通知が表示されます。「状況」ページでは、プラットフォームまたはサービスに関して既知の問題があるかどうかも確認できます。「状況」ページについて詳しくは、『[状況の表示](../admin/index.html#oc_status)』を参照してください。

通知を、Web フックをサポートする Web サービスと統合したい場合は、[通知およびイベント・サブスクリプション](../admin/index.html#oc_eventsubscription)で、通知機能の拡張方法についての説明を参照してください。

![インシデント対応プロセス](../local/images/incidentresponseprocess.png "インシデント対応プロセス")

*図 2. インシデント対応プロセス*

問題に応じて、お客様または IBM が問題を修正するか、または協力して問題を修正します。インシデントに関する質問がある場合、または、問題を解決するために IBM 担当員の支援を必要とする場合、サポート・チケットをオープンすることができます。サポートへの連絡方法について詳しくは、[サポートへのお問い合わせ](../support/index.html#contacting-bluemix-support-local)を参照してください。

**注**: 重大度 1 のサポート・チケットは、1 日 24 時間、週に 7 日間モニターされます。その他のチケットは、日曜 10:00 pm GMT から土曜 12:00 am GMT まで処理されます。サポート・チケットの重大度とサポートとの協力について詳しくは、<a href="../support/index.html#contacting-bluemix-support-local">サポートへのお問い合わせ</a>を参照してください。


## 災害復旧
{: #dr}

{{site.data.keyword.Bluemix_short}} Dedicated の災害復旧は、{{site.data.keyword.Bluemix_short}} Public を使用する場合と同様にセットアップできます。{{site.data.keyword.Bluemix_short}} Public は、イノベーションのために継続的に使用可能なプラットフォームを提供し、そこでは複数のフェイルセーフ動作手段により、組織、スペース、およびアプリが常に使用可能です。アプリを複数の地域にデプロイすることで連続可用性が実現し、複数のハードウェアやソフトウェアのコンポーネントが計画外で同時に失われたり、データ・センター全体が失われたりしないように保護されます。これにより、ある地理的場所で自然災害が発生した場合でも、代替の地理的場所にある分散 {{site.data.keyword.Bluemix_notm}} Public アプリ・インスタンスが使用可能になります。
{: shortdesc}

{{site.data.keyword.Bluemix_short}} Dedicated の災害復旧が可能になるのは、アプリの継続的可用性、プラットフォームに本来備わっている高可用性、および、障害時にインスタンスをリストアできる機能を通してです。お客様は、複数の地域にデプロイすることで、アプリの連続可用性を実現する責任を持ちます。高可用性は、Cloud Foundry およびその他のコンポーネントに含まれているテクノロジーによって、プラットフォーム・レベルで組み込まれています。また、IBM と連携して、インスタンスをリストアする必要がある場合はいつでもデータが適切にバックアップされているようにすることもできます。

### {{site.data.keyword.Bluemix_notm}} Dedicated の継続的可用性の有効化
{: #enabling}

デフォルトでは、{{site.data.keyword.Bluemix_notm}} Public は複数の地理的場所にデプロイされます。ただし、グローバルに分散された {{site.data.keyword.Bluemix_notm}} Dedicated インスタンスを有効にするには、以下を行う必要があります。

* 開発者が手動プロセスまたは自動化プロセスのいずれかで複数の地域にアプリをデプロイすることを確認します。地域間の距離は 200 km より大きくして、1 つの自然災害が両方の地域に影響しないようにする必要があります。
* Akamai や Dyn のようなグローバル・ロード・バランサーを構成し
て、少なくとも 2 つの異なる地域にあるアプリを指すようにする。


**注**: すべての {{site.data.keyword.Bluemix_notm}} サービスが地域の分散をサポートするわけではありません。地域の分散を行いたい場合は、アプリケーションを作成するときに、そのアプリケーションで使用されるサービスが主要機能の 1 つとしてデータ同期を備えていることを確認する必要もあります。

#### 複数の地域への {{site.data.keyword.Bluemix_notm}} Dedicated アプリのデプロイ
{: #deploying}

2 つ目の場所または複数の場所にデプロイするには、以下のように、1 次地理的場所を使用可能にする際に実行したのと同じようなプロセスに従う必要があります。

1. アプリケーションの追加インスタンスをホストするための新しい専用環境を使用可能にします。新規環境を作成するには、このプロセスを開始するために IBM 営業チームに連絡してください。専用インスタンスのセットアップについて詳しくは、『[{{site.data.keyword.Bluemix_notm}} Dedicated のセットアップ](../dedicated/index.html#setupdedicated)』を参照してください。各環境にアクセスするには、別個にログインする必要があります。ホストされている環境の各物理的場所は、可用性を確保するために、元の場所から最小でも 200 km 離れている必要があります。
2. 新たにデプロイされたアプリがホストされる固有のドメイン・ネームを入手します。例えば、元のドメインが *mycompany.east.bluemix.net* の場合、*mycompany.west.bluemix.net* などの新規ドメインで新規専用環境を作成し、その新規ドメインにデプロイできます。
3. 元のアプリをデプロイするたびに、新規ロケーションにもデプロイします。デプロイについて詳しくは、『[アプリのアップロード](../starters/upload_app.html)』を参照してください。


#### {{site.data.keyword.Bluemix_notm}} Dedicated のグローバル・ロード・バランサーの使用可能化
{: #glb}

グローバル・ロード・バランサーは、連続可用性を確保し、災害復旧に必要なだけではなく、以下のような追加の利点ももたらします。

* デフォルトで、ユーザーを最も近い {{site.data.keyword.Bluemix_notm}} 地域にルーティングする
* パフォーマンスに基づいてルーティングする
* 新規アプリケーション・バージョンに特定の割合のトラフィックを選択的に送信する
* 地域ヘルス・チェックに基づいてサイト・フェイルオーバーを提供する
* アプリケーション・ヘルス・チェックに基づいてサイト・フェイルオーバーを提供する
* 複数のエンドポイント間で重み付きルーティングを使用する

Akamai や Dyn などのグローバル・ロード・バランサーを選択できます。グローバル・ロード・バランサーとしての Akamai の使用について詳しくは、『 [GLOBAL TRAFFIC MANAGEMENT](https://www.akamai.com/jp/ja/solutions/products/web-performance/global-traffic-management.jsp){: new_window} 』を参照してください。グローバル・ロード・バランサーとしての Dyn の使用について詳しくは、『 [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}』を参照してください。

### 高可用性
{: #ha}

連続的可用性を可能にすることに加えて、{{site.data.keyword.Bluemix_notm}} は、Cloud Foundry およびその他のコンポーネントに組み込まれたテクノロジーを使用して、プラットフォーム全体に高可用性も提供します。

これらのテクノロジーには、以下のものがあります。

<dl>
<dt>Cloud Foundry での DEA スケーラビリティー</dt>
<dd>Cloud Foundry <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">Droplet Execution Agent (DEA)</a> は、その内部で実行しているアプリに対するヘルス・チェックを実行します。アプリまたは DEA 自体に問題が生じた場合、代替 DEA にアプリの追加インスタンスがデプロイされ、問題が解決されます。詳しくは、『<a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configuring CF for High Availability with Redundancy</a>』を参照してください。
<br />
<p>アプリケーションの高可用性を確保するには、負荷のバランスを取るための十分な計算リソースが必要であり、さらに、起こりうる障害に対応するために追加の計算リソースが必要になる場合もあります。障害に備えて、あるいはアプリ・インスタンスの負荷のスパイクに対処できるように、DEA プールを増やすことで環境を拡張する必要がある場合は、IBM 担当者と連携して、追加の DEA を発注できます。
</p>
</dd>
<dt>SoftLayer 冗長性</dt>
<dd>専用環境での SoftLayer によって、各クラウド・ストレージ・クラスター内のデータは複数回書き込まれ、ストレージ・クラスターはドライブ障害に備えて自動修復機能を持つように構成されます。仮想サーバーで問題があった場合、SoftLayer はその仮想サーバーを別のホストで再始動することを試みます。</dd>
<dt>メタデータのバックアップ</dt>
<dd>SoftLayer EVault Backup を使用して、メタデータは最低でも 200 km 離れた場所にバックアップされます。</dd>
</dl>

##専用インスタンスのリストア
{: #restorededicated}

{{site.data.keyword.Bluemix_notm}} Dedicated の設定、メタデータ、および構成は、環境における計画外停止に備えるために定期的にバックアップされます。お客様の責任でバックアップする必要があるデータには、アプリケーション・データ、クラウド・データベース・サービス・データ、およびオブジェクト・ストアがあります。

システム・メタデータおよび構成を含むデータのバックアップの一環として、IBM は以下のタスクを実行します。

<ul>
<li>すべてのバックアップ・コピーを暗号化し、暗号鍵を管理します。</li>
<li>バックアップ・アクティビティーをモニターおよび管理します。</li>
<li>暗号化されたバックアップ・ファイルを提供します。</li>
<li>要求されたデータをリストアします。</li>
<li>バックアップとフィックス管理の操作のスケジュール競合を管理します。</li>
</ul>

プライベート・データの保護は重要です。そのため、IBM は、ファイルをお客様のデータ・センターの外部に移動しないようにするために、バックアップ・ファイル管理においてお客様に協力して作業していただく必要があります。具体的に、IBM は以下の作業をお客様にお願いします。

<ul>
<li>お客様が管理する他のバックアップ・データと同様に、暗号化されたバックアップ・データのコピーをオフサイトに移動する。</li>
<li>リストアが必要な場合には、IBM オペレーターにバックアップ・ファイルを提供する。</li>
</ul>

# 関連リンク
## 一般
* [詳細: {{site.data.keyword.Bluemix_notm}} Dedicated](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
* [{{site.data.keyword.Bluemix_notm}} の新機能](../whatsnew/index.html)
* [{{site.data.keyword.Bluemix_notm}} 用語集](../overview/glossary/index.html)
* [{{site.data.keyword.Bluemix_notm}} Local および {{site.data.keyword.Bluemix_notm}} Dedicated の管理](../admin/index.html#mng)
* [サポートへのお問い合わせ](../support/index.html#getting-customer-support)
