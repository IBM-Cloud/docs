---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Continuous Delivery 파이프라인과 통합

도구 체인에 {{site.data.keyword.DRA_short}}를 추가하고 모니터하는 정책을 정의한 다음 {{site.data.keyword.deliverypipeline}}과 통합하십시오. 파이프라인에 대한 자세한 정보는 [공식 문서](/docs/services/ContinuousDelivery/pipeline_working.html)를 참조하십시오.

## 파이프라인 단계 준비
{: #integrate_pipeline}

Deployment Risk가 프로젝트를 분석하려면 파이프라인에서 스테이징 및 프로덕션 단계를 정의해야 합니다. **환경 특성**에 있는 각 단계의 구성 메뉴 ![파이프라인 단계 구성 아이콘](images/pipeline-stage-configuration-icon.png)에 있는 텍스트 환경 특성을 사용하여 단계를 정의합니다.

1. 스테이징 단계에서 `LOGICAL_ENV_NAME` 특성을 `STAGING`으로 설정하십시오. 

2. 프로덕션 단계에서 `LOGICAL_ENV_NAME` 특성을 `PRODUCTION`으로 설정하십시오. 

앱을 빌드하거나 배치하는 단계에 다음 특성도 추가할 수 있습니다.

* `LOGICAL_APP_NAME` - 대시보드에 앱의 이름을 정의합니다.
* `BUILD_PREFIX` - 단계의 빌드에 접두어로 추가된 텍스트를 정의합니다. 이 텍스트도 대시보드에 표시됩니다. 

## 테스트 작업 추가
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

## 게이트 정의
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

파이프라인이 구성되면 {{site.data.keyword.DRA_short}}를 사용하십시오.  
