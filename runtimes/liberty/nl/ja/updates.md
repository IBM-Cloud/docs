---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty ビルドパックに対する最新の更新
{: #latest_updates}

## Liberty ビルドパックの最新更新のリスト。

### 2016 年 11 月 1 日: Liberty ビルドパック v3.4.1-20161030-2241 の更新
* このビルドパックには、特定のタイプのアプリケーションの開始に関する問題の修正が含まれています。具体的には、アプリケーションがサーバー・ディレクトリーまたはパッケージされたサーバーとしてデプロイされ、アプリケーション・ファイルが `dropins` ディレクトリーにある場合です。

### 2016 年 10 月 21 日: Liberty ビルドパック v3.4-20161018-2004 の更新
* デフォルトの Liberty ランタイム・バージョン `16.0.0.3` が、[PI68805](http://www-01.ibm.com/support/docview.wss?uid=swg1PI68805) および [PI69141](http://www-01.ibm.com/support/docview.wss?uid=swg1PI69141) の iFix を含むように更新されました。 
* 月次 Liberty ランタイム・バージョンが [2016.9.0.1](https://developer.ibm.com/wasdev/blog/2016/09/23/beta-websphere-liberty-and-tools-october-2016/) リリースに更新されました。 
* このビルドパックには、更新されたバージョンの IBM JRE 8.0: SR3 FP12 も含まれています。
* IBM JRE 8.0 および 7.1 は、Oracle の JRE の動作に一致させるために、[`SSLContext.getContext("TLS")` の呼び出し時にすべての TLS プロトコル](https://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/matchsslcontext_tls.html)を有効に構成するようになりました。また、IBM JRE 7.1 は、IBM の JRE 8.0 動作に一致させるために、[`SSLContext.getDefault()` の呼び出し時にすべての TLS プロトコル](https://www.ibm.com/support/knowledgecenter/SSYKE2_7.1.0/com.ibm.java.security.component.71.doc/security-component/jsse2Docs/overrideSSLprotocol.html)も有効に構成されます。
* このビルドパックでは、[Monitoring and Analytics サービス](/docs/services/monana/index.html#monana_oview)用の更新されたデータ・コレクターが提供されます。
* このビルドパックでは、[MySQL タイプのサービスの自動構成](autoConfig.html)の実行時に、最新の 1.5.x [MariaDB Connector/J JDBC ドライバー](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/)をダウンロードするように変更して元に戻されました。
* このビルドパックでは、`LBP_SERVICE_CONFIG_<serviceType>` 環境変数により、サービスの自動構成の動作のカスタマイズに対するサポートが導入されました。例えば、この環境変数を使用して、MySQL サービス用にダウンロードする JDBC ドライバーのロケーションやバージョンを変更できます。詳しくは、[自動構成をサポートするサービス](autoConfig.html)の資料を参照してください。 
* このビルドパックには、アプリケーションのヘルス・チェックおよび[アプリケーション管理 ](/docs/manageapps/app_mng.html)機能に関連した多数の [Diego](https://docs.cloudfoundry.org/concepts/diego/diego-architecture.html) の改善も含まれています。

### 2016 年 9 月 16 日: 更新された Liberty ビルドパック v3.3-20160912-1729
* デフォルトの Liberty ランタイム・バージョンが [16.0.0.3](http://www-01.ibm.com/support/docview.wss?uid=swg27009661) リリースに更新されました。月次 Liberty ランタイム・バージョンが [2016.9.0.0](https://developer.ibm.com/wasdev/blog/2016/08/26/beta-websphere-liberty-and-tools-september-2016/) リリースに更新されました。これらの更新によって、前にベータ・フィーチャーとして使用可能だった `cloudant-1.0` Liberty フィーチャーと `passwordUtilities-1.0` Liberty フィーチャーが、実動で使用可能なフィーチャーになりました。
* Liberty ランタイムの[セキュリティー修正](http://www-01.ibm.com/support/docview.wss?uid=swg21990527)が含まれています。
* このビルドパックには、更新されたバージョンの IBM JRE 8.0: SR3 FP11 も含まれています。
* このビルドパックは、最新の 1.5.x ドライバーの問題が原因で、[MySQL タイプのサービスの自動構成](autoConfig.html)を実行したときに最新の 1.4.x [MariaDB Connector/J JDBC ドライバー](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/)をダウンロードするように調整されました。

### 2016 年 8 月 26 日: 更新された Liberty ビルドパック v3.2-20160822-2200
* このビルドパックには、IBM JRE: 8 SR3 FP10 および 7.1 SR3 FP50 の更新版が含まれています。
* 月次 Liberty ランタイム・バージョンが [2016.8.0.0](https://developer.ibm.com/wasdev/blog/2016/07/28/beta-websphere-liberty-and-tools-august-2016/) リリースに更新されました。
* [SQL Database](/docs/services/SQLDB/index.html#SQLDB) サービス用の[自動構成サポート](autoConfig.html)を提供するサービス・プラグインは、TLS を介したサービスへの接続時に常に JVM のトラステッド証明書を使用するように更新されました。

### 2016 年 7 月 22 日: 更新された Liberty ビルドパック v3.1-20160717-2254
* [アプリケーション管理](/docs/manageapps/app_mng.html)機能が更新され、フェデレーテッド認証をサポートするようになりました。また、`devconsole` ユーティリティーと `shell` ユーティリティーによって使用される Node.js ランタイムが、最新バージョンの `0.12.15` に更新されました。 
* このビルドパックは、[Dynatrace Ruxit](http://www.dynatrace.com/en/ruxit/) アプリケーション・モニター・エージェントに対するサポートを追加します。
* このビルドパックでは、[Monitoring and Analytics サービス](/docs/services/monana/index.html#monana_oview)用の更新されたデータ・コレクターが提供されます。
* このビルドパックでは、[Auto-Scaling サービス](/docs/services/Auto-Scaling/index.html)用の更新版のエージェントも提供されます。 
* 月次 Liberty ランタイム・バージョンが [2016.7.0.0](https://developer.ibm.com/wasdev/blog/2016/06/30/beta-websphere-liberty-and-tools-july-2016/) リリースに更新されました。

### 2016 年 6 月 17 日: 更新された Liberty ビルドパック v3.0-20160608-1450
* ビルドパックには、WebSphere Liberty の 2 つのバージョン (最新の安定リリースと最新の月次リリース) が含まれるようになりました。具体的には、[16.0.0.2](http://www-01.ibm.com/support/docview.wss?uid=swg21984970) 安定リリースと [2016.6.0.0](https://developer.ibm.com/wasdev/blog/2016/06/03/beta-websphere-liberty-and-tools-june-2016/) 月次リリースが提供されます。デフォルトでは、安定リリースが使用されます。詳しくは、[『Liberty のバージョン』](buildpackDefaults.html#liberty_versions)を参照してください。 
* このビルドパックには、[Apache Standard Taglibs の脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21985531)に対するセキュリティー・フィックスも含まれています。

### 2016 年 5 月 25 日: 更新された Liberty ビルドパック v2.9-20160519-1249
* このビルドパックには、[May beta](https://developer.ibm.com/wasdev/blog/2016/05/06/beta-websphere-liberty-and-tools-may-2016/) に基づく更新版の WebSphere Liberty が含まれています。この更新版の Liberty により、*bluemixLogCollector-1.1* および *logstashCollector-1.1* の各ベータ・フィーチャーが Bluemix で使用可能になります。

### 2016 年 5 月 5 日: 更新された Liberty ビルドパック v2.8-20160430-1011
* このビルドパックには、[April beta](https://developer.ibm.com/wasdev/blog/2016/04/08/beta-websphere-liberty-and-tools-april-2016/) に基づく更新版の WebSphere Liberty が含まれています。この更新版の Liberty により、*logstashCollector-1.0* GA フィーチャーおよび *logmetCollector-1.0* ベータ・フィーチャーが Bluemix で使用可能になります。
* このビルドパックには、IBM JRE: 8 SR3 および 7.1 SR3 FP40 の更新版も含まれています。 
* このビルドパックは、[AppDynamics](https://www.appdynamics.com/) アプリケーション・モニター・エージェントに対する初期サポートを追加します。
* [Dynatrace](dynatrace.html) サポートは、エージェントのインストールを簡素化するように改善されました。
* このビルドパックでは、[Monitoring and Analytics サービス](/docs/services/monana/index.html#monana_oview)用の更新されたデータ・コレクターが提供されます。これには、最大ヒープ・データの収集に関する問題の修正が含まれています。
* [アプリケーション管理ユーティリティー devconsole および shell](/docs/manageapps/app_mng.html#app_management) によって使用される Node.js ランタイムは、最新の 0.12.13 バージョンに更新されました。

### 2016 年 3 月 25 日: 更新された Liberty ビルドパック v2.7-20160321-1358
* このビルドパックには、[March beta](https://developer.ibm.com/wasdev/blog/2016/03/18/new-websphere-liberty-features-march-2016/) に基づく更新版 WebSphere Liberty が含まれています。
Liberty の更新版により、cloudant-1.0 ベータ・フィーチャーが Bluemix で使用可能になります。
* このビルドパックには、IBM JRE: 8 SR2 FP12 および 7.1 SR3 FP32 の更新版も含まれています。 
* このビルドパックは、[Auto-Scaling サービス](/docs/services/Auto-Scaling/index.html)用のエージェントの更新版を提供します。 
* このビルドパックには、[Monitoring and Analytics サービス](/docs/services/monana/index.html#monana_oview)用の新しいデータ収集機能が付属しています。新しいコレクターにより、モニタリングしきい値の構成が可能になります。このコレクターにはいくつかのバグ修正が含まれています。
* このビルドパックは、更新された DB2® JDBC ドライバー・バージョン 4.19.49 を提供します。 
* [アプリケーション管理ユーティリティー devconsole および shell](/docs/manageapps/app_mng.html#app_management) によって使用される Node.js ランタイムは最新の 0.12.12 バージョンに更新されました。

### 2016 年 3 月 7 日: 更新された Liberty ビルドパック v2.6-20160225-1649
* このビルドパックは、Dynatrace アプリケーション・モニタリングのサポートを追加します。詳しくは、[『Dynatrace の使用』](dynatrace.html)を参照してください。
* このビルドパックは、[DynamicPULSE](www.fujitsu.com/jp/group/fsweb/products/dynamic-pulse/) のサポートを追加します。

### 2016 年 2 月 10 日: 更新された Liberty ビルドパック v2.5-20160209-1336
* このビルドパックには、[February beta](https://developer.ibm.com/wasdev/blog/2016/02/12/beta-websphere-liberty-and-tools-february/) に基づく更新版 WebSphere Liberty が含まれています。この更新版 Liberty プロファイルは、Bluemix で apiDiscovery-1.0 GA フィーチャーを使用可能にします。

### 2016 年 2 月 4 日: 更新された Liberty ビルドパック v2.4-20160127-1437
* このビルドパックには、January beta に基づく更新版 WebSphere Liberty が含まれています。この更新により、以前にベータ・フィーチャーとして使用可能だった scim-1.0 Liberty フィーチャーが、実動対応フィーチャーとして使用可能になりました。また、Liberty の更新版により、passwordUtilities-1.0 ベータ・フィーチャーが Bluemix で使用可能になります。
* このビルドパックには、更新された IBM JRE 7.1 SF3 FP20 および IBM JRE 8 SR2 FP10 も含まれています。
* このビルドパックは、[MySQL タイプのサービスの自動構成](autoConfig.html)を実行したときに最新の 1.x [MariaDB Connector/J JDBC ドライバー](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/)をダウンロードするように更新されました。

### 2015 年 12 月 16 日: 更新された Liberty ビルドパック v2.3-20151208-1311
* このビルドパックには、[December beta](https://developer.ibm.com/wasdev/blog/2015/11/20/beta-was-liberty-beta-with-tools-december-2015/) に基づく更新版 Liberty プロファイルが含まれています。この更新版 Liberty プロファイルは、Bluemix で spnego-1.0 および wsSecuritySaml-1.1 の GA フィーチャーおよび scim-1.0 ベータ・フィーチャーを使用可能にします。
* このビルドパックには、更新された IBM JRE 8 SR2 も含まれています。
* このビルドパックはまた、PostgreSQL または MySQL タイプのサービスの[自動構成](autoConfig.html)を実行したときに最新の [9.4.x PostgreSQL JDBC ドライバー](https://jdbc.postgresql.org/)および 1.2.x [MariaDB Connector/J JDBC ドライバー](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/)をダウンロードするように更新されました。

### 2015 年 11 月 23 日: 更新された Liberty ビルドパック v2.2-20151119-1720
* このビルドパックには、[Apache Commons Collection の脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21971426)に対するセキュリティー修正の適用された、Liberty プロファイル・ランタイムおよび WebSphere eXtreme Scale Client の更新版が含まれています。
* このビルドパックには、[Java MongoDB Driver](https://docs.mongodb.org/ecosystem/drivers/java/) の更新版、v2.13.3 も含まれています。この新しいドライバーは、MongoDB バージョン 2.4、2.6、および 3.0 と互換性があります。
* このビルドパックでは、[Monitoring and Analytics サービス](/docs/services/monana/index.html)用のデータ・コレクターの更新版も提供されています。更新されたデータ・コレクターには、改善されたメソッド・トレース機能があります。

### 2015 年 10 月 16 日: 更新された Liberty ビルドパック v2.1-20151006-0912
* このビルドパックには、[October beta](https://developer.ibm.com/wasdev/blog/2015/09/25/beta-was-liberty-beta-with-tools-october-2015/) に基づく更新版 Liberty プロファイルが含まれています。この更新によって、前にベータ・フィーチャーとして使用可能だった Liberty フィーチャー bells-1.0、rtcomm-1.0、rtcommGateway-1.0、samlWeb-2.0、sipServlet-1.1 が、実動で使用可能なフィーチャーになりました。
* このビルドパックには、更新された IBM JRE 8 SR1 FP11 も含まれています。
* このビルドパックでは、次のような多くのパフォーマンス改善および最適化も行われました。
  * [CDI 1.2](optionsForPushing.html) 暗黙的 Bean アーカイブのスキャン機能は、WAR ファイルまたは EAR ファイルをデプロイする場合はデフォルトで使用不可にされます。
  * ドロップレットのサイズを削減するため、[アプリケーション管理ユーティリティー](/docs/manageapps/app_mng.html) devconsole および shell は、再始動の代わりに再ステージング操作を必要とします。
  * IBM JRE の共有クラス・キャッシュは、Bluemix 環境では再使用されていなかったため、使用不可にされます。

### 2015 年 9 月 18 日: 更新された Liberty ビルドパック v2.0-20150914-1535
* このビルドパックで導入された主な変更は次の 2 つです。
  * WAR ファイルおよび EAR ファイルのデフォルト構成では、Java EE 6 Web Profile フィーチャーではなく Java EE 7 Web Profile フィーチャーが使用可能にされます。
  * デフォルト Java バージョンはバージョン 7 ではなくバージョン 8 です。
* これらの変更の詳細とアプリケーションに与える可能性のある影響については、[Upcoming Liberty for Java buildpack changes](https://developer.ibm.com/bluemix/2015/09/08/upcoming-liberty-for-java-buildpack-changes/) blog post を参照してください。
* このビルドパックでは、JBP_CONFIG_LIBERTY 環境変数を介して appstate フィーチャーを使用不可にするための app_state 構成オプションの導入も行われました。appstate フィーチャーは、Cloud Foundry ヘルス・チェック処理と統合されて、Liberty アプリケーションが HTTP 要求を受信する前に完全に初期設定されることを確実にします。JBP_CONFIG_LIBERTY 環境変数を「app_state: false」に設定すると、appstate フィーチャーを使用不可にすることができます。

### 2015 年 9 月 4 日: 更新された Liberty ビルドパック v1.22-20150824-1104
* このビルドパックは、[HTTP_PROXY 環境変数および HTTPS_PROXY 環境変数](environmentVariables.html)をサポートします。設定されている場合、ビルドパックは、さまざまなビルドパック・コンポーネントをダウンロードするときに、これらの環境変数によって指定されたプロキシー・サーバーを使用します。

### 2015 年 8 月 19 日: 更新された Liberty ビルドパック v1.21-20150811-1342
* このビルドパックには、[August beta](https://developer.ibm.com/wasdev/blog/2015/07/30/beta-was-liberty-beta-with-tools-august-2015/) に基づく更新版 Liberty プロファイルが含まれています。この更新版 Liberty プロファイルは、新規[ベータ・フィーチャー](usingBetaFeatures.html)である bells-1.0、rtcommGateway-1.0、samlWebSso-2.0 を Bluemix で使用可能にします。

### 2015 年 7 月 31 日: 更新された Liberty ビルドパック v1.20.1-20150729-1255
* このビルドパックには、更新版の IBM JRE: 7.1 SR1 FP10 および 8 SR1 FP10 が含まれています。これらの更新版 JRE には [最新のセキュリティー・フィックス](http://www-01.ibm.com/support/docview.wss?uid=swg21964161)およびその他の改善が含まれています。
* [Cloudant NoSQL Database](/docs/services/Cloudant/index.html#Cloudant) サービス用の[自動構成サポート](autoConfig.html)を提供するサービス・プラグインは、サービスへの接続がセキュア・チャネルを介して確立されるように更新されました。

### 2015 年 7 月 21 日: 更新された Liberty ビルドパック v1.20-20150713-1450
* このビルドパックには、[8.5.5.6 リリース](https://developer.ibm.com/wasdev/blog/2015/06/25/java-ee-7-has-landed-in-was-liberty/)に基づく更新版 Liberty プロファイルが含まれています。このリリースでは、前にベータ・フィーチャーとして使用可能だったすべての Java EE 7 Liberty フィーチャーが、実動で使用可能なフィーチャーになりました。Bluemix でのポートに関する制限およびその他の制限のため、例えばリモート EJB など一部のフィーチャーは、プラットフォームで完全にはサポートされません。
* このビルドパックは、[distZip スタイル](https://docs.gradle.org/current/userguide/application_plugin.html)でパッケージされたアプリケーションを認識し、実行します。
* このビルドパックでは、新しい Liberty ランタイム・バージョンをサポートする [Monitoring and Analytics サービス](/docs/services/monana/index.html)および WebSphere eXtreme Scale Client 用にデータ・コレクターが更新されました。

### 2015 年 6 月 30 日: 更新された Liberty ビルドパック v1.19.1-20150622-1509
* このバージョンのビルドパックには、[LogJam 脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21961390)に対するセキュリティー・フィックス適用済みの更新された IBM JRE が含まれています。
* [New Relic](newRelic.html) エージェントはバージョン 3.17 に更新されました。この新バージョンでは Liberty プロファイル・ランタイムとの統合が改善されました。

### 2015 年 6 月 14 日: 更新された Liberty ビルドパック v1.19-20150608-1717
* このビルドパックには、開発コンソールおよび Web ベースのシェル・アクセスのサポートなど、アプリケーション管理機能に関する多くの機能拡張が含まれています。詳細については、[アプリケーション管理についての文書](/docs/manageapps/app_mng.html)を参照してください。
* このビルドパックでは、[Monitoring and Analytics サービス](/docs/services/monana/index.html)用の Liberty フィーチャーが検出されないという問題も修正されました。

### 2015 年 5 月 27 日: 更新された Liberty ビルドパック v1.18-20150519-1642
* このビルドパックには、[May beta](https://developer.ibm.com/wasdev/blog/2015/05/08/beta-liberty-and-tools-may-2015/) に基づく更新版 Liberty プロファイルが含まれています。

### 2015 年 5 月 5 日: 更新された Liberty ビルドパック v1.17-20150501-1729
* このビルドパックには、[April beta](https://developer.ibm.com/wasdev/blog/2015/04/10/announcing-liberty-beta-with-tools-aprilmay-2015/) に基づく更新版 Liberty プロファイルが含まれています。この更新によって、前にベータ・フィーチャーとして使用可能だった Liberty フィーチャー jsp-2.3、el-3.0、および jdbc-4.1 が、実動で使用可能なフィーチャーになりました。また、jsf-2.2、javaMail-1.5、webProfile-7.0、および javaee-7.0 などの追加 Java EE 7 フィーチャーが[ベータ・フィーチャー](usingBetaFeatures.html)として使用可能になりました。
* このビルドパックは、Java 8 のサポートを初めて提供します。デフォルト JRE は IBM JRE 7.1 のままですが、JBP_CONFIG_IBMJDK 環境変数を設定することによって、アプリケーションに対して IBM JRE 8 を使用可能にすることができます。OpenJDK のバージョンの構成もサポートされます。すべての詳細については、[JRE のカスタマイズ](customizingJRE.html)を参照してください。
* このビルドパックは、新しい JBP_CONFIG_LIBERTY 環境変数を提供します。これを使用すると、WAR ファイルまたは EAR ファイルをデプロイするときにアプリケーションに対して使用可能にされるデフォルトの Liberty フィーチャー・セットをオーバーライドできます。詳細については、[スタンドアロン・アプリケーション](optionsForPushing.html#stand_alone_apps)を参照してください。
* [Monitoring and Analytics サービス](/docs/services/monana/index.html)のサービス・プラグインが更新され、このサービスに対して生成されるログのサイズが削減されました。
* このバージョンのビルドパックでは、ドロップレットでのアプリケーション・ファイルのレイアウトが変更されました。ファイル構造の変更によってシンボリック・リンクの保守に関連する複雑さが軽減されました。変更によるアプリケーションへの影響はありません。

### 2015 年 4 月 15 日: 更新された Liberty ビルドパック v1.16-20150407-1737
* このバージョンのビルドパックには、[Bar Mitzvah 脆弱性に対するセキュリティー・フィックス](http://www-01.ibm.com/support/docview.wss?uid=swg21882777)適用済みの更新された IBM JRE 7.1-2.11 が含まれています。
* スタンドアロン WAR ファイルがデプロイされるときに、このビルドパックは、提供されている場合、組み込み **ibm-web-ext.xml** ファイル内に指定されたコンテキスト・ルートをアプリケーションのコンテキスト・ルートとして使用します。この変更によって、前はルート・コンテキストの下にデプロイされていたアプリケーションは、**ibm-web-ext.xml** ファイル内の設定に基づいて、異なるコンテキストの下にデプロイされる可能性があります。

### 2015 年 4 月 3 日: 更新された Liberty ビルドパック v1.15-20150402-1422
* このビルドパックには、[March beta](https://developer.ibm.com/wasdev/blog/2015/03/13/announcing-liberty-beta-tools-march-2015/) に基づく更新版 Liberty プロファイルが含まれています。この更新版 Liberty プロファイルは、Bluemix で jsf-2.2 ベータ・フィーチャーを使用可能にします。
* このビルドパックには、[Monitoring and Analytics サービス](/docs/services/monana/index.html)用の更新版データ・コレクターも含まれています。

### 2015 年 3 月 20 日: 更新された Liberty ビルドパック v1.14-20150319-1159
* このバージョンのビルドパックには、[FREAK 脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21699864)に対するセキュリティー・フィックス適用済みの更新された IBM JRE 7.1.2.11 が含まれています。
* [SQL Database](services/SQLDB/index.html#SQLDB) サービスは、SSL プロトコルを介してデータベース・サーバーと接続するオプションのある有料プランを提供します。ビルドパックの SQL Database サービス自動構成サポートが更新され、SSL 接続情報が使用可能な場合は SSL を介してデータベースと接続するようランタイムを構成するようになりました。
* このビルドパックは、アプリケーション・アーカイブのルートに **server.xml ** 構成ファイルを含んでいるスタンドアロン WAR ファイルまたは EAR ファイルがデプロイされたらエラーを報告するように更新されました。
* このビルドパックには、特定のケースでは無効な **server.xml** 構成を生成することがあった MongoDB の自動構成サービス・プラグインに対する修正が含まれています。

### 2015 年 2 月 10 日: 更新された Liberty ビルドパック v1.13-20150209-1122
* このビルドパックには、[Apache HttpComponents および Java オーバーレイ機能の脆弱性](https://www-304.ibm.com/connections/blogs/PSIRT/entry/ibm_security_bulletin_multiple_vulnerabilities_fixed_in_liberty_for_java_for_ibm_bluemix_cve_2012_6153_cve_2014_3577_cve_2015_0178?lang=en_us)に対するセキュリティー・フィックスが含まれています。
* このビルドパックには、[February beta](https://developer.ibm.com/wasdev/blog/2015/02/13/announcing-liberty-beta-tools-february-2015/) に基づく更新版 Liberty プロファイルが含まれています。この更新版 Liberty プロファイルは、更新版の WebSocket GA フィーチャー websocket-1.1 を提供します。また、以下の Java EE 7 ベータ・フィーチャーが Bluemix で使用可能になりました。
  * cdi-1.2、el-3.0、jsp-2.3、jca-1.7、jacc-1.5、および jaspic-1.1 
* このビルドパックにより、[ZeroTrunaround の JRebel ツール](http://zeroturnaround.com/software/jrebel/)と統合されます。この統合によって、Bluemix アプリケーションでの JRebel の使用、およびアプリケーションの再デプロイまたは再ステージングなしでのアプリケーションの即時更新が簡単に実行できるようになります。スタンドアロン Web アプリケーションのみがサポートされます。

### 2015 年 2 月 6 日: 更新された Liberty ビルドパック v1.12-20150130-1016
* このビルドパックには、[January beta](https://developer.ibm.com/wasdev/blog/2015/01/16/announcing-liberty-beta-tools-january-2015/) に基づく更新版 Liberty プロファイルが含まれています。
* このビルドパックには、[Monitoring and Analytics サービス](/docs/services/monana/index.html#gettingstartedtemplate)用のトリム版データ・コレクターが含まれています。

### 2015 年 1 月 23 日: 更新された Liberty ビルドパック v1.11-20150119-1511
* このビルドパックには、更新された IBM JRE バージョン 7.1 SR2 FP1 が含まれています。
* また、更新された WebSphere eXterme Scale Client バージョン 8.6.0.6、および、Auto-Scaling サービス用の更新されたエージェントも含まれています。
* [New Relic](newRelic.html) サービスのサポートが、ユーザー定義サービスをサポートするように拡張されました。
* このビルドパックは、Liberty プロファイルおよび IBM JRE の詳細なバージョンを報告するように改善されました。

### 2014 年 12 月 19 日: 更新された Liberty ビルドパック v1.10-20141218-0103
* このビルドパックはアプリケーションの開発モードを提供します。開発モードは、以前は実行できなかったアプリケーション・インスタンスに関する多数のアクティビティーを開発者が実行できるようになる特別なモードです。このフィーチャーを使用することによって、このバージョンの IBM Eclipse Tools for Bluemix は、Bluemix で実行中の Liberty アプリケーションに対して増分ファイル更新を行うリモート・デバッグをサポートできるようになりました。これにより、Eclipse を使用する開発者が、クラウド内のアプリケーションのデバッグとそのアプリケーションへの即時の変更適用を行いやすくなりました。
* このビルドパックには、
[December
beta](https://developer.ibm.com/wasdev/blog/2014/12/10/announcing-liberty-beta-december/) に基づく Liberty プロファイルの更新版が含まれています。
* さらに、以前はベータ・フィーチャーだった以下の 4 つの Liberty フィーチャーが、実動に使用できるようになりました。
  * concurrent-1.0
  * jsonp-1.0
  * servlet-3.1
  * websocket-1.0.  
* このビルドパックは New Relic サービスとの統合を提供します。
アプリケーションが New Relic サービスにバインドされると、ビルドパックは New Relic エージェントと共にランタイムを自動的にダウンロードして構成します。
* このビルドパックには以下のような既知の制限があります。
  * 開発モードの場合、SessionCache サービスをバインドできません。
  * 開発モードの場合、スレッド・ダンプを作成できません。
  * servlet-3.1 または websocket-v1.0 フィーチャーを使用している場合、Monitoring & Analytics サービスをバインドできません。

### 2014 年 12 月 5 日: 更新された Liberty ビルドパック v1.9-20141202-0947
* このビルドパックは拡張 JVM オプションのサポートを提供します。再始動操作で JVM オプションが適用できるようになりました。アプリケーションの再ステージングは必要ありません。また、デフォルト JVM オプションは、高速障害に最適化されており、生成されたダンプを検出しやすくする共通ロケーションが事前構成されています。詳細は、[Custom Configuration of Java JVM for the Liberty Runtime article](https://developer.ibm.com/bluemix/2014/12/12/custom-configurations-java-jvm-liberty-runtime/) を参照してください。
* このビルドパックには更新された DB2 JDBC ドライバー、バージョン 4.17.29 が含まれています。
* Monitoring &
Analytics サービスの Liberty スレッド・プール使用情報の収集が妨げられ
る問題の修正も含まれています。

### 2014 年 11 月 21 日: 更新された Liberty ビルドパック v1.8-20141118-1610
* このビルドパックには、[POODLE 脆弱性](http://www-01.ibm.com/support/docview.wss?uid=swg21687173)の修正を提供する、更新された IBM JRE バージョン 7.1 SR2 が含まれています。
* また、
[November
beta](https://developer.ibm.com/wasdev/blog/2014/11/07/announcing-liberty-profile-beta-november/) に基づく Liberty プロファイルの更新版が含まれています。

### 2014 年 10 月 30 日: 更新された Liberty ビルドパック v1.7-20141020-1759
* このビルドパックには、更新された IBM JRE バージョン 7.1 SR1 FP3 が含まれています。
* また、Unicode 文字を含むサーバー構成でのアプリケーションのデプロイメントが妨げられる問題の修正も提供します。

### 2014 年 10 月 23 日: 更新された Liberty ビルドパック v1.6-20141013-1628
* このビルドパックには、[Monitoring and Analytics](/docs/services/monana/index.html) 用の新しいデータ収集機能が付属しています。この新規データ収集機能は、
診断用の詳細情報を収集し、サービスの診断プランのユーザーがユーザーのアプリケーションでの問題を特定行のコードまで探って診断することを可能にします。
* ビルドパックに含まれる管理および自動スケーリングのエージェントが更新され、バグ修正とマイナーな機能強化が行われました。
また、更新版の [Liberty プロファイル](https://developer.ibm.com/wasdev/)および [Java MongoDB Driver](https://docs.mongodb.org/ecosystem/drivers/java/) (v2.12.3) が含まれています。
* cloudAutowiring フィーチャーで、一部のアプリケーションでリソース・インジェクションのエラーの原因になっていたバグが修正されました。

### 2014 年 10 月 3 日: 更新された Liberty ビルドパック v1.5-20140923-1143
* 更新されたこのビルドパックでは、アプリケーションは、WebSocket 1.0、Servlet 3.1、および JAX-RS 2.0 を含めて、Liberty ベータ・フィーチャーを使用できるようになりました。詳しくは、[『ベータ・フィーチャーの使用』](usingBetaFeatures.html)を参照してください。

### 2014 年 9 月 30 日: 更新された Liberty ビルドパック v1.4-20140908-1803
* このビルドパックでは、ElephantSQL および ClearDB MySQL Database サード・パーティー・サービスをサポートするようになりました。自動構成サポートも posgresql および mysql 試験サービスと共に機能します。全部で 13 個の新規サービスと共に、Liberty ビルドパック内の自動構成サポートによって、Libertyアプリケーションでの Bluemix サービスの取り込みを素早く簡単にできるようになります。
* ビルドパックが実行する自動構成および他のアクションに関して、アプリケーションのステージング中にビルドパックが表示するログが改善されました。
* このビルドパックは、フィックスおよび機能強化が適用された更新版の Liberty プロファイルを含みます。
* また、パフォーマンスが改善された更新版の IBM JRE バージョン 7.1 を含みます。変更内容の詳細については、[新機能](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.71.doc/diag/preface/changes_71/changes.html)ページを参照してください。

### 2014 年 8 月 28 日: 更新された Liberty ビルドパックv1.3-20140818-1538
* ビルドパックは、最新のフィックスおよび機能強化が適用された更新版の [Liberty Profile](https://developer.ibm.com/wasdev/) を含みます。
* このバージョンのビルドパック・フィックスは、追加の JVM オプションをアプリケーション・ランタイムに渡すための JAVA_OPTS 環境変数をサポートします。
* また、Spring ベースのスタンドアロン Jar アプリケーションのデプロイメントを妨げていた問題を修正します。
* Bluemix UI を使用して IBM JVM スナップ・トレースを生成およびダウンロードできるようになりました。JVM によって生成されるスナップ・トレースまたは他の診断情報について詳しくは、IBM JVM 資料で[トラブルシューティングのトピック](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/troubleshooting.html)のトピックを参照してください。

### 2014 年 7 月 29 日: 更新された Liberty ビルドパック v1.1-20140725-1341
* Liberty の Bluemix Edition の新しいバージョンです。
  * このバージョンの Liberty では、新規フィーチャーに加えてフィックスがあり、Bluemix サービスをより効率的に取り込むことが可能になりました。
  * 新規 CouchDB フィーチャーを使用可能にすると、Cloudant® サービスは自動的にそれを構成でき、コネクター・オブジェクトを簡単に使用できるようになりました。VCAP_SERVICES の構文解析および ektorp の提供により、クライアント jar は不要になりました。
* IBM SDK for Java のバージョンが新しくなりました。
  * アプリケーションは、再プッシュされると IBM SDK for Java バージョン 7.1-1.0 を使用します。これに伴って性能が大幅に向上します。アプリケーションのスループットが改善され、メモリー使用量は減少します。IBM Java SDK について詳しくは、[ここ](http://www-01.ibm.com/support/docview.wss?uid=swg21671466)を参照してください。

# 関連リンク
{: #rellinks}
## 一般
{: #general}
  * [Liberty ランタイム](index.html)
  * [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
