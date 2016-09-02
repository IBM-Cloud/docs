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

마지막 업데이트 날짜: 2016년 8월 18일
{: .last-updated} 

{{site.data.keyword.Bluemix}} 액세스와 관련한
일반적인 문제점으로는 사용자가 {{site.data.keyword.Bluemix_notm}}에
로그인할 수 없거나, 계정이 보류 상태로 남아 있는 경우 등이 있습니다. 그러나 대부분의 경우
몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다. 
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음
{: #ts_logintobm}

{{site.data.keyword.Bluemix_notm}}에 로그인하려면 올바른 IBM ID와 비밀번호가 있어야 합니다. 


{{site.data.keyword.Bluemix_notm}}에
로그인하려고 할 때 다음과 같은 오류 메시지가 표시됩니다. 
{: tsSymptoms} 

`입력한 비밀번호가 올바르지 않습니다.`


{{site.data.keyword.Bluemix_notm}}에 로그인하는 데 사용한 IBM ID와 비밀번호가 올바르지 않습니다.
{: tsCauses} 
 

올바른 IBM ID와 비밀번호를 얻으려면 내 IBM 프로파일 페이지로 이동하여 다음 단계 중 하나를 완료하십시오.
{: tsResolve}
  * IBM ID를 이미 등록했으며 ID와 비밀번호가 올바른지 확인하려면 **로그인**을 클릭하고 로그인 페이지에 IBM ID와 비밀번호를 입력하십시오. 비밀번호를 잊어버린 경우에는 로그인 페이지에서 **비밀번호를 잊으셨습니까?**를 클릭하여 비밀번호를 재설정하십시오. IBM ID를 잊어버렸거나 비밀번호와 관련된 문제가 지속되는 경우 전세계 IBM Registration 헬프 데스크에 지원을 요청하십시오.  
  * IBM ID가 없는 경우에는 **등록**을 클릭하여 IBM ID와 비밀번호를 등록하십시오.  
  
**참고:** IBM 직원의 경우 IBM ID와 인트라넷 로그인 ID는 서로 다를 수 있습니다.  



<!-- begin STAGING ONLY --> 

## 외부 웹 사이트에 액세스하는 중에 문제점 발생
{: #ts_bmlinkid}

인트라넷 ID와 IBM ID를 링크하지 않으면 IBM 인트라넷 ID를 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없습니다. 


{{site.data.keyword.Bluemix_notm}} 로그인 페이지에서 **인트라넷 ID를 사용하여 로그인**을 선택하면 다음 오류 메시지가 표시됩니다.
{: tsSymptoms} 

`Problem Accessing External Website`



IBM ID에 링크되지 않은 IBM 인트라넷 ID를 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하는 경우 이 문제점이 발생합니다. IBM ID는 www.ibm.com에 로그인하는 데 사용하는 ID입니다.
{: tsCauses}


IBM 직원의 경우 IBM 인트라넷 ID를 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인하려면 먼저 인트라넷 ID와 외부 IBM ID를 링크해야 합니다. 두 ID를 링크하려면 다음 단계를 완료하십시오.
{: tsResolve} 

  1. [Central Sign-on](https://w3-03.sso.ibm.com/tools/cso/index.jsp){: new_window} 페이지에서 **내 사인온**을 클릭하십시오. 
  2. 내 사인온 페이지에서 **ID 링크**를 클릭하고 {{site.data.keyword.Bluemix_notm}} 로그인 페이지에 IBM ID와 비밀번호를 입력하십시오. 그러면 인트라넷 ID와 IBM ID가 자동으로 링크됩니다. 
  

<!-- end STAGING ONLY -->




## 저장되지 않은 변경사항이 있음
{: #ts_unsaved_changes}


앱 세부사항 페이지에서 탐색할 때 조치를 수행하지 못하고 계속하기 전에 변경사항을 저장하라는 메시지가 표시될 수 있습니다. 


앱 세부사항 페이지에서 앱 또는 서비스를 확인하려고 하면 다음 오류 메시지가 계속 표시됩니다.
{: tsSymptoms} 

`You have unsaved changes in page app_name. Save or cancel the changes.`


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

DNS 설정을 구성할 때 앱이 실행 중인 {{site.data.keyword.Bluemix_notm}} 지역의 공인 IP 주소를 지정해야 합니다. {{site.data.keyword.Bluemix_notm}} 지역의 공인 IP 주소를 가져오려면 `nslookup` 명령을 사용하십시오. 예를 들어, 명령행 창에 다음 명령을 입력할 수 있습니다. 
```
nslookup stage1.mybluemix.net
```



## 계정이 보류 중임
{: #ts_accntpding}

계정이 보류 중인 경우 {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없습니다.

 
{{site.data.keyword.Bluemix_notm}} 평가판 계정에 등록하면 {{site.data.keyword.Bluemix_notm}}에 로그인하지 못할 수 있습니다. 대신 다음 메시지가 표시됩니다.
{: tsSymptoms}

<code>사용자 계정이 보류 중입니다. 여러분 계정의 이메일 확인을 위해 최대 24시간 동안 기다려야 할 수 있습니다. 스팸 폴더도 확인하십시오. 아직 이메일 확인을 받지 못했다면, <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix 지원</a>에 문의하십시오.</code>


{{site.data.keyword.Bluemix_notm}} 평가판 계정에 등록하면 확인 이메일을 받습니다. 확인 이메일에 있는 링크를 클릭하여 등록 프로세스를 완료해야 합니다.
{: tsCauses} 

확인 이메일이 사용자가 제공한 이메일 주소로 전송됩니다. 받은 편지함과 정크 메일 폴더를 확인하십시오. 확인 이메일을 받지 못한 경우, [{{site.data.keyword.Bluemix_notm}} 지원](http://ibm.biz/bluemixsupport.com){: new_window}에 문의하십시오.  
{: tsResolve}



## 사용자를 조직에 추가할 수 없음
{: #ts_adduser}

동일한 조직에서 작업할 사용자를 두 명 이상 초대할 수 있습니다. 계정 소유자이거나 조직의 관리자이자 구성원인 경우에만 조직에 사용자를 추가할 수 있습니다.
 

**조직 관리** 섹션에 **새 사용자 초대** 링크가 보이지 않습니다.
{: tsSymptoms}

 

다음 {{site.data.keyword.Bluemix_notm}} 사용자만 사용자를 조직에 초대할 수 있습니다.
{: tsCauses}
  * 조직의 계정 소유자
  * 조직의 협업자가 아니라 구성원인 조직 관리자
  
{{site.data.keyword.Bluemix_notm}}에서 사용자는 조직의 구성원이거나 협업자일 수 있습니다.

<dl><dt>협업자</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 계정이 이미 있으며 다른 사용자가 자신을 조직으로 초대한 경우, 조직의 협업자입니다.</dd>
<dt>구성원</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 계정이 없지만 다른 사용자가 자신을 초대하여 초대장을 통해 {{site.data.keyword.Bluemix_notm}}에 등록한 경우, 조직의 구성원입니다.</dd>
</dl>


조직의 협업자인 경우에는 조직 관리자로 지정되었더라도 조직에 사용자를 초대할 수 없습니다.

**참고:** 조직의 협업자를 비롯한 모든 조직 관리자는 조직에 이미 있는 사용자를 추가, 수정 및 제거할 수 있습니다.

 

사용자를 조직에 초대할 수 없으며 초대를 위해 다른 역할이 필요한 경우 조직 관리자에게 역할 변경을 요청하십시오. 조직 관리자를 확인하려면 다음 단계를 수행하십시오.
{: tsResolve}

  1. {{site.data.keyword.Bluemix_notm}} 대시보드로 이동하여 메뉴 표시줄에서 {{site.data.keyword.avatar}} 아이콘 ![아바타 아이콘](images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오. 
  2. 자신의 조직으로 이동하여 **사용자** 탭에서 조직 관리자에 대한 정보를 확인하십시오.  
  
구성원이 아니라 협업자이기 때문에 사용자를 초대할 수 없는 경우 이전 {{site.data.keyword.Bluemix_notm}} 계정을 삭제한 다음 조직의 구성원으로 참여할 수 있도록 초대를 받아야 합니다. 이전 계정을 삭제하고 구성원으로 계정에 참여하려면 다음 단계를 수행하십시오. 

  1. [{{site.data.keyword.Bluemix_notm}} 지원 부서에 연락](http://ibm.biz/bluemixsupport){: new_window}하여 지원 티켓을 열고 계정 삭제를 요청하십시오. 이전 계정과 연관된 데이터가 있어 이 데이터를 저장한 다음 새 계정으로 이동하려면 이메일에 이 정보를 포함시키십시오. 
  2. 계정이 삭제되면 조직 관리자 역할을 보유한 사용자가 자신을 조직 관리자로 조직에 초대하도록 하십시오. 그런 다음 초대장을 통해 {{site.data.keyword.Bluemix_notm}}에 등록하십시오. 




## 사용자 일괄 등록이 지원되지 않음
{: #ts_batchregistration}

{{site.data.keyword.Bluemix_notm}}에 사용자를 등록할 경우 각 사용자를 개별적으로 등록해야 합니다.
 

{{site.data.keyword.Bluemix_notm}}에서는 여러 사용자를 한 번에 등록하는 기능을 제공하지 않습니다.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}}에서는 사용자 일괄 등록을 지원하지 않습니다. {{site.data.keyword.Bluemix_notm}}에 사용자를 등록하려면 각 사용자를 개별적으로 등록해야 합니다.
{: tsCauses}
 

{{site.data.keyword.Bluemix_notm}}에 여러 사용자를 등록하려면 사용자마다 다음 단계를 수행해야 합니다.
{: tsResolve}

  1. {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에서 **등록**을 클릭하십시오. 
  2. 마법사의 안내에 따라 단계를 완료하십시오.

    

## {{site.data.keyword.Bluemix_notm}} 페이지를 로드할 수 없음
{: #ts_err}

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용하는 경우 {{site.data.keyword.Bluemix_notm}} 페이지를 로드하지 못할 수 있습니다. 대신, BXNUI0001E 또는 BXNUI0016E 오류 메시지가 표시될 수 있습니다.
 

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용할 경우 다음과 같은 오류 메시지가 표시될 수 있습니다.
{: tsSymptoms}

`BXNUI0001E: The page wasn't loaded because Bluemix didn't detect whether a session exists.`


`BXNUI0016E: The apps and services weren't retrieved because a Bluemix page didn't load.`

 

필요한 경우 다음 조치 중 하나 이상을 수행할 수 있습니다.
{: tsResolve}

  * 브라우저를 새로 고치거나 다시 시작하십시오.
  * {{site.data.keyword.Bluemix_notm}}에서 로그아웃한 후 다시 로그인하십시오.
  * 브라우저의 개인용 브라우징 모드를 사용하십시오. 
  * 브라우저의 쿠키와 캐시를 지우십시오.
  * 다른 브라우저를 사용하십시오. {{site.data.keyword.Bluemix_notm}}에서 지원하는 브라우저 버전에 대한 정보는 [{{site.data.keyword.Bluemix_notm}}전제조건](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}을 참조하십시오.
  * cf 명령행 인터페이스를 설치한 경우 `cf apps` 명령을 입력하여 애플리케이션이 실행 중인지 확인하십시오.
  
  
  
  
  

