---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk(베타)
{: #gettingstarted}

{{site.data.keyword.DRA_short}}에서는 배치, 특히 위험성에 대한 풍부한 정보를 제공합니다. 이 정보를 사용하면 정책과 게이트를 사용하여 Delivery Pipeline에서 품질 보호를 자동화할 수 있습니다.
{:shortdesc}

도구 체인에서 {{site.data.keyword.DRA_short}}를 연 다음 **Deployment Risk**를 클릭하십시오. 여기에서 스테이징 및 프로덕션 환경에서 애플리케이션의 개요를 가져오고 코드 적용 범위, 테스트 성능 및 보안 보고서를 이해하도록 드릴다운할 수 있습니다. 이러한 대시보드는 파이프라인의 {{site.data.keyword.DRA_short}} 테스트에 있는 최신 정보로 자동으로 채워집니다. 

## Deployment Risk 정보
{: #about}

정책과 게이트를 통해 도구 체인에 품질 표준을 적용하는 데 Deployment Risk를 사용할 수 있습니다. 정책은 규칙 세트로 구성되며, 게이트가 정책을 적용합니다. 예를 들어, 단위 테스트와 테스트 적용 범위 표준을 만족시키는 빌드가 필요한 "단위 테스트 및 테스트 적용 범위" 정책을 작성할 수 있습니다. 그런 다음 정책을 나타내는 게이트를 Continuous Delivery 프로세스에 추가합니다. 정책을 만족하지 않는 빌드가 해당 게이트에서 중지됩니다. 

Deployment Risk는 {{site.data.keyword.contdelivery_full}}의 일부인 {{site.data.keyword.deliverypipeline}}과 작동하고 Jenkins 프로젝트와 작동합니다. 대략적으로 이 둘을 사용하는 지시사항은 비슷합니다.   

{{site.data.keyword.deliverypipeline}}을 사용하는 경우 다음 단계를 따르십시오.

1. 관리할 {{site.data.keyword.DRA_short}}의 [정책 및 규칙을 작성](#policies_and_rules)하십시오.
2. {{site.data.keyword.DRA_short}}와 통합할 [파이프라인의 단계를 준비](#integrate_pipeline)하십시오.

3. 파이프라인에서 {{site.data.keyword.DRA_short}}에 결과를 업로드하는 [테스트 작업을 작성하거나 편집](#configure_pipeline_jobs)하십시오.
4. 해당 결과와 정책을 기반으로 승격 의사결정을 하는 파이프라인에 [게이트를 추가](#configure_pipeline_gates)하십시오.
5. 파이프라인을 실행하고 [결과 보기](#view_results)를 수행하십시오.

Jenkins를 사용하는 경우 다음 단계를 따르십시오.

1. 관리할 {{site.data.keyword.DRA_short}}의 [정책 및 규칙을 작성](#policies_and_rules)하십시오.
2. [Jenkins 플러그인을 설치 및 구성](#integrate_jenkins)하십시오.
3. [플러그인 지시사항에 설명된 대로 테스트 작업과 게이트를 작성](#integrate_jenkins)하십시오. 분석을 위해 테스트를 통해 결과를 {{site.data.keyword.DRA_short}}에 업로드하고, 게이트에서 해당 결과를 사용하여 승격 의사결정을 내립니다.
4. 프로젝트를 실행하고 [결과 보기](#view_results)를 수행하십시오. 

코드를 빌드하고 배치하는 방법과 상관없이 결과는 동일합니다. 표준에 맞는 빌드는 Deployment Risk 게이트를 통과하고 표준을 만족하지 않는 빌드는 중지됩니다. 

## 전제조건
{: #prerequisites}

Deployment Risk에는 [{{site.data.keyword.DRA_short}} 시작하기](/docs/services/DevOpsInsights/index.html)에 설명된 내용 이상의 구성이 필요합니다.

Deployment Risk를 사용하려면 다음 두 가지가 필요합니다.

* {{site.data.keyword.deliverypipeline}} 또는 Jenkins 프로젝트의 인스턴스
* 프로젝트를 평가하는 데 사용할 테스트

## 정책 및 규칙 작성
{: #policies_and_rules}

정책은 Delivery Pipeline에서 게이트를 제어하는 규칙 세트입니다. 코드가 특정 게이트에서 규정되는 정책을 만족하지 않거나 초과하는 경우 위험한 변경사항이 릴리스되지 못하도록 배치가 정지됩니다.

{{site.data.keyword.DRA_short}}에 정책을 정의합니다. 정책은 {{site.data.keyword.DRA_short}}가 포함된 {{site.data.keyword.Bluemix_notm}} 조직(org)에 작성됩니다. 동일 조직의 모든 애플리케이션에서 정책을 사용할 수 있습니다. 

### 정책 작성
{: #create_policies}

정책을 작성하려면 다음을 수행하십시오.

1. 왼쪽 탐색에서 **설정**을 클릭하십시오.

2. **정책**을 클릭하십시오.

3. **정책 작성**을 클릭한 다음 새 정책의 이름과 설명을 입력하십시오.

4. **다음**을 클릭하십시오. 

4. 정책에 규칙을 하나 이상 추가하십시오. 
  1. **정책에 규칙 추가**를 클릭하십시오.
  2. 규칙 유형을 선택하십시오. 
  3. 규칙의 세부사항과 조건을 입력하십시오. 
  4. **저장**을 클릭하십시오. 

5. 정책에 규칙을 추가한 다음 **완료**를 클릭하십시오.

### 규칙 작성
{: #creating_rules}

성공 또는 실패를 판단하기 위해 규칙을 통해 정책에서 사용하는 기준을 정의합니다. 80% 단위 테스트가 성공해야 하는 단위 테스트 규칙과 100% 코드 적용 범위가 필요한 테스트 적용 범위 규칙을 포함하는 "단위 테스트 및 테스트 적용 범위" 정책을 작성할 수 있습니다. 파이프라인에서 이 규칙을 나타내는 게이트를 추가하면 게이트에서 이 두 규칙을 모두 만족하지 않는 빌드를 처리하지 못하게 합니다. 

테스트를 중요로 표시하여 테스트가 항상 성공이 되도록 할 수 있습니다. 규칙을 작성하려면 정책을 선택한 다음 **정책에 규칙 추가**를 클릭하십시오. 

#### 기능 검증 테스트 규칙 작성
{: #criteria_fvt}

1. 설명을 입력하고 형식을 선택하십시오. 

2. 성공한 것으로 선언하기 위해 패스해야 하는 테스트 케이스의 백분율을 지정하십시오. 

3. 중요한 테스트 케이스를 정의하십시오. 

4. 테스트 케이스 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오. 

5. **저장**을 클릭하십시오. 


#### 단위 테스트 규칙 작성
{: #criteria_ut}

1. 설명을 입력하고 형식을 선택하십시오. 

2. 성공한 것으로 선언하기 위해 패스해야 하는 테스트 케이스의 백분율을 지정하십시오. 

3. 중요한 테스트 케이스를 정의하십시오. 

4. 테스트 케이스 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오. 

5. **저장**을 클릭하십시오. 


#### 코드 적용 범위 규칙 작성
{: #criteria_codecoverage}

1. 설명을 입력하고 형식을 선택하십시오. 

2. 성공한 것으로 선언하는 데 필요한 코드 적용 범위의 백분율을 지정하십시오. 

3. 코드 적용 범위 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오. 

4. **저장**을 클릭하십시오. 

#### 정적 보안 스캔 규칙 작성
{: #criteria_static}

정적 코드 및 동적 앱 스캔을 실행하도록 {{site.data.keyword.DRA_short}}를 IBM Application Security on Cloud와 통합할 수 있습니다. Application Security on Cloud에 대한 자세한 정보는 [공식 문서](/docs/services/ApplicationSecurityonCloud/index.html)를 참조하십시오.

1. 설명을 입력하십시오.

2. 규칙에서 허용하는 심각도가 높음, 중간 및 낮음인 문제의 최대수를 지정하십시오. 

3. **저장**을 클릭하십시오. 

#### 동적 보안 스캔 규칙 작성
{: #criteria_dynamic}

{{site.data.keyword.DRA_short}}와 {{site.data.keyword.appseccloudfull}}를 통합하여 동적 앱 스캔을 실행할 수 있습니다. Application Security on Cloud에 대한 자세한 정보는 [공식 문서](/docs/services/ApplicationSecurityonCloud/index.html)를 참조하십시오.

1. 설명을 입력하십시오.

2. 규칙에서 허용하는 심각도가 높음, 중간 및 낮음인 문제의 최대수를 지정하십시오. 

3. **저장**을 클릭하십시오. 

## {{site.data.keyword.deliverypipeline}} 구성 
{: #configuration}

도구 체인에 {{site.data.keyword.DRA_short}}를 추가하고 모니터하는 정책을 정의한 다음 {{site.data.keyword.deliverypipeline}}과 통합하십시오. 파이프라인에 대한 자세한 정보는 [공식 문서](/docs/services/ContinuousDelivery/pipeline_working.html)를 참조하십시오.

### 파이프라인 단계 준비
{: #integrate_pipeline}

Deployment Risk가 프로젝트를 분석하려면 파이프라인에서 스테이징 및 프로덕션 단계를 정의해야 합니다. **환경 특성**에 있는 각 단계의 구성 메뉴 ![파이프라인 단계 구성 아이콘](images/pipeline-stage-configuration-icon.png)에 있는 텍스트 환경 특성을 사용하여 단계를 정의합니다.

1. 스테이징 단계에서 `LOGICAL_ENV_NAME` 특성을 `STAGING`으로 설정하십시오. 

2. 프로덕션 단계에서 `LOGICAL_ENV_NAME` 특성을 `PRODUCTION`으로 설정하십시오. 

앱을 빌드하거나 배치하는 단계에 다음 특성도 추가할 수 있습니다.

* `LOGICAL_APP_NAME` - 대시보드에 앱의 이름을 정의합니다.
* `BUILD_PREFIX` - 단계의 빌드에 접두어로 추가된 텍스트를 정의합니다. 이 텍스트도 대시보드에 표시됩니다. 

### 테스트 작업 추가
{: #configure_pipeline_jobs}

분석을 위해 {{site.data.keyword.DRA_short}}에 결과를 업로드하는 유형과 해당 분석에 따라 조치를 수행하는 게이트와 같은 두 가지 유형의 테스트 작업을 사용하여 파이프라인에 {{site.data.keyword.DRA_short}}를 통합합니다. 

먼저 테스트를 실행하고 결과를 업로드하기 위해 파이프라인에 고급 테스터 작업을 추가합니다. 

**참고:** {{site.data.keyword.DRA_short}}에 결과를 업로드하기 위해 테스트 작업을 업데이트하려면 계속하기 전에 편리한 위치에 구성을 저장하십시오. 그런 다음 작업 구성 메뉴를 열고 3단계로 건너뛰십시오. 

1. 결과를 업로드하는 작업을 추가하려는 단계에서 **단계 구성** 아이콘 ![파이프라인 단계 구성 아이콘](images/pipeline-stage-configuration-icon.png)을 클릭하십시오. **구성 단계**를 클릭하십시오.
2. 테스트 작업을 작성하고 이름을 입력하십시오. 
3. 작업 유형에 대해 **고급 테스터**를 선택하십시오.
4. 정상 파이프라인 테스트 작업에서와 마찬가지로 **테스트 명령** 및 **작업 디렉토리** 필드를 완료하십시오. 
5. 나머지 필드를 작성하여 특정 테스트 유형의 테스트 결과를 업로드하십시오.  

 1. 사용하려는 {{site.data.keyword.DRA_short}} 정책에 정의된 사항과 일치하는 메트릭의 유형을 선택하십시오.
 2. 결과 파일 위치를 입력하십시오. 이 위치는 작업 디렉토리에 상대적입니다. 

6. 같은 작업에서 두 번째 테스트 유형의 결과를 업로드하려면 *추가* 접두부가 있는 필드를 작성하십시오.
7. **저장**을 클릭하여 파이프라인을 리턴하십시오. 

**메트릭 유형** 및 **결과 파일 위치** 필드의 값은 올바른 형식을 따라야 합니다. 

<table><thead>
<tr>
<th>메트릭 유형</th>
<th>지원되는 형식</th>
</tr>
</thead><tbody>
<tr>
<td>기능 검증 테스트</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>단위 테스트</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>코드 적용 범위</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

그림 1은 단위 테스트를 실행하여 결과를 Mocha 형식으로 업로드한 다음 코드 적용 범위 결과를 Istanbul 형식으로 업로드하는 테스트 작업을 보여줍니다. 

![DevOps Insights 업로드 작업](images/insights_upload_job.png)
*그림 1. DevOps Insights에 결과 업로드*

### 게이트 정의
{: #configure_pipeline_gates}

{{site.data.keyword.DRA_short}} 게이트는 테스트 결과가 정의된 정책을 준수하는지 확인합니다. 정책을 준수하지 못하는 경우 기본적으로 {{site.data.keyword.DRA_short}} 게이트가 실패합니다. 실패한 후에도 파이프라인이 진행할 수 있도록 자문 역할로 조치를 수행하도록 게이트를 구성할 수 있습니다.

Deployment Risk 대시보드는 스테이징 배치 작업 후의 게이트 존재에 따라 달라집니다. 대시보드를 사용하려면 스테이징 환경에 배치한 후, 프로덕션 환경에 배치하기 전에 게이트가 있는지 확인하십시오.

일반적으로 파이프라인의 빌드 승격 전에 게이트를 배치합니다. 이 위치는 정책에 대해 빌드 품질을 점검하여 하나의 환경에서 다른 환경으로 승격하기에 안전한지 확인하는 데 적합합니다. 그러나 게이트는 특정 기준을 점검할 파이프라인의 임의 위치에 배치할 수 있습니다. 스테이징 환경에 배치하기 전에 배치한 게이트가 여전히 정책을 적용하지만 Deployment Risk 대시보드에 표시되지 않습니다.

1. 단계에서 **단계 구성** 아이콘 ![파이프라인 단계 구성 아이콘](images/pipeline-stage-configuration-icon.png)을 클릭한 다음 **구성 단계**를 클릭하십시오.
2. **작업 추가**를 클릭하십시오. 작업 유형에 **테스트**를 선택하십시오.
3. 테스터 유형으로 **{{site.data.keyword.DRA_short}} 게이트**를 선택하십시오.
4. 환경 이름을 지정하십시오. 이 값이 [환경 특성](#toolchain_pipeline_props)에 정의된 값과 일치하는지 확인하십시오.
5. 이 게이트에서 검사할 정책 이름을 입력하십시오.

 이 이름은 정의된 정책 이름 중 하나와 정확히 일치해야 합니다. 같은 {{site.data.keyword.Bluemix_notm}} 조직에 정의된 정책만 도구 체인으로 지정할 수 있습니다. 

6. 선택사항: 게이트 기능을 권장 모드로 작성하려면 **작업 실패 시 이 단계 실행 중지** 선택란을 선택 취소하십시오. 권장 모드에서는 {{site.data.keyword.DRA_short}}가 게이트에서 동일한 정책 분석을 완료하고 보고서를 생성하지만 실패하는 경우 파이프라인이 중지되지 않습니다. 
7. **저장**을 클릭하여 파이프라인을 리턴하십시오. 
8. 이러한 단계를 반복하여 모든 {{site.data.keyword.DRA_short}} 정책의 게이트를 설정하십시오. 

![Deployment Risk Mocha 작업](images/insights_gate_job.png)
*그림 2. DevOps Insights 게이트*

파이프라인이 구성되면 {{site.data.keyword.DRA_short}}를 사용하십시오. 지시사항은 [Delivery Pipeline 실행](/docs/services/DevOpsInsights/pipeline_decision_reports.html#toolchain_reports)을 참조하십시오.

## Jenkins 프로젝트 구성
{: #integrate_jenkins}

개방형 도구 체인에 {{site.data.keyword.DRA_full}}를 추가하고 이를 모니터하는 정책을 정의한 후에 Jenkins 프로젝트와 통합할 수 있습니다. 

Jenkins용 IBM Cloud DevOps 플러그인은 Jenkins 프로젝트를 도구 체인과 통합합니다. *도구 체인*은 개발, 배치 및 운영 태스크를 지원하는 도구 통합 세트입니다. 도구 체인의 전체 기능은 개별 도구 통합을 합한 것보다 강력합니다. 개방형 도구 체인은 {{site.data.keyword.contdelivery_full}} 서비스의 일부입니다. {{site.data.keyword.contdelivery_short}} 서비스에 대한 자세한 정보는 [해당 문서](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html)를 참조하십시오.

IBM Cloud DevOps 플러그인을 설치한 후 {{site.data.keyword.DRA_short}}에 테스트 결과를 공개하고 자동화된 품질 게이트를 추가하며 Deployment Risk를 추적할 수 있습니다. 또한 도구 체인에서 Slack 및 PagerDuty와 같은 기타 도구에 작업 알림을 보낼 수 있습니다. 배치를 추적할 수 있도록 도구 체인은 Git 커미트와 관련 Git 또는 JIRA 문제에 배치 메시지를 추가할 수 있습니다. 도구 체인의 연결 페이지에서도 배치를 볼 수 있습니다. 

플러그인은 통합을 지원하는 사후 빌드 조치 및 CLI를 제공합니다. {{site.data.keyword.DRA_short}}에서는 단위 테스트, Functional Test, 코드 적용 범위 도구, 정적 보안 코드 스캔 및 동적 보안 코드 스캔의 결과를 집계하고 분석하여 코드가 배치 프로세스의 게이트에서 사전 정의된 정책을 만족하는지 판별합니다. 코드가 정책을 충분히 준수하지 못하는 경우, 위험한 변경이 릴리스되지 않도록 배치가 정지됩니다. {{site.data.keyword.DRA_short}}를 Continuous Delivery 환경의 안전망으로 사용할 수 있는데 이를 통해 시간 경과에 따라 품질 표준을 구현 및 개선하고 프로젝트 상황을 파악하는 데이터 시각화 도구로 사용할 수 있습니다. 

### 전제조건
{: #jenkins_prerequisites}

Jenkins 프로젝트를 실행하는 서버에 액세스할 수 있어야 합니다.

### 도구 체인 작성
{: #jenkins_create}

도구 체인을 작성해야 {{site.data.keyword.DRA_short}}를 Jenkins 프로젝트와 통합할 수 있습니다. 

1. 도구 체인을 작성하려면 [도구 체인 페이지 작성](https://console.ng.bluemix.net/devops/create)으로 이동하여 해당 페이지의 지시사항을 따르십시오. 

2. 도구 체인을 작성한 다음 {{site.data.keyword.DRA_short}}를 추가하십시오. 지시사항은 [{{site.data.keyword.DRA_short}}문서](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html)를 참조하십시오. 

### 플러그인 설치
{: #jenkins_install}

먼저 {{site.data.keyword.DRA_short}}에서 플러그인을 다운로드하십시오.  

1. 도구 체인의 개요 페이지에서 **DevOps Insights**를 클릭하십시오.
2. **설정**을 클릭한 다음 **Jenkins 플러그인 설정**을 클릭하십시오.
3. 페이지의 지시사항을 따라 플러그인을 다운로드하십시오.

그런 다음 Jenkins 서버에서 플러그인을 설치하십시오.

1. **Jenkins 관리 &gt; 플러그인 관리**를 클릭하고 **고급** 탭을 클릭하십시오.
2. **파일 선택**을 클릭하고 IBM Cloud DevOps 플러그인 설치 파일을 선택하십시오. 
3. **업로드**를 클릭하십시오. 
4. Jenkins를 다시 시작하고 플러그인이 설치되었는지 확인하십시오.

### Deployment Risk 대시보드에 맞게 Jenkins 작업 구성
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
    
### 구성 알림
{: #jenkins_notifications}

[Bluemix 문서](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins)의 지시사항을 따라 Slack 또는 PagerDuty와 같은 도구에 알림을 보내도록 Jenkins 작업을 구성할 수 있습니다.

이 예에서는 작업 구성에 맞게 `ICD_WEBHOOK_URL`을 구성하는 방법을 보여줍니다.
![ICD_WEBHOOK_URL 매개변수 설정](images/Set-Parameterized-Webhook.png "매개변수화된 WebHook 설정")

이 예에서는 작업 알림의 사후 빌드 조치 구성 방법을 보여줍니다.
![WebHook 알림의 사후 빌드 조치](images/PostBuild-WebHookNotification.png "사후 빌드 조치의 WebHook 알림 구성")

## 결과 보기
{: #view_results}

파이프라인을 실행한 후에 {{site.data.keyword.DRA_short}}를 시작하여 해당 테스트 결과를 수집하고 분석하여 기준선을 설정합니다. 모든 후속 실행 데이터를 수집하여 이전 결과와 비교합니다. 의사결정 게이트는 이 데이터를 사용하여 배치 중지 시점을 결정합니다.  

Deployment Risk 대시보드에서 배치와 게이트 평가 데이터를 볼 수 있습니다. 대시보드를 열려면 {{site.data.keyword.DRA_short}}를 열고 사이드 메뉴에서 **Deployment Risk**를 클릭하십시오.

{{site.data.keyword.contdelivery_short}} 파이프라인을 사용하려면 파이프라인 자체에서 개별 게이트 실행 보고서를 볼 수 있습니다. 파이프라인에서 게이트의 의사결정 보고서를 보려면 다음을 수행하십시오.

1. 검사할 게이트가 포함된 단계에서 **로그 및 히스토리 보기**를 클릭하십시오. 

2. 게이트를 포함하는 작업에서 게이트의 이름을 클릭하십시오.

3. 로그 보기에서 `여기서 {{site.data.keyword.DRA_short}} 보고서 확인` 메시지를 찾아서 링크를 클릭하여 보고서를 여십시오.






