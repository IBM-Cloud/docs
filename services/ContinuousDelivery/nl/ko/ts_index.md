---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.contdelivery_short}} 문제점 해결
{: #ts_cd}

{{site.data.keyword.contdelivery_full}}의 사용에 대한 공통 문제점 해결 질문에 대한 응답을 받습니다.
{:shortdesc}


## GitHub에서 권한을 부여할 수 없음
{: #cannot_authorize_github}

GitHub에서 권한이 부여되지 않았습니다.
{:shortdesc}

GitHub 계정에 액세스할 수 있도록 {{site.data.keyword.Bluemix_notm}}에 권한 부여하지 않았으면 다음과 같은 문제가 발생할 수 있습니다.
{: tsSymptoms}

 * 도구 체인에 GitHub 도구 통합을 추가하려고 시도할 때 도구 통합이 추가되지 않습니다. 
 * GitHub 또는 GitHub Enterprise 저장소에 변경사항을 푸시할 때 파이프라인이 자동으로 실행되지 않습니다. 

GitHub에 액세스할 권한이 {{site.data.keyword.Bluemix_notm}}에 없습니다.   
{: tsCauses}
 
도구 체인을 작성하는 동안 GitHub 도구 통합을 구성 중이면 다음 단계를 따르십시오.
{: tsResolve}
 
  1. 구성 가능한 통합 섹션에서 **GitHub**를 클릭하십시오.  
  1. {{site.data.keyword.Bluemix_notm}} 퍼블릭에 도구 체인을 작성 중이고 GitHub에 액세스하는 권한을 {{site.data.keyword.Bluemix_notm}}에 부여하지 않은 경우 **권한 부여**를 클릭하여 GitHub 웹 사이트로 이동하십시오.  
  1. 활성 GitHub 세션이 없으면 로그인을 요구하는 프롬프트가 표시됩니다. **애플리케이션에 권한 부여**를 클릭하여 {{site.data.keyword.Bluemix_notm}}에서 사용자의 GitHub 계정에 액세스할 수 있도록 허용하십시오. 활성 GitHub 세션이 있지만 최근에 비밀번호를 입력하지 않은 경우 확인을 위해 GitHub 비밀번호 입력을 요구하는 프롬프트가 표시될 수 있습니다. 
  
이미 도구 체인이 있으면 GitHub 도구 통합의 구성을 업데이트하십시오. 

 1. DevOps 대시보드의 **도구 체인** 페이지에서 도구 체인을 클릭하여 해당 개요 페이지를 여십시오. 또는 앱 개요 페이지의 지속적 딜리버리 카드에서 **도구 체인 보기**를 클릭한 후에 **개요**를 클릭하십시오. 
 1. GitHub 카드에서 메뉴를 클릭하고 **구성**을 클릭하십시오. 
 1. 구성 설정을 업데이트하여 GitHub에 액세스할 수 있도록 {{site.data.keyword.Bluemix_notm}}에 권한 부여하십시오. **권한 부여**를 클릭하여 GitHub 웹 사이트로 이동하십시오. 활성 GitHub 세션이 없으면 로그인을 요구하는 프롬프트가 표시됩니다. **애플리케이션에 권한 부여**를 클릭하여 {{site.data.keyword.Bluemix_notm}}에서 사용자의 GitHub 계정에 액세스할 수 있도록 허용하십시오. 활성 GitHub 세션이 있지만 최근에 비밀번호를 입력하지 않은 경우 확인을 위해 GitHub 비밀번호 입력을 요구하는 프롬프트가 표시될 수 있습니다. 
 1. 설정 업데이트를 완료하면 **통합 저장**을 클릭하십시오. 


## 도구 통합이 구성되지 않음
{: #tool_integration_error}

도구 체인에 대한 도구 통합이 구성되면 `설정 실패` 오류가 해당 도구 카드에 표시됩니다.
{:shortdesc}

도구 통합이 구성된 후에 사용자는 도구 체인의 개요 페이지에서 해당 도구 카드를 보고 설정이 실패했음을 파악합니다.
{: tsSymptoms}

 ![설정 실패 오류](images/tool_setup_failed.png)
 
도구 통합을 추가하는 경우, 도구 체인은 도구 통합에 의해 표시된 도구와 통신하여 필수 자원을 프로비저닝하고 이를 도구 체인과 연관시킵니다. 설정 프로세스 중에 오류가 발생하거나 도구 체인과 도구 간의 통신이 제대로 완료되지 않은 경우, 도구 통신은 오류 상태가 됩니다.
{: tsCauses}

도구 통합을 다시 구성하십시오.
{: tsResolve}

1. 해당 도구 카드에서 `설정 실패` 메시지 위에 마우스 커서를 올려놓고 **재구성**을 클릭하십시오. 

 ![재구성 단추](images/tool_reconfigure.png)
 
1. 올바른 구성 매개변수를 사용 중인지 확인하십시오. 올바르지 않은 구성 때문에 오류가 발생한 경우에는 오류 메시지가 표시됩니다. 예: `통합을 설정할 수 없습니다. 설정을 확인하고 다시 시도하십시오. 이유: 올바르지 않은 api_key:fakeKey`. 도구 통합에 대한 설정을 업데이트하고 **통합 저장**을 클릭하십시오. 
1. 통신 문제점 때문에 오류가 발생한 경우에는 **통합 저장**을 클릭하여 다시 시도하십시오. 
