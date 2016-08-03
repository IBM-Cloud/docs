---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 도구 통합 구성
{: #integrations}

*마지막 업데이트 날짜: 2016년 6월 17일*
{: .last-updated}

도구 체인을 작성하는 동안 개발, 배치 및 운영 태스크를 지원하는 도구 통합을 구성하거나 기존 도구 체인을 사용자 정의하도록 도구 통합을 추가하여 구성할 수 있습니다.  
{:shortdesc}

**중요**: 이 기능은 실험적으로 사용됩니다. 도구 체인이 안정적이지 않거나 이전 버전과 호환되지 않는 방식으로 변경될 수 있습니다. 프로덕션 환경에서는 사용하지 않는 것이 좋습니다. 도구 체인을 사용하려면 일회성 [액세스 요청](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}을 수행해야 합니다. 도구 체인은 미국 남부 지역에서만 사용할 수 있습니다.

**팁**: 소스 코드 개발을 시작하려면 {{site.data.keyword.deliverypipeline}}을 구성하기 전에 GitHub와 GitHub Issues 도구 통합을 구성해야 합니다.

## Delivery Pipeline 구성
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}}은 입력을 검색하고 작업(예: 빌드, 테스트 및 배치)을 실행하는 일련의 단계를 통해 자동으로 프로젝트를 연속 배치합니다. 

앱을 자동으로 연속 빌드, 테스트 및 배치하도록 {{site.data.keyword.deliverypipeline}}를 구성하십시오. 

