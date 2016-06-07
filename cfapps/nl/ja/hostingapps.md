---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#{{site.data.keyword.Bluemix_notm}} でのアプリのホスティング

*最終更新日: 2016 年 5 月 9 日*

<!--The whole topic is staging only -->

{{site.data.keyword.Bluemix}} を使用して、アプリケーションを作成することも、既存のアプリケーションをホストすることもできます。クラウド対応のアプリであれば、{{site.data.keyword.Bluemix_notm}} にマイグレーションできます。{{site.data.keyword.Bluemix_notm}} では、アプリケーションを実行するための方法として、例えば Cloud Foundry、IBM Containers、Virtual Machines など、さまざまな方法が用意されています。

##アプリをクラウド対応にする
{: #cloud-readyapps}

クラウド対応のアプリケーションは、アプリケーションが設計およびビルドされるときにクラウド・プラットフォームの基本原則に従います。クラウド対応のアプリケーションは、クラウド・プラットフォームによって提供される機能を使用できます。

以下のすべての基本原則がアプリケーション内で守られている場合、そのアプリケーションはクラウド対応であり、{{site.data.keyword.Bluemix_notm}} にマイグレーションできます。アプリケーション内でいずれかの基本原則に対する違反がある場合、通常は基本原則に従うようにアプリケーションを変更できます。

* アプリケーションを、直接特定のトポロジー用にコーディングしないでください。

  非クラウド環境では、アプリケーションは特定のデプロイメント・トポロジーを使用する場合があります。しかし、クラウド対応のアプリケーションおよびサービスは即時のスケーラビリティーの変更を許容するため、アプリケーション・トポロジーはクラウド・アプリケーションでは変わる可能性があります。スケーラビリティーの変更には、動的なスケーリングと、手動でのアプリケーションのインスタンス数の変更があります。

  スケーラビリティー変更によってアプリケーションが影響を受けないように、アプリケーションをできるだけ汎用的かつステートレスになるようビルドしてください。

* ローカル・ファイル・システムが永続することを前提としないでください。

  アプリケーション・インスタンスはクラウド上でいつでも移動、削除、複製される可能性があるため、ファイル・システムに書き込まれたファイルに依存しないようにしてください。頻繁に使用される情報 (アプリケーション・ログなど) のキャッシュとしてアプリケーションがローカル・ファイル・システムを使用する場合、その情報は、インスタンスがシャットダウンされ、別の場所または別の VM で再始動されると失われます。

  ローカル・ファイル・システムの代わりに、SQL または NoSQL データベースなどのサービスに情報を保管できます。動的クラウド環境では、ログが生成されるアプリケーション・インスタンスよりも長く存続するサービスでログを使用可能にしておくことも重要です。

* アプリケーション内にセッション状態を保管しないでください。

  システムの状態は、実行中の個々のアプリケーション・インスタンスではなく、データベースおよび共有ストレージによって定義されます。ステートフルであるという性質はどのような種類であっても、アプリケーションのスケーラビリティーを制限します。サーバー上の集中管理される場所にセッション状態を保管することによって、セッション状態の影響を最小化するようにしてください。

  セッション状態を完全に除去できない場合は、アプリケーション・サーバーの外部にある可用性の高い保管場所にセッション状態を格納してください。その保管場所としては、IBM WebSphere Extreme Scale、Redis、Memcached、外部データベースなどがあります。

* 特定のインフラストラクチャー依存関係を使用しないでください。

  これは 1 つの一般原則ですが、いくつかの現れ方があります。例えば、アプリケーションが使用するサービスに特定のホスト名または IP アドレスが割り振られていると想定しないでください。それらのサービスはクラウド環境では再配置されたり再生成されたりする可能性があるため、ホスト名および IP アドレスも変わる可能性があります。

  環境特有の依存関係を一連のプロパティー・ファイルに抽出することは改善ではありますが、まだ不十分です。ベスト・プラクティスは、外部サービス・レジストリーを使用してサービス・エンドポイントを解決することか、または、ルーティング機能全体を仮想名を持つ 1 つのサービス・バスまたはロード・バランサーに委任することです。

* アプリケーション内でインフラストラクチャー API を使用しないでください。

  インフラストラクチャー API はソフトウェア・スタック内の多くのさまざまなレイヤーを参照することがあるため、アプリケーション内で特定のインフラストラクチャー API に依存している場合、そのインフラストラクチャーの変更がより難しいものになります。

  代わりに、既存のオープン・ソース製品または市販製品に依存し、PaaS ソリューションは PaaS レイヤーに残したままにしてアプリケーション・コードの外に保持するようにできます。

* あいまいなプロトコルを使用しないでください。

  回復力のために余分な構成を必要とするようなあいまいなプロトコルを使用しないでください。

  標準プロトコルに基づくアプリケーションのほうが、構成項目をプラットフォームに委任でき、より回復力があります。標準プロトコルには、HTTP、SSL、標準データベース、キューイング、Web サービス接続などがあります。

* OS 固有の機能に依存しないでください。

  既に OS 固有の機能を使用している場合は、例えば Cygwin および Monoなどの互換ライブラリーを使用して、この問題を修正できます。Cygwin は、Windows 環境で Linux ツールのセットを提供する互換ライブラリーです。Mono は、Linux で Windows .NET 機能を提供する互換ライブラリーです。

  OS 固有の依存関係を避けて、代わりにミドルウェア・インフラストラクチャーまたはサービス・プロバイダーによって提供されるサービスを使用してください。

* アプリケーションを手動でインストールしないでください。

  動的クラウド環境では、アプリケーションがオンデマンドで頻繁にインストールされる可能性があります。インストール・プロセスはスクリプト化されて信頼できるものでなければならず、構成データはスクリプトの外部に置く必要があります。

  少なくとも、アプリケーションのインストールを、オペレーティング・システムから独立した一様なスクリプトのセットとして捉えてください。さまざまな自動化技法に適応できるよう、アプリケーションのインストールを小さくポータブルなものにしてください。また、アプリケーションのインストールに必要な依存関係を最小限にしてください。

クラウド対応アプリケーションについて詳しくは、「[The 12-factor application](http://12factor.net/){:new_window}」を参照してください。

##アプリのマイグレーション
{: #ht_hostapp}

アプリケーションを完全にクラウド環境に移す代わりに、アプリケーションを {{site.data.keyword.Bluemix_notm}} にインクリメンタルにマイグレーションできます。アプリケーションの一部を先にマイグレーションし、Cloud Integration サービスを使用して、既存のデータまたは SoR (Systems of Record、定型業務処理システム) に接続することができます。

クラウド・アプリケーション内で、バックエンドのデータまたはサービス (例えば、SoR) にアクセスすることが必要になる場合があります。{{site.data.keyword.Bluemix_notm}} では、Secure Gateway サービスを使用して、{{site.data.keyword.Bluemix_notm}} 組織とエンタープライズ・バックエンド・ネットワークの間にセキュア・トンネルを確立できます。このサービスによって、{{site.data.keyword.Bluemix_notm}} 上のアプリケーションがバックエンド・ネットワークのデータおよびサービスにアクセスできるようになります。詳細については、「[Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}」を参照してください。

アプリケーションを Cloud Foundry アプリケーションとして {{site.data.keyword.Bluemix_notm}} にデプロイするには、{{site.data.keyword.Bluemix_notm}} カタログからランタイムを選択します。ランタイムには、スターター・アプリケーション Hello World が含まれていて、これを自分のアプリケーションに置き換えることができます。使用したいランタイムを提供するスターターが見つからない場合は、cf push コマンドで -b オプションを使用して、Cloud Foundry 互換のカスタム・ビルドパックを {{site.data.keyword.Bluemix_notm}} に持ち込むことができます。詳しくは、『[コミュニティー・ビルドパックの使用](../cfapps/byob.html)』を参照してください。

{{site.data.keyword.Bluemix_notm}} が提供する以下のツールおよびサービスを使用できます。

*表 1. {{site.data.keyword.Bluemix_notm}} ツール*

| ツール	|  方法  |
|:------|:--------|
|Cloud Foundry コマンド・ライン・インターフェース (cf cli)	|ローカル・クライアントでコードを管理し、Cloud Foundry コマンド・ライン・インターフェースを使用してアプリケーションを手動で {{site.data.keyword.Bluemix_notm}} にプッシュします。詳しくは、『[アプリケーションのアップロード](../starters/upload_app.html)』を参照してください。|
|Eclipse	|Eclipse でコードを管理し、IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} を使用してアプリケーションをプッシュします。|
|Git 統合	|GitHub でコードを管理し、Git を {{site.data.keyword.Bluemix_notm}} に統合します。他の開発者と共同作業することができます。コードの変更をコミットすると、アプリケーションは自動的に {{site.data.keyword.Bluemix_notm}} にデプロイされます。アプリケーションを手動でプッシュする必要はありません。|
|{{site.data.keyword.Bluemix_notm}} DevOps Delivery Pipeline	|DevOps GitHub リポジトリーでコードを管理し、DevOps Delivery Pipeline を使用してアプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイします。|


アプリケーションの要件が Cloud Foundry プラットフォームではサポートされない場合、カスタマイズされた追加のオプションを使用してランタイムがセットアップされ、構成され、保守される、コンテナーまたは VM を使用できます。

##cf CLI を使用したアプリのアップロード
{: #ht_cfcli}

ローカル・クライアントでコードを管理し、Cloud Foundry コマンド・ライン・インターフェースを使用してアプリケーションを手動で {{site.data.keyword.Bluemix_notm}} にアップロードすることができます。コードを変更した場合、更新後のコードを実行するには、アプリケーションを再度 {{site.data.keyword.Bluemix_notm}} にプッシュする必要があります。

アプリケーションをマイグレーションするには、以下の手順を実行します。

<ol>
<li>Cloud Foundry コマンド・ライン・インターフェースをインストールします。最新バージョンの cf コマンド・ライン・インターフェースを使用するようにしてください。
<ol>
<li>ご使用のオペレーティング・システム用のインストール・プログラムをダウンロードします。</li>
<li>ツールのウィザードに従ってコマンド・ラインをインストールします。</li>
<li>次のコマンドを使用して、cf コマンド・ライン・インターフェースのバージョンを確認します。
<pre>cf -v</pre></li>
</ol>
</li>

<li>オプション: アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュする前にデプロイメントの詳細を指定して保存したい場合は、以下の手順を実行してアプリケーション・マニフェストを追加できます。
<ol>
<li>アプリケーションの作業ディレクトリーに移動し、manifest.yml という名前 (これはデフォルト名です) のファイルを作成します。</li>
<li>このマニフェスト・ファイル内にデプロイメント詳細を指定します。以下は、Java™ アプリケーション用のマニフェスト・ファイルの例です。
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>このファイル内で使用できるサポートされるオプションについて詳しくは、『[アプリケーション・マニフェスト](../manageapps/depapps.html#appmanifest)』を参照してください。

</p></li></ol>
</li>

<li>アプリケーションをプッシュします。cf push コマンドを使用してアプリケーションをアップロードできます。
<ol>
<li>以下のコマンドを実行して、{{site.data.keyword.Bluemix_notm}} に接続し、ログインします。プロンプトが出されたら、組織とスペースを選択します。
<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>アプリケーション・ディレクトリーから、アプリケーション名を指定して cf push コマンドを入力します。アプリケーション名は {{site.data.keyword.Bluemix_notm}} 環境内で固有でなければなりません。
<pre>cf push appname</pre></li>
<li>オプション: 外部ビルドパックを使用する場合、cf push コマンドで -b オプションを使用する必要があります。以下に例を示します。<pre>cf push appname -b buildpack_URL</pre>
<p>詳しくは、『コミュニティー・ビルドパックの使用』を参照してください。</p>
</li></ol>
</li>

<li>オプション: アプリケーションを変更した場合、再度 cf push コマンドを入力して、変更をアップロードする必要があります。cf コマンド・ライン・インターフェースは、アプリケーションの実行中のインスタンスを新規コードで更新するようプロンプトを出されたときに、ユーザーの過去のオプションとユーザーの応答を使用します。</li>
</ol>

**注:**

* cf コマンド・ライン・インターフェースは、cf push コマンドが使用されると、すべてのファイルおよびディレクトリーを現行ディレクトリーから {{site.data.keyword.Bluemix_notm}} にコピーします。アプリケーション・ディレクトリーには必要なファイルだけを保管しておくようにしてください。
* 組織のメモリーがアプリケーションのすべてのインスタンスにとって十分であることを確認してください。組織のメモリー割り当て量を表示するには、cf org org_name を使用します。
* cf push について詳しくは、『[cf コマンド](../cli/reference/cfcommands/index.html)』を参照してください。

##データのマイグレーションおよびサービスの使用
{: #ht_service}

アプリケーションを {{site.data.keyword.Bluemix_notm}} にアップロードした後、アプリケーションが接続されるサービスを {{site.data.keyword.Bluemix_notm}} カタログから選択し、サービス・インスタンスを作成し、そのインスタンスをアプリケーションにバインドし、その後でアプリケーションを再始動します。

アプリケーションの VCAP_SERVICES 環境変数は、{{site.data.keyword.Bluemix_notm}} でサービス・インスタンスと対話する方法についての情報を含んでいる JSON オブジェクトです。その情報には、サービス・インスタンス名、資格情報、およびサービス・インスタンスへの接続 URL が含まれます。

{{site.data.keyword.Bluemix_notm}} でコードを実行するには、VCAP_SERVICES 変数を解析してサービス接続についての情報を取得するためのコード・ロジックを追加する必要があります。サービス・インスタンスの動的に割り当てられたホストおよびポートを環境変数を通して取得するように、アプリケーションを変更してください。次の例は、Ruby アプリケーションで Postgre SQL サービス・インスタンスの資格情報を取得する方法を示します。

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

{{site.data.keyword.Bluemix_notm}} 用にアプリケーションを変更した後、アプリケーションをローカル環境で確実に実行できるようにするため、すべての {{site.data.keyword.Bluemix_notm}} Cloud Foundry アプリケーションに対して設定される VCAP_SERVICES 環境変数があるかどうかをチェックしてください。


# 関連リンク
{: #rellinks}

## 関連リンク
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [Virtual Machines](../virtualmachines/vm_index.html)
* [Delivery Pipeline 入門](../services/DeliveryPipeline/index.html)
* [IBM Eclipse Tools for Bluemix を使用したアプリのデプロイ](../manageapps/eclipsetools/eclipsetools.html)
* [The twelve-factor app](http://12factor.net/){:new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
