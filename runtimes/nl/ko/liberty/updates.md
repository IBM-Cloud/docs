---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty 빌드팩의 최신 업데이트
{: #latest_updates}

## Liberty 빌드팩의 최신 업데이트 목록

*마지막 업데이트 날짜: 2016년 3월 23일*

### 2016년 3월 25일: 업데이트된 Liberty 빌드팩 v2.7-20160321-1358
* 이 빌드팩에는 [3월 베타](https://developer.ibm.com/wasdev/blog/2016/03/18/new-websphere-liberty-features-march-2016/)를 기반으로 하는 WebSphere Liberty의 업데이트된 버전이 포함되어 있습니다. Liberty의 업데이트된 버전을 이용하면 cloudant-1.0 베타 기능을 Bluemix에서 사용할 수 있습니다. 
* 또한 이 빌드팩에는 IBM JRE: 8 SR2 FP12 및 7.1 SR3 FP32의 업데이트된 버전이 포함되어 있습니다. 
* 이 빌드팩은 [Auto-Scaling 서비스](../../services/Auto-Scaling/index.html)를 위해 업데이트된 버전의 에이전트를 제공합니다.  
* 이제 이 빌드팩에 [Monitoring and Analytics 서비스](../../services/monana/index.html#monana_oview)를 위한 새로운 데이터 콜렉터가 제공됩니다. 새 콜렉터를 사용하면 모니터링 임계값을 구성할 수 있으며 몇 가지 버그 수정이 포함됩니다. 
* 이 빌드팩은 업데이트된 DB2® JDBC 드라이버 버전 4.19.49를 제공합니다. 
* [devconsole 및 shell App Management 유틸리티](../../manageapps/app_mng.html#app_management)에서 사용되는 Node.js 런타임이 최신 0.12.12 버전으로 업데이트되었습니다. 

### 2016년 3월 7일: 업데이트된 Liberty 빌드팩 v2.6-20160225-1649
* 이 빌드팩은 Dynatrace 애플리케이셔 모니터링에 대한 지원을 추가합니다. 자세한 내용은 [Dynatrace 사용](dynatrace.html)을 참조하십시오. 
* 이 빌드팩은 [DynamicPULSE](www.fujitsu.com/jp/group/fsweb/products/dynamic-pulse/)에 대한 지원을 추가합니다.

### 2015년 2월 10일: 업데이트된 Liberty 빌드팩 v2.5-20160209-1336
* 이 빌드팩에는 [2월 베타](https://developer.ibm.com/wasdev/blog/2016/02/12/beta-websphere-liberty-and-tools-february/)를 기반으로 하는 WebSphere Liberty의 업데이트된 버전이 포함되어 있습니다. Liberty 프로파일의 업데이트된 버전을 이용하면 apiDiscovery-1.0 GA 기능을 Bluemix에서 사용할 수 있습니다. 

### 2015년 2월 4일: 업데이트된 Liberty 빌드팩 v2.4-20160127-1437
* 이 빌드팩에는 1월 베타를 기반으로 하는 ebSphere Liberty의 업데이트된 버전이 포함되어 있습니다. 이 업데이트로 이전에 베타 기능으로 사용 가능했던 scim-1.0 Liberty 기능이 이제 프로덕션-준비 기능으로 사용 가능합니다. 또한 Liberty의 업데이트된 버전을 이용하면 passwordUtilities-1.0 베타 기능을 Bluemix에서 사용할 수도 있습니다. 
* 이 빌드팩에는 업데이트된 IBM JRE 7.1 SF3 FP20 및 IBM JRE 8 SR2 FP10이 포함되어 있습니다. 
* 이 빌드팩은 [MySQL 유형 서비스에 대한 자동 구성](autoConfig.html) 수행 시 최신 1.x [MariaDB Connector/J JDBC 드라이버](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/)를 다운로드하도록 업데이트되었습니다. 

### 2015년 12월 16일: 업데이트된 Liberty 빌드팩 v2.3-20151208-1311
* 이 빌드팩에는 [12월 베타](https://developer.ibm.com/wasdev/blog/2015/11/20/beta-was-liberty-beta-with-tools-december-2015/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. Liberty 프로파일의 업데이트된 버전을 이용하면 spnego-1.0 및 wsSecuritySaml-1.1 GA 기능과 scim-1.0 베타 기능을 Bluemix에서 사용할 수 있습니다. 
* 또한 이 빌드팩에는 업데이트된 IBM JRE 8 SR2가 포함되어 있습니다. 
* 또한 이 빌드팩은 PostgreSQL 또는 MySQL 유형의 서비스에 대한 [자동 구성](autoConfig.html) 수행 시 최신 [9.4.x PostgreSQL JDBC 드라이버](https://jdbc.postgresql.org/) 및 1.2.x [MariaDB Connector/J JDBC 드라이버](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/)를 다운로드하도록 업데이트되었습니다. 

### 2015년 11월 23일: 업데이트된 Liberty 빌드팩 v2.2-20151119-1720
* 빌드팩에는 [Apache Commons Collection 취약성](http://www-01.ibm.com/support/docview.wss?uid=swg21971426)의 보안 수정사항이 포함된 WebSphere eXtreme Scale Client 및 Liberty 프로파일 런타임의 업데이트된 버전이 있습니다. 
* 빌드팩에는 [Java MongoDB Driver](https://docs.mongodb.org/ecosystem/drivers/java/), v2.13.3의 업데이트된 버전도 포함되어 있습니다. 새 드라이버는 MongoDB 버전 2.4, 2.6 및 3.0과 호환 가능합니다.
* 또한 이 빌드팩은 [Monitoring and Analytics 서비스](../../services/monana/index.html)에 대한 데이터 콜렉터의 업데이트된 버전도 제공합니다. 업데이트된 데이터 콜렉터에서는 메소드 추적 기능이 향상되었습니다. 

### 2015년 10월 16일: 업데이트된 Liberty 빌드팩 v2.1-20151006-0912
* 빌드팩에는 [10월 베타](https://developer.ibm.com/wasdev/blog/2015/09/25/beta-was-liberty-beta-with-tools-october-2015/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. 이 업데이트로 이전에는 베타 기능으로 사용 가능했던 bells-1.0, rtcomm-1.0, rtcommGateway-1.0, samlWeb-2.0, sipServlet-1.1 Liberty 기능이 이제 프로덕션-준비 기능으로 사용 가능합니다. 
* 이 빌드팩에는 업데이트된 IBM JRE 8 SR1 FP11이 포함되어 있습니다. 
* 또한 빌드팩에서 여러 성능 개선사항 및 최적화 기능도 제공합니다.
  * WAR 또는 EAR 파일을 배치할 경우 [CDI 1.2](optionsForPushing.html) 암시적 Bean 아카이브 스캔 기능이 기본적으로 사용하지 않도록 설정되어 있습니다.
  * 드롭릿(droplet) 크기를 줄이려면 [앱 관리 유틸리티](../../manageapps/app_mng.html) devconsole 및 shell에서 재시작 대신 다시 스테이징 작업이 필요합니다.
  * Bluemix 환경에서 다시 사용되지 않으므로 IBM JRE의 공유 클래스 캐시가 사용 안함으로 설정됩니다.

### 2015년 9월 18일: 업데이트된 Liberty 빌드팩 v2.0-20150914-1535
* 이 빌드팩에서는 다음과 같은 두 가지 주요 변경사항을 소개합니다.
  * WAR 및 EAR 파일에 대한 기본 구성에서 Java EE 6 웹 프로파일 기능 대신 Java EE 7 웹 프로파일 기능을 사용합니다.
  * 기본 Java 버전은 버전 7 대신 버전 8입니다.
* 이러한 변경사항 및 이 변경사항이 애플리케이션에 미치는 영향에 대한 자세한 내용은 [예정된 Liberty for Java 빌드팩 변경사항](https://developer.ibm.com/bluemix/2015/09/08/upcoming-liberty-for-java-buildpack-changes/) 블로그 게시를 참조하십시오.
* 이 빌드팩에서는 또한 JBP_CONFIG_LIBERTY 환경 변수를 통해 appstate 기능을 사용 안함으로 설정하는 app_state 구성 옵션을 소개합니다. appstate 기능은 Cloud Foundry 상태 검사 프로세스와 통합되어 Liberty 애플리케이션이 완전히 초기화되어야 HTTP 요청을 수신할 수 있도록 합니다. appstate 기능을 사용 안함으로 설정하려면 JBP_CONFIG_LIBERTY 환경 변수를 "app_state: false"로 설정합니다.

### 2015년 9월 4일: 업데이트된 Liberty 빌드팩 v1.22-20150824-1104
* 이 빌드팩은 [HTTP_PROXY 및 HTTPS_PROXY 환경 변수](environmentVariables.html)를 지원합니다. 설정된 경우 빌드팩은 다양한 빌드팩 컴포넌트를 다운로드할 때 이 환경 변수로 지정된 프록시 서버를 사용합니다.

### 2015년 8월 19일: 업데이트된 Liberty 빌드팩 v1.21-20150811-1342
* 이 빌드팩에는 [8월 베타](https://developer.ibm.com/wasdev/blog/2015/07/30/beta-was-liberty-beta-with-tools-august-2015/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. Liberty 프로파일의 업데이트된 버전을 이용하면 다음과 같은 새 [베타 기능](usingBetaFeatures.html)을 Bluemix: bells-1.0, rtcommGateway-1.0, samlWebSso-2.0에서 사용할 수 있습니다.

### 2015년 7월 31일: 업데이트된 Liberty 빌드팩 v1.20.1-20150729-1255
* 이 빌드팩에는 IBM JRE의 업데이트된 버전인 7.1 SR1 FP10 및 8 SR1 FP10이 포함되어 있습니다.
업데이트된 JRE는 [최신 보안 수정사항](http://www-01.ibm.com/support/docview.wss?uid=swg21964161)과 기타 개선사항을 포함하고 있습니다. 
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant) 서비스에 [자동 구성 지원](autoConfig.html)을 제공하는 서비스 플러그인이 보안 채널을 통해 서비스에 연결되도록 합니다.

### 2015년 7월 21일: 업데이트된 Liberty 빌드팩 v1.20-20150713-1450
* 빌드팩에는 [8.5.5.6 릴리스](https://developer.ibm.com/wasdev/blog/2015/06/25/java-ee-7-has-landed-in-was-liberty/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. 이 릴리스로 이전에는 베타 기능으로 사용 가능했던 모든 Java EE 7 Liberty 기능은 이제 프로덕션-준비 기능으로 사용 가능합니다. Bluemix의 포트 및 기타 제한사항 때문에, 일부 기능(예: 원격 EJB)은 플랫폼에서 완벽히 지원되지 않습니다. 
* 빌드팩은 [distZip-style](https://docs.gradle.org/current/userguide/application_plugin.html)에서 패키징된 애플리케이션을 인식하고 실행합니다. 
* 빌드팩에는 새 Liberty 런타임 버전을 지원하는 WebSphere eXtreme Scale Client 및 [Monitoring and Analytics 서비스](../../services/monana/index.html)에 대한 업데이트된 데이터 콜렉터가 포함됩니다. 

### 2015년 6월 30일: 업데이트된 Liberty 빌드팩 v1.19.1-20150622-1509
* 이 빌드팩 버전에는 [LogJam 취약성](http://www-01.ibm.com/support/docview.wss?uid=swg21961390)에 대한 보안 수정사항이 있는 업데이트된 IBM JRE가 포함됩니다. 
* [New Relic](newRelic.html) 에이전트는 버전 3.17로 업데이트되었습니다. 새 버전은 Liberty 프로파일 런타임과의 개선된 통합을 제공합니다. 

### 2015년 6월 14일: 업데이트된 Liberty 빌드팩 v1.19-20150608-1717
* 빌드팩에는 개발 콘솔 및 웹 기반 쉘 액세스에 대한 지원을 포함하여 다수의 애플리케이션 관리 개선사항이 포함되어 있습니다. 자세한 내용은 [앱 관리 문서](../../manageapps/app_mng.html)를 참조하십시오. 
* 빌드팩에는 [ Monitoring and Analytics 서비스](../../services/monana/index.html)의 Liberty 기능을 찾을 수 없는 문제점에 대한 수정사항도 포함되어 있습니다. 

### 2015년 5월 27일: 업데이트된 Liberty 빌드팩 v1.18-20150519-1642
* 빌드팩에는 [5월 베타](https://developer.ibm.com/wasdev/blog/2015/05/08/beta-liberty-and-tools-may-2015/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. 

### 2015년 5월 5일: 업데이트된 Liberty 빌드팩 v1.17-20150501-1729
* 빌드팩에는 [4월 베타](https://developer.ibm.com/wasdev/blog/2015/04/10/announcing-liberty-beta-with-tools-aprilmay-2015/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. 이 릴리스로 이전에는 베타 기능으로 사용 가능했던 jsp-2.3, el-3.0 및 jdbc-4.1 Liberty 기능이 이제 프로덕션-준비 기능으로 사용 가능합니다. 또한 추가 Java EE 7 기능(예: jsf-2.2, javaMail-1.5, webProfile-7.0 및 javaee-7.0)가 이제 [베타 기능](usingBetaFeatures.html)으로 사용 가능합니다. 
* 이 빌드팩은 Java 8에 대한 초기 지원도 제공합니다. IBM JRE 7.1은 기본 JRE를 유지하지만, IBM JRE 8은 JBP_CONFIG_IBMJDK 환경 변수를 설정하여 애플리케이션에 대해 사용이 가능합니다. OpenJDK의 구성 버전도 지원됩니다. 자세한 내용은 [JRE 사용자 정의](customizingJRE.html)를 참조하십시오. 
* 빌드팩은 WAR 또는 EAR 파일을 배치할 때 애플리케이션에 대해 사용되는 기본 Liberty 기능 설정을 대체하기 위해 사용될 수 있는 새 JBP_CONFIG_LIBERTY 환경 변수를 제공합니다. 자세한 정보는 [독립형 애플리케이션](optionsForPushing.html#stand_alone_apps)을 참조하십시오. 
* [Monitoring and Analytics Service](../../services/monana/index.html)의 서비스 플러그인은 서비스에 대해 생성되는 로그의 크기를 줄일 수 있도록 업데이트되었습니다. 
* 이 빌드팩 버전에서는 애플리케이션 파일이 드롭릿(droplet)에서 레이아웃되는 방법이 변경되었습니다. 파일 구조가 변경되어 기호 링크의 유지보수와 관련된 복잡도가 제거되었으며, 이 변경으로 인해 애플리케이션에는 영향이 없어야 합니다. 

### 2015년 4월 15일: 업데이트된 Liberty 빌드팩 v1.16-20150407-1737
* 이 빌드팩 버전에는 [Bar Mitzvah 취약성에 대한 보안 수정사항](http://www-01.ibm.com/support/docview.wss?uid=swg21882777)이 있는 업데이트된 IBM JRE 7.1-2.11이 포함되어 있습니다. 
* 독립형 WAR 파일을 배치할 때 제공된 경우에는 빌드팩에서 이제 애플리케이션의 컨텍스트 루트로서 임베디드 **ibm-web-ext.xml** 파일에 지정된 컨텍스트 루트를 사용합니다. 이 변경사항으로, 이전에 루트 컨텍스트 하에서 배치된 애플리케이션은 **ibm-web-ext.xml** 파일의 설정을 기반으로 다른 컨텍스트 하에서 배치될 수 있습니다. 

### 2015년 4월 3일: 업데이트된 Liberty 빌드팩 v1.15-20150402-1422
* 빌드팩에는 [3월 베타](https://developer.ibm.com/wasdev/blog/2015/03/13/announcing-liberty-beta-tools-march-2015/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. Liberty 프로파일의 업데이트된 버전을 이용하면 jsf-2.2 베타 기능을 Bluemix에서 사용할 수 있습니다. 
* 빌드팩에는 [Monitoring and Analytics 서비스](../../services/monana/index.html)에 대한 데이터 콜렉터의 업데이트된 버전도 포함되어 있습니다. 

### 2015년 3월 20일: 업데이트된 Liberty 빌드팩 v1.14-20150319-1159
* 이 빌드팩 버전에는 [FREAK 취약성](http://www-01.ibm.com/support/docview.wss?uid=swg21699864)에 대한 보안 수정사항이 있는 업데이트된 IBM JRE 7.1.2.11이 포함되어 있습니다.
* [ SQL Database](services/SQLDB/index.html#SQLDB) 서비스는 SSL 프로토콜에서 데이터베이스 서버와의 연결을 위한 옵션을 제공하는 유료 사용제를 제공합니다. SQL Database 서비스에 대한 빌드팩의 자동 구성 지원은 SSL 연결 정보가 사용 가능한 경우 SSL에서 데이터베이스와 연결하기 위한 런타임을 구성할 수 있도록 업데이트되었습니다. 
* 빌드팩은 애플리케이션 아카이브의 루트의 **server.xml** 구성 파일을 포함하는 독립형 WAR 또는 EAR 파일이 배치될 때 오류를 보고하도록 업데이트되었습니다. 
* 빌드팩에는 특정 경우에 올바르지 않은 **server.xml** 구성을 생성하던 MongoDB의 자동 구성 서비스 플러그인에 대한 수정사항이 포함되어 있습니다. 

### 2015년 2월 10일: 업데이트된 Liberty 빌드팩 v1.13-20150209-1122
* 이 빌드팩에는 [Apache HttpComponents 및 Java 오버레이 기능 취약성](https://www-304.ibm.com/connections/blogs/PSIRT/entry/ibm_security_bulletin_multiple_vulnerabilities_fixed_in_liberty_for_java_for_ibm_bluemix_cve_2012_6153_cve_2014_3577_cve_2015_0178?lang=en_us)에 대한 보안 수정사항이 포함되어 있습니다.
* 빌드팩에는 [2월 베타](https://developer.ibm.com/wasdev/blog/2015/02/13/announcing-liberty-beta-tools-february-2015/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. Liberty 프로파일의 업데이트된 버전은 WebSocket GA 기능 websocket-1.1의 업데이트된 버전을 제공합니다. 또한 다음 Java EE 7 베타 기능을 Bluemix에서 사용할 수 있도록 합니다. 
  * cdi-1.2, el-3.0, jsp-2.3, jca-1.7, jacc-1.5 및 jaspic-1.1 
* 이 빌드팩은 [ZeroTrunaround의 JRebel 도구](http://zeroturnaround.com/software/jrebel/)와의 통합을 제공합니다. 이와 같이 통합하면 Bluemix 애플리케이션에서 JRebel을 사용하고 애플리케이션을 다시 배치하거나 다시 스테이징하지 않고 즉시 애플리케이션 업데이트를 수행하기가 쉽습니다. 독립형 웹 애플리케이션만 지원됩니다. 

### 2015년 2월 6일: 업데이트된 Liberty 빌드팩 v1.12-20150130-1016
* 빌드팩에는 [1월 베타](https://developer.ibm.com/wasdev/blog/2015/01/16/announcing-liberty-beta-tools-january-2015/)를 기반으로 하는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. 
* 이 빌드팩에는 [Monitoring and Analytics 서비스](../../services/monana/index.html#gettingstartedtemplate)에 대한 데이터 콜렉터의 트림된 버전이 포함되어 있습니다. 

### 2015년 2월 23일: 업데이트된 Liberty 빌드팩 v1.11-20150119-1511
* 이 빌드팩에는 업데이트된 IBM JRE 버전 7.1 SR2 FP1이 포함되어 있습니다. 
* 또한 업데이트된 WebSphere eXterme Scale Client 버전 8.6.0.6 및 Auto-Scaling 서비스용으로 업데이트된 에이전트도 포함되어 있습니다. 
* [New Relic](newRelic.html) 서비스 지원이 사용자 정의 서비스를 지원할 수 있도록 개선되었습니다. 
* 이 빌드팩은 Liberty 프로파일 및 IBM JRE의 세부 버전을 보고하도록 개선되었습니다. 

### 2014년 12월 19일: 업데이트된 Liberty 빌드팩 v1.10-20141218-0103
* 이 빌드팩은 애플리케이션 개발 모드를 제공합니다. 개발 모드는 이전에는 불가능했던 애플리케이션 인스턴스에 대한 많은 활동을 개발자가 수행할 수 있도록 허용하는 특수 모드입니다. 이 기능을 이용하여, IBM Eclipse Tools for Bluemix의 이 버전은 이제 Bluemix에서 실행되는 Liberty 애플리케이션에 대해 증분 파일 업데이트의 원격 디버깅을 지원할 수 있습니다. 이로 인해 Eclipse를 사용하는 개발자가 클라우드에서 애플리케이션을 디버깅하고 변경사항을 애플리케이션에 바로 적용하는 작업이 편리해졌습니다.
* [12월 베타](https://developer.ibm.com/wasdev/blog/2014/12/10/announcing-liberty-beta-december/)를 기준으로 Liberty 프로파일의 업데이트된 버전도 포함되어 있습니다.
* 또한, 이전에 베타 기능으로 사용 가능했던 다음 네 가지 Liberty 기능이 정식으로 지원될 예정입니다.
  * concurrent-1.0
  * jsonp-1.0
  * servlet-3.1
  * websocket-1.0.
* 빌드팩에서 New Relic 서비스와 통합 기능을 제공합니다. 일단 애플리케이션이 New Relic 서비스에 바인드되면, 빌드팩은 New Relic 에이전트로 런타임을 자동으로 다운로드하고 구성합니다. 
* 빌드팩에는 다음과 같은 알려진 제한사항이 있습니다.
  * 개발 모드에서 SessionCache 서비스를 바인드할 수 없습니다.
  * 개발 모드에서 스레드 덤프를 작성할 수 없습니다.
  * servlet-3.1 또는 websocket-v1.0 기능을 사용하는 경우에는 Monitoring & Analytics 서비스를 바인드할 수 없습니다. 

### 2014년 12월 5일: 업데이트된 Liberty 빌드팩 v1.9-20141202-0947
* 이 빌드팩은 향상된 JVM 옵션을 지원합니다. JVM 옵션은 이제 재시작 조작에서 적용될 수 있습니다. 애플리케이션을 다시 스테이징할 필요가 없습니다. 또한, 기본 JVM 옵션이 긴급 장애에 최적화되어 있고 생성된 덤프를 쉽게 찾을 수 있도록 공통 위치가 사전 구성되어 있습니다. 자세한 내용은 [Liberty 런타임용 Java JVM의 사용자 정의 구성 문서](https://developer.ibm.com/bluemix/2014/12/12/custom-configurations-java-jvm-liberty-runtime/)에 나와 있습니다. 
* 이 빌드팩에는 업데이트된 DB2 JDBC 드라이버 버전 4.17.29가 포함되어 있습니다. 
* Monitoring & Analytics 서비스에 사용할 Liberty 스레드 풀 사용량 정보의 수집을 막는 문제점에 대한 수정사항도 들어 있습니다.

### 2014년 11월 21일: 업데이트된 Liberty 빌드팩 v1.8-20141118-1610
* 이 빌드팩에는 [POODLE 취약성](http://www-01.ibm.com/support/docview.wss?uid=swg21687173)에 대한 수정사항을 제공하는 업데이트된 IBM JRE 버전 7.1 SR2가 포함되어 있습니다. 
* [11월 베타](https://developer.ibm.com/wasdev/blog/2014/11/07/announcing-liberty-profile-beta-november/) 기준으로 Liberty 프로파일의 업데이트된 버전도 포함되어 있습니다. 

### 2014년 10월 30일: 업데이트된 Liberty 빌드팩 v1.7-20141020-1759
* 이 빌드팩에는 업데이트된 IBM JRE 버전 7.1 SR1 FP3이 포함되어 있습니다. 
* 유니코드 문자가 포함된 서버 구성으로 애플리케이션의 배치를 막는 문제점에 대한 수정사항도 제공합니다. 

### 2014년 10월 23일: 업데이트된 Liberty 빌드팩 v1.6-20141013-1628
* 이제 이 빌드팩에 [Monitoring and Analytics](../../services/monana/index.html)를 위한 새로운 데이터 콜렉터가 제공됩니다. 이러한 새로운 데이터 콜렉터는 서비스의 진단 플랜 사용자가 애플리케이션의 문제점을 구체적인 코드 행 수준으로까지 진단할 수 있도록 진단 상세 정보를 수집합니다. 
* 빌드팩에 버그 수정과 사소한 개선사항을 포함한 관리 및 Auto-Scaling 에이전트의 업데이트된 버전이 포함되어 있습니다. 또한 [Liberty 프로파일](https://developer.ibm.com/wasdev/)과 [Java MongoDB Driver](https://docs.mongodb.org/ecosystem/drivers/java/), v2.12.3의 업데이트된 버전도 포함되어 있습니다.
* cloudAutowiring 기능에서 일부 애플리케이션의 자원 인젝션 오류를 일으키던 버그가 수정되었습니다. 

### 2014년 10월 3일: 업데이트된 Liberty 빌드팩 v1.5-20140923-1143
* 이 업데이트된 빌드팩을 적용하면 애플리케이션이 WebSocket 1.0, Servlet 3.1 또는 JAX-RS 2.0와 같은 Liberty 베타 기능을 사용할 수 있습니다. 자세한 정보는 [베타 기능 사용](usingBetaFeatures.html)을 참조하십시오.

### 2014년 9월 30일: 업데이트된 Liberty 빌드팩 v1.4-20140908-1803
* 이 빌드팩은 이제 ElephantSQL 및 ClearDB MySQL Database 써드파티 서비스에 대한 지원을 제공합니다. posgresql 및 mysql 같은 시범 서비스에서도 자동 구성 지원이 작동합니다. 총 13개의 새로운 서비스를 사용하는 경우, Liberty 빌드팩의 자동 구성 지원을 통해 Liberty 애플리케이션에서 Bluemix 서비스를 보다 쉽고 빠르게 이용할 수 있습니다.
* 애플리케이션을 스테이징하는 동안 자동 구성 및 기타 수행 조치에 대한 향상된 로그 메시지가 빌드팩에 표시됩니다.
* 빌드팩에는 수정사항 및 개선 기능이 있는 Liberty 프로파일의 업데이트된 버전이 포함되어 있습니다. 
* 성능을 강화시키는 IBM JRE 버전 7.1의 업데이트된 버전도 포함되어 있습니다. 자세한 변경사항은 [새로운 기능](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.71.doc/diag/preface/changes_71/changes.html) 페이지를 참조하십시오.

### 2014년 8월 28일: 업데이트된 Liberty 빌드팩 v1.3-20140818-1538
* 이 빌드팩에는 최신 수정사항, 개선 기능이 들어 있는 [ Liberty 프로파일](https://developer.ibm.com/wasdev/)의 업데이트된 버전이 포함되어 있습니다.
* 이 버전의 필드팩은 추가 JVM 옵션을 애플리케이션 런타임에 전달하기 위한 JAVA_OPTS 환경 변수의 지원을 수정합니다.
* 독립형 Spring 기반 Jar 애플리케이션의 배치를 막는 문제점도 수정합니다. 
* 이제 Bluemix UI를 사용하여 IBM JVM 스냅 추적을 생성하고 다운로드할 수 있습니다. 스냅 추적 또는 JVM에서 생성하는 기타 진단 정보에 대해 자세히 알아보려면 IBM JVM 문서의 [문제점 해결 주제](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/troubleshooting.html)를 참조하십시오. 

### 2014년 6월 29일: 업데이트된 Liberty 빌드팩 v1.1-20140725-1341
* Liberty용 Bluemix Edition의 새 버전이 출시되었습니다! 
  * 이 Liberty 버전에는 Bluemix 서비스를 보다 효과적으로 이용할 수 있도록 허용하는 새 기능과 더불어 수정사항이 있습니다. 
  * 새로운 CouchDB 기능을 사용하는 경우, Cloudant® 서비스는 커넥터 오브젝트를 바로 사용할 수 있도록 이 기능을 자동으로 구성합니다. 더 이상 VCAP_SERVICES를 구문 분석하고 ektorp 클라이언트 jar을 제공할 필요가 없습니다. 
* IBM SDK for Java의 새 버전이 출시되었습니다! 
  * 애플리케이션이 다시 푸시되는 경우, 이는 IBM SDK for Java 버전7.1-1.0을 사용합니다. 이는 중요한 성능 업그레이드와 함께 제공합니다. 애플리케이션은 보다 뛰어난 처리량과 감소된 메모리 사용량을 보여줍니다. [여기](http://www-01.ibm.com/support/docview.wss?uid=swg21671466)에서 IBM Java SDK에 대해 자세히 알아보십시오.

  # 관련 링크
  ## 일반
  * [Liberty 런타임](index.html)
  * [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
