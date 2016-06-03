---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 

# {{site.data.keyword.Bluemix_notm}} 액세스 문제점 해결 
{: #accessing}

*마지막 업데이트 날짜: 2016년 5월 16일*

{{site.data.keyword.Bluemix}} 액세스와 관련한
일반적인 문제점으로는 사용자가 {{site.data.keyword.Bluemix_notm}}에
로그인할 수 없거나, 계정이 보류 상태로 남아 있는 경우 등이 있습니다. 그러나 대부분의 경우
몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다. 
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음
{: #ts_logintobm}

{{site.data.keyword.Bluemix_notm}}에 로그인하려면
유효한 IBM ID와 비밀번호가 필요합니다.


{{site.data.keyword.Bluemix_notm}}에
로그인하려고 할 때 다음과 같은 오류 메시지가 표시됩니다. 
{: tsSymptoms} 

`아래에 입력한
IBM ID 및/또는 비밀번호가 올바르지 않습니다. 다시 시도하십시오.`


{{site.data.keyword.Bluemix_notm}}
로그인에 사용한 IBM ID와 비밀번호가 올바르지 않습니다.
{: tsCauses} 
 

올바른 IBM ID와 비밀번호를 얻으려면 내 IBM 프로파일 페이지로 이동하여 다음 단계 중 하나를 완료하십시오.
{: tsResolve}
  * IBM ID를 이미 등록했으며 이 ID와 비밀번호가 올바른지 확인하려는 경우, **로그인**을 클릭하고 로그인 페이지에 IBM ID와 비밀번호를 입력하십시오. 비밀번호를 잊어버린 경우 로그인 페이지의 오른쪽에 있는
**비밀번호를 잊으셨습니까?**를 클릭하여 비밀번호를 재설정하십시오. IBM ID를 잊어버렸거나 비밀번호에 계속 문제가 있는 경우 전 세계 IBM 등록 헬프 데스크에 지원을 요청하십시오. 
  * IBM ID가 없는 경우, **등록**을 클릭하여 IBM ID와 비밀번호를
등록하십시오. 
  
**참고:** IBM 직원의 경우 IBM ID와 인트라넷 로그인 ID가 다를 수 있습니다. 





## 저장되지 않은 변경사항이 있음
{: #ts_unsaved_changes}


앱 세부사항 페이지에서 탐색할 때 조치를 수행하지 못하고 계속하기 전에 변경사항을 저장하라는 메시지가 표시될 수 있습니다. 


앱 세부사항 페이지에서 앱 또는 서비스를 확인하려고 하면 다음 오류 메시지가 계속 표시됩니다.
{: tsSymptoms} 

`app_name 페이지에 저장되지 않은 변경사항이 있습니다. 변경사항을 저장하거나 취소하십시오.`


런타임 분할창에서 **인스턴스** 또는 **메모리 할당량** 필드 위로 마우스를 스크롤하면 값이 변경됩니다. 설계상 이런 동작이 발생하는 것이며, 페이지에서 벗어나기 전에 메모리 또는 인스턴스 설정을 저장하라는 오류 메시지가 표시됩니다.
{: tsCauses}


메시지 창을 닫고 런타임 분할창에서 **재설정** 단추를 클릭하십시오.
{: tsResolve} 




    
    
## {{site.data.keyword.Bluemix_notm}} 지역 간의 자동 장애 복구를 사용할 수 없음
{: #ts_failover}

{{site.data.keyword.Bluemix_notm}} 지역 간의 자동 장애 복구를 사용할 수 없습니다. 하지만 여러 IP 주소 간의 장애 복구를 지원하는 DNS 제공자를 임시 해결책으로 사용할 수 있습니다.
 

{{site.data.keyword.Bluemix_notm}} 지역을 사용할 수 없게 되면 동일한 앱이 다른 {{site.data.keyword.Bluemix_notm}} 지역에서 실행 중이더라도 해당 지역에서 실행 중인 앱도 사용할 수 없습니다.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}}는 아직 한 지역에서 다른 지역으로의 자동 장애 복구를 제공하지 않습니다.
{: tsCauses}

 
여러 IP 주소 간의 지능형 장애 복구를 지원하는 DNS 제공자를 사용하여 {{site.data.keyword.Bluemix_notm}} 지역 간의 자동 장애 복구를 지원하도록 DNS 설정을 수동으로 구성할 수 있습니다. 이 기능이 있는 DNS 제공자에는 NSONE, Akamai, Dyn이 포함됩니다.
{: tsResolve}

DNS 설정을 구성할 때 앱이 실행 중인 {{site.data.keyword.Bluemix_notm}} 지역의 공용 IP 주소를 지정해야 합니다. {{site.data.keyword.Bluemix_notm}} 지역의 공용 IP 주소를 가져오려면 `nslookup` 명령을 사용하십시오. 예를 들어, 명령행 창에 다음 명령을 입력할 수 있습니다.
```
nslookup mybluemix.net
```



## 계정이 보류 중임
{: #ts_accntpding}

계정이 보류 중인 경우 {{site.data.keyword.Bluemix_notm}}에
로그인할 수 없습니다.

 
{{site.data.keyword.Bluemix_notm}}
평가판 계정에 등록하면 {{site.data.keyword.Bluemix_notm}}에
로그인하지 못할 수 있습니다. 대신 다음 메시지가 표시됩니다.
{: tsSymptoms}

<code>사용자 계정이 보류 중입니다. 여러분 계정의 이메일 확인을 위해 최대 24시간 동안 기다려야 할 수 있습니다.
스팸 폴더도 확인하십시오. 아직 이메일 확인을 받지 못했다면, <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix 지원</a>에 문의하십시오.</code>


{{site.data.keyword.Bluemix_notm}}
평가판 계정에 등록하면 확인 이메일을 받습니다. 확인 이메일에 있는 링크를 클릭하여
등록 프로세스를 완료해야 합니다.
{: tsCauses} 

확인 이메일이
사용자가 제공한 이메일 주소로 전송됩니다. 받은 편지함과 정크 메일 폴더를
확인하십시오. 확인 이메일을 받지 못한 경우, [{{site.data.keyword.Bluemix_notm}} 지원](http://ibm.biz/bluemixsupport.com){: new_window}에 문의하십시오.  
{: tsResolve}



## 조직에 사용자를 추가할 수 없음
{: #ts_adduser}

동일한 조직에서 작업할 사용자를 두 명 이상 초대할 수 있습니다. 계정 소유자이거나
조직의 관리자이자 구성원인 경우에만 조직에 사용자를 추가할 수 있습니다.
 

**조직 관리**
섹션에 **새 사용자 초대** 링크가 보이지 않습니다. 
{: tsSymptoms}

 

다음 {{site.data.keyword.Bluemix_notm}}
사용자만 사용자를 조직에 초대할 수 있습니다.
{: tsCauses}
  * 조직의 계정 소유자
  * 조직의 협업자가 아니라 구성원인 조직 관리자
  
{{site.data.keyword.Bluemix_notm}}에서
사용자는 조직의 구성원이거나 협업자일 수 있습니다.

<dl><dt>협업자</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 계정이 이미
있으며 다른 사용자가 자신을 조직으로 초대한 경우, 조직의 협업자입니다.</dd>
<dt>구성원</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 계정이 없지만
다른 사용자가 자신을 초대하여 초대장을 통해 {{site.data.keyword.Bluemix_notm}}에
등록한 경우, 조직의 구성원입니다.</dd>
</dl>


조직의 협업자인 경우에는
조직 관리자로 지정되었더라도 조직에 사용자를 초대할 수 없습니다.

**참고:** 조직의 협업자를 비롯한 모든 조직 관리자는 조직에 이미 있는 사용자를 추가, 수정 및 제거할 수 있습니다.

 

사용자를 조직에 초대할 수 없으며 초대를 위해 다른 역할이 필요한 경우
조직 관리자에게 역할 변경을 요청하십시오. 조직 관리자를 확인하려면 다음 단계를 수행하십시오.
{: tsResolve}

  1. {{site.data.keyword.Bluemix_notm}} 대시보드로 이동하여 상단 메뉴 표시줄에서 **계정 및 지원** 아이콘 ![계정 및 지원](images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오.
  2. 자신의 조직으로 이동하여 **사용자** 탭에서 조직 관리자에
대한 정보를 확인하십시오.  
  
구성원이 아니라 협업자이기 때문에
사용자를 초대할 수 없는 경우 이전 {{site.data.keyword.Bluemix_notm}}
계정을 삭제한 다음 조직의 구성원으로 참여할 수 있도록 초대를 받아야 합니다. 이전 계정을 삭제하고 구성원으로 계정에 참여하려면 다음 단계를 수행하십시오. 

  1. [{{site.data.keyword.Bluemix_notm}} 지원 부서에 연락](http://ibm.biz/bluemixsupport){: new_window}하여 지원 티켓을 열고 계정 삭제를 요청하십시오. 이전 계정과 연관된 데이터가 있어
이 데이터를 저장한 다음 새 계정으로 이동하려면 이메일에 이 정보를 포함시키십시오. 
  2. 계정이 삭제되면 조직 관리자 역할을 보유한 사용자가 자신을 조직 관리자로 조직에
초대하도록 하십시오. 그런 다음 초대장을 통해 {{site.data.keyword.Bluemix_notm}}에
등록하십시오. 




## 사용자 일괄 등록이 지원되지 않음
{: #ts_batchregistration}

{{site.data.keyword.Bluemix_notm}}에 사용자를
등록할 경우 각 사용자를 개별적으로 등록해야 합니다.
 

{{site.data.keyword.Bluemix_notm}}에서는
여러 사용자를 한 번에 등록하는 기능을 제공하지 않습니다.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}}에서는
사용자 일괄 등록을 지원하지 않습니다. {{site.data.keyword.Bluemix_notm}}에
사용자를 등록하려면 각 사용자를 개별적으로 등록해야 합니다.
{: tsCauses}
 

{{site.data.keyword.Bluemix_notm}}에
여러 사용자를 등록하려면 사용자마다 다음 단계를 수행해야 합니다.
{: tsResolve}

  1. {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스의
오른쪽 위에 있는 **등록**을 클릭하십시오.
  2. 마법사의 안내에 따라 단계를 완료하십시오.

    

## {{site.data.keyword.Bluemix_notm}} 페이지를 로드할 수 없음
{: #ts_err}

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용하는 경우 {{site.data.keyword.Bluemix_notm}} 페이지를 로드하지 못할 수 있습니다. 대신, BXNUI0001E 또는 BXNUI0016E 오류 메시지가 표시될 수 있습니다.
 

{{site.data.keyword.Bluemix_notm}}
사용자 인터페이스를 사용할 경우 다음과 같은 오류 메시지가 표시될 수 있습니다.
{: tsSymptoms}

`BXNUI0001E: Bluemix에서 세션이 존재하는지 여부를 발견하지 않았기 때문에 페이지가 로드되지 않았습니다.`


`BXNUI0016E: Bluemix 페이지가 로드되지 않았기 때문에 앱과 서비스가 검색되지 않았습니다.`

 

필요한 경우 다음 조치 중 하나 이상을 수행할 수 있습니다.
{: tsResolve}

  * 브라우저를 새로 고치거나 다시 시작하십시오.
  * {{site.data.keyword.Bluemix_notm}}에서 로그아웃한 후 다시 로그인하십시오.
  * 브라우저의 개인용 브라우징 모드를 사용하십시오. 
  * 브라우저의 쿠키와 캐시를 지우십시오.
  * 다른 브라우저를 사용하십시오. {{site.data.keyword.Bluemix_notm}}에서 지원하는 브라우저 버전에 대한 정보는 [{{site.data.keyword.Bluemix_notm}}전제조건](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}을 참조하십시오.
  * cf 명령행 인터페이스를 설치한 경우 `cf apps` 명령을 입력하여 애플리케이션이 실행 중인지 확인하십시오.
  
  
  
  
  
## {{site.data.keyword.Bluemix_notm}} 맨 위 메뉴 표시줄이 사라짐
{: #ts_topmenubar}

브라우저 창의 크기를 조정하거나 모바일 디바이스를 사용할 때 {{site.data.keyword.Bluemix_notm}} 맨 위 메뉴 표시줄을 볼 수 없습니다.


브라우저 창의 크기를 조정하거나 모바일 디바이스를 사용할 때 {{site.data.keyword.Bluemix_notm}} 맨 위 메뉴 표시줄이 사라집니다. 맨 위 메뉴 표시줄이 사라지면 누적 꺾은선형 아이콘으로 표시되는 측면 드로어 메뉴가 왼쪽 위 모서리에 나타납니다.
{: tsSymptoms}

 

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스는 반응형으로 설계되었습니다. 보기 환경이 변경되면 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스의 레이아웃도 변경될 수 있습니다.
{: tsCauses}
 

왼쪽 위 모서리의 측면 드로어 메뉴를 대신 사용하십시오.
{: tsResolve}








# 앱 관리 문제점 해결
{: #managingapps}

애플리케이션 관리와 관련된 일반적인 문제점으로는 애플리케이션을
업데이트할 수 없거나 2바이트 문자가 표시되지 않는 경우가 있습니다. 그러나 대부분의 경우
몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다. 
{:shortdesc}





## 앱을 디버그 모드로 전환할 수 없음
{: #ts_debug}

JVM(Java Virtual Machine)이 버전 8 이하인 경우에는 디버그 모드를 사용하지 못할 수 있습니다.  


**애플리케이션 디버그 사용**을 선택한 이후, 도구는 해당 애플리케이션을 디버그 모드로 전환하려고 시도합니다. 그리고 Eclipse 워크벤치는 디버그 세션을 시작합니다. 도구에서 디버그 모드를 정상적으로 사용하는 경우, 웹 애플리케이션 상태는 `업데이트 모드`, `개발` 및 `디버깅`을 표시합니다.
{: tsSymptoms}

그러나 도구에서 디버그 모드를 사용할 수 없는 경우, 웹 애플리케이션 상태는
`업데이트 모드` 및 `개발`만 표시하며 `디버깅`은 표시하지 않습니다. 도구가 콘솔 보기에서 다음 오류 메시지를 표시할 수도 있습니다.

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```
 

IBM JVM 7, IBM JVM 8 및 Oracle JVM 8의 이전 버전 등의 JVM(Java Virtual Machine) 버전은 디버그 세션을 설정할 수 없습니다.
{: tsCauses}

워크벤치 JVM이 이 버전 중 하나인 경우에는 디버그 세션을 작성할 때 문제가 발생할 수 있습니다. 워크벤치 JVM 버전은 일반적으로 로컬 컴퓨터의 시스템 JVM입니다. 시스템 JVM은 실행 중인 Bluemix Java 애플리케이션의 JVM과 동일하지 않습니다. Bluemix Java 애플리케이션은 거의 항상 IBM JVM에서 실행되며, 가끔은 OpenJDK JVM에서 실행됩니다.
  

IBM Eclipse Tools for Bluemix가 실행 중인 Java의 버전을 확인하려면 다음 단계를 완료하십시오.
{: tsResolve}

  1. IBM Eclipse Tools for Bluemix에서 **도움말** > **Eclipse 정보** > **설치 세부사항** > **구성**을 선택하십시오.
  2. 목록에서 `eclipse.vm` 특성을 찾으십시오. 다음 행은 `eclipse.vm` 특성의 예입니다.
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. 명령행에서, Java 설치의 `bin` 디렉토리에서 `java -version`을 입력하십시오. IBM JVM 버전 정보가 표시됩니다.

워크벤치 JVM이 IBM JVM 7 또는 8, 또는 Oracle JVM 8의 이전 버전인 경우에는 다음 단계를 완료하여 Oracle JVM 8로 전환하십시오.

  1. Oracle JVM 8을 다운로드한 후에 이를 설치하십시오. 세부사항은 [Java SE 다운로드](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window}를 참조하십시오.
  2. Eclipse를 다시 시작하십시오.
  3. `eclipse.vm` 특성이 Oracle JVM 8의 새 설치를 지시하는지 확인하십시오.







## 요청된 조치를 수행할 수 없음
{: #ts_authority}

해당 액세스 권한이 없으면 조치를 완료하지 못할 수 있습니다.

 

서비스 인스턴스 또는 앱 인스턴스에 대해 조치를 수행하려 할 때 요청된 조치를 완료할 수 없고 다음 오류 메시지 중 하나가 표시됩니다. 
{: tsSymptoms}

`BXNUI0514E: <orgName> 조직의 영역에 대한 개발자가 아닙니다.`


`서버 오류, 상태 코드: 403, 오류 코드: 10003, 메시지: 요청된 조치를 수행할 권한이 없습니다.`

 

조치 수행에 필요한 적절한 수준의 권한이 없습니다. 
{: tsCauses}

  

해당 권한 레벨을 확보하려면 다음 방법 중 하나를 사용하십시오. 
{: tsResolve}
 * 개발자 역할이 있는 다른 조직과 영역을 선택하십시오. 
 * 조직 관리자에게 문의하여 사용자의 역할을 개발자 역할로 변경하거나 영역을 작성한 다음 사용자에게 개발자 역할을 지정하십시오. 세부사항은 [조직 관리](../admin/orgs_spaces.html)를 참조하십시오.
 

 


## 권한 오류로 인해 {{site.data.keyword.Bluemix_notm}} 서비스에 액세스할 수 없습니다.
{: #ts_vcap}

사용자 앱에서 서비스 신임 정보가 하드 코딩된 경우 사용자 앱이 {{site.data.keyword.Bluemix_notm}} 서비스에 액세스하려 하면 권한 오류가 발생합니다. 

{{site.data.keyword.Bluemix_notm}} 서비스와 통신하도록 사용자 앱을 구성한 다음 {{site.data.keyword.Bluemix_notm}}에 앱을 배치하십시오. 그러나 앱을 사용하여 {{site.data.keyword.Bluemix_notm}} 서비스에 액세스할 수는 없으며 권한 오류가 수신됩니다.
{: tsSymptoms}

앱에 하드 코딩된 신임 정보가 올바르지 않습니다. 서비스가 다시 작성될 때마다 이에 액세스하기 위한 신임 정보가 변경됩니다.
{: tsCauses}


앱에서 신임 정보를 하드 코딩하는 대신 VCAP_SERVICES 환경 변수의 연결 매개변수를 사용하십시오. VCAP_SERVICES 환경 변수를 통해 연결 매개변수를 사용하는 메소드는 프로그램 언어마다 다릅니다. 예를 들어, Node.js 앱의 경우에는 다음 명령을 사용할 수 있습니다. 
{: tsResolve}

```
process.env.VCAP_SERVICES
```
다른 프로그램 언어로 사용할 수 있는 명령에 대한 자세한 정보는 [Java](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} 및
[Ruby](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}를 참조하십시오. 
 

 
 




## IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}를 사용하여 앱을 배치할 수 없음
{: #ts_bm_tools_facet}

지원되지 않는 패싯이 Eclipse 프로젝트에 적용되는 경우 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}를 사용하여 사용자 앱을 {{site.data.keyword.Bluemix_notm}}에 배치할 수 없습니다. 

 

Cloud Foundry CLI를 사용하여 {{site.data.keyword.Bluemix_notm}}에 앱을 배치할 수 있습니다. 그러나, IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}를 사용하여 앱을 {{site.data.keyword.Bluemix_notm}}에 배치할 수 없으며 다음과 같은 오류 메시지가 표시됩니다. `프로젝트 패싯 <facet_name>이(가) 지원되지 않습니다.` 예를 들어, `Project facet Cloud Foundry Standalone Application 버전 1.0은 지원되지 않습니다.`
{: tsSymptoms}

 

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}는 프로젝트 패싯 단위로 {{site.data.keyword.Bluemix_notm}} 런타임에 프로젝트를 맵핑합니다. 패싯은 Eclipse에서 Java EE 프로젝트의 요구사항을 정의하고, 서로 다른 런타임이 서로 다른 프로젝트와 연관될 수 있도록 런타임 구성의 일부로 사용됩니다. IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}에서 지원하지 않는 프로젝트에 패싯이 적용되는 경우, IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}를 사용하여 앱을 배치할 수 없습니다.
{: tsCauses}


IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}를 사용하여 앱을 배치할 수 있으려면 Eclipse 프로젝트에서 패싯을 제거해야 합니다.
{: tsResolve} 

패싯을 제거하려면 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}에서 프로젝트에 대해 **프로젝트>특성>프로젝트 패싯**을 클릭하십시오. 그런 다음 지원되지 않는 패싯의 선택란을 선택 취소하십시오. 



## 502 잘못된 게이트웨이 오류가 수신됨
{: #ts_502_error}

{{site.data.keyword.Bluemix_notm}}에서 앱과 상호작용할 때 502 잘못된 게이트웨이 오류가 수신되면 {{site.data.keyword.Bluemix_notm}} 상태 페이지를 확인한 후 적절하게 조치를 취하십시오.

 

502 Bad Gateway로 시작하는 오류 메시지를 수신합니다. 예를 들어, `502 Bad Gateway: Registered endpoint failed to handle the request`가 표시될 수 있습니다.
{: tsSymptoms}

 

잘못된 게이트웨이 오류는 사이트를 호스팅하는 기본 서버의 데이터를 저장하고 릴레이하기 위해 프록시 서버를 사용하는 웹 사이트를 방문할 때 일반적으로 발생합니다. 기본 서버와 프록시 서버가 제대로 연결되지 않았을 수 있으므로 브라우저 창에 HTTP 상태 코드 502가 표시됩니다. 이 상태 코드는 사이트의 기본 서버가 프록시 서버로부터 예상한 HTTP 구현을 수신하지 않았음을 나타냅니다.
{: tsCauses}

잘못된 게이트웨이 오류의 덜 일반적인 기타 원인은 ISP(Internet Service Provider) 드롭아웃, 잘못된 방화벽 구성 및 브라우저 캐시 오류입니다. 

 

{{site.data.keyword.Bluemix_notm}} 서비스가 작동 중지되었다고 의심하는 경우에는 먼저 [{{site.data.keyword.Bluemix_notm}} 상태](https://developer.ibm.com/bluemix/support/#status){: new_window} 페이지를 확인하십시오. 다른 {{site.data.keyword.Bluemix_notm}} 지역의 서비스를 임시 해결책으로 사용할 수 있습니다. 자세한 정보는 [다른 지역에서 서비스 사용](../services/reqnsi.html#cross_region_service){: new_window}에서 확인할 수 있습니다. 서비스 상태가 정상이면 다음의 단계를 수행하여 문제를 해결하십시오.
{: tsResolve}

  * 조치 재시도:
    * 키보드에서 F5를 누르거나 새로 고치기 단추를 클릭하여 페이지를 다시 로드하십시오. 이 단계가 작동하지 않는 경우에는 브라우저의 캐시 및 쿠키를 지운 후 다시 로드하십시오.
	* 다른 브라우저를 사용하십시오.
	* 라우터, 모뎀 및 컴퓨터를 다시 부팅하십시오. 이 디바이스를 다시 부팅하면 오류 502의 원인이 되는 다양한 오류를 정리할 수 있습니다. 
  * 대기한 후 나중에 다시 시도하십시오. 일부 경우에는 인터넷 서비스 제공업체 또는 {{site.data.keyword.Bluemix_notm}} 서비스에 일시적인 문제점이 발생할 수 있습니다. 일시적인 문제점이 해결될 때까지 대기할 수 있습니다.
  * 문제점이 계속 존재하면 {{site.data.keyword.Bluemix_notm}} 지원 센터에 문의하십시오. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 지원 센터에 문의](../support/index.html#contacting-bluemix-support){: new_window}를 참조하십시오. 




## 디스크 할당량이 초과됨
{: #ts_disk_quota}

디스크 공간이 부족한 경우에는 디스크 할당량을 수동으로 수정하여 추가 디스크 공간을 얻을 수 있습니다.

  

디스크 공간이 부족하면 디스크 할당량이 초과되었다는 메시지가 표시됩니다. 이 문제점을 해결하기 위해 앱 인스턴스를 확장하여 추가 디스크 공간을 얻도록 시도했을 수 있습니다. 예를 들어, 앱 세부사항 페이지에서 메모리 할당량을 변경하여 256MB에서 1256MB로 확장했을 수 있습니다. 하지만 디스크 할당량은 동일하게 유지되었기 때문에 추가 디스크 공간을 얻지 못했습니다.
{: tsSymptoms}


하나의 앱에 대해 할당되는 기본 디스크 할당량은 1GB입니다. 추가 디스크 공간이 필요한 경우에는 디스크 할당량을 수동으로 지정해야 합니다.
{: tsCauses}

 
다음 방법 중 하나를 사용하여 디스크 할당량을 지정하십시오. 지정할 수 있는 최대 디스크 할당량은 2GB입니다. 2GB로도 충분하지 않은 경우에는 [오브젝트 저장소](../services/ObjectStorage/index.html){: new_window} 등의 외부 서비스를 사용해 보십시오.
{: tsResolve}

  * manifest.yml 파일에서 다음 항목을 추가하십시오.
    ```
	disk_quota: <disk_quota>
	```
  * 앱을 {{site.data.keyword.Bluemix_notm}}에 푸시할 때
**-k** 옵션을 `cf push` 명령과 함께 사용하십시오.
    ```
	cf push appname -p app_path -k <disk_quota>
	```

	
	
## Git 저장소를 추가할 수 없음
{: #ts_cannot_addgit}

대시보드에서 앱을 작성한 후 Git 추가를 클릭하여 Git 저장소를 작성할 수 있지만 처리할 수는 없습니다.



**Git 추가**를 클릭하면
창이 열리고 다음 문제 중 하나가 발생합니다.
{: tsSymptoms} 

  * 창이 빈 화면 상태로 정지합니다.
  * 써드파티 쿠키와 관련하여 문제점이 발생했다는 메시지가 표시됩니다.



쿠키가 설정되지 않도록 브라우저를
구성할 수 있습니다. 해당 쿠키는 {{site.data.keyword.Bluemix_notm}} 콘솔 컨텍스트 내 hub.jazz.net 인터넷 도메인에 있는 IBM® Bluemix DevOps Services 사이트에서 설정해야 합니다.
{: tsCauses}  

 

다음 방법 중 하나를 사용하여 이러한 문제점을 해결할 수 있습니다.
{: tsResolve}

  * {{site.data.keyword.Bluemix_notm}} 콘솔에서 열리는 창에 나와 있는 지시사항을 따르십시오. 단추를 클릭하십시오. 다른 브라우저 창이 일시적으로 열립니다. 해당 창에서 DevOps Services는 인증 쿠키를 설정합니다.
  * 다른 브라우저 탭에서 https://hub.jazz.net으로 이동하여 로그인하십시오. {{site.data.keyword.Bluemix_notm}} 콘솔로 돌아가서 페이지를 새로 고치십시오. **Git 추가**를 다시 클릭하십시오.
  * 써드파티 쿠키를 지원하도록 브라우저 설정을 변경하고 Git 추가를 다시 클릭하십시오. 설정을 구성하는 방법에 대한 자세한 정보는
브라우저 관련 문서를 참조하십시오.
    * [Mozilla Firefox](https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences#w_how-do-i-change-cookie-settings){: new_window}
	* [Google
Chrome](https://support.google.com/chrome/answer/95647){: new_window}
	* [Apple Safari](https://support.apple.com/kb/PH17191){: new_window}
	* [Microsoft Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies#ie=ie-11){: new_window}
이러한 임시 해결책으로 문제점을 해결하지 못한 경우 idslogin@jazz.net으로 이메일을 보내십시오.



## Android 앱이 푸시 알림을 받을 수 없음
{: #ts_push}

Google이 액세스할 수 없는 특정 지역의 Android 앱은 IBM 푸시 서비스를 통해 사용자가 전송하는 알림을 수신할 수 없습니다. 이 경우에는 써드파티 서비스를 임시 해결책으로 사용할 수 있습니다.

 

Bluemix 앱을 위한 푸시 서비스를 바인딩하고 등록된 디바이스에 메시지를 전송합니다. 하지만 Android 플랫폼에서 개발된 앱이 특정 지역에서 알림을 수신할 수 없습니다.
{: tsSymptoms}

 
IBM 푸시 서비스는 GCM(Google Cloud Messaging) 서비스를 사용하여 알림을 Android 플랫폼에서 개발되는 모바일 앱에 디스패치합니다. Android 앱이 알림을 수신하도록 설정하려면 모바일 앱이 GCM(Google Cloud Messaging) 서비스에 액세스할 수 있어야 합니댜. Android 앱이 GCM 서비스에 도달할 수 없는 지역에서는 Android 앱이 푸시 알림을 수신할 수 없습니다.
{: tsCauses}

 
GCM 서비스에 의존하지 않는 써드파티 서비스를 임시 해결책으로 사용하십시오(예: [Pushy](https://pushy.me){: new_window}, [igetui](http://www.getui.com/){: new_window}, [jpush](https://www.jpush.cn/){: new_window}).
{: tsResolve}



## 조직의 서비스 한계가 초과됨
{: #ts_servicelimit}

평가판 계정 사용자인 경우 조직의 서비스 한계를 초과하면 {{site.data.keyword.Bluemix_notm}}에서 애플리케이션을 작성할 수 없습니다.
 

{{site.data.keyword.Bluemix_notm}}에서 애플리케이션을 작성하려고 할 때 다음과 같은 오류 메시지가 표시됩니다.
{: tsSymptoms}

`BXNUI2032E: <service_instances> 자원이 작성되지 않았습니다. 자원을 작성하기 위해 Cloud Foundry에 접속하는 동안 오류가 발생했습니다. Cloud Foundry 메시지: "조직의 서비스 한계를 초과했습니다."`



이 오류는 사용 중인 계정이 보유할 수 있는 서비스 인스턴스 수에 대한 한계를 초과한 경우에 발생합니다. 평가판 계정의 최대 서비스 인스턴스 수는 10입니다.
{: tsCauses} 

 

필요하지 않은 서비스 인스턴스를 삭제하거나, 보유할 수 있는 서비스 인스턴스 수에 대한 한계를 제거하십시오.
{: tsResolve}
 
  * 서비스 인스턴스를 삭제하려면 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스 또는 명령행 인터페이스를 사용할 수 있습니다.
    {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용하여 서비스 인스턴스를 삭제하려면 다음 단계를 수행하십시오.
	  1. {{site.data.keyword.Bluemix_notm}} 대시보드의 왼쪽 분할창에서 **서비스**를 클릭하십시오. 서비스 타일이 표시됩니다. 
	  2. 삭제하려는 서비스 타일에서 **메뉴** 아이콘을 클릭하십시오.
	  3. **서비스 삭제**를 클릭하십시오. 서비스 인스턴스를 삭제한 후에는 서비스 인스턴스가 바인딩되었던 애플리케이션을 다시 스테이징하라는 메시지가 표시됩니다.
    명령행 인터페이스를 사용하여 서비스 인스턴스를 삭제하려면 다음 단계를 수행하십시오.
	  1. `cf unbind-service <appname> <service_instance_name>`을 입력하여 애플리케이션에서 서비스 인스턴스의 바인드를 해제하십시오.
	  2. `cf delete-service <service_instance_name>`을 입력하여 서비스 인스턴스를 삭제하십시오.
	  3. 서비스 인스턴스를 삭제한 후에는 `cf restage <appname>`을 입력하여 서비스 인스턴스가 바인딩되었던 애플리케이션을 다시 스테이징할 수 있습니다.
  * 보유할 수 있는 서비스 인스턴스 수에 대한 한계를 제거하려면 평가판 계정을 유료 계정으로 변환하십시오. 평가판 계정을 유료 계정으로 변환하는 방법은 [플랜 변경 방법](../pricing/index.html#changing){: new_window}을 참조하십시오.

  
  
## {{site.data.keyword.Bluemix_notm}}에서 실행 파일을 실행할 수 없음
{: #ts_executable}

실행 파일이 다른 환경에서 개발되고 빌드된 경우 해당 실행 파일을 {{site.data.keyword.Bluemix_notm}}에서 실행할 수 없습니다. 

 

실행 파일이 다른 환경에서 개발되고 빌드된 경우 해당 실행 파일을 {{site.data.keyword.Bluemix_notm}}에서 실행할 수 없습니다.
{: tsSymptoms}

 

{{site.data.keyword.Bluemix_notm}}로 푸시하려는 컨텐츠가 이미 실행 파일인 경우 이미 빌드되었으므로 {{site.data.keyword.Bluemix_notm}}에서 빌드할 필요가 없습니다. 이 경우 {{site.data.keyword.Bluemix_notm}}에서 실행 파일을 실행하는 데 빌드팩이 필요하지 않습니다. 그러나 빌드팩이 필요하지 않음을 {{site.data.keyword.Bluemix_notm}}에 명시적으로 표시해야 합니다.
{: tsCauses}

 

실행 파일을 {{site.data.keyword.Bluemix_notm}}로 푸시할 때 빌드팩이 필요하지 않음을 나타내는 null-buildpack을 지정해야 합니다. null-buildpack을 지정하려면 **-b** 옵션을 `cf push` 명령과 함께 사용하십시오.
{: tsResolve}

```
cf push appname -p <app_path> -c <start_command> -b <null-buildpack>
```
예:
```
cf push appname -p <app_path> -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## 조직의 메모리 한계를 초과함
{: #ts_outofmemory}

평가판 계정 사용자인 경우 조직의 메모리 한계를 초과하면 {{site.data.keyword.Bluemix_notm}}에 앱을 배치할 수 없습니다. 앱에서 사용하는 메모리를 줄이거나, 계정의 메모리 할당량을 늘릴 수 있습니다. 



{{site.data.keyword.Bluemix_notm}}에 앱을 배치할 때 다음과 같은 오류 메시지가 표시됩니다.
{: tsSymptoms} 

`서버 실패 오류, 상태 코드: 400, 오류 코드: 100005, 메시지: 조직의 메모리 한계를 초과했습니다. `

 

이 오류는 조직의 남아 있는 메모리의 양이 배치하려는 앱에 필요한 메모리의 양보다 적을 경우에 발생합니다. 평가판 계정의 최대 메모리 할당량은 2GB입니다.
{: tsCauses}



계정의 메모리 할당량을 늘리거나, 앱에서 사용하는 메모리를 줄일 수 있습니다.
{: tsResolve} 

  * 계정의 메모리 할당량을 늘리려면 평가판 계정을 유료 계정으로 변환하십시오. 평가판 계정을 유료 계정으로 변환하는 방법은 [유료 계정](../pricing/index.html#pay-accounts){: new_window}을 참조하십시오. 
  * 앱에서 사용하는 메모리를 줄이려면 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스 또는 cf 명령행 인터페이스를 사용하십시오.
    {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용하는 경우 다음 단계를 완료하십시오.
	  1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 애플리케이션을 선택하십시오. 앱 세부사항 페이지가 열립니다.
	  2. 런타임 페이지에서 앱에 대한 최대 메모리 한계 또는 앱 인스턴스 수를 줄이거나 둘 다 줄일 수 있습니다. 
	cf 명령행 인터페이스를 사용하는 경우 다음 단계를 완료하십시오.
	  1. 앱에 사용 중인 메모리의 양을 확인하십시오.
	  ```
	  cf apps
	  ```
	     cf 앱 명령은 현재 영역에 배치된 앱을 모두 나열합니다. 각 앱의 상태도 표시됩니다.
      2. 앱에서 사용하는 메모리의 양을 줄이려면 앱 인스턴스 수 또는 최대 메모리 한계를 줄이거나 둘 다 줄이십시오.
	  ```
	  cf push <appname> -p <app_path> -i <instance_number> -m <memory_limit>
      ```
	  3. 변경사항이 적용되도록 앱을 다시 시작하십시오.



	  
## 앱이 자동으로 다시 시작되지 않음
{: #ts_apps_not_auto_restarted}


앱에 바인딩된 서비스의 작동이 중지될 때 앱이 자동으로 다시 시작되지 않습니다.	  
	  
 

앱에 바인딩된 서비스가 충돌할 경우 가동 중단, 예외, 연결 실패 등의 문제가 앱에서 발생할 수 있습니다. {{site.data.keyword.Bluemix_notm}}에서는 이러한 문제점에서 복구하기 위해 앱을 자동으로 다시 시작하지 않습니다.
{: tsSymptoms}



이 동작은 Cloud Foundry의 의도된 동작입니다.
{: tsCauses} 

 

명령행 인터페이스에 다음 명령을 입력하여 앱을 수동으로 다시 시작할 수 있습니다.
{: tsResolve}

```
cf push <appname> -p <app_path>
```
또한 가동 중단, 예외, 연결 실패 등의 문제점을 식별하고 이러한 문제점에서 복구하도록 앱을 코딩할 수 있습니다. 

	  

## 애플리케이션이 푸시될 때 사용자 정의 변수가 손실됨
{: #ts_varsnotretained}

앱을 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.Bluemix_notm}}로 푸시하는 경우 Manifest 파일에 변수를 저장하지 않으면 지정한 값이 재설정됩니다.



앱을 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.Bluemix_notm}}로 푸시한 후 지정한 변수가 손실됩니다.
{: tsSymptoms} 


지정한 변수는 Manifest 파일에 저장한 경우에만 저장됩니다.
{: tsCauses} 

 

앱을 IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.Bluemix_notm}}로 푸시하는 경우 애플리케이션 마법사의 애플리케이션 세부사항 페이지에서 **Manifest 파일에 저장** 선택란을 선택하십시오. 그러면 마법사에서 지정한 변수가 애플리케이션의 Manifest 파일에 저장됩니다. 다음에 마법사를 열면 변수가 자동으로 표시됩니다.
{: tsResolve}



## {{site.data.keyword.Bluemix_notm}} Live Sync 아이콘이 표시되지 않음
{: #ts_llz_lkb_3r}

IBM Bluemix DevOps Services에서 앱을 작성했지만 IBM Bluemix Live Sync 아이콘이 Web IDE에 표시되지 않습니다.

 

DevOps Services Web IDE에서 Node.js 앱을 편집할 때 {{site.data.keyword.Bluemix_notm}} 실시간 편집, 빠른 다시 시작 및 디버그 아이콘이 표시되지 않습니다.
{: tsSymptoms}

 

다음과 같은 경우 이 아이콘을 사용할 수 없습니다.
{: tsCauses}

  * `manifest.yml` 파일이 프로젝트의 최상위 레벨에 저장되지 않았습니다.
  * 앱이 프로젝트의 최상위 레벨이 아닌 서브디렉토리에 저장되었지만, 이 서브디렉토리의 경로가 `manifest.yml` 파일에 지정되어 있지 않습니다.
  * 앱에 `package.json` 파일이 없습니다.


다음 방법 중 하나를 사용하여 문제점을 해결하십시오. 
{: tsResolve} 

  * `manifest.yml` 파일이 프로젝트의 최상위 레벨에 저장되지 않은 경우 여기에 저장하십시오.
  * 앱이 서브디렉토리에 저장된 경우 `manifest.yml` 파일에 서브디렉토리의 경로를 지정하십시오.
  ```
   path: path_to_application
   ```
  * 앱과 동일한 디렉토리에 `package.json` 파일을 작성하십시오.

  
  
  

  
  

  
  
## {{site.data.keyword.Bluemix_notm}}에서 조직을 찾을 수 없음
{: #ts_orgs}

{{site.data.keyword.Bluemix_notm}} 지역에서 작업할 때 {{site.data.keyword.Bluemix_notm}}에서 조직을 찾을 수 없습니다.
  
 

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에 로그인할 수는 있지만, cf 명령행 인터페이스 또는 Eclipse 플러그인을 사용하여 앱을 푸시할 수 없습니다.
{: tsSymptoms}

cf 명령행 인터페이스를 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}로 푸시하려고 할 때 다음과 같은 오류 메시지가 표시되고 해당 메시지에 지정된 조직 이름도 함께 표시됩니다. 

`조직을 찾는 중 오류 발생`

`조직을 찾을 수 없음`


Cloud Foundry Eclipse 플러그인을 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}로 푸시하려고 할 때 다음과 같은 오류 메시지가 표시됩니다.

`cloudspace를 찾을 수 없습니다.`



이 문제점은 작업하는 지역의 API 엔드포인트를 지정하지 않은 경우에 발생합니다. 찾고 있는 조직이 다른 지역에 있을 수 있습니다.
{: tsCauses} 

   
  
cf 명령행 인터페이스를 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}로 푸시한 경우 cf api 명령을 입력하고 지역의 API 엔드포인트를 지정하십시오. 예를 들어 다음 명령을 입력하여 {{site.data.keyword.Bluemix_notm}} 유럽 영국 지역에 연결하십시오.
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Eclipse 도구를 사용하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}로 푸시한 경우 먼저 {{site.data.keyword.Bluemix_notm}} 서버를 작성한 다음 조직이 작성된 {{site.data.keyword.Bluemix_notm}} 지역의 API 엔드포인트를 지정하십시오. Eclipse 도구에 대한 자세한 정보는 [IBM Eclipse Tools for Bluemix를 사용하여 앱 배치](../manageapps/eclipsetools/eclipsetools.html){: new_window}를 참조하십시오.  
  
  


## 앱 라우트를 작성할 수 없음
{: #ts_hostistaken}

앱을 {{site.data.keyword.Bluemix_notm}}에 배치할 때 지정한 호스트 이름이 이미 사용 중일 경우 앱 라우트를 작성할 수 없습니다.



{{site.data.keyword.Bluemix_notm}}에 앱을 배치할 때 다음과 같은 오류 메시지가 표시됩니다. 
{: tsSymptoms} 

`hostname.domainname 라우트 작성 중... 서버 실패 오류, 상태 코드: 400, 오류 코드: 210003, 메시지: 호스트가 사용됨: hostname`



이 문제점은 지정한 호스트 이름이 이미 사용 중일 경우에 발생합니다.
{: tsCauses} 


  
지정한 호스트 이름은 사용 중인 도메인 내에서 고유해야 합니다. 다른 호스트 이름을 지정하려면 다음 방법 중 하나를 사용하십시오.
{: tsResolve} 

  * `manifest.yml` 파일을 사용하여 애플리케이션을 배치하는 경우 host 옵션에 호스트 이름을 지정하십시오.	 
    ```
    host: <hostname>	
	```
  * 명령 프롬프트에서 애플리케이션을 배치하는 경우 `cf push` 명령을 **-n** 옵션과 함께 사용하십시오.
    ```
    cf push <appname> -p <app_path> -n <hostname>
    ```


## cf push 명령을 사용하여 WAR 앱을 푸시할 수 없음
{: #ts_cf_war}

앱 위치를 올바르게 지정하지 않은 경우 cf push 명령을 사용하여 아카이브된 웹 앱을 {{site.data.keyword.Bluemix_notm}}에 배치할 수 없습니다.
	


`cf push` 명령을 사용하여 WAR 앱을 {{site.data.keyword.Bluemix_notm}}에 업로드할 때 `스테이징 오류: 스테이징 실패로 인스턴스를 가져올 수 없음`이라는 오류 메시지가 표시됩니다.
{: tsSymptoms} 

 

이 문제점은 WAR 파일을
지정하지 않았거나 WAR 파일의 경로를 지정하지 않은 경우에 발생할 수 있습니다. 
{: tsCauses}

 	
	
**-p** 옵션을
사용하여 WAR 파일을 지정하거나 WAR 파일의 경로를 추가하십시오. 예:
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
`cf push` 명령에
대한 자세한 정보를 보려면 `cf push -h`를 입력하십시오. 	





## Liberty 애플리케이션을 {{site.data.keyword.Bluemix_notm}}로 푸시할 때 2바이트 문자가 올바르게 표시되지 않음
{: #ts_doublebytes}

서블릿 또는 JSP 파일에 대해 유니코드 지원이 제대로 구성되지 않은 경우 2바이트 문자가 올바르게 표시되지 않을 수 있습니다.

 

Liberty 애플리케이션을 {{site.data.keyword.Bluemix_notm}}로 푸시할 때 앱 내에 지정된 2바이트 문자가 올바르게 표시되지 않습니다.
{: tsSymptoms}

 

이 문제점은 서블릿 또는
JSP 파일에 대해 유니코드 지원이 제대로 구성되지 않은 경우에 발생할 수 있습니다.
{: tsCauses}


서블릿 또는
JSP 파일에서 다음 코드를 사용할 수 있습니다.
{: tsResolve} 

  * 서블릿 소스 파일 
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * JSP 
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## Node.js 앱을 배치할 수 없음
{: #ts_nodejs_deploy}

Node.js 앱을 업데이트하거나 {{site.data.keyword.Bluemix_notm}}에 배치할 때 문제점이 발생할 수 있습니다.



Node.js 앱을 업데이트하거나 {{site.data.keyword.Bluemix_notm}}에 배치할 때 다음 오류 메시지 중 하나가 표시될 수 있습니다.
{: tsSymptoms} 

`사용 가능한 빌드팩에서 앱을 발견하지 못했습니다.`


`인스턴스(인덱스 0)가 연결 승인을 시작하는 데 실패했습니다.`


`스테이징 실패로 인스턴스를 가져올 수 없음`


 

다음과 같은 이유가 문제점의 원인일 수 있습니다.
{: tsCauses}
 
  * 시작 명령을 지정하지 않았습니다.
  * Node.js 앱을 배치하는 데 필요한 파일이 앱에서 누락되었거나 루트 디렉토리 이외의 다른 폴더에 있습니다.
  


	
문제점의 원인에 따라 다음 조치를 수행하십시오.
{: tsResolve} 

  * 다음 방법 중 하나로 시작 명령을 지정하십시오. 
      * cf 명령행 인터페이스를 사용하십시오. 예: 
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * [package.json](https://docs.npmjs.com/json){: new_window} 파일을 사용하십시오. 예를 들어, 다음과 같습니다.
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
	  * `manifest.yml` 파일을 사용하십시오. 예를 들어, 다음과 같습니다. 
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Node.js 빌드팩에서 앱을 인식할 수 있게 하려면 Node.js 앱에 `package.json` 파일이 존재하도록 하십시오. 또한 이 파일을 앱의 루트 디렉토리에 두어야 합니다.	
    다음 예에서는 단순한 `package.json` 파일을 보여줍니다.  
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
Node.js 앱에 대한 추가 팁은 [Node.js 애플리케이션에 대한 팁](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}의 내용을 참조하십시오.	




## {{site.data.keyword.Bluemix_notm}} Liberty 앱을 Bluemix DevOps Services에서 Eclipse로 가져온 후 `server.xml` 파일에서 구성 오류가 나타남
{: #ts_eclipse}

{{site.data.keyword.Bluemix_notm}} Liberty 앱을 IBM Bluemix DevOps Services에서 Eclipse로 가져온 후 `server.xml` 파일에 구성 오류가 표시될 경우, 프로젝트에서 `server.xml` 파일을 제거해야 할 수 있습니다. 

 

{{site.data.keyword.Bluemix_notm}} Liberty 앱을 {{site.data.keyword.Bluemix_notm}} DevOps Services에서 Eclipse로 가져온 후 Eclipse 문제점 보기의 `server.xml` 파일에 구성 오류가 표시됩니다. 
{: tsSymptoms}

 

Liberty 앱이 {{site.data.keyword.Bluemix_notm}}로 푸시되면 Liberty 빌드팩은 `server.xml` 파일을 사용하여 앱을 구성하고 `runtime-vars.xml` 파일을 생성합니다. 앱을 Eclipse로 가져오면 `runtime-vars.xml` 파일이 로컬 환경에 없습니다.
{: tsCauses}

 

이 문제점은 프로젝트에서 server.xml 파일을 제거하여 해결할 수 있습니다. 앱을 WAR 앱으로 푸시하면 빌드팩이 동적으로 `server.xml` 파일을 작성합니다. 자세한 정보는 [Liberty for Java](../runtimes/liberty/index.html){: new_window}를 참조하십시오.
{: tsResolve}
	
	
## 사용자 정의 빌드팩을 사용하여 앱을 스테이징할 수 없음
{: #ts_bp_compilation}

빌드팩 내에 있는 스크립트가 실행 가능하지 않을 경우 사용자 정의 빌드팩을 사용하여 앱을 {{site.data.keyword.Bluemix_notm}}에 배치할 수 없습니다.



사용자 정의 빌드팩을 사용하여 앱을 {{site.data.keyword.Bluemix_notm}}에 배치할 때 `애플리케이션이 스테이징에 실패했으므로 표시할 인스턴스가 없습니다.`라는 오류 메시지가 표시됩니다.
{: tsSymptoms} 


이 문제점은 발견 스크립트, 컴파일 스크립트, 릴리스 스크립트 등의 스크립트가 실행 가능하지 않을 경우에 발생합니다.
{: tsCauses}

 

[git update](http://git-scm.com/docs/git-update-index){: new_window} 명령을 사용하여 각 스크립트의 권한을 실행 가능으로 변경할 수 있습니다. 예를 들어 `git update --chmod=+x script.sh`를 입력합니다.
{: tsResolve}
	
	
	
## 앱을 DevOps Services에서 {{site.data.keyword.Bluemix_notm}}로 배치할 수 없음
{: #ts_devops_to_bm}

앱 내에 `manifest.yml` 파일이 없는 경우 앱을 IBM Bluemix DevOps Services에서 {{site.data.keyword.Bluemix_notm}}로 푸시할 수 없습니다.

 

앱을 DevOps Services에서 {{site.data.keyword.Bluemix_notm}}로 배치할 때 `지원되는 애플리케이션 유형을 찾을 수 없음`이라는 오류 메시지가 표시될 수 있습니다.
{: tsSymptoms}

 

앱을 {{site.data.keyword.Bluemix_notm}}에 배치하려면 DevOps Services에 `manifest.yml` 파일이 필요하기 때문에 이 문제점이 발생합니다.
{: tsCauses}

 

이 문제점을 해결하려면 `manifest.yml` 파일을 작성해야 합니다. `manifest.yml` 파일을 작성하는 방법에 대한 자세한 정보는 [애플리케이션 Manifest](../manageapps/depapps.html#appmanifest){: new_window}를 참조하십시오.
{: tsResolve}	
	




## Meteor 앱을 푸시할 수 없음
{: #ts_meteor}

빌드팩을 올바르게 지정하지 않은 경우 Meteor 애플리케이션을 {{site.data.keyword.Bluemix_notm}}로 푸시할 수 없습니다.

 

Meteor 앱을 {{site.data.keyword.Bluemix_notm}}에 배치할 때 `애플리케이션이 스테이징에 실패했으므로 표시할 인스턴스가 없습니다.`라는 오류 메시지가 표시될 수 있습니다.
{: tsSymptoms}


이 문제점은 Meteor 앱에 기본 제공 빌드팩이 제공되지 않은 경우에 발생합니다. 사용자 정의 빌드팩을 사용해야 합니다.
{: tsCauses} 


 

Meteor 앱에 대해 사용자 정의 빌드팩을 사용하려면 다음 방법 중 하나를 사용하십시오.
{: tsResolve}

  * `manifest.yml` 파일을 사용하여 앱을 배치하는 경우 buildpack 옵션을 사용하여 사용자 정의 빌드팩의 URL 또는 이름을 지정하십시오. 예:
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * 명령 프롬프트에서 애플리케이션을 배치하는 경우 `cf push` 명령을 사용하되 **-b** 옵션을 사용하여 사용자 정의 빌드팩을 지정하십시오. 예:
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor
	```
	
  

    
## {{site.data.keyword.Bluemix_notm}}에 배치 단추로 앱이 배치되지 않음
{: #deploytobluemixbuttondoesntdeployanapp}

{{site.data.keyword.Bluemix_notm}}에 배치 단추를 클릭해도 Git 저장소가 복제되지 않거나 앱이 배치되지 않는 경우 다음 문제에 대한 문제점 해결 방법을 사용해 보십시오.
  * [Bluemix DevOps Services 프로젝트를 작성할 수 없음](#project-cannot-be-created)
  * [Git 저장소를 찾을 수 없어 DevOps Services에 복제할 수 없음](#repo-not-found)
  * [Git 저장소가 DevOps Services에 복제되었지만 앱이 {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed)에 배치되지 않음.
단추 작성 방법에 대한 자세한 정보는 {{site.data.keyword.Bluemix_notm}}로 배치 단추 작성을 참조하십시오.

### Bluemix DevOps Services 프로젝트를 작성할 수 없음
{: #project-cannot-be-created}

DevOps Services 프로젝트를 작성할 수 없다면 IBM {{site.data.keyword.Bluemix_notm}} 계정이 만료된 것일 수 있습니다.



**Bluemix에 배치** 단추를 클릭했지만 "프로젝트 작성" 단계가 성공적으로 완료되지 않았습니다.
{: tsSymptoms} 


{{site.data.keyword.Bluemix_notm}} 계정이 만료되었을 수 있습니다.
{: tsCauses} 

다음 방법 중 하나를 사용하여 문제점을 수정하십시오.
{: tsResolve}

  * {{site.data.keyword.Bluemix_notm}}에 로그인하여
자신의 계정 정보를 업데이트하십시오.
  * **Bluemix에 배치** 단추를 다시 클릭하십시오.


### Git 저장소를 찾을 수 없어 DevOps Services에 복제할 수 없음
{: #repo-not-found}

Git 저장소가 복제되지 않은 경우 저장소 또는 단추 스니펫 관련 문제일 수 있습니다.



**Bluemix에 배치** 단추를 클릭했지만 Git 저장소를 찾을 수 없어 DevOps Services에 복제할 수 없습니다. "저장소 복제" 단계가 성공적으로 완료되지 않았습니다. 따라서 앱을 {{site.data.keyword.Bluemix_notm}}에 배치할 수 없습니다. 
{: tsSymptoms} 

이 문제점은 다음과 같은 이유로 발생할 수 있습니다.
{: tsCauses} 

  * Git 저장소가 없거나 Git 저장소에 액세스할 수 없습니다.
  * 단추 스니펫에 대한 HTML 또는 마크다운에 문제가 있을 수 있습니다.
  * 특수 문자, 조회 매개변수 또는 URL의 단편으로 인해 Git 저장소에 올바르게 액세스할 수 없는 문제가 있을 수 있습니다.

다음 방법 중 하나를 사용하여 문제점을 수정하십시오.
{: tsResolve}

  * Git 저장소가 있고, 공개적으로 액세스할 수 있으며, URL이 올바른지 확인하십시오.
  * 스니펫에 HTML 또는 마크다운 오류가 있지 않은지 확인하십시오.
  * 특수 문자, 조회 매개변수 또는 단편으로 인해 Git 저장소 URL에 문제가 있는 경우, 단추 스니펫에서 URL을 인코딩하십시오.
  

  
  
### Git 저장소가 DevOps Services에 복제되었지만 앱이 {{site.data.keyword.Bluemix_notm}}에 배치되지 않음
{: #repo-cloned-app-not-deployed}

앱이 배치되지 않은 경우 저장소의 코드와 관련한 문제가 발생할 수 있습니다.
     


**Bluemix에 배치** 배치 단추를 클릭한 후 Git 저장소가 DevOps Services에 복제되었지만, 앱이 {{site.data.keyword.Bluemix_notm}}에 배치되지 않았습니다. "Bluemix에 배치" 단계가 성공적으로 완료되지 않았습니다.
{: tsSymptoms} 

이 문제점은 다음과 같은 이유로 발생할 수 있습니다.
{: tsCauses}  

  * {{site.data.keyword.Bluemix_notm}} 영역에 앱 배치에 필요한
충분한 공간이 없을 수 있습니다. 
  * 필수 서비스가 `manifest.yml` 파일에서 선언되지 않았을 수 있습니다.
  * 필수 서비스가 `manifest.yml` 파일에서 선언되었지만
해당 서비스가 이미 대상 영역에 있을 수 있습니다.
  * 저장소의 코드에 문제가 있을 수 있습니다.
문제를 진단하려면
배치에서 빌드 및 배치 로그를 검토하십시오.
  1. "Bluemix에 배치" 단계가 성공적으로 완료되지 않은 경우, 이전 "파이프라인 구성" 단계에 있는 링크를 클릭하여 Delivery Pipeline을 여십시오.
  2. 실패한 빌드 또는 배치 단계를 식별하십시오.
  3. 실패한 단계에서 **로그 및 히스토리 보기**를 클릭하십시오.
  4. 오류 메시지를 찾으십시오.
   
다음 방법 중 하나를 사용하여 문제점을 수정하십시오.
{: tsResolve}

  * {{site.data.keyword.Bluemix_notm}} 영역에
앱 배치에 필요한 충분한 공간이 없다고 오류 메시지에 표시된 경우 다른 영역을 대상으로 지정하십시오.
  * 필수 서비스가 `manifest.yml` 파일에서 선언되지
않았다고 오류 메시지에 표시된 경우 필수 서비스를 추가해야 한다는 사실을 저장소 소유자에게
알리십시오.
  * 필수 서비스가 이미 대상 영역에 있다고 오류 메시지에 표시된 경우 다른 영역을 사용하도록
선택하십시오.
  * 빌드와 관련하여 문제가 있다고 오류 메시지에 표시된 경우 앱 빌드를 방해하는
코드와 관련된 문제를 수정하십시오. 코드에 문제가 없는지 확인하려면 Git 명령을
사용하여 코드를 빌드하십시오.
    1. Git 저장소를 복제하십시오.
    ```
    git clone <git_repository_URL>
    ```
	2. 앱 디렉토리를 여십시오.
	```
	cd <appname>
	```
	3. 앱을 작성하십시오.
	```
	<appname> create
	```
	4. 필요한 경우 추가 기능을 프로비저닝하십시오.
	5. 필요한 구성 변수를 추가하십시오.
	6. 코드를 푸시하십시오.
	```
	git push <appname> master
	```
	7. 앱이 올바르게 빌드되었는지 확인하십시오.
	8. 필요한 경우 배치 후 명령을 실행하십시오.
	```
	<appname> run
	```
	9. 앱을 열고 앱이 올바르게 작동하는지 확인하십시오.
	```
	<appname> open
	```
	



# 계정 관리 문제점 해결
{: #managingaccounts}

계정을 관리할 때 여러 앱이 동일한 도메인 이름을 공유하거나 관리자가 일부 조직을 볼 수 없는 것과 같은 문제점이 발생할 수 있습니다. 그러나 대부분의 경우
몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다. 
{:shortdesc}


## 계정이 비활성화됨
{: #ts_accnt_inactive}

계정이 비활성 상태일 경우 {{site.data.keyword.Bluemix_notm}}에서 앱을 작성할 수 없습니다. 이 문제점을 해결하려면 지원 팀에 문의해야 합니다.



{{site.data.keyword.Bluemix_notm}}에서 앱을 작성하려고 할 때 다음과 같은 오류 메시지가 표시됩니다.
{: tsSymptoms} 

`BXNUI0096E: 앱이 작성되지 않았습니다. 계정이 취소되었거나 일시중단되었으므로
비활성 상태입니다.`


계정이 취소되었거나 일시중단된 경우 {{site.data.keyword.Bluemix_notm}} 계정의 상태가 비활성화됩니다.
{: tsCauses}

 

계정을 다시 활성화하려면 [{{site.data.keyword.Bluemix_notm}} 지원 센터](http://ibm.biz/bluemixsupport.com){: new_window}에 문의하십시오. 이메일에 다음 정보를 포함해야 합니다.
{: tsResolve}

  * {{site.data.keyword.Bluemix_notm}}에 로그인하는 데 사용할 IBM ID
  * 작성하는 앱이 속할 조직의 이름. 이 정보는 지원 팀이 조직 내 사용자에게 올바른 역할 또는 멤버십이 지정되었는지 판별하는 데 도움이 됩니다.



## 영역이 현재 조직과 연관되어 있지 않음
{: #ts_no_space}

영역이 현재 조직과 연관되어 있지 않은 경우
애플리케이션을 작성할 수 없습니다.



{{site.data.keyword.Bluemix_notm}}에서 앱을 작성하려고 할 때 다음과 같은 오류 메시지가 표시됩니다.
{: tsSymptoms} 


`BXNUI0097E: 앱을 추가하려면 하나 이상의 영역을 조직 및 지역과 연관시켜야 합니다. 대시보드에서 **영역 작성**을 클릭하십시오. 영역이 작성되면 다시 시도하십시오.`



{{site.data.keyword.Bluemix_notm}}의 앱은 조직 아래의 영역 내에 작성되어야 합니다.
{: tsCauses} 

 

영역을 작성하려면 다음 방법 중 하나를 사용하십시오. 
{: tsResolve}
 
  * {{site.data.keyword.Bluemix_notm}} 대시보드에서 영역을 작성할 조직을 선택한 다음 **영역 작성**을 클릭하십시오.
  * cf 명령행 인터페이스에서 ```cf create-space <space_name> -o <organization_name>```을 입력하십시오.
  
  
  
  
## 서로 다른 애플리케이션의 도메인 이름이 동일함
{: #ts_domain_diff}

{{site.data.keyword.Bluemix_notm}}에서
여러 애플리케이션이 동일한 URL을 공유할 수 있습니다.

 

이 문제점은 한 영역 내의 서로 다른 애플리케이션에 대해 동일한 URL 라우트를 지정한 경우에 발생할 수 있습니다.
{: tsCauses}

예를 들어, myApp1 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 푸시하고 도메인을 "mynewapp.mybluemix.net"으로 설정합니다. 그런 다음 다른 myApp2 애플리케이션을 동일한 영역에 푸시하고 URL 라우트 중 하나를 "mynewapp.mybluemix.net"으로 설정하십시오. 이제 해당 라우트가 두 애플리케이션 모두에 맵핑되었습니다.

 

이는 {{site.data.keyword.Bluemix_notm}}의 지원되는 동작이므로 이 동작을 사용하여 애플리케이션 업그레이드 시 무중단을 실현할 수 있습니다. 자세한 정보는 Blue-Green 배치를 참조하십시오.
{: tsResolve}
  
	
	





## 신용카드를 추가할 수 없음
{: #ts_addcc}

평가판 계정을 종량과금제 계정으로 변환하기 위해 신용카드 정보를 제출할 수 없습니다.

 

신용카드 추가 페이지의 제출 단추가 비활성화되어 있습니다.
{: tsSymptoms}

 

이 문제점은 신용카드 추가 페이지에 정보가 올바르게 채워지지 않은 경우에 발생합니다.
{: tsCauses}

 

이 문제점을 해결하려면 다음 단계를 수행하십시오.
{: tsResolve}

  1. 신용카드 추가 페이지에서 연락처 정보, 연락처 주소, 청구 주소 섹션에 있는 모든 필수 필드에 정보를 입력하십시오.
  2. **IBM 이용 약관을 읽고 동의함**을 선택한 다음 **제출**을 클릭하십시오. **지불 방법** 섹션이 표시됩니다.
  3. 신용카드 번호, 카드 만기 날짜 및 카드 상의 보안 코드를 입력하십시오. 그런 다음 **제출**을 클릭하십시오.





# 런타임 문제점 해결
{: #runtimes}

IBM® Bluemix™ 런타임을 사용할 때 문제점이 발생할 수 있습니다. 그러나 대부분의 경우
몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다. 
{:shortdesc}


## 앱을 푸시할 때 더 이상 사용되지 않는 빌드팩이 캐시에서 로드됨
{: #ts_loading_bp}


앱을 푸시할 때 최신 빌드팩 컴포넌트를 사용하지 못할 수 있습니다. 더 이상 사용되지 않는 컴포넌트가 로드되지 않도록 기본 제공되는 메커니즘이 있는 빌드팩을 사용하거나, 앱을 푸시하거나 다시 스테이징하기 전에 앱의 캐시 디렉토리에서 컨텐츠를 삭제할 수 있습니다. 

 

빌드팩을 업데이트한 후 앱을 푸시하거나 다시 스테이징할 때 최신 빌드팩 컴포넌트가 자동으로 로드되지 않습니다. 결과적으로 앱에서 더 이상 사용되지 않는 빌드팩 컴포넌트를 사용합니다. 앱을 마지막으로 푸시한 후 빌드팩에 적용한 업데이트는 구현되지 않습니다. 
{: tsSymptoms}



사용자가 항상 최신 버전을 사용하도록 일부 빌드팩은 인터넷에서 업데이트된 모든 컴포넌트를 자동으로 다운로드하도록 구성되지 않았습니다.
{: tsCauses} 

 

더 이상 사용되지 않는 컴포넌트를 로드하지 않도록 기본 제공 메커니즘이 있는 빌드팩을 사용할 수 있습니다. 두 가지 예로 다음 빌드팩이 있습니다. 
{: tsResolve}

  * [Cloud Foundry Java 빌드팩](https://github.com/cloudfoundry/java-buildpack){: new_window}. 최신 버전의 빌드팩을 사용하도록 이 빌드팩에는 기본 메커니즘이 포함되어 있습니다. 이 메커니즘의 작동 방식에 대한 자세한 정보는 [extending-caches.md](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}를 참조하십시오. 
  * [Cloud Foundry Node.js 빌드팩](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. 이 빌드팩은 환경 변수를 사용하여 비슷한 기능을 수행합니다. Node.js 빌드팩이 항상 인터넷에서 노드 모듈을 다운로드하게 하려면 cf 명령행 인터페이스에서 다음 명령을 입력하십시오. 	
  ```
  set NODE_MODULES_CACHE=false
  ```
사용 중인 빌드팩에서 자동으로 최신 컴포넌트를 로드하는 메커니즘을 제공하지 않는 경우 수동으로 캐시 디렉토리에서 컨텐츠를 삭제하고 다음 단계를 수행하여 앱을 푸시할 수 있습니다.
  1. 널 빌드팩의 분기를 체크아웃합니다(예: https://github.com/ryandotsmith/null-buildpack). 분기를 체크아웃하는 방법에 대한 정보는 [Git 기본 - Git 저장소 가져오기](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}를 참조하십시오.  
  2. `null-buildpack/bin/compile` 파일에 다음 링크를 추가하고 변경사항을 커미트합니다. 변경사항을 커미트하는 방법에 대한 정보는 [Git 기본 - 저장소에 변경사항 기록](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}을 참조하십시오.
  ```
  rm -rfv $2/*
  ```
  3. 다음 명령을 사용하여 캐시를 삭제하기 위해 수정한 널 빌드팩으로 앱을 푸시합니다. 이 단계를 완료하고 나면 앱의 캐시 디렉토리에 있는 모든 컨텐츠가 삭제됩니다.
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
  4. 다음 명령을 사용하여 사용할 최신 빌드팩으로 앱을 푸시합니다. 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
  
	


## PHP 빌드팩의 NOTICE 메시지
{: #ts_phplog}

로그에 NOTICE가 포함된 메시지가 표시될 수 있습니다. 로깅 레벨을 변경하여 이러한 메시지의 로깅을 중지할 수 있습니다.	
	
 

PHP 빌드팩을 사용하여 애플리케이션을 Bluemix로 푸시할 때 `NOTICE`가 포함된 메시지가 표시될 수 있습니다.
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



PHP 빌드팩에서 error_log 매개변수는 로깅 레벨을 정의하는 데 사용됩니다. 기본적으로 `error_log` 매개변수의 값은 **stderr notice**입니다. 다음 예에서는 Cloud Foundry에서 제공하는 PHP 빌드팩의 `nginx-defaults.conf` 파일에 있는 기본 로깅 레벨 구성을 보여줍니다. 자세한 정보는 [cloudfoundry/php-buildpack](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}을 참조하십시오.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
`NOTICE` 메시지는 정보 메시지일 뿐 반드시 문제점이 발생했음을 의미하는 것은 아닙니다. 빌드팩의 nginx-defaults.conf 파일에서 로깅 레벨을 stderr notice에서 stderr error로 변경하여 메시지 로깅을 중지할 수 있습니다. 예를 들어, 다음과 같습니다. 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
기본 로깅 구성을 변경하는 방법에 대한 자세한 정보는 [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}를 참조하십시오.
	

## 써드파티 Python 라이브러리를 {{site.data.keyword.Bluemix_notm}}로 가져올 수 없음
{: #ts_importpylib}

써드파티 Python 라이브러리를 {{site.data.keyword.Bluemix_notm}}로 가져오지 못할 수 있습니다. Python 애플리케이션의 루트 디렉토리에 구성 파일을 추가하여 이 문제를 해결할 수 있습니다.


써드파티 Python 라이브러리(예: `web.py` 라이브러리)를 가져오려고 하면 `cf push` 명령이 실패합니다.
{: tsSymptoms}


 

이 문제점은 Python 애플리케이션에 대한 구성 정보가 누락된 경우에 발생합니다.
{: tsCauses}


 

문제점을 해결하려면 `requirements.txt` 파일과 `Procfile` 파일을 Python 앱의 루트 디렉토리에 추가하십시오. 다음 정보는 web.py 라이브러리를 가져온다고 가정합니다.
{: tsResolve}

  1. `requirements.txt` 파일을 Python 앱의 루트 디렉토리에 추가하십시오.
     `requirements.txt` 파일에는 Python 애플리케이션에 필요한 라이브러리 패키지와 패키지 버전이 지정되어 있습니다. 다음 예에서는 `requirements.txt` 파일의 컨텐츠를 보여줍니다. 여기서 `web.py==0.37`은 다운로드할 `web.py` 라이브러리의 버전이 0.37임을 나타내고, `wsgiref==0.1.2`는 web.py 라이브러리에 필요한 웹 서버 게이트웨이 인터페이스가 0.1.2임을 나타냅니다.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	`requirements.txt` 파일을 구성하는 방법에 대한 자세한 정보는 [Requirements files](https://pip.readthedocs.org/en/1.1/requirements.html)를 참조하십시오. 
	 
  2. `Procfile` 파일을 Python 애플리케이션의 루트 디렉토리에
추가하십시오.
	`Procfile` 파일에는 Python 애플리케이션의
시작 명령이 포함되어 있어야 합니다. 다음 명령에서 *yourappname*은 Python 애플리케이션의 이름이고, *PORT*는 Python 애플리케이션이 앱 사용자로부터 요청을 수신할 때 사용해야 하는 포트 번호입니다. *$PORT*는 선택사항입니다. 시작 명령에 PORT를 지정하지 않으면 앱 내에 있는 `VCAP_APP_PORT` 환경 변수 아래의 포트 번호가 대신 사용됩니다. 
	```
	web: python <yourappname>.py $PORT
	```
이제 써드파티
Python 라이브러리를 {{site.data.keyword.Bluemix_notm}}로
가져올 수 있습니다.	



## 인스턴스 세부사항 페이지의 조치 단추가 비활성화됨
{: #ts_actionsbutton}



인스턴스 세부사항 페이지의 조치 단추가 비활성화되어 있습니다.
{: tsSymptoms} 

 

이 문제점은 다음과 같은 이유로
발생합니다.
{: tsCauses}

  * 애플리케이션이 Java™ 웹 애플리케이션이 아닙니다. RMU(Runtime Management Utilities)에서는 Liberty 빌드팩을 사용하여 배치된 웹 애플리케이션만
지원합니다.
  * 애플리케이션이 임베디드 Liberty 빌드팩을 사용하여 배치되지 않았습니다.
  * 애플리케이션이 이전 버전의 Liberty 빌드팩을 사용하여 배치되었습니다.



이전 버전의 Liberty 빌드팩으로 인해 문제점이 발생한 경우 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 다시 배치하십시오. 그렇지 않은 경우 다음과 같은 클라이언트 애플리케이션 로그 파일을 지원 팀에 제공하십시오.
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## 추적 또는 덤프 창을 열 때 신임 정보가 필요함
{: #ts_username}


 

추적 및 덤프 창을 열 때
사용자 이름과 비밀번호가 필요합니다.
{: tsSymptoms}

 

이 문제점은 로그인 세션 제한시간 초과로
인해 발생합니다.
{: tsCauses}

 

솔루션은 사용자 이름과 비밀번호를 다시 입력하는 것입니다.
{: tsResolve}




## 추적 또는 덤프 오퍼레이션이 실행 중일 때 오류 발생
{: #ts_target}

 

추적 또는 덤프 오퍼레이션이 실행 중일 때
오류 메시지가 표시됩니다. 앱의 대상 인스턴스가 실행 중 상태가 아니라는
메시지가 표시됩니다.	
{: tsSymptoms}

```
Instance 0: Trace specification is set successfully
Instance 2: Trace specification is set successfully
Instance 1: Target instance 1 for app abcd is not in the running state.
Instance 3: Trace specification is set successfully
Instance 4: Trace specification is set successfully
```



이 문제점은 다음과 같은 이유로
발생합니다.
{: tsCauses} 

  * 추적 및 덤프 관리 기능은 실행 중인 애플리케이션 인스턴스에만 사용할
수 있습니다. 중지, 시작 중 또는 충돌됨 상태의 애플리케이션 인스턴스에는
추적 및 덤프 오퍼레이션을 사용할 수 없습니다.
  * 추적 또는 덤프 대화 상자가 열린 경우 애플리케이션 인스턴스의 상태가 변경됩니다. 
  


솔루션은
창을 닫았다가 다시 여는 것입니다.
{: tsResolve} 



## 인스턴스별 traceSpecification 구성이 다름
{: #ts_different_config}

 

하나의 애플리케이션의 다른 인스턴스에서 traceSpecification 구성이 다를 수 있습니다.
{: tsSymptoms}

 

이 문제점은 다음과 같은 이유로
발생합니다.
{: tsCauses}

  * 이전에는 하나 이상의 인스턴스에 대한 구성을 변경할 수 있었습니다. 하나의 인스턴스에 대한 traceSpecification 구성을 변경한 경우, 동일한 애플리케이션의 다른 인스턴스에 적용되지 않습니다. 예를 들어, 애플리케이션이 log4j를 사용하고 이 애플리케이션에 대해 2개의 인스턴스가 있습니다. 인스턴스 0의 로그 레벨을 정보에서 디버그로 변경할 수 있지만, 인스턴스 1의 로그 레벨은 정보로 남아 있습니다. 
  * 애플리케이션이 스케일 확장되고 새 인스턴스를 갖습니다. RMU에서 기존 인스턴스의 traceSpecification 구성을 스케일 확장된 새 인스턴스에 적용하지 않습니다. 새 인스턴스는 기본 구성을 사용합니다. 예를 들어, 애플리케이션이 log4j를 사용하고 1개의 인스턴스가 있습니다. 이 인스턴스의 로그 레벨을 정보에서 디버그로 변경할 수 있습니다. 이렇게 변경한 후 애플리케이션을 두 개의 인스턴스로 스케일 확장하는 경우 새 인스턴스의 로그 레벨은 디버그가 아닌 정보입니다.
  


이는 예상된 동작입니다.
{: tsResolve} 





## 디스크 할당량이 초과됨
{: #ts_diskquota}

앱 로그에 디스크 할당량이 초과되었다고 표시될 수 있습니다.

 

앱 로그에 `디스크 할당량 초과` 오류 메시지가 표시됩니다.
{: tsSymptoms}



이 문제점은 다음 이유 중 하나로
발생합니다. 
{: tsCauses} 

  * 애플리케이션 인스턴스가 실행 중인 상태에서 덤프 파일이 생성되었으며,
파일이 디스크 할당량을 모두 사용했습니다. 기본적으로 한 애플리케이션 인스턴스의
디스크 할당량은 1GB입니다. **대시보드>애플리케이션>앱
런타임**을 클릭하면 디스크 사용량을 확인할 수 있습니다. 다음 예에서는 애플리케이션의 두 디스크 인스턴스에 대해 디스크 사용량 등의
런타임 정보를 보여줍니다.
    ```
    인스턴스	상태	CPU	메모리 사용량	디스크 사용량

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * 디스크 할당량은 현재 조직 할당량으로 제한됩니다.
  
  


이 문제를 해결하려면
다음 방법 중 하나를 사용하십시오.
{: tsResolve} 

  * 덤프 파일을 다운로드한 후 삭제하십시오.
  * 배치 Manifest에 다음 항목을 포함시켜 디스크 할당량 늘려
애플리케이션을 다시 배치하십시오.
    ```
	disk_quota: 2048
	```
	
	


