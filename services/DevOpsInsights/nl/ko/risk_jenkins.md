---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 자유 양식 Jenkins 프로젝트와 통합

개방형 도구 체인에 {{site.data.keyword.DRA_full}}를 추가하고 이를 모니터하는 정책을 정의한 후에 자유 양식 Jenkins 프로젝트와 통합할 수 있습니다. 자유 양식 Jenkins 프로젝트는 Jenkins 웹 인터페이스에서 구성하고 관리합니다. 

Jenkins용 IBM Cloud DevOps 플러그인은 Jenkins 프로젝트를 도구 체인과 통합합니다. *도구 체인*은 개발, 배치 및 운영 태스크를 지원하는 도구 통합 세트입니다. 도구 체인의 전체 기능은 개별 도구 통합을 합한 것보다 강력합니다. 개방형 도구 체인은 {{site.data.keyword.contdelivery_full}} 서비스의 일부입니다. {{site.data.keyword.contdelivery_short}} 서비스에 대한 자세한 정보는 [해당 문서](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)를 참조하십시오.

IBM Cloud DevOps 플러그인을 설치한 후 {{site.data.keyword.DRA_short}}에 테스트 결과를 공개하고 자동화된 품질 게이트를 추가하며 Deployment Risk를 추적할 수 있습니다. 또한 도구 체인에서 Slack 및 PagerDuty와 같은 기타 도구에 작업 알림을 보낼 수 있습니다. 배치를 추적할 수 있도록 도구 체인은 Git 커미트와 관련 Git 또는 JIRA 문제에 배치 메시지를 추가할 수 있습니다. 도구 체인의 연결 페이지에서도 배치를 볼 수 있습니다. 

플러그인은 통합을 지원하는 사후 빌드 조치 및 CLI를 제공합니다. {{site.data.keyword.DRA_short}}에서는 단위 테스트, Functional Test, 코드 적용 범위 도구, 정적 보안 코드 스캔 및 동적 보안 코드 스캔의 결과를 집계하고 분석하여 코드가 배치 프로세스의 게이트에서 사전 정의된 정책을 만족하는지 판별합니다. 코드가 정책을 충분히 준수하지 못하는 경우, 위험한 변경이 릴리스되지 않도록 배치가 정지됩니다. {{site.data.keyword.DRA_short}}를 Continuous Delivery 환경의 안전망으로 사용할 수 있는데 이를 통해 시간 경과에 따라 품질 표준을 구현 및 개선하고 프로젝트 상황을 파악하는 데이터 시각화 도구로 사용할 수 있습니다. 

