{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.autoscaling}} 서비스 시작하기
{: #autoscaling}

*마지막 업데이트 날짜: 2015년 1월 18일*

{{site.data.keyword.Bluemix_notm}}에서 자동으로 애플리케이션
용량을 관리할 수 있습니다. {{site.data.keyword.autoscalingfull}} 서비스를 사용하여 애플리케이션의
계산 성능을 자동으로 높이거나 낮출 수 있습니다. 애플리케이션 인스턴스의 수는 사용자가 정의한
{{site.data.keyword.autoscaling}} 정책에 따라 동적으로 조정됩니다. {:shortdesc} 

## {{site.data.keyword.Bluemix_notm}}에서 {{site.data.keyword.autoscaling}} 서비스 사용
{: #as-service}

{{site.data.keyword.autoscaling}} 서비스를 사용하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 *서비스 또는 API 추가*를 클릭한 다음 서비스 카탈로그의 DevOps 섹션에서 {{site.data.keyword.autoscaling}} 서비스를 선택하십시오. {{site.data.keyword.autoscaling}} 서비스의 개요를 제공하는 새 창이 표시됩니다.
2. {{site.data.keyword.autoscaling}} 서비스를 바인딩할 애플리케이션을 선택하고
*작성*을 클릭하십시오. <br/>
*참고:* 하나의 애플리케이션에는 하나의 {{site.data.keyword.autoscaling}} 서비스만 바인드할 수 있습니다. 이 애플리케이션이 이미 다른 {{site.data.keyword.autoscaling}} 서비스에 바인드되어 있는 경우
						이 단계에서 애플리케이션을 선택하지 마십시오. 그렇지 않으면, CWSCV2004E 오류가 발생합니다.<br/>애플리케이션 다시 스테이징 창이 표시됩니다.
3. 추가한 새 {{site.data.keyword.autoscaling}} 서비스를 사용하기 전에 애플리케이션 다시 스테이징 창에서 *다시 스테이징*을 클릭하여 애플리케이션을 다시 스테이징하십시오. 애플리케이션 다시 스테이징이 완료된 후
애플리케이션에 대한 {{site.data.keyword.autoscaling}} 서비스 구성을 시작할 수 있습니다.
4. 애플리케이션의 {{site.data.keyword.autoscaling}}을
구성하려면 {{site.data.keyword.Bluemix_notm}} 사용자
인터페이스에서 {{site.data.keyword.autoscaling}} 서비스가 바인드된 애플리케이션을 클릭하십시오.
5. 대시보드의 서비스 섹션에서
*Auto-Scaling* 아이콘을 클릭하십시오.
6. 완료하지 못한 경우 *{{site.data.keyword.autoscaling}} 정책 작성*을 클릭하여 애플리케이션에 대해 {{site.data.keyword.autoscaling}} 정책을 정의하십시오.

이제 {{site.data.keyword.autoscaling}} 정책을 구성하거나 메트릭 통계를 보거나
애플리케이션에 대한 스케일링 히스토리를 볼 수 있습니다.
<dl>
<dt>정책 구성</dt>
<dd>이 섹션은 특정 스케일링 활동을 트리거하는 조건을 지정하기 위해 스케일링 규칙을 작성하거나 편집하는 데 사용합니다.<ul>
<li> Liberty for Java™ 애플리케이션의 경우, JVM 힙, 메모리 및 처리량과 관련된 스케일링 규칙을 정의할 수 있습니다.
<li> Node.js 애플리케이션의 경우, 메모리와 관련된 스케일링 규칙을 정의할 수 있습니다. <li> Ruby 애플리케이션의 경우, 메모리와 관련된 스케일링 규칙을
정의할 수 있습니다. </ul>
*참고:* 둘 이상의 메트릭 유형에 여러 개의 스케일링 규칙을 정의할 수 있습니다. 그러나 {{site.data.keyword.autoscaling}} 서비스는 스케일링 정책 간의
충돌을 발견하지 않습니다.
스케일링 정책을 정의하는 경우, 여러 스케일링 규칙이 서로 충돌하지 않는지 확인해야 합니다. 그렇지 않으면, 애플리케이션이 스케일 축소했다가 1분 이내에 바로 스케일 확장하여 총 인스턴스 수의 변동이 클 수 있습니다.<br/><br/>
최대 시간과 여유 시간 동안 애플리케이션의 워크로드가 대폭 변경되는 경우, 서로 다른 기간에 각기 다른 스케일링 요구사항을 처리하도록 스케일링 스케줄을 작성합니다. 스케일 축소 및 스케일 확장 조치를 트리거하도록 동적 스케일링 규칙이 스케줄에 적용되는 동안 스케줄에 지정된 최소 인스턴스 수 매개변수를 사용하여 애플리케이션 인스턴스 수의 기준선을 정의하십시오. </dd>
<dt>메트릭 통계</dt>
<dd>애플리케이션 인스턴스에 대한 메트릭 통계를 표시합니다.
평균 통계를 확인하고 특정 인스턴스를 선택하여
해당 인스턴스의 통계를 확인할 수 있습니다. </dd>
<dt>스케일링 히스토리</dt>
<dd>애플리케이션의 스케일링 히스토리를 표시합니다.<ul>
<li> 지난 주:
지난 주의 스케일링 히스토리를 표시합니다.<li> 지난 달:
지난 달의 스케일링 히스토리를 표시합니다.<li> 사용자 정의 범위:
기간을 설정할 수 있습니다.</ul>
*참고:* 히스토리 레코드를 필터링하려면 스케일링 상태 또는 스케일 축소/확장을 선택하면 됩니다.</dd>
</dl>


## {{site.data.keyword.autoscaling}} 서비스의 정책 필드
{: #policyfields}

| 필드 이름  | 설명 |
|-------------|----------------------|
|*허용되는 최대 인스턴스
개수* |	시작할 수 있는 애플리케이션 인스턴스의
최대 수입니다. 현재 애플리케이션 인스턴스 수가 이 값과
같으면 {{site.data.keyword.autoscaling}} 서비스는 애플리케이션의 스케일을 더 이상 확장하지 않습니다. 기본 최소 인스턴스 수는 시작할 수 있는 애플리케이션 인스턴스의 최소 수입니다. 인스턴스 수가 이 값과
같으면 {{site.data.keyword.autoscaling}} 서비스는 애플리케이션의 스케일을 더 이상 축소하지 않습니다.  |
| *메트릭 유형*	| 	지원되고 모니터링 가능한
메트릭 유형입니다. 자세한 정보는 표 2를 참조하십시오. |
| *스케일 확장* | 	스케일 확장 조치가 트리거될 때 스케일 확장 조치를 트리거하는 임계값 및 인스턴스 증가 개수를 지정합니다.  |
| *스케일 축소* |	스케일 축소 조치가 트리거될 때 스케일 축소 조치를 트리거하는 임계값 및 인스턴스 감소 개수를 지정합니다.  |
| *통계 기간* |	받은 메트릭 값이 유효하게 인식되는
과거 기간입니다. 시간소인이 이 기간에
속하는 경우에만 메트릭 값이 유효합니다. 통계 기간(Statistic Window) 매개변수는 초 단위를 사용합니다. |
| *위반 기간*	| 스케일링 조치가 트리거될 수 있는
과거 기간입니다. 수집된 메트릭 값이 상한
임계값보다 높거나 하한 임계값(지정된 시간보다 더 긴 값)보다 낮은 경우
스케일링 조치가 트리거됩니다. 위반 기간(Breach Duration) 매개변수는 초 단위를 사용합니다. |
| *스케일 축소의 쿨다운 기간* | 스케일 축소 조치가 발생한 후 스케일 축소 쿨다운 기간 매개변수에 지정된 기간 동안 다른 스케일링 요청이 무시됩니다. 이 매개변수는 초 단위를 사용합니다. |
| *스케일 확장 쿨다운 기간*	| 스케일 확장 조치가 발생한 후 스케일 확장 쿨다운 기간 매개변수에 지정된 기간 동안 다른 스케일링 요청이 무시됩니다. 이 매개변수는 초 단위를 사용합니다. |
| *시간대*	| 스케줄이 적용되는 시간대입니다. |
| *시작 시간*  |	순환 스케줄의 시작 시간입니다. |
| *종료 시간*    |	순환 스케줄의 종료 시간입니다.	|
| *반복 날짜*	|	순환 스케줄이 적용되는 요일입니다.  |
| *최소 인스턴스 개수* |	스케줄의 지정된 기간 동안 애플리케이션에 대해
시작할 수 있는 최소 인스턴스 수입니다. |
| *시작 날짜 및 시간* |	특정 날짜에 설정된 스케줄의 시작 날짜 및 시간입니다. |
| *종료 날짜 및 시간* |	특정 날짜에 설정된 스케줄의 종료 날짜 및 시간입니다.	|

표 1. 스케일링 정책의 정책 필드

| 메트릭 이름 | 설명 | 지원되는
애플리케이션 유형 |
|-------------|----------------------| ------------------- |
| *JVM 힙* |	JVM 힙 메모리의 이용률입니다.	| Liberty for Java |
| *메모리*   |	메모리의 이용률입니다.	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *처리량* | 초당 처리되는
요청의 수입니다. | Liberty for Java |
| *응답 시간* |	처리된 요청의
응답 시간입니다.	| Liberty for Java |

표 2. 지원되는 메트릭 이름

## 오류 메시지
{: #errmsgs}
이 절에는 {{site.data.keyword.autoscaling}} 서비스를 통해 생성되는 경고 및 오류 메시지 목록이 표시됩니다.
 
### CWSCV2004E 다른 {{site.data.keyword.autoscaling}} 서비스가
이미 애플리케이션에 바인드되어 있습니다. 
**하나의 애플리케이션에는 하나의 {{site.data.keyword.autoscaling}} 서비스만 바인드할 수 있습니다. 이 오류는 이미 다른 {{site.data.keyword.autoscaling}} 서비스에 바인드된 애플리케이션에 {{site.data.keyword.autoscaling}} 서비스를 바인드하려는 경우 발생합니다.**

다른 {{site.data.keyword.autoscaling}} 서비스가 바인드되어 있지 않은 다른 애플리케이션을 선택하거나
대상 {{site.data.keyword.autoscaling}} 서비스를 이 애플리케이션에 바인드하십시오. 그 외 다른 경우에 이 오류가 발생하면 IBM 지원 센터에 문의하십시오.

### CWSCV6001E API 서버가 API에 대한 입력 JSON 문자열을 구문 분석할 수 없음: {0}
**입력 JSON 문자열을 구문 분석할 때 문제점이 발생합니다. **

API 문서에서 입력 JSON을 확인하고 오류를 정정하십시오. 

### CWSCV6002E API 서버가 API에 대한 출력 JSON 문자열을 구문 분석할 수 없음: {0}
**입력 JSON 문자열을 구문 분석할 때 문제점이 발생합니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 

### CWSCV6003E API에 대한 입력 JSON({1})에서 입력 JSON 문자열 형식 오류 발생({0})
**입력 JSON 문자열을 구문 분석할 때 형식 오류가 발견되었습니다. **

API 문서에서 입력 JSON을 확인하고 오류를 정정하십시오. 

### CWSCV6004E API에 대한 출력 JSON({1})에서 출력 JSON 문자열 형식 오류 발생({0})
**출력 JSON 문자열을 구문 분석할 때 형식 오류가 발견되었습니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 

### CWSCV6005E {0} 중에 내부 서버 오류 발생
**요청을 처리하는 중에 내부 서버 오류가 발생합니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 

### CWSCV6006E CloudFoundry API 호출 실패: {0}
**CloudFoundry API를 호출할 때 오류가 발생했습니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 

### CWSCV6007E 애플리케이션을 찾을 수 없음: {0}
**애플리케이션을 찾을 수 없습니다. **

자세한 내용은 애플리케이션 정보를 확인하십시오. 

### CWSCV6008E {0} 애플리케이션 정보 검색 중 다음 오류 발생: {1} 
**오류가 발생하여 애플리케이션 정보 검색에 실패했습니다. **

자세한 내용은 애플리케이션 정보를 확인하십시오. 

### CWSCV6009E {1} 앱에 대한 {0} 서비스를 찾을 수 없음
**이 애플리케이션에 대한 서비스를 찾을 수 없습니다. **

자세한 내용은 이 애플리케이션의 서비스 바인딩을 확인하십시오. 

### CWSCV6010E {0} 앱에 대한 정책을 찾을 수 없음
**이 애플리케이션에 대한 정책을 찾을 수 없습니다. **

자세한 내용은 애플리케이션 구성을 확인하십시오. 

### CWSCV6011E {0} 중 내부 인증 실패
**내부 인증에 실패했습니다. **

자세한 정보는 클라우드 관리자에게 문의하십시오. 


# rellinks
## 샘플
* [Tutorial: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## SDK
* [IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}의 Rest API](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window}

## 일반
* [{{site.data.keyword.Bluemix_notm}} 가격 책정 시트](https://console.{DomainName}/pricing/){:new_window}
* [{{site.data.keyword.Bluemix_notm}} 필수 소프트웨어](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}

