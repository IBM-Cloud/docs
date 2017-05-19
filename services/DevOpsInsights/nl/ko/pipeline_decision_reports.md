---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 대시보드 및 보고서 보기
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}}에서는 프로젝트에 수행 가능한 조치에 대한 정보를 자세히 제공합니다.
{:shortdesc}

## {{site.data.keyword.DRA_short}} 대시보드    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}}에서는 Bluemix 조직 전반의 성능 정보를 표시하는 대시보드를 제공합니다. 이 대시보드를 보려면 {{site.data.keyword.DRA_short}}를 열고 **빌드 검증** 또는 **배치 검증**을 클릭하십시오.

이러한 대시보드는 파이프라인의 {{site.data.keyword.DRA_short}} 테스트 작업에 있는 최신 정보로 자동으로 채워집니다. 자세한 정보를 보려면 대시보드 내에 있는 요소를 클릭하십시오. 

### 빌드의 핵심성과지표(KPI)    
{: #DI_key_performance_indicators}

**빌드 검증** 페이지에는 선택된 개발 분기의 상태 정보가 있는 세 개의 그래프가 있습니다. 

<table>
<thead>
<tr>
<th>그래프</th>
<th>설명</th>
</tr>
</thead>

<tbody>
<tr>
<td>최신 빌드</td>
<td>완료된 최신 빌드 수를 최신 전체 빌드 수에 비교한 그래프입니다. </td>
</tr>
<tr>
<td>테스트</td>
<td>패스된 테스트 수를 총 테스트 수에 비교한 그래프입니다. </td>
</tr>
<tr>
<td>코드 적용 범위</td>
<td>테스트에서 호출한 코드 명령문과 함수의 백분율입니다. </td>
</tr>
</tbody></table>

## 의사결정 보고서 보기    
{: #DI_decision_reports}

파이프라인을 실행한 후에 {{site.data.keyword.DRA_short}}를 시작하여 해당 테스트 결과를 수집하고 분석하여 기준선을 설정합니다. 모든 후속 실행 데이터를 수집하여 이전 결과와 비교합니다. 의사결정 게이트는 이 데이터를 사용하여 배치 중지 시점을 결정합니다.  

파이프라인의 게이트에 대한 의사결정 보고서를 보려면 다음 단계를 수행하십시오. 

   1. 검사할 게이트가 포함된 단계에서 **로그 및 히스토리 보기**를 클릭하십시오. 

   2. 단계의 작업 창에서 게이트 이름을 클릭하십시오. 

   3. 로그 보기에서 '여기서 {{site.data.keyword.DRA_short}} 보고서 확인' 메시지를 찾아서 제공된 링크를 클릭하여 보고서를 여십시오. 
