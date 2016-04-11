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

アプリケーションを含んでいるサーバー・パッケージを、単一インスタンスに制限してプッシュします。server.xml ファイルには、monitor-1.0 フィーチャーおよび restConnector-1.0 フィーチャーが含まれていなければなりません。また、basicRegistry エレメントおよび administrator-role エレメントも含まれている必要があります。
<pre>
       &lt;featureManager&gt;
    	   &lt;feature&gt;jsp-2.2&lt;/feature&gt;
    	   &lt;feature&gt;monitor-1.0&lt;/feature&gt;
    	   &lt;feature&gt;restConnector-1.0&lt;/feature&gt;
       &lt;/featureManager&gt;

       &lt;basicRegistry&gt;
    	   &lt;user name="jconuser" password="jconpassw0rd"/&gt;
       &lt;/basicRegistry&gt;

       &lt;administrator-role&gt;
    	   &lt;user&gt;jconuser&lt;/user&gt;
       &lt;/administrator-role&gt;
</pre>
{: #codeblock}

   * 注: パスワードは、Liberty によって提供される securityUtility ツールを使用してエンコードする必要があります。

### JConsole アプリケーションの開始
{: #start_jconsole_app}

JConsole は Java インストールに含まれています。JConsole アプリケーションを開始するには、<java-home>/bin (Java 1.7 以上) に移動し、次のコマンドを実行します。
<pre>
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
</pre>
{: #codeblock}

  * ほとんどの場合に機能するトラストストア・パラメーターのデフォルトを以下に示します。
<pre>
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/acerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
</pre>
{: #codeblock}
  * 必要な場合は、トラストストアに関するパラメーターに適切な値を指定してください。

### 接続の実行
{: #start_jconsole_app}
  * 次の URL を「リモート・プロセス」フィールドに入力します。    
    * service:jmx:rest://<appName>.mybluemix.net:443/IBMJMXConnectorREST  
  *  「ユーザー名」フィールドと「パスワード」 フィールドに、server.xml ファイルからの administrator-role ロールのユーザーとパスワードを指定します。
  * 「接続」をクリックします。

接続が成功すると、JConsole はモニターを開始します。

接続が失敗する場合、問題の診断に役立てるためにログを生成できます。
最初に、jconsole コマンドに **-J-Djava.util.logging.config.file=c:/tmp/logging.properties** を追加することによって、クライアント・サイドのトレースを収集してみてください。ロギング・プロパティー・ファイルのサンプルを以下に示します。

<pre>
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST
</pre>
{: #codeblock}

jconsole コマンドに <b>&dash;J&dash;Djavax.net.debug=ssl</b> を追加することもできます。そうすると、別の JConsole 出力ウィンドウに SSL 診断トレースが生成されます。最後に、以下を server.xml ファイルに追加することにより、サーバー・サイドでトレースを有効にすることができます。
<pre>
    &lt;logging traceSpecification="com.ibm.ws.jmx.&ast;=all"/&gt;
</pre>
{: codeblock}

# 関連リンク
## 一般
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