## 전제조건
{: #jenkins_prerequisites}

Jenkins 프로젝트를 실행하는 서버에 액세스할 수 있어야 합니다.

## 도구 체인 작성
{: #jenkins_create}

도구 체인을 작성해야 {{site.data.keyword.DRA_short}}를 Jenkins 프로젝트와 통합할 수 있습니다. 

1. 도구 체인을 작성하려면 [도구 체인 페이지 작성](https://console.ng.bluemix.net/devops/create)으로 이동하여 해당 페이지의 지시사항을 따르십시오. 

2. 도구 체인을 작성한 다음 {{site.data.keyword.DRA_short}}를 추가하십시오. 지시사항은 [{{site.data.keyword.DRA_short}}문서](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)를 참조하십시오. 

## 플러그인 설치
{: #jenkins_install}

우선 Jenkins 서버에 플러그인을 설치하십시오. 서버 인터페이스를 열고 다음을 수행하십시오. 

1. **Jenkins 관리**를 클릭하십시오. 
2. **플러그인 관리**를 클릭하십시오.  
3. **사용 가능** 탭을 클릭하십시오. 
4. `IBM Cloud DevOps`에 대해 필터링하십시오.  
5. IBM Cloud DevOps를 선택하십시오. 
6. **지금 다운로드 및 재시작 이후 설치**를 클릭하십시오.  

서버가 다시 시작되면 플러그인을 사용할 수 있습니다.   

## Deployment Risk 대시보드에 맞게 Jenkins 작업 구성
{: #jenkins_configure}

플러그인이 설치되고 나면 Jenkins 프로젝트에 {{site.data.keyword.DRA_short}}를 통합할 수 있습니다. 

다음 단계를 따라 Deployment Risk의 게이트와 대시보드를 프로젝트와 사용하십시오.

1. 빌드, 테스트 또는 배치와 같은 작업의 구성을 여십시오.

2. 해당 유형에 맞는 사후 빌드 조치를 추가하십시오.

   * 빌드 작업에 대해 **IBM Cloud DevOps에 빌드 정보 공개**를 사용하십시오.
   
   * 테스트 작업에 대해 **IBM Cloud DevOps에 테스트 결과 공개**를 사용하십시오.
   
   * 배치 작업에 대해 **IBM Cloud DevOps에 배치 정보 공개**를 사용하십시오.
   
3. 필수 필드를 완료하십시오. 이러한 필드는 작업 유형에 따라 다릅니다. 

   * **신임 정보** 목록에서 {{site.data.keyword.Bluemix_notm}} ID와 비밀번호를 선택하십시오. Jenkins에서 저장하지 않은 경우 **추가**를 클릭하여 추가하고 저장하십시오. **연결 테스트**를 클릭하여 {{site.data.keyword.Bluemix_notm}}와의 연결을 테스트하십시오.
   
   * **빌드 작업 이름** 필드에서 Jenkins에 지정한 것과 동일하게 빌드 작업의 이름을 지정하십시오. 빌드가 테스트 작업과 수행되는 경우 이 필드를 비워 두십시오. 빌드 작업이 Jenkins 외부에서 발생하는 경우 **빌드를 Jenkins 외부에서 수행함** 선택란을 선택하고 빌드 번호와 빌드 URL을 지정하십시오.
   
   * 환경의 경우, 빌드 단계에서 테스트를 실행 중인 경우 빌드 환경만 선택하십시오. 배치 단계에서 테스트를 실행 중이면 배치 환경을 선택하고 환경 이름을 지정하십시오. `STAGING`과 `PRODUCTION`의 두 값이 지원됩니다.
   
   * **결과 파일 위치** 필드에 결과 파일의 위치를 지정하십시오. 테스트에서 결과 파일을 생성하지 않으면 이 필드를 비워 두십시오. 이 플러그인은 현재 테스트 작업의 상태를 기반으로 기본 결과 파일을 업로드합니다.

   이러한 이미지는 예제 구성을 보여줍니다.
   
   ![빌드 정보 업로드](images/Upload-Build-Info.png "DRA에 빌드 정보 공개")
   *빌드 정보 공개*
   
   ![테스트 결과 업로드](images/Upload-Test-Result.png "DRA에 테스트 결과 공개")
   *테스트 결과 공개*
   
   ![배치 정보 업로드](images/Upload-Deployment-Info.png "DRA에 배치 정보 공개")
   *배치 정보 공개*

4. {{site.data.keyword.DRA_short}} 정책 게이트를 사용하여 다운스트림 배치 작업을 제어하려면 사후 빌드 조치, **IBM Cloud DevOps Gate**를 추가하십시오. 정책을 선택하고 테스트 결과의 범위를 지정하십시오. 정책 게이트가 다운스트림 배치를 방지할 수 있도록 **정책 규칙을 기반으로 빌드 실패** 선택란을 선택하십시오. 다음 이미지는 예제 구성을 보여줍니다.

    ![DevOps Insights Gate](images/DRA-Gate.png "DevOps Insights Gate")

5. Jenkins 빌드 작업을 실행하십시오.

6. [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops)로 이동하고 도구 체인을 선택한 다음 **DevOps Insights**를 클릭하여 Deployment Risk 대시보드를 보십시오.

Deployment Risk 대시보드는 스테이징 배치 작업 후의 게이트 존재에 따라 달라집니다. 대시보드를 사용하려면 스테이징 환경에 배치한 후, 프로덕션 환경에 배치하기 전에 게이트가 있는지 확인하십시오.
    
## 구성 알림
{: #jenkins_notifications}

[Bluemix 문서](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)의 지시사항을 따라 Slack 또는 PagerDuty와 같은 도구에 알림을 보내도록 Jenkins 작업을 구성할 수 있습니다.
