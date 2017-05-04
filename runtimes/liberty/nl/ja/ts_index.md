---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Liberty for Java のトラブルシューティング
{: #ts}


ここでは、{{site.data.keyword.Bluemix_notm}} 上での Liberty for Java の使用に関する一般的なトラブルシューティングの質問に対する回答を示します。
{:shortdesc}

## アプリケーションが接続を受け入れて開始できない
{: #health_check_timeout}


Liberty アプリケーションを開始できず、「接続を受け入れて開始できませんでした (Failed to start accepting connections)」エラーが出されます。例えば、ログ内のエラーは、次のようになっています。{: tsSymptoms}

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698}
   2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```
{: #codeblock}

Bluemix は、アプリケーション上でヘルス・チェックを実行して、アプリケーションが正常に開始されたかどうかを確認します。このヘルス・チェックでは、アプリケーションがそのアプリケーションに割り当てられたポート上で listen しているかどうかをテストします。このチェックのデフォルトのタイムアウトは 60 秒ですが、アプリケーションによっては開始に 60 秒より長くかかることもあります。アプリケーションの開始に時間がかかる理由はさまざまです。例えば、[Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate) や [New Relic](/docs/runtimes/liberty/newRelic.html) といったサービスをバインドしたり、[デバッガーを有効化](/docs/manageapps/app_mng.html#debug)したりすると、開始時間は長くなります。また、そういったアプリケーションが、終了までに時間のかかる初期化ステップを実行している可能性もあります。
{: tsCauses}

最初に、ログを調べて Liberty アプリケーションが失敗する原因になった可能性のある明らかなエラーがないか確認します。明らかなエラーが見つからない場合は、以下を試みてください。{: tsResolve}

### **ヘルス・チェックのタイムアウト値を増やします。**

* 「cf push」コマンドを使用してアプリケーションをデプロイする際に、「-t」オプションを使用して、アプリケーションの開始タイムアウトをより長い値に指定します。例えば、以下のように指定します。

            $ cf push myApp -t 180
{: #codeblock}

* ヘルス・チェックのタイムアウトは、manifest.yml ファイルに指定することもできます。例えば、以下のように指定します。

        ---
           ...
           timeout: 180
{: #codeblock}

### **appstate フィーチャーを使用不可にします。**

appstate フィーチャーは、Bluemix ヘルス・チェック処理と統合されて、Liberty アプリケーションが HTTP 要求を受信する前に完全に初期設定されることを確実にします。アプリケーションの完全な初期化が完了すると、appstate フィーチャーの効力はなくなります。このフィーチャーの副次作用は、一部のアプリケーションの始動に長い時間がかかる場合があることです。appstate フィーチャーを使用不可にするには、アプリケーションで以下の環境プロパティーを設定し、アプリケーションを再ステージします。

```
   $ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```
{: #codeblock}

### **アプリケーションのリファクタリングを検討します。**

アプリケーションの初期化に長時間かかる場合、アプリケーションをリファクタリングして、遅延または非同期 (あるいは、その両方での) 初期化を行うことが必要になる可能性があります。

### **「no-route」オプションを指定してデプロイします。**

1. 「--no-route」オプションを指定してアプリケーションをデプロイします。これにより、ポートのヘルス・チェックが使用不可になります。例えば、以下のように指定します。

           $ cf push myApp –no-route
{: #codeblock}

2. アプリケーションが初期化された時点で、ルートをアプリケーションにマップします。例えば、以下のように指定します。

           $ cf map-route myApp mybluemix.net
{: #codeblock}

## IBM のゲートウェイでの SSL エラー
{: #ssl_handshake_failure}


ログに次のようなエラーが表示され、アプリケーションの開始に失敗することがあります。{: tsSymptoms}

```
    2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
    2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  The signer might need to be added to local trust store /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks, located in SSL configuration alias defaultSSLConfig.  The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is:
    2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is:
    2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: codeblock}

このエラーは、Monitoring & Analytics サービスが Liberty アプリケーションにバインドされた後、Liberty アプリケーションが、Liberty ssl-1.0 フィーチャーを構成する server.xml を含むサーバー・ディレクトリーまたはパッケージされたサーバーとしてデプロイされた場合に生成される可能性があります。Monitoring & Analytics サービスを Liberty アプリケーションにバインドすると、ランタイムはセキュア接続を介してサービスに接続するようになります。このセキュア接続はデフォルトの SSL 設定を使用して確立されます。デフォルトの SSL 設定は Liberty の server.xml に指定されており、構成済みトラストストアが Monitoring & Analytics サービスで使用される証明書を信頼していない場合があります。
{: tsCauses}

以下のいずれかのオプションを指定して JVM のトラストストアを使用するように、構成を変更します。変更を行った後、アプリケーションの再ステージングを忘れずに行ってください。
{: tsResolve}

### Liberty の server.xml を更新します

server.xml を更新し、トラストストアとして JVM の cacerts ファイルを使用するようにします。以下を server.xml に追加します。

        <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/>
        <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
        {: codeblock}

### 構成済みトラストストアを更新します

DigitCert ROOT CA を信頼するように、構成済みトラストストアを変更します。
  1. https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt から DigiCert Root CA をダウンロードします。
  2. トラストストアとして resources/security/key.jks が使用されると想定し、Java の keytool ユーティリティーを使用して CA をこの鍵にインポートします。

            $ keytool -importcert --storepass <keyStorePassword> -keystore &lt;path&gt;/resources/security/key.jks -file DigiCertGlobalRootCA.crt
{: codeblock}
