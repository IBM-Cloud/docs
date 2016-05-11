---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# JConsole を使用した Bluemix での Liberty のモニタリング
{: #jconsole}

*最終更新日時: 2016 年 3 月 23 日*

## JConsole を使用して Bluemix Liberty ランタイムをモニターする手順は以下のとおりです。
{: #steps_to_monitor}

1. 適切な server.xml を含むサーバー・パッケージ内のアプリケーションをプッシュします。
2. 適切なシステム・プロパティーを指定してコマンド・ラインで JConsole アプリケーションを開始します。
3. 正しいリモート・プロセス url、ユーザー名、および パスワードを JConsole に対して指定します。

### サーバー・パッケージのプッシュ
{: #push_server_package}

アプリケーションを含んでいるサーバー・パッケージを、単一インスタンスに制限してプッシュします。server.xml ファイルには ``monitor-1.0`` フィーチャーおよび ``restConnector-1.0` フィーチャーが含まれている必要があります。また、basicRegistry エレメントおよび administrator-role エレメントも含まれている必要があります。```xml
       <featureManager>
           <feature>jsp-2.2</feature>
           <feature>monitor-1.0</feature>
           <feature>restConnector-1.0</feature>
       </featureManager>

       <basicRegistry>
           <user name="jconuser" password="jconpassw0rd"/>
       </basicRegistry>

       <administrator-role>
           <user>jconuser</user>
       </administrator-role>
```
{: #codeblock}

   * 注: パスワードは、Liberty によって提供される securityUtility ツールを使用してエンコードする必要があります。

### JConsole アプリケーションの開始
{: #start_jconsole_app}

JConsole は Java インストール済み環境に含まれています。JConsole アプリケーションを開始するには、&lt;java-home&gt;/bin に移動し、次のコマンドを実行します。
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar```
{: #codeblock}

Java trustStore を構成するために追加のパラメーターを渡さなければならない場合があります。次のパラメーターはほとんどの場合に機能します。
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks```
{: #codeblock}

### 接続の実行
{: #start_jconsole_app}
  * 次の URL を「リモート・プロセス」フィールドに入力します。
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST
  *  「ユーザー名」フィールドと「パスワード」 フィールドに、server.xml ファイルからの administrator-role ロールのユーザーとパスワードを指定します。
  * 「接続」をクリックします。

接続が成功すると、JConsole はモニターを開始します。

接続が失敗する場合、問題の診断に役立てるためにログを生成できます。
最初に、jconsole コマンドに **-J-Djava.util.logging.config.file=c:/tmp/logging.properties** を追加することによって、クライアント・サイドのトレースを収集してみてください。ロギング・プロパティー・ファイルのサンプルを以下に示します。```
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST```
{: #codeblock}

jconsole コマンドに <b>&dash;J&dash;Djavax.net.debug=ssl</b> を追加することもできます。そうすると、別の JConsole 出力ウィンドウに SSL 診断トレースが生成されます。最後に、以下を server.xml ファイルに追加することにより、サーバー・サイドでトレースを有効にすることができます。```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# 関連リンク
## 一般
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
