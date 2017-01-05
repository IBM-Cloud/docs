---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.DRA_short}}를 {{site.data.keyword.deliverypipeline}}과 통합
{: #toolchain_configure_pipeline}

도구 체인에 {{site.data.keyword.DRA_full}}를 추가하고 이를 모니터하는 정책을 정의한 후에는 {{site.data.keyword.DRA_short}}를 파이프라인과 통합해야 합니다.
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## {{site.data.keyword.DRA_short}}의 파이프라인 단계 준비
{: #toolchain_pipeline_props}

빌드 또는 배치 작업이 포함된 각 파이프라인 단계에서 여러 환경 특성을 작성해야 합니다. 

1. **단계 구성**을 클릭한 다음 **구성 단계**를 클릭하십시오. 

2. **환경 특성**을 클릭하십시오.

3. 다음 세 개의 텍스트 특성을 추가한 다음 단계의 변경사항을 저장하십시오.

<table><thead>
<tr>
<th>환경 특성</th>
<th>설명</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>{{site.data.keyword.DRA_short}} 대시보드에 표시되는 앱 이름입니다. </td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>앱을 실행 중인 환경의 이름입니다. 이 특성은 {{site.data.keyword.DRA_short}} 대시보드에서 앱을 분류하는 데 사용합니다. </td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>{{site.data.keyword.DRA_short}} 대시보드의 표시와 같이 빌드에 추가되는 접두부입니다. </td>
</tr>
</tbody></table>


## {{site.data.keyword.DRA_short}}의 테스트 작업 업데이트
{: #toolchain_pipeline_upload}

시작하려면 테스트 작업에서 설정 정보를 검색하십시오. 

1. 테스트 작업이 포함된 단계에서 **단계 구성** 아이콘 ![파이프라인 단계 구성 아이콘](images/pipeline-stage-configuration-icon.png)을 클릭하십시오. **구성 단계**를 클릭하십시오.
2. 작업을 작성하십시오. 작업 유형에 **테스트**를 선택하십시오.
3. 단순 테스터 유형을 사용하는 테스트 작업을 선택하고 **테스트 명령** 및 **작업 디렉토리** 필드의 정보를 편집기에 복사하십시오. 나중에 이 정보가 필요합니다. 
4. 동일한 단순 테스트 작업에서 **고급 테스터**를 선택하여 테스터 유형을 변경하십시오. 
5. **테스트 명령** 필드에 단순 테스트 작업의 **테스트 명령** 필드에서 복사한 명령을 붙여 넣으십시오. 
6. **작업 디렉토리** 필드에 단순 테스트 작업의 **작업 디렉토리** 필드에서 복사한 경로를 붙여 넣으십시오. 
7. 나머지 필드를 작성하여 특정 테스트 유형의 테스트 결과를 업로드하십시오. 같은 작업에서 두 번째 테스트 유형의 결과를 업로드하려면 *추가* 접두부가 있는 필드도 작성하십시오. 

 * 메트릭 유형
 * 형식
 * 결과 파일 위치
8. **저장**을 클릭하여 파이프라인을 리턴하십시오. 

**메트릭 유형** 및 **결과 파일 위치** 필드의 값은 올바른 형식을 따라야 합니다. 

<table><thead>
<tr>
<th>메트릭 유형</th>
<th>지원되는 형식</th>
</tr>
</thead><tbody>
<tr>
<td>기능 검증 테스트</td>
<td>Mocha, JUnit</td>
</tr>
<tr>
<td>단위 테스트</td>
<td>Mocha, JUnit, Karma/Mocha</td>
</tr>
<tr>
<td>코드 적용 범위</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

*그림 1*은 단위 테스트를 실행하여 결과를 Mocha 형식으로 업로드한 다음 코드 적용 범위 결과를 Istanbul 형식으로 업로드하는 테스트 작업을 보여줍니다. 

![배치 위험성 분석 업로드 작업](images/DRA_upload_job.png)
*그림 1. DevOps Analytics에 결과 업로드*

## 파이프라인에 {{site.data.keyword.DRA_short}} 게이트 정의
{: #toolchain_pipeline_gates}

{{site.data.keyword.DRA_short}} 게이트는 테스트 결과가 정의된 정책을 준수하는지 확인합니다. 정책을 준수하지 못하는 경우 {{site.data.keyword.DRA_short}} 게이트가 실패합니다. 일반적으로 게이트는 파이프라인의 각 단계 끝에 있습니다. 이 위치는 정책에 대해 빌드 품질을 점검하여 하나의 환경에서 다른 환경으로 승격하기에 안전한지 확인하는 데 적합합니다. 그러나 게이트는 특정 기준을 점검할 파이프라인의 임의 위치에 배치할 수 있습니다. 

1. 단계에서 **단계 구성** 아이콘 ![파이프라인 단계 구성 아이콘](images/pipeline-stage-configuration-icon.png)을 클릭한 다음 **구성 단계**를 클릭하십시오.
2. **작업 추가**를 클릭하십시오. 작업 유형에 **테스트**를 선택하십시오.
3. 새 작업의 이름을 입력하십시오(예: *게이트(단위 테스트)*).
4. 테스터 유형으로 **{{site.data.keyword.DRA_short}} 게이트**를 선택하십시오.
5. 환경 이름을 지정하십시오. 이 값이 [환경 특성](#toolchain_pipeline_props)에 정의된 값과 일치하는지 확인하십시오.
6. 이 단계에서 점검할 정책 이름을 정의하십시오. 

 이 이름은 정의된 정책 이름 중 하나와 정확히 일치해야 합니다. 같은 {{site.data.keyword.Bluemix_notm}} 조직에 정의된 정책만 도구 체인으로 지정할 수 있습니다. 

7. 선택사항: 게이트 기능을 권장 모드로 작성하려면 **작업 실패 시 이 단계 실행 중지** 선택란을 선택 취소하십시오. 권장 모드에서는 {{site.data.keyword.DRA_short}}가 게이트에서 동일한 정책 분석을 완료하고 보고서를 생성하지만 실패하는 경우 파이프라인이 중지되지 않습니다. 
8. **저장**을 클릭하여 파이프라인을 리턴하십시오. 
9. 이러한 단계를 반복하여 모든 {{site.data.keyword.DRA_short}} 정책의 게이트를 설정하십시오. 

![배치 위험성 분석 Mocha 작업](images/DRA_gate_job.png)
*그림 2. DevOps Analytics 게이트*

파이프라인이 구성되면 {{site.data.keyword.DRA_short}}를 사용하십시오. 지시사항은 [Delivery Pipeline 실행](./pipeline_decision_reports.html#toolchain_reports)을 참조하십시오.