1. 도구 체인을 작성하면서 이 도구 통합을 구성하는 경우 구성 가능한 통합 섹션에서 **Delivery Pipeline**을 클릭하십시오. 사용하는 템플리트에 따라 여러 다른 필드를 사용할 수 있습니다. 기본 필드 값을 검토하고 필요한 경우 해당 설정을 변경하십시오.
1. 보유한 도구 체인에 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. 추가 단추(+)를 클릭하십시오.
1. 도구 통합 섹션에서 **Delivery Pipeline**을 클릭하십시오.
1. 새 파이프라인의 이름을 지정하십시오.
1. 파이프라인을 통해 사용자 인터페이스를 배치하려는 경우 **볼 수 있는 앱** 선택란을 선택하십시오. 파이프라인에서 작성하는 모든 앱이 도구 체인의 도구 통합 페이지에 있는 **앱 보기** 목록에 표시됩니다. 
1. **통합 작성**을 클릭하여 도구 체인에 {{site.data.keyword.deliverypipeline}}을 추가하십시오.
1. {{site.data.keyword.deliverypipeline}}의 타일을 클릭하여 파이프라인을 보고 구성하십시오. 파이프라인 구성에 대한 기본사항을 알아보려면 [파이프라인 빌드 및 배치](../services/DeliveryPipeline/build_deploy.html){: new_window}를 참조하십시오.

  **팁**: GitHub 저장소(repo)에 변경사항을 푸시할 때 파이프라인을 트리거하려면 파이프라인의 단계를 정의하기 전에 도구 체인의 GitHub를 구성해야 합니다. 파이프라인 단계에는 GitHub 저장소의 Git URL이 필요합니다. 각 파이프라인 단계는 도구 체인과 연관된 GitHub 저장소 중 하나만 참조할 수 있습니다. GitHub 구성 지시사항은 [GitHub 및 GitHub Issues](#github) 섹션을 참조하십시오.
  
1. 선택사항: Sauce Labs에서 앱에 대한 테스트를 실행하도록 하려면 Sauce Labs 테스트 작업을 추가하도록 {{site.data.keyword.deliverypipeline}}을 구성하십시오. 테스트 작업을 구성하는 데 관한 지시사항은 [파이프라인에서 Sauce Labs 테스트 작업 구성](#config_saucelabs) 섹션을 참조하십시오.

### 파이프라인에서 Sauce Labs 테스트 작업 구성
{: #config_saucelabs}

파이프라인에서 Sauce Labs 테스트 작업을 구성하기 전에 앱을 빌드하고 배치하는 단계가 포함된 작동하는 파이프라인이 있어야 하며 도구 체인에 맞게 Sauce Labs를 구성해야 합니다. Sauce Labs를 구성하는 데 관한 지시사항은 [Sauce Labs](#saucelabs) 섹션을 참조하십시오.

다음과 같이 Sauce Labs 테스트 작업을 추가하도록 {{site.data.keyword.deliverypipeline}}을 구성하십시오.

1. 앱의 테스트 버전을 배치하는 단계가 없으면 하나를 작성하십시오.
1. 이 단계에서 배치 작업 다음에 테스트 작업을 추가하십시오. 이러한 작업을 동일한 단계에 배치하면 동일한 환경 특성 세트에 액세스할 수 있습니다.
  ![테스트 작업](images/toolchain_test_job.png) 

1. 다음과 같이 단계를 구성하십시오. 

  a. **환경 특성** 탭에서 세 가지 특성(CF_APP_NAME, SAUCE_USERNAME 및 SAUCE_ACCESS_KEY)을 작성하십시오.
  
  b. Sauce Labs 사용자 이름과 액세스 키를 입력하십시오. 그러면 테스트에서 사용할 수 있도록 이 값을 구체화할 수 있습니다. 
  
1. 배치 작업을 구성하십시오. **스크립트 배치** 필드에 export CF_APP_NAME="$CF_APP" 명령을 포함하십시오. 이 명령은 앱 이름을 환경 특성으로 내보냅니다.
1. 테스트 작업을 구성하십시오. 다음 이미지의 값은 예입니다. 현재 사용 중인 Sauce Labs 사용자 이름, 영역, 조직 및 공간이 **서비스 인스턴스**, **대상**, **조직** 및 **공간** 필드에 입력됩니다.
![작업 구성](images/toolchain_configure_job.png)

  a. 테스터 유형으로 **Sauce Labs**를 선택하십시오.
  
  b. 서비스 인스턴스의 경우, 도구 체인의 Sauce Labs를 구성할 때 사용한 Sauce Labs 사용자 이름을 선택하십시오. 
  
   **팁**: 도구 체인의 Sauce Labs를 구성할 때 사용한 사용자 이름과 액세스 키를 확인하려면 **구성**을 클릭하십시오. 
  
  c. **테스트 실행 명령** 필드에 테스트에 필요한 종속 항목을 설치한 다음 테스트를 실행하는 명령을 입력하십시오. 예를 들어, 가상의 Node.js 앱의 경우 다음을 입력할 수 있습니다.
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. 테스트 작업 로그에서 테스트 보고서를 보려면 **테스트 보고서 사용** 선택란을 선택하고 테스트 결과 파일 패턴을 `test/*.xml`로 설정하십시오.
  
1. **저장**을 클릭하십시오. 이제 파이프라인을 실행할 때마다 Sauce Labs 테스트가 실행됩니다.

자세한 정보는 [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}을 참조하십시오.

## 배치 위험성 분석 추가
{: #dra}

{{site.data.keyword.DRA_full}}에서는 코드가 배치 프로세스의 지정된 게이트에 사전 정의된 기준을 만족하는지 판별하기 위해 단위 테스트, Functional Test 및 코드 적용 범위 도구에서 결과를 수집하여 분석합니다. 코드가 기준을 만족하지 않거나 초과하는 경우 위험이 확산되지 않도록 배치가 중지됩니다. 배치 위험성 분석을 Continuous Delivery 환경의 안전망 또는 품질 표준을 구현하고 개선하는 방법으로 사용할 수 있습니다. 

 **팁**: 이 도구 통합은 사전 구성됩니다. 구성 매개변수가 필요하지 않고 이 통합을 다시 구성할 수 없습니다. 
 
위험이 확산되기 전에 식별하기 위해 배치를 모니터링하여 Bluemix의 코드 품질을 유지보수하고 개선하도록 배치 위험성 분석을 추가하십시오.

1. 보유한 도구 체인에 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. 추가 단추(+)를 클릭하십시오.
1. 도구 통합 섹션에서 **배치 위험 분석**을 클릭하십시오. 
1. **통합 작성**을 클릭하십시오.
1. 배치 위험성 분석 타일을 클릭한 다음 시작하기 단계를 완료하십시오. 즉, 기준을 클릭하고, 기준을 파이프라인에 연결한 다음 파이프라인을 실행하십시오. 자세한 정보는 [배치 위험성 분석](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}을 확인하십시오.

## Eclipse Orion {{site.data.keyword.webide}} 추가
{: #webide}

Eclipse Orion {{site.data.keyword.webide}}는 소스 제어 태스크를 작성, 편집, 실행, 디버그 및 완료할 수 있는 통합 웹 기반 환경입니다. 편집부터 실행, 제출 및 디버깅으로 원활하게 이동할 수 있습니다. 

 **팁**: 이 도구 통합은 사전 구성됩니다. 구성 매개변수가 필요하지 않고 이 통합을 다시 구성할 수 없습니다. 
 
소스 제어 태스크를 완료하려면 다음과 같이 Eclipse Orion {{site.data.keyword.webide}} 도구 통합을 추가하십시오.

1. 보유한 도구 체인에 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. 추가 단추(+)를 클릭하십시오.
1. 도구 통합 섹션에서 **Eclipse Orion Web IDE**를 클릭하십시오. 
1. **통합 작성**을 클릭하십시오.
1. 새 Eclipse Orion Web IDE의 타일을 클릭하십시오. 작업공간이 GitHub 저장소로 미리 채워집니다. 현재 도구 체인과 연관된 저장소는 강조표시됩니다.

자세한 정보는 [Web IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}를 확인하십시오.


## GitHub 및 GitHub Issues 구성
{: #github}

GitHub는 Git 저장소의 웹 기반 호스팅 서비스입니다. 쉽게 협업할 수 있도록 저장소의 로컬 및 원격 사본을 모두 보유할 수 있습니다. 

GitHub Issues는 작업과 플랜을 모두 한 위치에 보관하는 추적 도구입니다. 중요한 태스크에 초점을 맞출 수 있도록 개발 저장소와 통합됩니다. 

클라우드의 소스 코드를 관리하도록 GitHub 및 GitHub Issues를 구성하십시오.

1. 도구 체인을 작성하면서 이 도구 통합을 구성하는 경우 다음 단계를 따르십시오.

 a. 구성 가능한 통합 섹션에서 **GitHub**를 클릭하십시오. GitHub에 액세스하도록 {{site.data.keyword.Bluemix}}에 권한을 부여하지 않은 경우 **권한 부여**를 클릭하여 GitHub 웹 사이트로 이동하십시오. 활성 GitHub 세션이 없으면 로그인하도록 메시지를 표시합니다. **애플리케이션 권한 부여**를 클릭하여 {{site.data.keyword.Bluemix}}에서 GitHub 계정에 액세스하도록 허용하십시오. 활성 GitHub 세션이 있지만 최근에 비밀번호를 입력하지 않은 경우 확인을 위해 GitHub 비밀번호를 입력하도록 메시지가 표시될 수 있습니다.
 
 b. GitHub 저장소의 기본 대상 저장소 위치를 검토하십시오. 해당 저장소는 샘플 저장소에서 복제됩니다. 필요한 경우 대상 저장소의 이름을 변경하십시오.
 ![기본 대상 저장소 위치](images/toolchain_github_config.png)
   
1. 보유한 도구 체인에 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. 추가 단추(+)를 클릭하십시오.
1. 도구 통합 섹션에서 **GitHub**를 클릭하십시오.
1. 보유한 GitHub 저장소를 사용하려는 경우 URL을 입력하십시오. 저장소 유형으로는 **링크**를 클릭하십시오.
1. 새 GitHub 저장소를 사용하려면 다음과 같이 GitHub 저장소의 이름을 입력하고 복제 또는 분기 중인 저장소의 URL을 입력한 다음 저장소 유형을 선택하십시오. 

 a. 비어 있는 저장소를 작성하려면 **새로 작성**을 선택하십시오. 
 
 b. GitHub 저장소의 사본을 작성하려면 **복제**를 선택하십시오.
 
 c. 가져오기 요청을 통해 변경사항을 컨트리뷰션하도록 GitHub 저장소를 분기 실행하려면 **분기**를 선택하십시오.
 
1. GitHub Issues를 문제 추적에 사용하려는 경우 **GitHub Issues 사용** 선택란을 선택하십시오.
1. **통합 작성**을 클릭하십시오.
1. 작업할 GitHub 저장소의 타일을 클릭하여 github.com으로 이동하고 저장소의 컨텐츠를 보십시오.
 
  **팁**: Eclipse Orion Web IDE에서 통합 소스 코드 관리 도구를 사용하여 GitHub 저장소를 편집하고 작업공간에서 앱을 배치할 수 있습니다.

1. GitHub Issues를 사용하려면 GitHub Issues의 타일을 클릭하여 GitHub Issues로 이동하십시오.

자세한 정보는 [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} 및 [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}를 참조하십시오.    

##Dedicated {{site.data.keyword.ghe_short}} 사용
{: #ghe}

{{site.data.keyword.ghe_long}}는 IBM 클라우드에서 호스팅하며 완전히 관리되는 {{site.data.keyword.ghe_short}} 버전으로 Dedicated Bluemix 환경에 사용 가능합니다. GitHub에서는 개발자가 좋아하는 소셜 코딩 환경을 제공합니다. [{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window}에서는 네트워크에 통합된 물리적으로 격리된 하드웨어의 클라우드 컴퓨팅 환경을 제공합니다.

Dedicated {{site.data.keyword.ghe_short}}는 {{site.data.keyword.Bluemix_notm}} 전용 고객용입니다.

### 계정 설정 

{{site.data.keyword.ghe_short}}에는 {{site.data.keyword.Bluemix_notm}} Dedicated가 포함된 싱글 사인온이 있습니다. {{site.data.keyword.ghe_short}}로 로그인하려면 지역 관리자나 환경 이메일의 URL을 브라우저에 붙여넣으십시오. URL은 `github.your-company-dedicated-name.bluemix.net` 패턴을 따릅니다. {{site.data.keyword.Bluemix_notm}} Dedicated 사용자 ID 및 비밀번호로 로그인하십시오. 그러면 {{site.data.keyword.ghe_short}} 계정이 자동으로 작성됩니다. 

**참고:** 메시지에서 사용자 ID가 없음을 표시하면 지역 관리자에게 사용자 ID를 {{site.data.keyword.Bluemix_notm}} Dedicated 사용자 레지스트리에 추가하도록 요청하십시오. 지역 관리자인 경우 [{{site.data.keyword.Bluemix_notm}} Dedicated 사용자 및 권한 관리](https://new-console.stage1.ng.bluemix.net/docs/admin/index.html#oc_useradmin){: new_window}를 참조하십시오.

짧은 이름에 GitHub에서 지원하지 않는 문자(예: 마침표)가 포함된 경우를 제외하고는 대부분 GitHub 사용자 이름이 이메일의 짧은 이름입니다. 짧은 이름에 GitHub에서 지원하지 않는 문자가 포함된 경우 해당 문자를 대시로 바꿉니다.     

### 이메일 주소를 계정에 추가

알림을 받도록 {{site.data.keyword.ghe_short}} 계정 설정에 이메일 주소를 추가해야 합니다. 이메일 주소를 추가하고 나면 {{site.data.keyword.ghe_short}}의 소셜 코딩 기능을 이용할 수 있습니다.    
 
Dedicated {{site.data.keyword.ghe_short}} 계정에 이메일 주소를 추가하려면 다음 단계를 완료하십시오.    
1. GitHub 페이지의 오른쪽 상단 구석에서 프로파일 아이콘을 클릭하고 **설정**을 클릭하십시오.    
2. 사이드바에서 **이메일**을 클릭하십시오.    
3. 이메일 주소를 추가하고 **추가**를 클릭하십시오.     

{: #ghe_auth}
### 인증용 개인 액세스 토큰 또는 SSH 키 작성

로컬 Git 저장소에서 `복제` 또는 `푸시`와 같은 원격 Git 조작을 수행하려면 {{site.data.keyword.ghe_short}}를 인증할 개인 액세스 토큰 또는 SSH 키를 사용해야 합니다. HTTPS를 통한 인증은 액세스 토큰을 사용해서만 지원됩니다. 사용자 ID와 비밀번호를 사용하여 로컬 저장소에서 복제하거나 푸시할 수 없습니다. API 요청에는 개인 액세스 토큰도 필요합니다.

**참고:** 인증에 개인 액세스 토큰 또는 SSL 키를 사용하려는 경우 Git를 로컬로 설정해야 합니다. 지시사항은 [Git 설정](https://help.github.com/enterprise/2.6/user/articles/set-up-git/){: new_window}을 참조하십시오.    

개인 액세스 토큰을 작성하려면 다음 단계를 완료하십시오.    
   1. GitHub 페이지의 오른쪽 상단 구석에서 프로파일 아이콘을 클릭하고 **설정**을 클릭하십시오.    
   2. 사이드바에서 **개인 액세스 토큰**을 클릭하십시오.   
   3. **새 토큰 생성**을 클릭하십시오.
   4. 토큰 설명을 추가하고 **토큰 생성**을 클릭하십시오.
   5. 보안 위치나 비밀번호 관리 앱에 토큰을 복사하십시오.
     **참고:** 보안상의 이유로, 페이지를 종료하고 나면 더 이상 토큰을 볼 수 없습니다.    

HTTPS를 통한 명령행 액세스용 비밀번호 대신 개인 액세스 토큰을 사용하십시오. 


SSH 키를 작성하려면 다음 단계를 완료하십시오.
   1. Git Bash(Windows) 또는 새로운 터미널 창(Linux 및 Mac)을 여십시오.    
   2. {{site.data.keyword.ghe_short}} 계정에 추가한 이메일 주소를 대체하는 다음 텍스트를 붙여넣으십시오.
   
     ````
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     # Creates a new ssh key, using the provided email as a label
     공용/개인용 rsa 키 쌍을 생성합니다.
     ````

   3. 키를 저장할 파일을 지정하도록 메시지가 표시되면 Enter를 눌러 기본 위치를 승인하십시오.
   4. 프롬프트에서 보안 비밀번호 문구를 입력하십시오. 자세한 정보는 [SSH 키 비밀번호 문구에 대한 작업](https://help.github.com/enterprise/2.6/user/articles/working-with-ssh-key-passphrases/){: new_window}을 확인하십시오.   

다음과 같이 ssh-agent에 SSH 키를 추가하십시오.    
   1. ssh-agent가 사용되는지 확인하십시오. Git Bash를 사용하는 경우 ssh-agent를 사용하도록 다음 명령을 입력하십시오.
      ````
      # start the ssh-agent in the background
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ````    
  
   2. 다음 명령을 입력하여 ssh-agent에 SSH 키를 추가하십시오.
      ````
      $ ssh-add ~/.ssh/id_rsa
      ````    
   3. GitHub 계정에 SSH 키를 추가하십시오. 자세한 정보는 [GitHub 계정에 새 SSH 키 추가](https://help.github.com/enterprise/2.6/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}를 참조하십시오.    
   

### GitHub 조직, 팀 및 저장소 설정    

비슷한 프로젝트 또는 태스크에 대해 작업하는 개별 사용자 그룹을 작성하므로 GitHub 조직을 설정하면 유용합니다. 조직 내에 팀을 구성하면 저장소에 대한 액세스를 제어하는 이점이 추가됩니다. 자세한 정보는 [조직 및 팀](https://help.github.com/enterprise/2.6/admin/guides/user-management/organizations-and-teams/){: new_window}을 참조하십시오.

**참고:** GitHub 조직이 Bluemix 조직과 다릅니다.

다음 태스크를 완료하여 팀 프로젝트를 설정하십시오.

   1. [조직(org) 작성](https://help.github.com/enterprise/2.6/user/articles/creating-a-new-organization-account/){: new_window}.
   2. [조직의 저장소 작성](https://help.github.com/enterprise/2.6/user/articles/create-a-repo/){: new_window}.
   3. [조직에 참여하도록 사용자 초대](https://help.github.com/enterprise/2.6/user/articles/inviting-users-to-join-your-organization/){: new_window}.
   4. [조직에서 소유자 권한을 갖는 팀 구성원을 한 명 이상 신중하게 선택](https://help.github.com/enterprise/2.6/user/articles/changing-a-person-s-role-to-owner/){: new_window}.    
   
  **참고:** 조직에 사용자를 초대하기 전에 {{site.data.keyword.ghe_short}}에 한 번 이상 로그인해야 합니다. 그렇지 않으면 {{site.data.keyword.ghe_short}} 계정을 초대할 수 없습니다.
   
### 지원 받기
지금 응답을 받으려면 [스택 오버플로우](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}에 질문을 제출하십시오. 

추가 지원은 다음 자원을 사용하십시오.    
   1. 다음의 양식을 완료하십시오. https://ibm.biz/bluemixsupport   
   2. 다음의 클라이언트 성공 포털을 통해 새 티켓을 제출하십시오. https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix    


## PagerDuty 구성
{: #pagerduty}

PagerDuty에서는 여러 모니터링 시스템의 데이터를 단일 보기로 통합합니다. 문제가 발생하면 PagerDuty를 통해 현재 문제점을 가장 잘 해결할 수 있는 팀 구성원에게 해당 문제를 알릴 수 있습니다. 팀 구성원이 문제점에 응답하지 않으면 보조 엔지니어나 운영 관리자에게 라우팅하도록 에스컬레이션을 구성할 수 있습니다.

문제점을 더 빨리 수정하고 중단 시간을 단축시킬 수 있도록 파이프라인 단계 실패가 발생하면 알림을 보내도록 다음과 같이 PagerDuty를 구성하십시오.

1. 도구 체인을 작성하면서 이 도구 통합을 구성하는 경우 구성 가능한 통합 섹션에서 **PagerDuty**를 클릭하십시오. 
1. 보유한 도구 체인에 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. 추가 단추(+)를 클릭하십시오.
1. 도구 통합 섹션에서 **PagerDuty**를 클릭하십시오.
1. PagerDuty 계정과 연관된 PagerDuty 사이트 이름을 입력하십시오. PagerDuty 계정이 없으면 [하나를 등록](https://signup.pagerduty.com/accounts/new){: new_window}하십시오.
1. PagerDuty 계정의 API 액세스 키를 입력하십시오. 키를 찾는 데 관한 지시사항은 [API 인증](https://signup.pagerduty.com/accounts/new){: new_window}을 참조하십시오.
1. PagerDuty 서비스의 이름을 입력하십시오.
1. 기본 PagerDuty 담당자의 이메일 주소를 입력하십시오.
1. 기본 PagerDuty 담당자의 전화번호를 입력하십시오.
1. **통합 작성**을 클릭하십시오.
1. PagerDuty의 타일을 클릭하여 pagerduty.com으로 이동하십시오. 도구 체인에 대해 이 도구 통합을 구성할 때 지정한 PagerDuty 서비스와 연관된 이벤트를 볼 수 있습니다. 

자세한 정보는 [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}를 참조하십시오.


## Sauce Labs 구성
{: #saucelabs}

Sauce Labs는 기능 단위 테스트를 실행합니다. Sauce Labs 테스트 스위트가 {{site.data.keyword.deliverypipeline}}의 테스트 작업으로 구성된 경우 테스트 스위트에서 Continuous Delivery 프로세스의 일부로 웹이나 모바일 앱에 대해 테스트를 실행할 수 있습니다. 이러한 테스트는 프로젝트의 귀중한 플로우 제어를 제공하여, 잘못된 코드가 배치되지 못하게 하는 게이트 역할을 수행할 수 있습니다.

사용자가 웹 사이트나 애플리케이션을 사용할 수 있는 방법을 에뮬레이트할 수 있도록 여러 운영 체제와 브라우저에서 자동화된 Functional Test를 실행하도록 Sauce Labs를 구성하십시오.

1. 도구 체인을 작성하면서 이 도구 통합을 구성하는 경우 구성 가능한 통합 섹션에서 **Sauce Labs**를 클릭하십시오. 
1. 보유한 도구 체인에 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오. 
1. 추가 단추(+)를 클릭하십시오.
1. 도구 통합 섹션에서 **Sauce Labs**를 클릭하십시오.
1. Sauce Labs 계정과 연관된 사용자 이름을 입력하십시오. [Sauce Labs 계정 페이지 맨 위의 환영 페이지에서 사용자 이름 찾기](https://saucelabs.com/account){: new_window}를 수행할 수 있습니다.
1. Sauce Labs 계정의 액세스 키를 입력하십시오. [Sauce Labs 계정 페이지의 왼쪽 아래 구석에서 키 찾기](https://saucelabs.com/account){: new_window}를 수행할 수 있습니다.
1. **통합 작성**을 클릭하십시오.
1. Sauce Labs의 타일을 클릭하여 saucelabs.com으로 이동하고 도구 체인의 테스트 활동을 보십시오.

 **팁**: {{site.data.keyword.deliverypipeline}}에 Sauce Labs 테스트 작업을 추가한 경우 서비스 인스턴스를 선택할 수 있습니다.

자세한 정보는 [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}를 참조하십시오.


## Slack 구성
{: #slack}

**중요**: 공용 Slack 채널에 게시한 알림은 팀의 모든 사용자가 볼 수 있습니다. 각 사용자는 직접 게시한 컨텐츠에 대한 책임이 있습니다.

Slack은 클라우드 기반 실시간 메시징 및 알림 시스템입니다. Slack에서는 팀 협업용 이메일을 대체하며 대화식 특성이 강화된 지속적 대화를 제공합니다. 작업과 직접 연관된 채널 세트 또는 전용 채널에서 팀과 통신할 수 있습니다. 채널을 통하거나 둘 이상의 사용자 간 직접 메시지를 통해 파일과 이미지도 공유할 수 있습니다. 직접 메시지와 채널에서의 통신은 검색할 수 있도록 유지합니다.  

도구 통합에서 도구 체인에 대한 알림(예: 테스트 및 배치 활동)을 받도록 Slack을 구성하십시오.

1. 도구 체인을 작성하면서 이 도구 통합을 구성하는 경우 구성 가능한 통합 섹션에서 **Slack**을 클릭하십시오. 
1. 보유한 도구 체인에 도구 통합을 추가하는 경우 DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭하십시오. 그런 다음 **도구 통합**을 클릭하십시오.
1. 추가 단추(+)를 클릭하십시오.
1. 도구 통합 섹션에서 **Slack**을 클릭하십시오.
1. Slack 계정의 API 인증 토큰을 입력하십시오. 생성된 전체 액세스 토큰을 사용하여 Slack을 인증해야 합니다. 토큰을 찾는 데 관한 지시사항은 [Slack 인증](https://api.slack.com/web#authentication){: new_window}을 참조하십시오.
1. 알림을 보낼 Slack 채널의 이름을 입력하십시오. 지정하는 채널이 없으면 작성됩니다. 채널이 아카이브된 경우 재활성화됩니다.
1. **통합 작성**을 클릭하십시오.
1. Slack의 타일을 클릭하십시오. 구성된 Slack 채널에서 도구 체인의 활동을 모두 볼 수 있습니다. 

자세한 정보는 [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}을 참조하십시오.
