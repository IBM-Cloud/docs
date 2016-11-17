---

copyright:
  years: 2016
lastupdated: "2016-06-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# API 집계
{: #api_aggregation}

일부 {{site.data.keyword.weather_short}} API를 집계할 수 있습니다. 집계를 사용하여 둘 이상의 단위 API 호출을 단일 HTTP 요청으로
결합할 수 있습니다.
{: shortdesc}

단위 API 호출에서는 집계의 별칭을 정의하는 API를 참조합니다. 집계에 대해
별칭이 사용 가능한 경우 각 API 사용자 문서의 URL 형식 섹션에 집계 이름의
별칭이 포함됩니다. 예를 들어, 표준 일별 예보 API에는 집계된 요청의 일부로서
10일 동안의 일별 예보를 검색하는 데 사용할 수 있는 `v2fcstdaily10` 집계의
별칭이 있습니다.

집계에는 다음과 같은 제한사항이 있습니다.

* 전체 집계에 대해 압축이 풀린 총 응답 크기는 1MB 미만이어야
합니다.
* URL의 길이(프로토콜, 호스트 이름, 경로 및 쿼리 문자열 포함)는
대략 4,096자 미만이어야 합니다.
* 최대 10개의 단위 API를 집계할 수 있습니다.

**참고:** 요청 또는 응답이 이 제한사항을 위반하면,
500 HTTP 상태 코드의 오류 응답을 수신합니다(다른 상태 코드가 리턴될 수 있지만,
일반적으로는 500 또는 502임). 

## 집계 API URL
집계 API URL은 `/v2/aggregate/`로 시작하며
세미콜론으로 분리된 별칭이 뒤에 나옵니다.
예를 들어, 현재 관측(`v2obscurrent`)에서
10일 간의 일별 예보 API (`v2fcstdaily10`)를 집계하려면 다음 형식을 사용하십시오. 

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## 단위 API와 집계에 대한 쿼리 매개변수 규칙
쿼리 매개변수가 모든 요청에 대해
필요합니다. 집계에 대한 쿼리 매개변수는
몇 가지 추가 규칙과 함께 단위 API 호출과
동일한 방식으로 전달됩니다. 다음 절에서는
이를 적용하여 다양한 집계를 구성하는 방법을 설명합니다.

### 모든 단위 API에 적용되는 쿼리 매개변수 지정

가장 단순한 집계 형식은
쿼리 매개변수가 모든 단위 API에 적용되는 경우입니다. 이 경우에 쿼리 매개변수의 표준 형식은
`?param1=value1&amp;param2=value2`입니다. 

다음 예는
`geocode=31.44,84.33&amp;language=en&amp;units=e`를
`v2fcstdaily10` 및 `v2obscurrent` 단위 API에 대한
요청에 적용합니다. 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### 쿼리 매개변수를 받는 단위 API 지정 

특정 단위 API에 대한 매개변수를 지정해야 하는 경우, 쿼리 매개변수는
`?R1.param1=value1&amp;R2.param2=value2`의 위치 표기법을
사용할 수 있습니다. 이 형식은 첫 번째 단위 API에는 `param1`을 사용하며
두 번째 단위 API에는 `param2`를 사용합니다. 

다음 예는
`geocode=31.44,84.33&amp;language=en&amp;units=e`를
`v2fcstdaily10`에 적용하며, `geocode=44.44,50.23&amp;language=en&amp;units=e`를
`v2obscurrent`에 적용합니다. 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### 특정 단위 API에 대해 쿼리 매개변수 그룹화 

`?R1,R2.param1=value1&amp;param2=value2`의 쉼표로 구분된 형식으로서
위치 표기법을 사용하여 매개변수를 그룹화할 수 있습니다.
이 형식은 첫 번째와 두 번째 단위 API에는 `param1`을 사용하며
모든 단위 API에는 `param2`를 사용합니다. 

다음 예는 `geocode=34.06,84.21&amp;language=enUS&amp;units=e`를
`v2fcstdaily10` 및 `v2obscurrent`에 적용합니다. 
이는 `geocode= 33.06,81.11&amp;language=enUS&amp;units=e`를 `v2loc`에 적용합니다. 

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### 여러 가지 방식으로 동일한 리소스 요청

예를 들면, 다른 언어로 또는 다른 측정 단위를 사용하여
동일한 리소스를 여러 가지 방식으로 요청할 수 있습니다. 이 형식을 사용하면
단위 API가 요청에서 반복될 수 있으며(`/v2/aggregate/v2fcstdaily10;v2fcstdaily10`),
매개변수의 위치 표기법을 사용하여 어떤 API를 어떤 방법으로 요청하는지
표시할 수 있습니다(`?R1.param1=value1&amp;R2.param1=value2`). 이 경우 사용자는
서로 다른 방식으로 형식화되거나 변환된 동일한 리소스를 받습니다.

다음 예는 `geocode=31.44,84.33&amp;language=en&amp;units=e`를
첫 번째 `v2fcstdaily10`에 적용하며, `geocode=31.44,84.33&amp;language=fr&amp;units=m`을
두 번째 `v2fcstdaily10`에 적용합니다. 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

다음 예는 동일한 데이터에 대해 여러 위치를 검색하기 위해
`geocode=31.44,84.33&amp;language=en&amp;units=e`를
첫 번째 `v2fcstdaily10`에 적용하며,
`geocode=33.54,85.43&amp;language=en&amp;units=e`를
두 번째 `v2fcstdaily10`에 적용합니다. 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




