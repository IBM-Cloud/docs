---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# JRE 사용자 정의
{: #customizing_jre}

*마지막 업데이트 날짜: 2016년 3월 23일*

애플리케이션은 Liberty 빌드팩에 의해 제공되고 구성되는 Java 런타임 환경(JRE)에서 실행됩니다. 또한 Liberty 빌드팩은 JRE 버전 또는 유형을 구성하고 JVM 옵션을 사용자 정의하거나 JRE 기능을 오버레이할 수 있도록 합니다. 

## IBM JRE

기본적으로 애플리케이션은 IBM JRE의 경량 버전에서 실행되도록 구성되어 있습니다. 이 경량 JRE는 훨씬 줄어든 디스크 및 메모리 공간으로 코어, 핵심 기능을 제공할 수 있도록 불필요한 기능들을 모두 제거했습니다. 경량 JRE의 컨텐츠에 대한 자세한 정보는 [Liberty for Java 런타임](http://download.boulder.ibm.com/ibmdl/pub/software/dw/jdk/docs/bluemix/libertyforjava_jre.doc.html)을 참조하십시오.

기본적으로 IBM JRE 버전 8이 사용됩니다. JBP_CONFIG_IBMJDK 환경 변수를 사용하면 IBM JRE의 대체 버전을 지정할 수 있습니다. 예를 들어, 최신 IBM JRE 7.1을 사용하려면 다음 환경 변수를 설정하십시오.
```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "version: 1.7.+"
```
{: #codeblock}

버전 특성은 버전 범위로 설정될 수 있습니다. 두 개의 지원되는 버전 범위(1.7.+ 및 1.8.+) 가 있습니다. 최상의 결과를 얻으려면 Java 8을 사용하십시오. 

## OpenJDK
{: #openjdk}

선택사항으로, 애플리케이션을 JRE로서 OpenJDK에서 실행되도록 구성할 수 있습니다. 애플리케이션이 OpenJDK로 실행되도록 하려면 JVM 환경 변수를 "openjdk"로 설정하십시오. 예를 들어, cf 명령행 도구를 사용하여 다음 명령을 실행하십시오.
```
    $ cf set-env myapp JVM 'openjdk'
```
{: #codeblock}

사용으로 설정되는 경우 기본적으로 OpenJDK 버전 8이 사용됩니다. JBP_CONFIG_OPENJDK 환경 변수를 사용하면 OpenJDK의 대체 버전을 지정할 수 있습니다. 예를 들어, 최신 OpenJDK 7을 사용하려면 다음 환경 변수를 설정하십시오.
```
    $ cf set-env myapp JBP_CONFIG_OPENJDK "version: 1.7.+"
```
{: #codeblock}

버전 특성은 1.7.+ 등의 버전 범위 또는 [사용 가능한 OpenJDK 버전 목록](https://download.run.pivotal.io/openjdk/lucid/x86_64/index.yml)에 나열된 특정 버전으로 설정될 수 있습니다. 최상의 결과를 얻으려면 Java 8을 사용하십시오. 

## JRE 옵션 구성
{: #configuring_jre}

### JVM 기본 구성
{: #jvm_default_config}

Liberty 빌드팩은 다음을 고려하여 기본 JVM 옵션을 구성합니다.

* 애플리케이션의 메모리 제한. 적용되는 JVM 힙 설정은 다음을 기준으로 계산됩니다.
  * [메모리 제한 및 Liberty 빌드팩](memoryLimits.html#memory_limits)에 설명된 애플리케이션의 메모리 제한
  * JRE 유형. JVM의 힙 관련 옵션은 JRE의 지원 옵션에 따라 다릅니다. 

* [Bluemix에서 지원되는 Liberty 기능](libertyFeatures.html#libertyfeatures).
  * 2단계 커미트 글로벌 데이터베이스 트랜잭션이 Bluemix에서 지원되지 않으므로 -Dcom.ibm.tx.jta.disable2PC=true 설정으로 사용되지 않습니다. 

* Bluemix 환경. 

    JVM 옵션은 Bluemix 환경에서 최적화를 제공하고 메모리 관련 오류 조건의 진단에 도움이 되도록 구성되어 있습니다. 
  * 애플리케이션의 메모리가 전부 소모되었을 때 JVM 덤프 옵션과 프로세스 강제 종료를 비활성화하여 애플리케이션의 긴급 장애 및 복구가 구성됩니다.
  * 가상화 튜닝(IBM JRE만 해당).
  * 장애 발생 시 애플리케이션의 사용 가능한 메모리 자원 정보를 Loggregator로 라우팅. 
  * JVM 메모리 덤프를 사용하도록 애플리케이션이 구성되고, Java 프로세스의 강제 종료가 비활성 상태이며, JVM 메모리 덤프가 애플리케이션 "dumps" 공통 디렉토리로 라우팅되는 경우. 그리고 이 덤프는 Bluemix 대시보드 또는 CF CLI에서 볼 수 있습니다. 

다음은 512M 메모리 제한을 적용하여 배치된 애플리케이션에 대한 빌드팩이 생성하는 기본 JVM 구성 예제입니다.
```
    -Xtune:virtualized
    -Xmx384M
    -Xdump:none
    -Xdump:heap:defaults:file=../../../../../dumps/heapdump.%Y%m%d.%H%M%S.%pid.%seq.phd
    -Xdump:java:defaults:file=../../../../../dumps/javacore.%Y%m%d.%H%M%S.%pid.%seq.txt
    -Xdump:snap:defaults:file=../../../../../dumps/Snap.%Y%m%d.%H%M%S.%pid.%seq.trc
    -Xdump:tool:events=systhrow,filter=java/lang/OutOfMemoryError,request=serial+exclusive,exec=../../../../.buildpack-diagnostics/killjava.sh
    -Dcom.ibm.tx.jta.disable2PC=true
```
{: #codeblock}

### JVM 구성 사용자 정의
{: #customizing_jvm}

애플리케이션에서 이 애플리케이션에 구성된 JRE를 통해 정의되는 명세를 사용하여 JVM 옵션을 사용자 정의할 수 있습니다. JRE에 따라 옵션이 달라지므로, JRE 문서에서 옵션과 사용법을 지정하는 방법에 대한 가이드라인을 참조하십시오.

<table>
<tr>
<th align="left">JRE</th>
<th align="left">명령행 옵션 형식</th>
<th align="left">참조</th>
</tr>

<tr>
<td>IBM JRE</td>
<td>런타임 옵션(접두부 -X가 붙어 있음), Java 시스템 특성(접두부 -D가 붙어 있음)을 포함하며, 일상적인 사용에는 -XX를 권장하지 않습니다(이 옵션은 변경될 수 있음).
</td>
<td>[버전 8 명령행 옵션](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/appendixes/cmdline/cmdline.html), [버전 7 명령행 옵션](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/diag/appendixes/cmdline/cmdline.html)
</td>
</tr>

<tr>
<td> OpenJDK</td>
<td>표준이 아닌 옵션에서는 -X로, 개발자 옵션에서는 -XX로 표시되는 HotSpot 런타임와 옵션의 사용 여부를 설정하는 부울 플래그를 기반으로 합니다.</td>
<td>[HotSpot 런타임 개요](http://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html) </td>
</tr>
</table>

사용자 정의된 JVM 옵션이 필요한 애플리케이션은 Bluemix에서 IBM_JAVA_OPTIONS, JAVA_OPTS 또는 JVM_ARGS 환경 변수 중 하나의 값으로 옵션을 설정할 수 있습니다. 애플리케이션의 환경 변수를 설정하는 방법은 환경 변수 섹션을 참조하십시오. 환경 변수를 설정하는 대신 명령행 옵션이 들어 있는 jvm.options 파일이 패키지된 서버 또는 서버 디렉토리에 있을 수도 있습니다.

JVM 옵션을 JRE에 적용하면 Liberty 빌드팩의 기본 옵션이 먼저 적용된 다음 사용자 정의 옵션이 적용됩니다. 사용자 정의 옵션은 테이블에 나와 있는 특정 순서대로 추가됩니다. 적용된 Java 옵션의 순서에 따라 어떤 옵션이 우선하는지 정의됩니다. 마지막에 적용되는 옵션이 이전에 적용된 옵션보다 우선합니다. 

참고: 일부 옵션은 에이전트가 옵션을 트리거하지 않으면 적용되지 않을 수 있습니다.

<table>
<tr>
<th align="left">적용 순서</th>
<th align="left">애플리케이션 JVM 옵션 설정</th>
<th align="left">설명</th>
<th align="left">지원되는 애플리케이션 유형</th>
<th align="left">배치된 애플리케이션의 JVM 옵션 업데이트 방법</th>
<th align="left">OpenJDK JRE에 적용 가능 여부</th>
</tr>

<tr>
<td>1</td>
<td>IBM_JAVA_OPTIONS</td>
<td>IBM JRE에 지원되는 환경 변수</td>
<td>모두</td>
<td>애플리케이션 다시 시작 또는 다시 스테이징</td>
<td>아니오</td>
</tr>

<tr>
<td>2</td>
<td>JAVA_OPTS</td>
<td>Liberty 빌드팩 Java Options 프레임워크를 통한 환경 변수</td>
<td>모두</td>
<td>앱 다시 스테이징</td>
<td>예</td>
</tr>

<tr>
<td>3</td>
<td>jvm.options</td>
<td>Liberty 런타임 패키지된 서버 또는 서버 디렉토리에 지원되는 JVM 구성 파일</td>
<td>서버 패키지</td>
<td>앱 다시 스테이징</td>
<td>예</td>
</tr>

<tr>
<td>4</td>
<td>JVM_ARGS</td>
<td>Liberty 런타임에 지원되는 환경 변수</td>
<td>모두</td>
<td>앱 다시 시작 또는 다시 스테이징</td>
<td>예</td>
</tr>
</table>

### 실행 중인 애플리케이션에 적용된 JVM 옵션 판별
{: #determining_applied_jvm_options}

JVM_ARGS 환경 변수를 통해 지정된 애플리케이션 정의 옵션을 제외하고는, 작업 결과로 지정된 옵션이 런타임 환경에서 명령행 옵션(독립형 Java 애플리케이션)으로 또는 jvm.options 파일에(비독립형 Java 애플리케이션)에 지속됩니다. 애플리케이션에 대해 적용된 JVM 옵션은 Bluemix 대시보드 또는 CF CLI에서 볼 수 있습니다. 

독립형 Java 애플리케이션에 대한 JVM 옵션은 명령행 옵션으로서 유지됩니다. 이 옵션은 staging_info.yml 파일에서 확인할 수 있습니다.
```
    $ cf files myapp staging_info.yml
```
{: #codeblock}

WAR, EAR, 서버 디렉토리 및 패키지된 서버 배치에 대한 JVM 옵션은 jvm.options 파일에서 유지됩니다. 

WAR, EAR 및 서버 디렉토리에 대한 jvm.options 파일을 보려면 다음 명령을 실행하십시오.
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/jvm.options
```
{: #codeblock}

패키지된 서버의 jvm.options 파일을 보려면 <serverName>을 서버의 이름으로 대체하고 다음 명령을 실행하십시오.
```
    $ cf files myapp app/wlp/usr/servers/<serverName>jvm.options
```
{: #codeblock]

#### 사용 예제
{: #example_usage}

IBM JRE JVM 세부 가비지 콜렉션 로깅을 활성화하기 위해 사용자 정의 JVM 옵션을 사용하여 애플리케이션 배치:
* 애플리케이션의 manifest.yml 파일에 있는 JVM 옵션:
```
    env:
      JAVA_OPTS: "-verbose:gc -Xverbosegclog:./verbosegc.log,10,1000"
```
{: #codeblock}

* 생성된 JVM 세부 가비지 콜렉션 로깅을 확인합니다.
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/verbosegc.log.001
```
{: #codeblock}    

* 메모리 부족 조건에서 힙, 스냅 및 javacore를 트리거하도록 배치된 애플리케이션의 IBM JRE JVM 옵션 업데이트:

JVM 옵션을 사용하여 애플리케이션의 환경 변수를 설정하고 애플리케이션을 다시 시작합니다.
```
    $ cf set-env myapp JVM_ARGS '-Xdump:heap+java+snap:events=systhrow,filter=java/lang/OutOfMemoryError'
    $ cf restart myapp
```
{: #codeblock}

* 메모리 부족 조건에서 생성된 JVM 덤프를 확인합니다.
```
    $ cf files myapp dumps

    Getting files for app myapp in org myemail@email.com / space dev as myemail@email.com...
    OK

    Snap.20141106.100252.81.0003.trc           307.3K
    heapdump.20141106.100252.81.0001.phd       3.9M
    javacore.20141106.100252.81.0002.txt     870.5K
```
{: #codeblock}

### JRE 오버레이
{: #overlaying_jre}

기능을 지원하기 위해 파일을 JRE와 묶음으로 제공해야 하는 경우가 있습니다. 애플리케이션 개발자는 사용자 정의하기 위한 JRE 파일을 제공합니다.

오버레이되는 파일과 애플리케이션 WAR, EAR 또는 JAR을 아카이브 루트의 자원 폴더에 패키지로 만들 수 있습니다. 서버(압축 파일 또는 서버 디렉토리)의 경우, 서버 디렉토리의 자원 폴더에 이 파일과 server.xml 파일을 패키지로 만들 수 있습니다. 

* WAR 파일
  * WEB-INF
  * 자원
    * 기타 파일
    * .java-overlay


* EAR 파일
  * META-INF
  * 자원
    * 기타 파일
    * .java-overlay


* JAR 파일
  * META-INF
  * 자원
    * 기타 파일
    * .java-overlay


* server_name DIR
  * apps
  * dropins
  * server.xml
  * 자원
    * 기타 파일
    * .java-overlay

.java-overlay 디렉토리에는 오버레이되는 Java JRE와 동일한 파일 계층구조에 .java/jre로 시작하는 특정 파일이 있습니다. 

예를 들어, AES 256비트 암호화를 사용하려는 경우 이 Java 정책 파일을 오버레이해야 합니다.
```
    .java\jre\lib\security\US_export_policy.jar
    .java\jre\lib\security\local_policy.jar
```
{: #codeblock}

적절한 제한 없는 정책 파일을 다운로드하여 애플리케이션에 다음과 같이 추가하십시오.
```
    resources\.java-overlay\.java\jre\lib\security\US_export_policy.jar
    resources\.java-overlay\.java\jre\lib\security\local_policy.jar
```
{: #codeblock}

애플리케이션을 푸시하면 이 jar이 Java 런타임의 기본 정책 jar을 오버레이합니다. 이 프로세스를 통해 AES 256비트 암호화가 활성화됩니다.

# 관련 링크
## 일반
* [Liberty 런타임](index.html)
* [Liberty 프로파일 개요](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
