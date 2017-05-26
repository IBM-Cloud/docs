---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#システム・アクセス
{: #system_access}


このセクションでは、システムへのアクセス、およびシステムへのアクセスをセットアップするためのさまざまな方法とともに、サービス・インスタンスの作成および管理の方法について説明しています。
{: shortdesc}


## WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} における REST API の使用法
{: #restapi_usage}

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のインスタンスの作成、プロビジョン、管理、および削除は、以下のいずれかの方法で行われます。

* {{site.data.keyword.Bluemix_notm}} UI の {{site.data.keyword.Bluemix_notm}} カタログおよびサービス・ダッシュボードから。
* RESTful API を使用したアプリケーションまたはスクリプトの作成から。

Swagger 2.0 準拠 REST API を使用して、クライアントはポータルおよびダッシュボードで提供されるものと同じ機能にアクセスできます。サポートされる REST API とリソースについて詳しくは、WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API の資料](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api#/){: new_window}を参照してください。REST API の使用法を示すサンプル・コードについては、{{site.data.keyword.Bluemix_notm}} [REST API のサンプル](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}の Git でホストされた WebSphere Application Server をダウンロードしてください。

**注:** サービス・インスタンスを作成した後、作成された T シャツ・サイズによっては、サービスがすぐに使用可能状態にならないことがあります。戻された JSON の **Status** フィールドを照会してサービス・インスタンスの現在の状態を判別することをお勧めします。

**注: [REST API のサンプル](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}で参照されている ****apiEndpoint** URL は、米国南部地域を指しています。他の地域を使用する場合は、アプリケーションで適切な **apiEndpoint** を参照するようにしてください。

*表 1. Rest API 実装の API エンドポイント URL*

| **地域名** | **地理的位置** | **地域接頭部** | **API エンドポイント URL** |       
|:-------------:|:----------:|:--------------:|:-------------:|
| 米国南部 | ダラス、テキサス、米国 | ng | https://wasaas-broker.ng.bluemix.net/wasaas-broker/api  |
| 英国 | ロンドン、イングランド | eu-gb | https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api  |
| シドニー | シドニー、オーストラリア | au-syd | https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api  |
| フランクフルト | フランクフルト、ドイツ | eu-de | https://wasaas-broker.eu-de.bluemix.net/wasaas-broker/api  |



## サービス・ダッシュボード
{: #service_dashboard}

サービス・インスタンスの作成後は、サービス・ダッシュボードが表示されます。
組織ダッシュボードからは、サービス・アイコンをクリックすることで、
いつでもサービス・ダッシュボードに戻ることができます。サービス・ダッシュボードからは、次のものにアクセスできます。

* この文書へのリンク
* 必要な OpenVPN 構成ファイルをダウンロードするためのリンク
* 仮想マシンを始動および停止する機能。最初に VM が起動されます
* ホスト名
* 管理ユーザーと管理パスワード
* SSH 秘密鍵
* WebSphere® 管理ユーザーおよび管理パスワード
* 管理センターと管理コンソール の URL

**注**: 一定量の計算、メモリー、入出力のリソースのために、停止状態の累積 VM について 5 % 減額して課金されます。IP アドレス 10 個およびメモリー 64 GB を超えない決まった数の停止インスタンスに管理されます。


## WebSphere Application Server in Bluemix インスタンス用の openVPN のセットアップ
{: #setup_openvpn}

いずれの WebSphere Application Server in Bluemix 仮想マシンにアクセスするにも、OpenVPN が必要です。管理者特権を使用して OpenVPN がインストールされ、実行されている必要があります。

### Windows で OpenVPN をセットアップするには、以下の手順を使用します。

1. [OpenVPN Windows ダウンロード](http://swupdate.openvpn.org/community/releases/)のリンクから、以下をダウンロードします。
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} (64 ビットの場合)、または
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window} (32 ビットの場合)。
2. 必ず、[Windows 管理者として実行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}し、OpenVPN をインストールしてください。
3. サービス・ダッシュボードで、WebSphere Application Server in Bluemix インスタンスの OpenVPN ダウンロード・リンクから VPN 構成ファイルをダウンロードします。圧縮ファイル内の 4 ファイルすべてを、**{OpenVPN
home}\config** ディレクトリーに解凍します。例:

  <pre>  
C:\Program Files\OpenVPN\Config  </pre>
  {: codeblock}

4. OpenVPN クライアント・プログラム「OpenVPN GUI」を開始します。必ず、[「管理者として実行」](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}を選択して、プログラムを開始してください。そうでないと、接続できない場合があります。

### Linux で OpenVPN をセットアップするには、以下の手順を使用します。
1. OpenVPN をインストールするには、この[手順](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}に従ってください。
  * RPM Package Manager を手動でダウンロードしてインストールする必要がある場合には、
[OpenVPN の UNIX/LINUX 用のダウンロード](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}
に移動してください。
Linux 管理者からの支援が必要な場合があります。
3. サービス・ダッシュボードで、WebSphere Application Server in Bluemix インスタンスの OpenVPN ダウンロード・リンクから VPN 構成ファイルをダウンロードします。openVPN クライアントの開始に使用する予定のディレクトリーに、ファイルを解凍します。
4 ファイルがすべて同じディレクトリーにある必要があります。
3. OpenVPN クライアント・プログラムを開始します。端末ウィンドウを開いて、構成ファイルを含むディレクトリーに移動します。root として次のコマンドを実行します。

  <pre>
$ openvpn --config vt-wasaas-wasaas.ovpn  </pre>
  {: codeblock}  

### Mac で OpenVPN を構成するには、以下の手順を使用します。
1. 1 つの方法として、オープン・ソース・ソフトウェア製品の [Tunnelblick](https://tunnelblick.net/){: new_window} をインストールする方法があります。
2. WebSphere サービスから VPN 構成ファイルを抽出します。Tunnelblick によって、Mac の管理パスワードが求められ、接続に使用できる VPN セットにこの構成が追加されます。

3. VPN ネットワークに接続します。その後、仮想マシンにアクセスできます。最初にユーザーがアクセスした後、Tunnelblick は構成をキャッシュに入れます。ユーザーは [Tunnelblick](https://tunnelblick.net/){: new_window} から接続できます。トップ・メニュー・バーにアイコンを配置して、簡単にアクセスすることができます。


## SSH を使用した WebSphere Application Server in Bluemix VM へのアクセス
{: #using_ssh}

この手順では、クライアントとして OpenSSH を使用していることを想定しています。
OpenSSH は通常、Linux 上で使用でき、Windows 上で実行される Cygwin でも使用できます。Windows コマンド・プロンプトから実行するようにインストールすることもできます。

OpenSSH のインストールを確認するには、次のコマンドを入力します。

  ```
$ ssh -V
  ```
  {: codeblock}

以下のメッセージは応答例です。
  ```
OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

WebSphere Application Server in Bluemix VM への SSH アクセスをセットアップするには、以下の手順を使用します。

1. 初めて接続したときに表示される「The authenticity of host x.x.x.x cannot be established.」という警告メッセージを検討します。このメッセージは正常です。プロンプトが表示されたら、yes を選択します。この時点で、VM 上でユーザー「virtuser」に公開鍵がインストールされます。
2. 秘密鍵を使用して、virtuser にログインします。秘密鍵認証方式を使用するのが最適です。
3. 秘密鍵の内容をファイルにコピーします。
4. 次のコマンドを実行します。

  <pre>
$ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName  </pre>
  {: codeblock}

5. 次のコマンドを使用して virtuser から root に切り替えることにより、完全な sysadmin 権限を取得します。

  <pre>
$ sudo su root  </pre>
  {: codeblock}

6. 秘密 SSH 鍵でシステムにアクセスして問題が発生する場合は、提供された root パスワードを使用します。次のコマンドを実行して root としてログインし、パスワードを入力します。

 <pre>
$ ssh root@169.53.246.x  </pre>
  {: codeblock}

7. システムへのアクセスで秘密 SSH 鍵を使用した場合も、root パスワードを使用した場合も、すぐに root パスワードを変更してください。
8. SSH コマンドを単純化するために、「config」という名前のファイルを %HOME%/.ssh ディレクトリーに作成します。例:

  <pre>
Host VM1
Hostname 169.53.246.xxx
User virtuser
IdentityFile /path/privateKeyFileName  </pre>
  {: codeblock}

9. virtuser として接続するために、「ssh VM1」を実行します。

## システム・パス
{: #system_paths}

* Liberty プロファイルのコマンドは、*/opt/IBM/WebSphere/Liberty/bin* から実行可能です。
* Liberty プロファイルのサーバー・プロファイルがある場所は、*/opt/IBM/WebSphere/Profiles/Liberty/servers/server1* です。
* Traditional WebSphere Application Server コマンドは、*/opt/IBM/WebSphere/AppServer/bin* から実行できます。
* サーバー用の Traditional WebSphere Application Server プロファイルのロケーションは、*/opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1* です。

## 管理センターと管理コンソールのリンクの使用
{: #console_links}

管理センターまたは管理コンソールへのリンクをクリックしたときに、*「信頼できない接続」*の警告を受け取ることがあります。ブラウザーによって、示されるメッセージ・テキストも、警告を回避または除去するための手順も異なります。

{{site.data.keyword.IBM}} 提供のリンクを使用しているため、この警告は無視して接続して問題ありません。ブラウザーによってセキュリティー例外の保管が提案された場合は、そうすることで、最も簡単にこの警告を以降受け取らないようにすることができます。

もう 1 つのオプションとして、着信した署名者証明書をエクスポートして、トラステッド・ルート証明書としてブラウザーにインポートすることができます。
このオプションでは、*hosts* ファイルに、VM の IP アドレスを証明書発行者の共通名にマップするエントリーを作成する必要があります。この名前の形式は、wl<pureapplication.ibmcloud.com です。現在、URL で IP アドレスの代わりにホスト名を使用している場合は、スムーズに接続できます。
その後は、URL で IP アドレスではなく、そのホスト名を使用して管理センターまたは管理コンソールにアクセスする必要があります。

最後に、お客様が、外部化したアプリケーションの独自のルート証明書をインストールする場合がよくあります。
詳しくは、[WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} または [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} の IBM Knowledge Center を参照してください。

## ファイアウォール・ポート
{: #firewall_ports}

アプリケーションおよびデータベースへのアクセスを許可するために、ファイアウォール上でポートをオープンすることが必要になる可能性があります。
  * WebSphere Application Server in Bluemix の各ノードには、WAS_HOME/virtual/bin ディレクトリーに openFirewallPorts.sh スクリプトがあります。
  * 各 Liberty 集合ホスト上には、WAS_HOME/virtual/bin ディレクトリー内に openFirewallPorts.sh スクリプトがあります。

使用法: 
  ```
$ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT はポート番号です。
* PROTOCOL は、TCP または UDP のいずれかです。
* -persist は true または false のいずれかです。

複数のポートを指定するには、それらのポートをコンマ「,」で分離してください。

**注**: オープンしているポートの sport と dport は、ファイアウォールの INPUT セクションと OUTPUT セクションでオープンされます。このスクリプトは、sudo を使用して root として実行する必要があります。iptables を直接変更することもできます。

## Web サーバーの構成
{: #configure_webserver}

セルまたは集合をプロビジョンする際、事前構成された環境を受け取ります。特に従来の Network Deployment セルの場合は、以下の環境を受け取ります。

* 開発およびテストの目的で IBM HTTP Server と連結された Deployment Manager。

* Deployment Manager に統合されたカスタム・ノード。

* すべて初期に「開始済み」状態にプロビジョンされている、Deployment Manager、IHS Server、およびノード・エージェント。

Web サーバーですべてのユーザー要求を処理する必要がある場合は、アプリケーションのデプロイ後にプラグインを生成して伝搬する必要があるかもしれません。

**問題の回避:** プラグインの生成と伝搬を行う前に、以下の前提条件タスクが完了していることを確認してください。

* ローカルの Windows、Linux、または MAC 環境で、[openVPN](systemAccess.html#setup_openvpn) が構成済みで開始済みであり、適切な領域への接続が確立されていることを確認します。

* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のサービス・ダッシュボードから**管理コンソールを開き**、サービス・ダッシュボードで提供される wsadmin および管理パスワードでログインします。

* Deployment Manager は空のカスタム・ノードと統合されるため、管理コンソールからアプリケーション・サーバー (例えば ***server1*** など) を作成します。

* 作成したサーバーを始動します。

* アプリケーションのインストール時に、アプリケーションのモジュールが、始動したサーバーおよび Web サーバー (例えば***webserver1***) にマップされていることを確認します。

以下の概略的な手順は、前提条件タスクが完了していることを想定しています。

1. 管理コンソールで、環境オプションからプラグインを生成します。
   1. 「環境」>「グローバル Web サーバー・プラグイン構成の更新」を選択します
   2. **「OK」**または**「上書きして新規プラグイン構成ファイルを生成 (Overwrite to generate a new plug-in configuration file)」**のいずれかをクリックします
2. Deployment Manager から、プラグインを Web サーバー構成にコピーします。

  ```
   cp /opt/IBM/WebSphere/Profiles/DefaultDmgr01/config/cells/plugin-cfg.xml /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
  ```
  {: codeblock}
3. **IHS_HOME/conf** 内の **httpd.conf** を編集し (例えば */opt/IBM/WebSphere/HTTPServer/conf*)、以下の 2 行が存在することを確認します。

    ```
    LoadModule was_ap22_module /opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap22_http.so
    WebSpherePluginConfig /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
    ```
    {: codeblock}  
4. これらの 2 つのコマンドで、ポートを開きます。

  ```
   export serverPorts=2810:TCP,2810:UDP,8880:TCP,8880:UDP,9101:TCP,9101:UDP,9061:TCP,9061:UDP,9080:TCP,9080:UDP,9354:TCP,9354:UDP,9044:TCP,9044:UDP,9443:TCP,9443:UDP,5060:TCP,5060:UDP,5061:TCP,5061:UDP,11005:TCP,11005:UDP,11007:TCP,11007:UDP,9633:TCP,9633:UDP,7276:TCP,7276:UDP,7286:TCP,7286:UDP,5558:TCP,5558:UDP,5578:TCP,5578:UDP

   sudo /opt/IBM/WebSphere/AppServer/virtual/bin/openFirewallPorts.sh -ports $serverPorts -persist true
  ```
    {: codeblock}
5. 以下の 2 つのコマンドで、Web サーバーを停止し、始動します。
    ```
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k stop
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k start
    ```
    {: codeblock}
8. プラグインを使用してアプリケーションにアクセスします。
  ```
   http://169.53.246.xxx/contextRoot/
  ```
  {: codeblock}

**注:** Web サーバーを構成しようとしている場合、ここで提供されているステップは、数多くのパスのうちの 1 つを表しています。さらに支援が必要な場合は、[IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/search/configure%20web%20server?scope=SSAW57_9.0.0){: new_window} を参照してください。

**注:** アプリケーションにアクセスできない場合は、ファイアウォールでポート・アクセスの問題が発生していることが考えられます。このため、アプリケーション・サーバー、ノード・エージェント、Web サーバー、デプロイメント・マネージャーのうちいずれかのサーバーを再始動する必要がある可能性があります。また、WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のサービス・ダッシュボードにアクセスしてそれぞれの仮想マシンを再始動する必要がある場合もあります。

## SSL 構成
{: #ssl_configuration}

従来の WebSphere Application Server および Liberty プロファイルは、[SSL_TLSv2](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/protocols.html){: new_window} プロトコルで構成されています。プロトコルを変更するには、以下のファイルを変更します。

従来の WebSphere Application Server:

1. /opt/IBM/WebSphere/Profiles/*profile_name*/config/cell/*cell_name* 内の **security.xml** を編集して次の行を変更します。

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}

2. /opt/IBM/WebSphere/Profiles/*profile_name*/properties 内の **ssl.client.props** を編集して次の行を変更します。

  ```
  com.ibm.ssl.protocol=SSL_TLSv2
  ```
{: codeblock}

Liberty プロファイル:

1. /opt/IBM/WebSphere/Profiles/Liberty/servers/server1 内の **server.xml** を編集し、defaultSSLConfig ssl 構成エレメントにある次の行を変更します。

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}
