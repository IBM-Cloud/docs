---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# {{site.data.keyword.Bluemix_notm}} 액세스 문제점 해결 
{: #accessing}


{{site.data.keyword.Bluemix}} 액세스와 관련한 일반적인 문제점에는 {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없거나 계정이 보류 상태인 경우가 있습니다. 대부분 몇 가지 간단한 단계를 수행하여 이러한 문제점에서 복구할 수 있습니다.
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음: 올바르지 않은 비밀번호
{: #ts_logintobm}

{{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하려면 IBM ID와 연관된 올바른 비밀번호가 있어야 합니다.

[고객 포털](https://control.softlayer.com)을 통해 로그인하려면 IBM ID 또는 SoftLayer ID와 연관된 올바른 비밀번호가 있어야 합니다.

{{site.data.keyword.Bluemix_notm}}에 로그인하려고 할 때 다음 오류 메시지가 표시됩니다.
{: tsSymptoms} 

`입력한 비밀번호가 올바르지 않습니다.`

{{site.data.keyword.Bluemix_notm}}에 로그인하는 데 사용한 IBM ID 및 비밀번호가 올바르지 않습니다.
{: tsCauses} 
 
다음 솔루션 중 하나를 사용하십시오.
{: tsResolve}
 * 올바른 비밀번호를 입력하십시오. IBM ID와 비밀번호가 올바른지 확인하기 위해 내 IBM 프로파일 페이지로 이동하여 **로그인**을 클릭하고 로그인 페이지에 IBM ID와 비밀번호를 입력할 수 있습니다. 
 * 비밀번호를 잊어버린 경우에는 **비밀번호를 잊으셨습니까?**를 클릭하여 비밀번호를 재설정하십시오. 그런 다음 [Bluemix 콘솔](https://console.{DomainName}) 또는 [고객 포털](https://control.softlayer.com)로 돌아가 다시 로그인하십시오.
 * IBM ID를 잊어버렸거나 비밀번호와 관련된 문제점이 지속되는 경우 전세계 IBM Registration 헬프 데스크에 지원을 요청하십시오. 
 * 올바른 IBM ID 및 비밀번호를 얻으려면 내 IBM 프로파일 페이지로 이동한 다음 **등록**을 클릭하십시오.
  
**참고:** IBM 페이지에 로그인한 상태이고 로그인 프로세스가 어떤 이유로(예: 비밀번호 재설정) 방해 받는 경우 [Bluemix 콘솔](https://console.{DomainName}) 또는 [고객 포털](https://control.softlayer.com)로 돌아가 로그인 프로세스를 다시 시작하십시오.
 

## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음: 올바르지 않은 로그인 신임 정보
{: #ts_login_invalid_credentials}

IBM ID를 사용하여 로그인할 때 다음 메시지가 표시됩니다.
{: tsSymptoms}

올바르지 않은 로그인 신임 정보가 제공되었습니다. IBM ID가 계정과 연관되어 있는 경우 여기에 로그인하십시오.` 

* IBM ID로 전환했지만 이전 SoftLayer 사용자 이름 및 비밀번호를 사용하여 [고객 포털](https://control.softlayer.com)을 통해 로그인하려고 했습니다.
{: tsCauses}

* [고객 포털](https://control.softlayer.com)을 통해 로그인하려고 했지만 사용자 이름 및 비밀번호 필드에 IBM ID와 비밀번호를 입력했습니다. 

메시지에서 **여기에 로그인**을 클릭하거나 IBM ID 계정 로그인 섹션으로 이동하고 **IBM ID로 로그인**을 클릭하십시오.
{: tsResolve}

이전 Softlayer ID로 사용한 **사용자 이름** 및 **비밀번호** 필드를 사용하지 마십시오.


## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음: 인식할 수 없는 IBM ID 또는 이메일
{: #ts_softlayer_username}

{{site.data.keyword.Bluemix_notm}} 콘솔에 로그인할 때 다음 메시지가 표시됩니다.
{: tsSymptoms} 

`이 IBM ID 또는 이메일을 인식할 수 없습니다.`

{{site.data.keyword.Bluemix_notm}} 콘솔에 로그인하려고 했지만 올바른 IBM ID를 사용하지 않았습니다. 예를 들어, IBM ID의 완전한 이메일 주소를 입력하지 않았거나 SoftLayer 사용자 이름 및 비밀번호를 사용하려고 했습니다.
{: tsCauses}
 
{{site.data.keyword.Bluemix_notm}}에 로그인하려면 올바른 IBM ID와 비밀번호가 있어야 합니다. 

 * IBM ID의 완전한 이메일 주소를 입력했는지 확인하십시오.
 {: tsResolve}
 * SoftLayer ID를 가진 SoftLayer 사용자는 IBM ID 인증을 사용하여 로그인하기 전에 액세스할 수 있는 각 계정에서 고객 포털의 IBM ID 인증으로 전환해야 합니다.
 자세한 정보는 [IBM ID로 전환](/docs/admin/softlayerlink.html#ibmid_switch)을 참조하십시오.


## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음: IBM ID가 IBM 클라우드 계정과 연관되어 있지 않음
{: #ts_login_noswitch}

IBM ID를 사용하여 로그인할 때 다음 메시지가 표시됩니다.
{: tsSymptoms}

`인증에 성공하여 이 페이지로 이동되었습니다. 하지만 이 IBM ID는 IBM 클라우드 계정과 연관되어 있지 않습니다. 오류로 간주되면 계정 소유자 또는 마스터 사용자에게 문의하십시오.`

[고객 포털](https://control.softlayer.com)에서 올바른 IBM ID를 사용하여 로그인했지만 SoftLayer의 IBM ID 인증으로 전환되지 않았습니다.
{: tsCauses} 
 
다음 검사를 완료하십시오.
{: tsResolve}
 * IBM ID 인증으로 전환할 수 있는지 확인하려면 마스터 사용자 또는 계정 관리자에게 문의하십시오.
 * Softlayer 계정에서 IBM ID로 전환 단계를 완료했는지 확인하십시오. [IBM ID로 전환](/docs/admin/softlayerlink.html#ibmid_switch)을 참조하십시오.
 * **IBM ID와 SoftLayer 사용자 연관** 이메일에서 조치를 따르는지 확인하십시오. 받은 편지함과 스팸 폴더에서 이메일을 확인하십시오. 만료된 이메일을 다시 가져오려면 제어 포털의 사용자 프로파일 편집 페이지로 이동하고 **이메일 재발송**을 클릭하십시오. 또는 [{{site.data.keyword.Bluemix_notm}} 지원 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://ibm.biz/bluemixsupport.com){: new_window}에 문의하십시오.

**참고:** IBM ID로 직접 자신의 IBM ID를 작성한 경우 처리할 두 개의 이메일(IBM ID 등록 이메일과 Softlayer 이메일)을 수신합니다. 두 개의 이메일에 있는 조치를 따라야 합니다.

계정 설정의 방법에 따라 로그인 옵션 중 일부가 적용될 수 있습니다. 
 * SoftLayer ID가 있는 SoftLayer 사용자는 [고객 포털](https://control.softlayer.com)을 통해 로그인해야 합니다.
 * IBM ID가 있고 연결된 Bluemix 계정이 있거나 없는 SoftLayer 사용자는 [고객 포털](https://control.softlayer.com)을 통해 로그인하여 SoftLayer 고객 포털을 열 수 있거나 [Bluemix 콘솔](https://console.{DomainName})을 통해 인프라 대시보드를 열 수 있습니다. 


## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음: IBM ID가 {{site.data.keyword.Bluemix_notm}} 계정과 연관되어 있지 않음
{: #ts_unabletologin}

{{site.data.keyword.Bluemix_notm}}에 로그인할 때 다음 메시지가 표시됩니다.
{: tsSymptoms} 
 
`인증에 성공하여 이 페이지로 이동되었습니다. 하지만 이 IBM ID는 {{site.data.keyword.Bluemix_notm}} 계정과 연관되어 있지 않습니다.` 

[Bluemix 콘솔](https://console.{DomainName})에서 올바른 IBM ID로 로그인했지만 {{site.data.keyword.Bluemix_notm}} 계정이 아직 작성되지 않았습니다.
{: tsCauses} 

{{site.data.keyword.Bluemix_notm}} 계정을 작성하려면 등록 프로세스를 따르십시오.
{: tsResolve}

계정 설정의 방법에 따라 로그인 옵션 중 일부가 적용될 수 있습니다. 
 * 연결된 SoftLayer 계정이 없는 Bluemix 사용자는 Bluemix 콘솔을 통해 로그인해야 합니다.
 * 연결된 SoftLayer 계정이 있는 Bluemix 사용자는 [Bluemix 콘솔](https://console.{DomainName}) 또는 [고객 포털](https://control.softlayer.com)을 통해 로그인할 수 있습니다.
 

## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음: 콘솔이 열리지 않음
{: #ts_login_stalls}

IBM ID를 사용하여 로그인한 경우 로그인 성공 메시지가 표시되지만 [Bluemix 콘솔](https://console.{DomainName}) 또는 [고객 포털](https://control.softlayer.com)로 돌아가지 않습니다.
{: tsSymptoms}

다음 솔루션 중 하나를 사용하십시오.
{: tsResolve}
 * 브라우저를 닫고 캐시 및 쿠키를 지운 다음 다시 로그인을 시도하십시오.
 * IBM 인증 서비스를 직접 통하지 않고 [Bluemix 콘솔](https://console.{DomainName}) 또는 [고객 포털](https://control.softlayer.com)을 통해 로그인해야 합니다.
 
 
## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음: IBM ID 로그인이 완료되지 않음
{: #ts_login_ibmid}

{{site.data.keyword.Bluemix_notm}}에 로그인하면 IBM ID 인증이 완료되지 않습니다.
{: tsSymptoms}

IBM 인증 서비스에 문제점이 있을 수 있습니다.
{: tsCauses}

[IBM BlueID ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window}에서 서비스 상태를 검사한 다음 다시 시도하십시오.
{: tsResolve}


## {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없음: 계정이 보류 중임
{: #ts_accntpding}

계정이 보류 중인 경우 {{site.data.keyword.Bluemix_notm}}에 로그인할 수 없습니다.
 
{{site.data.keyword.Bluemix_notm}} 평가판 계정에 등록하면 {{site.data.keyword.Bluemix_notm}}에 로그인하지 못할 수 있습니다. 다음 메시지가 표시됩니다.
{: tsSymptoms}

<code>사용자 계정이 보류 중입니다. 사용자 계정의 이메일 확인을 위해 최대 24시간 동안 기다려야 할 수 있습니다. 스팸 폴더도 확인하십시오. 아직 이메일 확인을 받지 못했다면, <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix Support</a>에 문의하십시오.</code>


{{site.data.keyword.Bluemix_notm}} 평가판 계정에 등록하면 확인 이메일을 받습니다. 확인 이메일에 있는 링크를 클릭하여 등록 프로세스를 완료해야 합니다.
{: tsCauses} 

확인 이메일이 사용자가 제공한 이메일 주소로 전송됩니다. 받은 편지함과 스팸 폴더를 확인하십시오. 확인 이메일을 수신하지 못한 경우 [{{site.data.keyword.Bluemix_notm}} 지원 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://ibm.biz/bluemixsupport.com){: new_window}에 문의하십시오.  
{: tsResolve}


## 저장되지 않은 변경사항이 있음
{: #ts_unsaved_changes}

앱 세부사항 페이지에서 탐색할 때 조치를 수행하지 못하고 계속하기 전에 변경사항을 저장하라는 메시지가 표시될 수 있습니다. 

앱 세부사항 페이지에서 앱 또는 서비스를 확인하려고 하면 다음 오류 메시지가 계속 표시됩니다.
{: tsSymptoms} 

`app_name 페이지의 변경사항을 저장하지 않았습니다. 변경사항을 저장하거나 취소하십시오.`

런타임 분할창에서 **인스턴스** 또는 **메모리 할당량** 필드 위로 마우스를 스크롤하면 값이 변경됩니다. 설계상 이런 동작이 발생하는 것이며, 페이지에서 벗어나기 전에 메모리 또는 인스턴스 설정을 저장하라는 오류 메시지가 표시됩니다.
{: tsCauses}

메시지 창을 닫고 런타임 분할창에서 **재설정** 단추를 클릭하십시오.
{: tsResolve} 
  
    
## {{site.data.keyword.Bluemix_notm}} 지역 간 자동 장애 복구를 사용할 수 없음
{: #ts_failover}

{{site.data.keyword.Bluemix_notm}} 지역 간에 자동 장애 복구를 사용할 수 없습니다. 하지만 여러 IP 주소 간의 장애 복구를 지원하는 DNS 제공자를 임시 해결책으로 사용할 수 있습니다.

{{site.data.keyword.Bluemix_notm}} 지역을 사용할 수 없게 되면 동일한 앱이 다른 {{site.data.keyword.Bluemix_notm}} 지역에서 실행 중이더라도 해당 지역에서 실행 중인 앱도 사용할 수 없습니다.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}}는 하나의 지역에서 다른 지역으로의 자동 장애 복구를 아직 제공하지 않습니다.
{: tsCauses}
 
여러 IP 주소 간의 지능형 장애 복구를 지원하는 DNS 제공자를 사용하여 {{site.data.keyword.Bluemix_notm}} 지역 간의 자동 장애 복구를 지원하도록 DNS 설정을 수동으로 구성할 수 있습니다. 이 기능이 있는 DNS 제공자에는 NSONE, Akamai, Dyn이 포함됩니다.
{: tsResolve}

DNS 설정을 구성할 때 앱이 실행 중인 {{site.data.keyword.Bluemix_notm}} 지역의 공인 IP 주소를 지정해야 합니다. {{site.data.keyword.Bluemix_notm}} 지역의 공인 IP 주소를 가져오려면 `nslookup` 명령을 사용하십시오. 예를 들어, 명령행 창에 다음 명령을 입력할 수 있습니다. 
```
nslookup stage1.mybluemix.net
```

## 조직에 사용자를 추가할 수 없음
{: #ts_adduser}

동일한 조직에서 작업할 사용자를 두 명 이상 초대할 수 있습니다. 계정 소유자이거나 조직의 관리자이자 구성원인 경우에만 조직에 사용자를 추가할 수 있습니다.
 
**조직 관리** 섹션에서 **새 사용자 초대** 링크를 볼 수 없습니다.
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

조직에 사용자를 초대할 수 없고 초대를 위해 다른 역할이 필요한 경우 조직 관리자에게 문의하여 역할을 변경하십시오. 조직 관리자를 확인하려면 다음 단계를 수행하십시오.
{: tsResolve}

  1. {{site.data.keyword.Bluemix_notm}} 대시보드로 이동하십시오. 메뉴 표시줄에서 **계정** 메뉴 항목을 클릭하고 **조직 관리**를 클릭하십시오.
  2. 자신의 조직으로 이동하여 **사용자** 탭에서 조직 관리자에 대한 정보를 확인하십시오.  
  
구성원이 아닌 협업자이기 때문에 사용자를 초대할 수 없는 경우 이전 {{site.data.keyword.Bluemix_notm}} 계정을 삭제한 다음 조직의 구성원으로 계정을 결합하도록 초대 받아야 합니다. 이전 계정을 삭제하고 구성원으로 계정에 참여하려면 다음 단계를 수행하십시오. 

  1. [{{site.data.keyword.Bluemix_notm}} 지원 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](http://ibm.biz/bluemixsupport){: new_window}에 문의하여 지원 티켓을 열고 계정 삭제를 요청하십시오. 이전 계정과 연관된 데이터가 있어 이 데이터를 저장한 다음 새 계정으로 이동하려면 이메일에 이 정보를 포함시키십시오. 
  2. 계정이 삭제되면 조직 관리자 역할을 보유한 사용자가 자신을 조직 관리자로 조직에 초대하도록 하십시오. 그런 다음 초대장을 통해 {{site.data.keyword.Bluemix_notm}}에 등록하십시오. 

## 사용자 일괄 등록이 지원되지 않음
{: #ts_batchregistration}

{{site.data.keyword.Bluemix_notm}}에 사용자를 등록할 경우 각 사용자를 개별적으로 등록해야 합니다.

{{site.data.keyword.Bluemix_notm}}는 여러 사용자를 동시에 등록하는 기능을 제공하지 않습니다.
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}}에서는 사용자 일괄 등록을 지원하지 않습니다. {{site.data.keyword.Bluemix_notm}}에 사용자를 등록하려면 각 사용자를 개별적으로 등록해야 합니다.
{: tsCauses}
 
{{site.data.keyword.Bluemix_notm}}에 여러 사용자를 등록하려면 사용자마다 다음 단계를 완료하십시오.
{: tsResolve}

  1. {{site.data.keyword.Bluemix_notm}} 콘솔에서 **등록**을 클릭하십시오.
  2. 마법사의 안내에 따라 단계를 완료하십시오.
    

## {{site.data.keyword.Bluemix_notm}} 페이지를 로드할 수 없음
{: #ts_err}

{{site.data.keyword.Bluemix_notm}} 콘솔을 사용하는 경우 {{site.data.keyword.Bluemix_notm}} 페이지를 로드하지 못할 수 있습니다. 대신, BXNUI0001E 또는 BXNUI0016E 오류 메시지가 표시될 수 있습니다.
 
{{site.data.keyword.Bluemix_notm}} 콘솔을 사용할 경우 다음과 같은 오류 메시지가 표시될 수 있습니다.
{: tsSymptoms}

`BXNUI0001E: Bluemix에서 세션이 존재하는지 여부를 발견하지 않았기 때문에 페이지가 로드되지 않았습니다.`

`BXNUI0016E: Bluemix 페이지가 로드되지 않았기 때문에 앱과 서비스가 검색되지 않았습니다.`

필요에 따라 다음 조치 중 하나 이상을 완료하십시오.
{: tsResolve}

  * 브라우저를 새로 고치거나 다시 시작하십시오.
  * {{site.data.keyword.Bluemix_notm}}에서 로그아웃한 후 다시 로그인하십시오.
  * 브라우저의 개인용 브라우징 모드를 사용하십시오. 
  * 브라우저의 쿠키와 캐시를 지우십시오.
  * 다른 브라우저를 사용하십시오. {{site.data.keyword.Bluemix_notm}}에서 지원되는 브라우저 버전에 대한 정보는 [Bluemix 전제조건](/docs/overview/whatisbluemix.html#prereqs)을 참조하십시오.
  * cf 명령행 인터페이스를 설치한 경우 `cf apps` 명령을 입력하여 앱이 실행 중인지 확인하십시오.
