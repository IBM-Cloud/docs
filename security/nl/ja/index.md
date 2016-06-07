---

 

copyright:

  years: 2014, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_notm}} セキュリティー
{: #security}
*最終更新日: 2016 年 5 月 9 日*

{{site.data.keyword.Bluemix}} プラットフォームはセキュア・エンジニアリング・プラクティスを使用して設計されており、ネットワークおよびインフラストラクチャー全体における階層化セキュリティー管理機能を備えています。{{site.data.keyword.Bluemix_notm}} は、アプリケーション開発者がモバイル・アプリおよび Web アプリを保護するために使用できる一連のセキュリティー・サービスを備えています。これらのエレメントを組み合わせることで、{{site.data.keyword.Bluemix_notm}} は、セキュアなアプリケーション開発に対して明確な選択を提供するプラットフォームになっています。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} は、システム、ネットワーキング、およびセキュア・エンジニアリングに関する IBM のベスト・プラクティスに基づいたセキュリティー・ポリシーに準拠することで、セキュリティーが確保されている状態にします。これらのポリシーには、ソース・コード・スキャン、動的スキャン、脅威のモデル化、侵入テストなどのプラクティスが含まれます。{{site.data.keyword.Bluemix_notm}} は、セキュリティー・インシデントの管理について、IBM Product Security Incident Response Team (PSIRT) プロセスに従います。詳しくは、[IBM Security Vulnerability Management (PSIRT)](http://www-03.ibm.com/security/secure-engineering/process.html){: new_window} のサイトを参照してください。

{{site.data.keyword.Bluemix_notm}} Public および Dedicated では、IBM SoftLayer Infrastructure-as-a-Service (IaaS) クラウド・サービスを使用し、そのセキュリティー・アーキテクチャーを最大限に活用します。SoftLayer IaaS は、ご使用のアプリケーションとデータに対して何重にも重ねた層の保護を提供します。{{site.data.keyword.Bluemix_notm}} Local の場合、企業ファイアウォールの背後にあるお客様自身のデータ・センターに {{site.data.keyword.Bluemix_notm}} Local をホストすることで、お客様が物理的セキュリティーを所有し、インフラストラクチャーを提供します。さらに、{{site.data.keyword.Bluemix_notm}} は、Platform as a Service 層で各種カテゴリー (プラットフォーム、データ、およびアプリケーション) のセキュリティー機能を追加します。

## {{site.data.keyword.Bluemix_notm}} プラットフォームのセキュリティー
{: #platform-security}

{{site.data.keyword.Bluemix_notm}} は、(IBM SoftLayer を介して) コア・プラットフォームに対して機能、インフラストラクチャー、運用、および物理的なセキュリティーを提供します。ただし、{{site.data.keyword.Bluemix_notm}} Local は、お客様がインフラストラクチャーとデータ・センターを提供し、物理的セキュリティーを所有するという点で独自です。

SoftLayer の {{site.data.keyword.Bluemix_notm}} 環境は、ほとんどの制約的な IBM 情報技術 (IT) セキュリティー標準 (業界標準に適合しているか業界標準を上回る) に準拠しています。これらの標準には、
ネットワーク、データ暗号化、アクセス制御が含まれています。
 * アプリケーション ACL、アクセス権、侵入テスト
 * 識別、認証、許可
 * 情報とデータの保護
 * サービスの保全性と可用性
 * 脆弱性とフィックスの管理
 * サービス妨害と組織的攻撃の検出
 * セキュリティー・インシデント対応

![Bluemix プラットフォーム・セキュリティーの概要](images/platform_sec.svg)

*図 1. {{site.data.keyword.Bluemix_notm}} プラットフォームのセキュリティー概要*

{{site.data.keyword.Bluemix_notm}} Local では、企業ファイアウォールの背後で、データセンター内に {{site.data.keyword.Bluemix_notm}} をホストします。そのため、特定のセキュリティーの側面についてはお客様の責任となります。下図は、セキュリティーのうち、どの部分をお客様が担い、どの部分を IBM が管理、保守するかについての詳細です。

![Bluemix Local プラットフォームのセキュリティー概要](images/security_local_platform.svg)

*図 2. {{site.data.keyword.Bluemix_notm}} Local プラットフォームのセキュリティー概要*

IBM は、リレー ({{site.data.keyword.Bluemix_notm}} Local に付属のデリバリー機能) を使用して、お客様のデータ・センターに対して {{site.data.keyword.Bluemix_notm}} Local のインストール、リモート・モニター、および管理を行います。リレーは、各 {{site.data.keyword.Bluemix_notm}} Local インスタンスに固有の証明書にセキュアに接続します。{{site.data.keyword.Bluemix_notm}} Local およびリレーについて詳しくは、[Bluemix Local](../local/index.html) を参照してください。

### 機能セキュリティー

{{site.data.keyword.Bluemix_notm}} は、ユーザー認証、アクセス許可、重要な運用の監査、およびデータ保護など、さまざまな機能セキュリティーの能力を提供します。

<dl>
<dt>認証</dt>
<dd>アプリケーション開発者は、IBM Web ID を使用することで {{site.data.keyword.Bluemix_notm}} に対して認証されます。

{{site.data.keyword.Bluemix_notm}} Dedicated および Local の場合、デフォルトで、LDAP を介した認証がサポートされます。ご要望に応じて、 {{site.data.keyword.Bluemix_notm}} に対して、代わりに IBM Web ID を介した認証をセットアップできます。
</dd>

<dt>許可</dt>
<dd>{{site.data.keyword.Bluemix_notm}} は Cloud Foundry メカニズムを使用して、確実に各アプリケーション開発者が自分の作成したアプリケーションおよびサービス・インスタンスに対してのみアクセス権限を持つようにします。{{site.data.keyword.Bluemix_notm}} サービスに対する許可は OAuth に基づいています。{{site.data.keyword.Bluemix_notm}} プラットフォームのすべての内部エンドポイントへのアクセスは、外部ユーザーに制限されています。</dd>

<dt>監査</dt>
<dd>アプリケーション開発者の認証については、成功か失敗かに関わらずすべての試行に対して監査ログが作成されます。また、 {{site.data.keyword.Bluemix_notm}} アプリケーションが実行されるコンテナーをホストする Linux システムへの特権アクセスについても、監査ログが作成されます。</dd>

<dt>データの保護</dt>
<dd> すべての  {{site.data.keyword.Bluemix_notm}} トラフィックは、リバース・プロキシー、SSL 終了、およびロード・バランシング機能を提供する IBM WebSphere® DataPower® SOA アプライアンスを経由します。
以下の HTTP メソッドを使用できます。
 * DELETE
 * GET
 * HEAD
 * OPTIONS
 * POST
 * PUT
 * TRACE

HTTP の非活動タイムアウトは 2 分です。

以下のヘッダーには DataPower によりデータが取り込まれます。
<dl>
<dt>$wsis</dt>
<dd>クライアント・サイドの接続がセキュア (HTTPS) である場合は true に、その他の場合は false に設定されます。</dd>
<dt>$wssc</dt>
<dd>https、http、ws、または wss のうちいずれかのクライアント接続スキームに設定されます。</dd>
<dt>$wssn</dt>
<dd>クライアントが送信するホスト名に設定されます。</dd>
<dt>$wssp</dt>
<dd>クライアントの接続先のサーバー・ポートに設定されます。</dd>
<dt>x-client-ip</dt>
<dd>クライアントの IP アドレスに設定されます。</dd>
<dt>x-forwarded-proto</dt>
<dd>https、http、ws、または wss のうちいずれかのクライアント接続スキームに設定されます。</dd>
</dl>
</dd>

<dt>セキュア開発プラクティス</dt>
<dd> {{site.data.keyword.Bluemix_notm}} Public および Dedicated では、IBM Security AppScan® Dynamic Analyzer を使用して、さまざまな {{site.data.keyword.Bluemix_notm}} コンポーネントに対してセキュリティー脆弱性スキャンを定期的に実行します。{{site.data.keyword.Bluemix_notm}} デプロイメントに対しては、そのすべてのタイプについて潜在的な脆弱性を検出して解決するために、脅威のモデル化および侵入テストを実行します。さらに、アプリケーション開発者は AppScan Dynamic Analyzer サービスを使用して、{{site.data.keyword.Bluemix_notm}} にデプロイされている自分たちの Web アプリをセキュアにすることができます。</dd>
</dl>

### インフラストラクチャーのセキュリティー

{{site.data.keyword.Bluemix_notm}} は、Cloud Foundry に基づいて、アプリケーション実行のための堅固な基盤を提供します。アーキテクチャー内で、セキュリティーおよび独立性のためにいくつかのコンポーネントが提供されます。また、整合性および可用性を確保するために、変更管理およびバックアップとリカバリーの手順を実装します。

<dl>
<dt>環境の分離</dt>
<dd> {{site.data.keyword.Bluemix_notm}} Public では、開発環境と実稼働環境を互いから分離して、アプリケーションの安定性とセキュリティーを向上させています。</dd>

<dt>ファイアウォール</dt>
<dd> ファイアウォールを配備して、{{site.data.keyword.Bluemix_notm}} ネットワークへのアクセスを制限します。{{site.data.keyword.Bluemix_notm}} Local では、企業ファイアウォールにより、{{site.data.keyword.Bluemix_notm}} インスタンスからネットワークの残りの部分を分離します。</dd>

<dt>侵入防止</dt>
<dd>{{site.data.keyword.Bluemix_notm}} Public および Dedicated では、脅威への対処を可能にするため、不正侵入に対する防御によって脅威が検出できるようになっています。侵入防止ポリシーは、ファイアウォールで有効になります。</dd>

<dt>セキュアなアプリケーション・コンテナー管理</dt>
<dd>各 {{site.data.keyword.Bluemix_notm}} アプリケーションは分離され、プロセッサー、メモリー、およびディスクに対する特定のリソース制限のある独自のコンテナー内で実行されます。</dd>

<dt>オペレーティング・システム・セキュリティーの堅牢化</dt>
<dd>IBM 管理者は IBM Endpoint Manager などのツールを使用して、定期的にネットワークおよびオペレーティング・システムの堅牢化を実行しています。</dd>
</dl>

### 運用上のセキュリティー

{{site.data.keyword.Bluemix_notm}} は、以下の制御を備えた強固な運用上のセキュリティー環境を提供します。

<dl>
<dt>脆弱点スキャン</dt>
<dd>{{site.data.keyword.Bluemix_notm}} は、Tenable Network Security の脆弱性スキャン・ツールである Nessus を使用して、ネットワークに関する問題を検出し、構成をホストして、問題が解決されるようにします。</dd>

<dt>自動化フィックス管理</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 管理者は、オペレーティング・システムのフィックスが適切な頻度で確実に適用されるようにします。自動化フィックスは、IBM Endpoint Manager を使用して有効化されます。</dd>

<dt>監査ログの統合および分析</dt>
<dd>{{site.data.keyword.Bluemix_notm}} は IBMSecurity QRadar® ツールを使用して、Linux ログを統合し、Linux システムにおける特権アクセスをモニターします。また、{{site.data.keyword.Bluemix_notm}} は IBM QRadar Security Information and Event Management (SIEM) を使用して、アプリケーション開発者のログイン試行の成功および失敗をモニターします。</dd>

<dt>ユーザー・アクセス管理</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 内では職務分離ガイドラインに従い、ユーザーに細かいアクセス特権を割り当てて、ユーザーが持っているのは、最小特権の原則に基づいた、ジョブの実行に必要なアクセス権限のみであることを保証します。

{{site.data.keyword.Bluemix_notm}} Dedicated および Local 環境内では、割り当てられた管理者が、管理コンソールを使用して、組織内の {{site.data.keyword.Bluemix_notm}} ユーザーの役割および許可を管理できます。詳しくは、『[{{site.data.keyword.Bluemix_notm}} Local および Dedicated の管理](../admin/index.html#mng)』を参照してください。
</dd>
</dl>

### 物理的セキュリティー

{{site.data.keyword.Bluemix_notm}} Public および Dedicated は、物理的なネットワーク・セキュリティーに関し、SoftLayer のネットワーク内ネットワーク・トポロジーに依存しています。このネットワーク内ネットワーク・アーキテクチャーは、許可された職員のみがシステムに完全にアクセスできるようにします。{{site.data.keyword.Bluemix_notm}} Local の場合、お客様がローカル・インスタンスの物理的セキュリティーを所有します。お客様のデータ・センターは、お客様の企業ファイアウォールの背後で保護されます。

SoftLayer のネットワーク内ネットワークでは、パブリック・ネットワーク層 で、ホストされている Web サイトやオンライン・リソースへの公衆トラフィックを処理します。プライベート・ネットワーク層 では、SSL、PPTP、または IPSec VPN ゲートウェイを介して別個の独立したサード・パーティー通信会社を通じた真のアウト・オブ・バンド管理が可能です。データ・センターからデータ・センターへのネットワーク層 は、別々の SoftLayer 設備に収納されているサーバー間に、無料でセキュアな接続を提供します。

各 SoftLayer データ・センターは、SSAE 16 および 業界で認められた要件を例外なく満たす制御により、完全に保護されています。詳細については、SoftLayer の Security にある Compliance のページを参照してください。

## データ・セキュリティー
{: #data-security}

{{site.data.keyword.Bluemix_notm}} では、無許可アクセスからのデータの保護は、{{site.data.keyword.Bluemix_notm}} とお客様の共同作業です。

実行中のアプリケーションに関連したデータは、3 つの状態のいずれかになります (転送中のデータ、保存状態のデータ、および使用中のデータ)。

<dl>
<dt>転送中のデータ</dt>
<dd>ネットワーク上のノード間で転送されているデータ。</dd>

<dt>保存状態のデータ</dt>
<dd>保管されているデータ。</dd>

<dt>使用中のデータ</dt>
<dd>現在保管されておらず、エンドポイントで操作されているデータ。</dd>
</dl>

データ・セキュリティーについて計画する際には、それぞれのタイプのデータを考慮する必要があります。

{{site.data.keyword.Bluemix_notm}} プラットフォームは、ネットワーク全体で、データが {{site.data.keyword.Bluemix_notm}} 内部ネットワークの境界にある IBM DataPower Gateway に到達するまで、SSL を使用してアプリケーションへのエンド・ユーザー・アクセスを保護することで、転送中のデータを保護します。IBM DataPower Gateway はリバース・プロキシーとして機能し、SSL 終端を提供します。

使用中のデータと保存状態のデータのセキュリティーはともに、アプリケーションを開発するのがお客様であるため、お客様の責任になります。{{site.data.keyword.Bluemix_notm}} カタログで使用可能ないくつかのデータ関連サービスを利用して、この問題の解決に役立てることができます。

## {{site.data.keyword.Bluemix_notm}} アプリケーションのセキュリティー
{: #application-security}

アプリケーション開発者は、{{site.data.keyword.Bluemix_notm}} で実行されるアプリケーションのために、アプリケーション・データの保護を含むセキュリティー構成を使用可能にする必要があります。

いくつかの {{site.data.keyword.Bluemix_notm}} サービスによって提供されるセキュリティー機能を使用して、アプリケーションを保護することができます。IBM によって作成されたすべての {{site.data.keyword.Bluemix_notm}} サービスは、IBM セキュア・エンジニアリング開発プラクティスに従っています。

**注:** ここで説明されているサービスの一部は、Bluemix Dedicated と Local のいずれのインスタンスにも適用されない場合があります。

### SSO サービス

IBM Single Sign On for {{site.data.keyword.Bluemix_notm}} は、簡単に組み込めるシングル・サインオン機能を Node.js アプリケーションや Liberty for Java™ アプリケーションに提供する、ポリシー・ベースの認証サービスです。アプリケーション開発者がシングル・サインオン機能をアプリケーションに組み込めるようにするために、管理者はサービス・インスタンスを作成し、ID ソースを追加します。

Single Sign On サービスでは、以下に示すように、ユーザーの資格情報が保管されるいくつかの ID ソースがサポートされています。

<dl>
<dt>SAML エンタープライズ</dt>
<dd>SAML トークンを交換して認証を実行するユーザー・レジストリー。</dd>

<dt>クラウド・ディレクトリー</dt>
<dd>IBM Cloud にホストされているユーザー・レジストリー。</dd>

<dt>ソーシャル ID ソース</dt>
<dd> Google、Facebook、および LinkedIn によって保守されているユーザー・レジストリー。</dd>
</dl>

詳しくは、『[Single Sign On 入門 (Getting started with Single Sign On)](../services/SingleSignOn/index.html)』を参照してください。

### Application Security on Cloud

このサービスは、モバイル・アプリおよび Web アプリのセキュリティー分析を提供します。このサービスを使用して、ソース・コードのセキュリティー脆弱性をスキャンできます。詳しくは、『[Application Security on Cloud の概要 (Getting started with Application Security on Cloud)](../services/ApplicationSecurityonCloud/index.html)』を参照してください。

### アプリケーション・セキュリティー・テスト用の IBM UrbanCode プラグイン

IBM Application Security Testing for {{site.data.keyword.Bluemix_notm}} プラグインを使用すれば、{{site.data.keyword.Bluemix_notm}} でホストされている Web アプリや Android アプリに対してセキュリティー・スキャンを実行できるようになります。このプラグインは、IBM UrbanCode™ Deploy Community が IBM Bluemix DevOps Services プラットフォーム上で開発とサポートを行っています。

詳しくは、[IBM Application Security Testing for Bluemix](https://developer.ibm.com/urbancode/plugindoc/ibmucd/ibm-application-security-testing-bluemix/1-0/){: new_window} にアクセスしてください。

### dashDB

dashDB サービスは、ユーザー認証に組み込み LDAP サーバーを使用します。アプリケーションとデータベースの間の接続は、SSL 証明書によって保護されます。このサービスでは、DB2® 固有の暗号化機能を使用して、デプロイ済みのデータベースおよびデータベース・バックアップを自動的に暗号化します。マスター鍵のローテーションは、90 日ごとに自動で実施されます。

詳しくは、『[dashDB 入門 (Getting started with dashDB)](../services/dashDB/index.html)』を参照してください。

### Cloud Integration

Cloud Integration サービスにより、クラウドとオンプレミスのデータを統合できます。DB2、Oracle、SAP などのバックエンド・データベースと対話するサービスを追加できます。次に、データを移動したり、{{site.data.keyword.Bluemix_notm}} アプリケーションがアクセスおよび使用するための REST API を作成したりすることができます。このサービスにより、オンプレミスのセキュア・コネクターとのセキュア通信が可能になり、アプリケーションが使用する REST API としてバックエンド SoR (Systems of Record) が公開されます。

詳しくは、『[Cloud Integration 入門 (Getting started with Cloud Integration)](../services/CloudIntegration/index.html)』を参照してください。

### Secure Gateway

Secure Gateway サービスを使用すれば、{{site.data.keyword.Bluemix_notm}} アプリをオンプレミスまたはクラウドにあるリモート・ロケーションにセキュアに接続できるようになります。これにより、セキュア接続が実現し、{{site.data.keyword.Bluemix_notm}} 組織と接続先リモート・ロケーションとの間にトンネルが確立されます。{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースまたは API パッケージを使用して、セキュア・ゲートウェイを構成および作成できます。

詳しくは、『[Secure Gateway 入門 (Getting started with Secure Gateway)](../services/SecureGateway/secure_gateway.html)』を参照してください。

### SQL Database

SQL Database サービスは、完全にプロビジョンされたリレーショナル・データベースをアプリに追加します。このサービスでは、IBM Directory Server LDAP を使用して認証を行い、IBM InfoSphere® Guardium® Data Activity Monitor を使用してアプリケーションがアクセスするデータベースを保護します。アプリケーションとデータベースの間の接続は、DigiCert が署名する SSL 証明書によって保護されます。

このサービスを使用する特定のプランでは、{{site.data.keyword.Bluemix_notm}} 内の SQL データベース・コンソールを使用すると、以下の情報を含むレポートを取得できます。

 * アプリケーションがアクセスするデータベース内に存在する可能性のある機密データ。
 * 指定された期間内にデータベースにアクセスしたアプリケーション・ユーザー。
 * データベース内の機密データにアクセスしているアプリケーション・ユーザー。

SQL を使用してデータをマスクするには、データベースと共にデプロイされているマスキングのユーザー定義関数 (UDF) をアプリケーションから呼び出します。例えば、使用したいデータを別の場所でテスト用にマスクすることも可能です。UDF はこのデータ・マスキング・アルゴリズムを IBM Infosphere Optim™ から実装します。

このサービスのプレミアム・プランには、データ暗号化も含まれています。このサービスについて詳しくは、『[SQL Database 入門 (Getting started with SQL Database)](../services/SQLDB/index.html) 』を参照してください。

### SIEM (Security Information and Event Management)

SIEM (Security Information and Event Management) ツールを使用して、アプリケーション・ログ内のセキュリティー・アラートを分析できます。そのようなツールの 1 つに、IBM Security QRadar&reg; SIEM があります。このツールは、クラウド環境でセキュリティー・インテリジェンスを提供します。
詳しくは、
[IBM QRadar Security Intelligence Platform](http://www-01.ibm.com/support/knowledgecenter/SS42VS/welcome?lang=en){: new_window} を参照してください。

## {{site.data.keyword.Bluemix_notm}} セキュリティー・デプロイメント
{: #security-deployment}

{{site.data.keyword.Bluemix_notm}} セキュリティー・デプロイメント・アーキテクチャーには、セキュア・アクセスを確保するために、アプリのユーザーと開発者に対して異なる情報フローが含まれています。

![Bluemix セキュリティー・デプロイメント・アーキテクチャー](images/sec_deployment.svg)

*図 3. Bluemix セキュリティー・デプロイメント・アーキテクチャー*

{{site.data.keyword.Bluemix_notm}} *アプリ・ユーザー* の場合、**アプリ・ユーザーのフロー** は次のとおりです。
 1. 侵入防止およびネットワーク・セキュリティーが配備されているファイアウォールを介します。
 2. リバース・プロキシーおよび SSL 終端プロキシーを備えた IBM DataPower Gateway を介します。
 3. ネットワーク・ルーターを介します。
 4. Droplet Execution Agent (DEA) のアプリケーション・ランタイムに到達します。

{{site.data.keyword.Bluemix_notm}} *開発者*は、ログイン用と開発およびデプロイ用の 2 つのメイン・フローに従います。
 * **開発者のログイン・フロー**には、以下が含まれます。
    * {{site.data.keyword.Bluemix_notm}} Public にログインする開発者の場合、フローは以下のとおりです。
      1. IBM シングル・サインオン・サービスを介します。
      2. IBM Web ID を介します。
    * {{site.data.keyword.Bluemix_notm}} Dedicated または Local にログインする開発者の場合、フローは企業 LDAP を介します。
 * **開発およびデプロイメントのフロー**は、以下のとおりです。
    1. 侵入防止およびネットワーク・セキュリティーが配備されているファイアウォールを介します。これは、{{site.data.keyword.Bluemix_notm}} Dedicated にのみ適用されます。
    2. リバース・プロキシーおよび SSL 終端プロキシーを備えた IBM DataPower Gateway を介します。
    3. ネットワーク・ルーターを介します。
    4. Cloud Foundry クラウド・コントローラーを使用した許可を介します。これにより、開発者によって作成されたアプリおよびサービス・インスタンスにのみアクセスが確保されます。

{{site.data.keyword.Bluemix_notm}} Dedicated および {{site.data.keyword.Bluemix_notm}} Local *管理者* の場合、**管理者のフロー**は、以下のとおりです。
 1. 侵入防止およびネットワーク・セキュリティーが配備されているファイアウォールを介します。
 2. リバース・プロキシーおよび SSL 終端プロキシーを備えた IBM DataPower Gateway を介します。
 3. ネットワーク・ルーターを介します。
 4. {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースの「管理」ページにアクセスします。

上記のパスで説明したユーザーに加え、権限がある IBM セキュリティー運用チームが、以下に示すものなど、各種運用セキュリティー・タスクを実行します。
 * 脆弱点スキャン。{{site.data.keyword.Bluemix_notm}} Local では、お客様がファイアウォール内にある物理的セキュリティーとあらゆるスキャンを所有します。
 * ユーザー・アクセス管理。
 * IBM Endpoint Manager を使用してフィックスを定期的に適用することによる、オペレーティング・システムの堅牢化。
 * 侵入防止によるリスク管理。
 * QRadar を使用したセキュリティー・モニター。
 * 「管理」ページで入手可能なセキュリティー・レポート。

## セキュリティー・コンプライアンス
{: #compliance}

{{site.data.keyword.Bluemix}} は、信頼できる安全なクラウド・プラットフォームを提供します。{{site.data.keyword.Bluemix_notm}} のコンプライアンスは、ISO 27001 および ISO 27002 などの業界最高のセキュリティー規格を基盤としたプラットフォームおよびサービスの結果として作成されたものです。
{:shortdesc}

![EU のデータ保護モデル契約条項](images/icon_eumc.png)  **EU モデル契約条項**は、EU または欧州経済地域 (EEA) から第三国に転送される個人データを保護する取り決めです。EU モデル契約条項は、EU または EEA にデータ・エクスポーターとして位置するクライアントと、第三国にデータ・インポーターとして位置する IBM データ・プロセッサーとの間で署名されました。[IBM SaaS EU モデル契約条項](http://www-01.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ST&infotype=SA&htmlfid=KUJ12408USEN&attachment=KUJ12408USEN.PDF){: new_window}には、データ・エクスポーターとデータ・インポーターの権利と義務、およびデータ・サブジェクトの権利が記載されています。IBM SaaS EU モデル契約条項は、第三国で個人データの処理が行われる際に、その個人データに対して EU または EEA 内で使用可能な保護に似た保護を実行することを保証します。

![金融情報システム](images/FISC.gif)  日本国内の銀行業界および関連する金融業界の場合、コンピューター・システムは、金融情報システムセンター (FISC) の安全対策基準に基づいた安全対策手順を実施する必要があります。**FISC** 安全対策基準は、金融庁 (FSA)、日本銀行 (BOJ)、および FISC によって実施されています。

FISC 安全対策基準に関する {{site.data.keyword.Bluemix_notm}} の自己評価文書 (日本語版) は、[IBM Bluemix リスク調査結果](https://www.ibm.com/cloud-computing/jp/ja/bluemix_fisc.html){: new_window}から入手できます。 

![ISO 27001/2](images/icon_iso27k1.png)  {{site.data.keyword.Bluemix_notm}} は、機密保護管理プロセスでのベスト・プラクティスを定義する、**国際標準化機構 (ISO) 27001 および 27002 の規格**によって認定されています。ISO 27001 規格は、情報セキュリティー・マネジメント・システム (ISMS) を確立、実装、および文書化するための条件、および個々の組織のニーズに応じてセキュリティー管理を実装するための条件を指定しています。ISO 27002 規格は、ISO 27001 の各セキュリティー管理について詳細に説明しています。ISO 27000 規格群は、書面による情報、口頭による情報、および電子情報の機密性、保全性、および可用性の保護を目的として、アセットのリスクおよび評価の基準化プロセスを具体化したものです。

{{site.data.keyword.Bluemix_notm}} は、サード・パーティーのセキュリティー会社によって監査されており、ISO 27001 のすべての条件 ([Bluemix ISO 27001:2013 Certificate of Registration](ftp://public.dhe.ibm.com/cloud/bluemix/compliance/Bluemix_ISO27K1_WWCert_2016.pdf){: new_window}) を満たしています。

![SSAE16 SOC1/2/3](images/icon_aicpa.png) **Service Organization Controls (SOC)** レポートは、サービス組織でのセキュリティー、可用性、処理の完全性、機密性、およびプライバシーに関連した、主要な内部制御実施の評価を定義しています。米国公認会計士協会 (AICPA) ガイドを使用して生成されたこれらのレポートには、以下の項目が含まれています。 
  * 組織の監督
  * ベンダー管理プログラム
  * 社内のコーポレート・ガバナンスおよびリスク管理プロセス
  * 規制の監督

{{site.data.keyword.Bluemix_notm}} は、IBM SoftLayer Infrastructure as a Service (IaaS) クラウド・サービスを使用し、そのセキュリティー・アーキテクチャーを最大限に活用します。追加情報については、[{{site.data.keyword.Bluemix_notm}} の営業担当](mailto:bmxcert1@us.ibm.com){:new_window} チームまでお問い合わせください。

### プラットフォームとサービスの準拠
以下の表は、{{site.data.keyword.Bluemix_notm}} 内のどのサービスが各標準に準拠しているかを示しています。

|{{site.data.keyword.Bluemix_notm}} コンポーネント		|FISC		|ISO 27001	|SOC 2 タイプ 1		|
|:----------------------|:---------:|:---------:|:---------:|
|{{site.data.keyword.Bluemix_notm}} プラットフォーム		|Y			|Y	|Y	|
|{{site.data.keyword.APIM}}			|Y	|Y |			|
|{{site.data.keyword.autoscaling}}			|Y	|Y |			|
|{{site.data.keyword.bigicloudst}}			|Y |Y |Y |
|{{site.data.keyword.cloudant}}				|Y |Y |Y	|
|{{site.data.keyword.dashdbshort}}			|Y	|Y	|Y	|
|{{site.data.keyword.datacshort}}			|Y	|Y	|			|
|{{site.data.keyword.jazzhub_short}}					|Y	|Y	|			|
|{{site.data.keyword.containerlong}}			|Y		|Y	|			|
|{{site.data.keyword.mql}}				|Y	|Y	|	 		|
|{{site.data.keyword.SecureGateway}}			|Y	|Y |	 		|
|{{site.data.keyword.sescashort}}     |Y |Y | |

*表 1. プラットフォームとサービスの準拠*


# 関連リンク
{: #rellinks}

## 関連リンク
{: #general}

* [SoftLayer Security Compliance](http://www.softlayer.com/security)
* [Single Sign On 入門 (Getting started with Single Sign On)](../services/SingleSignOn/index.html)
