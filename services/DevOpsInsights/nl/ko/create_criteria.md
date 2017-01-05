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

# 정책 정의
{: #criteria}

{{site.data.keyword.DRA_short}} 제품으로 애플리케이션 정책을 쉽게 정의할 수 있습니다. 시작하려면 다음 단계를 수행하십시오.
{:shortdesc}

1. 측면 메뉴에서 **정책**을 클릭하십시오. 

2. **정책 작성(+)**을 클릭한 다음 새 정책의 이름과 설명을 입력하십시오. 

3. **다음**을 클릭하십시오. 

4. 정책에 규칙을 하나 이상 추가하십시오. 
  1. **규칙 작성(+)**을 클릭하십시오.
  2. 규칙 유형을 선택하십시오. 
  3. 규칙의 세부사항과 조건을 입력하십시오. 
  4. **저장**을 클릭하십시오. 

5. 정책에 규칙을 추가한 다음 **완료**를 클릭하십시오.

정책은 {{site.data.keyword.DRA_short}}가 추가된 {{site.data.keyword.Bluemix_notm}} 조직에 작성됩니다. 동일 조직의 모든 애플리케이션에서 정책을 사용할 수 있습니다. 

{{site.data.keyword.DRA_short}}는 이러한 유형의 메트릭과 형식을 지원합니다. 

* 기능 검증 테스트(Mocha, JUnit)
* 단위 테스트(Mocha, JUnit, Karma/Mocha)
* 코드 적용 범위(Istanbul을 JSON 요약 보고서 형식으로 사용한 Blanket.js)

{{site.data.keyword.DRA_short}}는 Selenium과 Jasmine 테스트도 지원합니다. 이러한 테스트는 공식 지원 도구(예: JUnit, xUnit, Mocha)에 포함되어 있어야 합니다. {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}}, Selenium을 함께 사용하는 방법을 보려면 [Delivery Pipeline의 명령행에서 Selenium 테스트 실행](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/)의 내용을 참조하십시오. 

테스트 케이스가 있는 항목의 경우 중요 테스트 케이스를 지정할 수 있으며 이는 허용 가능한 백분율인지와 관계 없이 패스해야 하는 테스트입니다. 중요 테스트 케이스 이름은 테스트 케이스의 `full title` 속성과 일치해야 합니다.     
* Karma/Mocha 테스트의 경우 `describe()` 및 `it()` 설명 문자열이 공백과 함께 링크됩니다. 
* JUnit 테스트의 경우, 패키지 이름, 클래스 이름, 기능 이름이 공백과 함께 링크됩니다.     

Sauce Labs 통합을 파이프라인에 추가하여 Sauce Labs을 {{site.data.keyword.DRA_short}}와 함께 사용할 수 있습니다. 그러면 `SAUCE_USERNAME` 및 `SAUCE_ACCESS_KEY` 환경 변수를 신임 정보로 사용하여 Selenium 테스트에 통합할 수 있습니다. 

실행 후 로그에서 전체 테스트의 전체 제목을 볼 수 있습니다.   

참고:
* {{site.data.keyword.DRA_short}}는 전체 제목 안에 하이픈이 포함된 중요 테스트를 지원하지 않습니다.     
* 조직 이름을 변경하는 경우, 이전 이름과 연관된 정책을 다시 작성해야 합니다. 이름 변경 전에 생성된 의사결정 보고서에 대한 액세스는 유실됩니다. 

## 기능 검증 테스트 규칙 작성
{: #criteria_fvt}

1. 설명을 입력하고 형식을 선택하십시오. 

2. 성공한 것으로 선언하기 위해 패스해야 하는 테스트 케이스의 백분율을 지정하십시오. 

3. 중요한 테스트 케이스를 정의하십시오. 

4. 테스트 케이스 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오. 

5. **저장**을 클릭하십시오. 


## 단위 테스트 규칙 작성
{: #criteria_ut}

1. 설명을 입력하고 형식을 선택하십시오. 

2. 성공한 것으로 선언하기 위해 패스해야 하는 테스트 케이스의 백분율을 지정하십시오. 

3. 중요한 테스트 케이스를 정의하십시오. 

4. 테스트 케이스 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오. 

5. **저장**을 클릭하십시오. 


## 코드 적용 범위 규칙 작성
{: #criteria_codecoverage}

1. 설명을 입력하고 형식을 선택하십시오. 

2. 성공한 것으로 선언하는 데 필요한 코드 적용 범위의 백분율을 지정하십시오. 

3. 코드 적용 범위 회귀를 모니터하려면 **테스트 케이스 회귀 모니터** 선택란을 선택하십시오. 

4. **저장**을 클릭하십시오. 
