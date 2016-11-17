---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.weather_short}} REST API 사용
{: #rest_apis}

[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}를 사용하여
기상 데이터를 검색할 수 있습니다. API 연산을 테스트하고 즉시 결과를 봄으로써 신속하게 애플리케이션을
빌드하는 데 도움을 받을 수 있습니다.
{: shortdesc}

각 연산에 대한 세부사항을 보려면 참조 문서에서 **연산 나열**을 클릭하십시오.
매개변수를 지정하고 **사용해 보십시오!**를
클릭하면 신임 정보를 제공하라는 요청을 받게 됩니다. `VCAP_SERVICES` 환경 변수의 사용자 이름과 비밀번호를 제공해야 합니다.
애플리케이션을 열고 목차에서 **환경 변수**를 클릭하면 이 정보를 찾을 수 있습니다.

**참고:** 각 지역은 독립적입니다. 한 지역에서 사용자에게
프로비저닝된 서비스 신임 정보를 사용하여 다른 지역의 서비스에 대해 인증할 수 없습니다.
적절한 신임 정보를 입력하지 않으면 응답 본문에 *Unauthorized* 메시지가 포함됩니다.

REST API를 사용하면 위치정보를 위도 및 경도 좌표로 제공하여 기상 데이터를 검색할 수 있습니다.
사용할 수 있는 API는 다음과 같습니다.

|**API**                                  |**설명**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |제공하는 형식에 따라 위치정보에 대해 그 다음 48시간 동안의 시간별 기상 예보를 반환합니다. `geocode/{latitude}/{longitude}` 또는 `location/{locationId}`를 제공할 수 있습니다. 시간별 예보 데이터에는 각 위치마다 최대 48개의 시간별 예보가 포함될 수 있습니다. 새 데이터를 받은 위치에 대해서는 이전의 시간별 예보를 모두 버려야 합니다. |
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |제공하는 형식에 따라 위치정보에 대해 3, 5, 7 또는 10일 동안의 일별 기상 예보를 반환합니다. 검색될 일 수는 `3day`, `5day`, `7day` 또는 `10day`의 형식으로 지정됩니다. `geocode/{latitude}/{longitude}` 또는 `location/{locationId}`를 제공할 수 있습니다. 각 일별 예보에는 주간 예보, 야간 예보 및 24시간 예보가 포함될 수 있습니다. 이들 세그먼트는 JSON 응답에서 별도 오브젝트입니다. 일간 예보의 주간 예보 데이터는 3:00 PM 현지 시간 이후에는 더 이상 사용될 수 없습니다. 현지 시간 오후 3시에는 애플리케이션이 주간 예보를 더 이상 표시하지 않아야 합니다.|
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|제공하는 형식에 따라 위치정보에 대해 3, 5, 7 또는 10일 동안 6시간 기간으로 일별 기상 예보를 반환합니다. 검색될 일 수는 `3day`, `5day`, `7day` 또는 `10day`의 형식으로 지정됩니다. `geocode/{latitude}/{longitude}` 또는 `location/{locationId}`를 제공할 수 있습니다. 각 일별 예보에는 오전, 오후, 저녁 및 심야 예보가 포함될 수 있습니다. 이들 세그먼트는 JSON 응답에서 별도 오브젝트입니다. |
|`GET /v1/{geocode or location ID}/observations.json`              |위치정보에 대한 현재 기상 상태를 리턴합니다. `geocode/{latitude}/{longitude}` 또는 `location/{locationId}`를 제공할 수 있습니다. 이 최신 관측치는 특정 리포팅 스테이션에서 최대 10분 동안 데이터베이스에 보관되며 스테이션마다 24시간 관측됩니다. 최신 관측 데이터는 계속하여 업데이트되며 관측 날짜/시간 스탬프를 기반으로 선입선출(FIFO) 방법론(최신 관측으로 데이터를 순환하고 가장 오래된 관측을 아카이브 스토리지로 이동함)을 사용하여 교체됩니다.|
|`GET /v1/{geocode or location ID}/observations/timeseries.json`   |위치정보에 대해 현재 관측 및 현재 날짜와 시간에서 최대 24시간까지의 과거 관측을 모두 리턴합니다. `geocode/{latitude}/{longitude}` 또는 `location/{locationId}`를 제공할 수 있습니다. 기상 관측은 전세계에 배치된 실제 디바이스와 현재 기상 관측으로부터 수집됩니다.|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |NWS(National Weather Service), Environment Canada 및 MeteoAlarm(유럽)에서 발행되고 49개 언어로 이벤트 설명, 국가 이름 및 경보 헤드라인의 번역을 포함하는 기상 감시, 경고, 명령문 및 보안 권고문을 반환합니다. `geocode/{latitude}/{longitude}`, `country/{countrycode}`, `country/{countrycode}/state/{statecode}`/ 또는 `country/{countrycode}/area/{areaid}`를 제공할 수 있습니다.|
|`GET /v1/alert/{detail_key}/details.json`                         |NWS(National Weather Service), Environment Canada 및 MeteoAlarm(유럽)에서 발행된 기상 감시, 경고, 명령문 및 보안 권고문을 반환합니다. 세부사항에는 지정된 영역에 대해 정부 기상 당국에서 발행된 경보에 대한 자세한 정보와 49개 언어로 이벤트 설명, 국가 이름 및 경보 헤드라인의 번역이 포함됩니다.|
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |10 - 30년 이상의 기간에서 National Weather Service 관측소의 일별 연감 정보(미국만)를 반환합니다. 이 정보는 NCDC(National Climatic Data Center)에서 수집되어 제공됩니다. `geocode/{latitude}/{longitude}` 또는 `location/{PostalLocationId}`를 제공할 수 있습니다.|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |10 - 30년 이상의 기간에서 National Weather Service 관측소의 월별 연감 정보(미국만)를 반환합니다. 이 정보는 NCDC(National Climatic Data Center)에서 수집되어 제공됩니다. `geocode/{latitude}/{longitude}` 또는 `location/{PostalLocationId}`를 제공할 수 있습니다.|
|`GET /v3/location/{search or point}`                                  |요청에 맞는 위치 세트를 검색하기 위해 위치 이름 또는 지오코드(위도 및 경도)를 검색하는 기능을 제공합니다. 위치 서비스는 구/군/시 이름 또는 우편번호별 검색을 지원합니다.|
*표 1. {{site.data.keyword.weather_short}} API 요약*

## 일별 및 일중 예보
{: #daily_intraday}
일별 예보 API에는 각 위치마다 여러 일의 일별 예보가 포함될 수 있습니다.
각 예보 일에는 최대 3개의 개별 예보가 포함될 수 있습니다. 임의의
예보 일의 경우 API가 주간, 야간 및 24시간 예보를 반환할 수 있습니다.

일중 예보 API에는 각 위치마다 여러 일의 일별 예보가 포함될 수 있습니다.
각 예보 일에는 오전(오전 7시부터 오후 1시),
오후(오후 1시부터 오후 7시), 저녁(오후 7시부터 새별 1시) 및 심야(새벽 1시부터 오전 7시) 동안의 4개의 개별 6시간 예보가 포함됩니다. 일중
예보는 구조적으로 일별 예보와 유사합니다.

각 세그먼트에는 일 부분 번호, 요일 이름 및 일 부분 이름이 있습니다. 예를 들어,
다음 예제에서는 목요일 오전에 API에서 생성되는 예보에 대해
`num`, `dow` 및 `daypart_name`의 데이터 필드 순서 및 데이터 값을
표시합니다.
* 1, 목요일, 오전
* 2, 목요일, 오후
* 3, 목요일, 저녁
* 4, 목요일, 심야
* 5, 금요일, 오전
* 6, 금요일, 오후
* 7, 금요일, 저녁
* 8, 금요일, 심야

## 현재 및 시계열 관측
{: #time_series}

현재 조건 및 시계열 기상 관측 데이터에서는
기온, 강우량, 바람, 기압, 가시성, 자외선(UV)
및 기타 관련된 관측 요소에 대한 정보를
관측소, 관측 날짜/시간, 기상 아이콘 코드 및 구문을 포함하여 제공합니다. 시계열 관측과 현재 관측의 차이점은
하나 이상의 관측 데이터 세트를 리턴하는 관측 기간입니다. 

현재 상태는 시간 매개변수 없이 요청한
해당 위치의 최신 관측입니다. 하나의 데이터 세트가 리턴됩니다.
시계열 관측에는 요청한 위치에 대해 최근 24시간을 포함하여
최대 24시간까지 발생한 지난 관측이 포함됩니다. 

특정 리포팅 스테이션에서 관측된 최신 관측치는
최대 48시간(2일) 동안 기본 데이터베이스에 보유됩니다.
최신 관측 데이터는 계속하여 업데이트되며 관측
날짜/시간 스탬프를 기반으로 선입선출(FIFO) 방법론(최신 관측으로
데이터를 순환하고 가장 오래된 관측을 아카이브 스토리지로 이동함)을
사용하여 교체됩니다. 보유되어 임의 스테이션에서 사용 가능한 데이터의
양은 24개 이상의 개별 관측 보고서일 수 있습니다. 관측의 수는 관측 유형으로
결정됩니다.

## 경보 헤드라인 및 세부사항
{: #alerts_levels}
경보 API는 심각한
뇌우, 토네이도, 지진 및 홍수와 관련된 활성 기상 경보 헤드라인을 반환합니다.
또한 이러한 API는 아동 납치 경보 및
법률 집행 경고 등의 비기상 경보를 반환합니다.

**참고**: 이 API는 미국, 캐나다 및 유럽에 대해서만 사용 가능합니다.

경보 헤드라인 API에서 `detail_key` 속성의 키 값을 제공하여
경보 세부사항 API의 경보 세부사항에 액세스합니다.
경보 헤드라인 API를 조회하여 `detail_key` 값을 가져온 후
경보 세부사항 API 응답을 `detail_key`와 함께 검색하십시오.

**참고**: 애플리케이션에 표시되는 경보 데이터의 데이터 소스 속성을 표시해야 합니다.

속성 단계에서는 다음 정보를 표시해야 합니다.

*발행자 <사무실 이름> - &lt;사무실 관리 지구 코드&gt;, &lt;사무실 국가 코드&gt;, &lt;소스&gt;, &lt;면책사항&gt;*

예를 들어, 다음과 같습니다.
* National Weather Service에서 발행됨 - 미국, 비스마르크
* Central Institute for Meteorology and Geodynamics에서 발행됨 - 오스트리아, EMETNET-Meteoalarm

## 연감 정보
{: #almanac_details}
연감 API에서는 위치 ID 및 위치 유형(도시 또는 우편번호)
또는 위도 및 경도 쌍을 요구하여 특정 위치의 정보를 검색합니다.

URL에서 `위치`를 사용하는 경우 위치에
위치 유형 및 국가 코드와 함께 위치 ID(우편번호)가
포함되어야 합니다. URL에서 `지오코드`를 사용하는 경우 검색 위치가
유효한 위도 및 경도 조합이어야 합니다.

연감 API에서는 매개변수를 사용하여 일별 또는 월별 데이터,
정보의 특정 날짜 또는 날짜 범위를 지정하며 데이터를 반환할 측정 단위를 지정합니다.

날짜 매개변수는 `start` 및 `end`입니다. `start` 매개변수는
필수 매개변수이지만 `end` 매개변수는 선택적입니다. 매개변수가 함께 사용되면 조합에서
데이터의 특정 월 또는 일 대신 데이터의 범위를 반환합니다.

일별 연감 결과를 검색하기 위한 날짜 형식은
필요한 데이터의 월 및 일을 나타내는 4자리 숫자 값입니다(즉, MMDD). 한 자리
일은 **반드시** 선행하는 0이 있어야 합니다(예: 01).

월별 연감 결과를 검색하기 위한 날짜 형식은 월입니다(즉, MM). 한 자리
월은 **반드시** 선행하는 0이 있어야 합니다(예: 01). 기타 형식에서는
API 오류가 발생하고 데이터가 반환되지 않습니다.

**참고**: 요청에 날짜 값을 제공하지 않으면
시스템이 404의 상태(잘못된 요청)를 반환합니다. API는 기본값을 제공하지 않습니다.

## URL 구성
{: #url_construction}

REST API는 공통 URL 구조 및 조회 매개변수를 사용하여 기상 데이터를 요청하고 필터링합니다.
API에 전달되는 URL은 다음과 같이 구성됩니다. 

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

예를 들어, 다음과 같습니다.

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**속성**     |**설명**                                    |
|------------------|---------------------------------------------------|
|`호스트 이름`        |호스팅된 URL 경로입니다. 예: `https://twcservice.mybluemix.net:443/api/weather`|
|`버전`         |현재 반복입니다. 예: `v1`|
|`위치`        |지오코드 또는 위치 ID입니다. 위치 그룹은 `geocode` 또는 `location`일 수 있습니다. 예를 들어, `geocode/45.4214/75.6919`는 캐나다 오타와를 나타냅니다. 지오코드 좌표를 제공하면 API가 사용 가능한 가장 근접한 위치의 데이터를 리턴합니다. 마침표는 소수점 구분 기호로 사용되고, 쉼표는 위도와 경도 값을 구분하기 위해 사용됩니다. 지오코드를 제공하면 사용되는 실제 위도 및 경도 값이 응답의 메타데이터로 리턴됩니다.|
|`제품 그룹`   |제품입니다. 예: `observations` 또는 `forecast`. 제품 서브그룹(예: `historical`)은 선택사항입니다.|
|`날짜`            |날짜 유형입니다. 예: `daily` 또는 `monthly`|
|`형식`          |형식입니다. 예: `3day`, `5day`, `7day` 또는 `10day`|
|`단위`           |응답을 리턴하는 선택적 단위. API는 English(e), Metric(m) 및 UK-Hybrid(h) 측정 단위를 지원합니다. 측정 단위를 제공하고 값은 제공하지 않으면 API가 언어 코드에 해당하는 측정 단위로 데이터를 리턴합니다. 기본값 또는 요청한 측정 단위가 응답의 메타데이터에 단위 매개변수로 리턴됩니다.|
|`언어`        |응답을 리턴하는 언어. 기본값은 en-US입니다. 기본값 또는 요청한 변환 언어가 응답의 메타데이터에 언어 매개변수로 리턴됩니다.|
*표 2. URL 세부사항*

**참고**: REST API는 국가 코드에 대해 ISO 3166 표준을 사용합니다. 자세한 정보는
[ISO 표준 온라인 찾아보기 플랫폼](https://www.iso.org/obp/ui/#search/code/){:new_window}을 참조하십시오.
API는 WGS84 지오코드 좌표 참조 시스템을 사용합니다. 자세한 정보는
[기본 지오 어휘](https://www.w3.org/2003/01/geo/){:new_window}를 참조하십시오.

## 아이콘 코드 및 이미지
{: #icon_code_images}

{{site.data.keyword.weather_short}} REST API가 응답으로 아이콘 코드를 리턴할 때
사용자가 아이콘 코드를 사용하여 앱에서 표시할 아이콘 이미지를 판별할 수 있습니다.
아이콘 이미지의 파일 이름 및 API 응답의 아이콘 코드 간에 일대일 관계가 있습니다.
예를 들어, API 응답에 1의 `icon_code`가 포함된 경우 파일 이름 `01.png`를 사용하여
일치하는 아이콘 이미지를 표시할 수 있습니다.

코드에서, 아이콘 이미지의 URL을 판별하는 데 `icon_code`를 사용하는
함수를 작성할 수 있습니다. 예를 들어, 다음과 같습니다.

```
function getIconURL(code) {
    return "images/weathericons/icon" + code + ".png";
}
```

다음 테이블에는
{{site.data.keyword.weather_short}} REST API와 함께 사용할 수 있는 아이콘 코드, 설명 및 이미지가 포함됩니다. 테이블에서는
아이콘이 예보 또는 관측 API에서 사용되는지 여부와 아이콘이 야간 또는 주간
예보 파트에서 사용 가능한지 여부를 표시합니다.

|**코드**    |**설명**|**이미지**|**API 사용법** |**야간 또는 주간**|
|----|--------------------------|------------|------------|--------------------|
| 0  | 토네이도                  | <img src="images/00.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 야간 및 주간 |
| 1  | 열대성 태풍           | <img src="images/01.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 2  | 허리케인                | <img src="images/02.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 야간 및 주간 |
| 3  | 강한 태풍            | <img src="images/03.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 야간 및 주간 |
| 4  | 천둥 및 우박         | <img src="images/04.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 5  | 비에서 소낙눈     | <img src="images/05.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 6  | 비/진눈깨비             | <img src="images/06.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 7  | 겨울 혼합 눈/진눈깨비  | <img src="images/07.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 8  | 결빙성 진눈깨비         | <img src="images/08.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 9  | 보슬비                  | <img src="images/09.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 10 | 얼어붙는 비            | <img src="images/10.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 11 | 약한 비               | <img src="images/11.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 12 | 비                     | <img src="images/12.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 13 | 산발적 돌풍       | <img src="images/13.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 14 | 적은 눈               | <img src="images/14.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 15 | 강풍/땅날림눈  | <img src="images/15.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 16 | 눈                     | <img src="images/16.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 17 | 우박                     | <img src="images/17.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 18 | 진눈깨비                    | <img src="images/18.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 19 | 풍진/모래 폭풍 | <img src="images/19.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 20 | 안개낌                    | <img src="images/20.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 21 | 연무/바람             | <img src="images/21.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 22 | 연기/바람            | <img src="images/22.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 23 | 미풍                   | <img src="images/23.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 야간 및 주간 |
| 24 | 날린 물보라/바람    | <img src="images/24.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 25 | 쌀쌀함/빙정    | <img src="images/25.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 26 | 흐림                   | <img src="images/26.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 27 | 대체로 흐림            | <img src="images/27.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 28 | 대체로 흐림            | <img src="images/28.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 주간         |
| 29 | 곳에 따라 흐림            | <img src="images/29.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간       |
| 30 | 곳에 따라 흐림            | <img src="images/30.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 주간         |
| 31 | 맑음                    | <img src="images/31.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간       |
| 32 | 햇빛                    | <img src="images/32.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 주간         |
| 33 | 좋음/대체로 맑음      | <img src="images/33.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간       |
| 34 | 좋음/대체로 햇빛      | <img src="images/34.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 주간         |
| 35 | 혼합 비 & 우박        | <img src="images/35.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 주간         |
| 36 | 더위                      | <img src="images/36.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 주간         |
| 37 | 고립된 뇌우   | <img src="images/37.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 주간         |
| 38 | 뇌우            | <img src="images/38.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 39 | 간간이 내리는 소나기        | <img src="images/39.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 주간         |
| 40 | 폭우               | <img src="images/40.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 41 | 간간이 내리는 소낙눈   | <img src="images/41.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 주간         |
| 42 | 폭설               | <img src="images/42.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
| 43 | 눈보라                 | <img src="images/43.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 야간 및 주간 |
| 44 | 해당 사항 없음(N/A)      | <img src="images/44.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 야간 및 주간 |
| 45 | 간간이 내리는 소나기        | <img src="images/45.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 야간       |
| 46 | 간간이 내리는 소낙눈   | <img src="images/46.png " width="100" height="100" alt="아이콘 이미지."/>| 예보                | 야간       |
| 47 | 산발적 뇌우  | <img src="images/47.png " width="100" height="100" alt="아이콘 이미지."/>| 예보 및 관측 | 야간 및 주간 |
*표 3. 아이콘 코드 및 이미지*

이 날씨 아이콘 세트를 [PNGs](https://twcdocs.mybluemix.net/download/weather_icons_200x200_png.zip){:new_window}
또는 [SVGs](https://twcdocs.mybluemix.net/download/weather_icons_200x200_svg.zip){:new_window}로 다운로드하여 앱에서 사용할 수 있습니다. 

또한
[{{site.data.keyword.weather_short}} 데모 앱](http://weather-company-data-demo.{APPDomain}){: new_window}이 사용하는 [아이콘 세트](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}를 다운로드할 수 있습니다.

## 측정 단위
{: #units_measure}

REST API를 사용하는 경우 측정 단위를 명시적으로 전달할 필요가 없습니다. API는 URL에서 언어 코드와 연관된 측정 단위를 기본값으로 사용합니다.
그러나 기본값과는 다른 측정 단위를 제공하려는 경우 기본값을 대체하는 측정 단위를 전달할 수 있습니다.

* en-US 또는 en의 경우 측정 코드의 기본 단위는 English/Imperial입니다. 단위 코드는 `e`입니다.
* en-GB의 경우 기본 측정 단위는 Hybrid-UK입니다. 단위 코드는 `h`입니다.
* 다른 모든 것의 경우 기본 측정 단위는 Metric입니다. 단위 코드는 `m`입니다.

## 언어 변환
{: #language_translation}

REST API는 구문과 측정 단위를 변환합니다. 요청 URL을 형식화할 때 올바른 언어를 제공해야 합니다.
변환되는 필드는 다음과 같습니다. 

|**필드**           |**설명**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |24시간 동안의 설명식 예보|
|`dow`               |요일|
|`wind_phrase`       |주간 12시간 동안의 풍향과 풍속을 기술하는 문구|
|`wdir_cardinal`     |기수 표기법의 주간 평균 풍향|
|`daypart_name`      |처음 48시간의 요일 이름이 포함되지 않은 주간 12시간의 이름|
|`temp_phrase`       |12시간 예보 기간 동안 예보된 고온 또는 저온이 포함된 짧은 문구|
|`shortcast`         |설명식 예보의 간결한 감각적 기상 부분|
|`long_daypart_name` |확장된 형식의 유효한 기상 예보에 대한 이름 지정된 시간 범위. 이름 지정된 시간 범위는 12시간 또는 24시간입니다.|
|`golf_category`     |골프 치기에 적절한 기상 상태의 문구로 표현된 골프 인덱스 카테고리|
|`phrase_nnchar`     |감각적 주간 기상 문구|
|`lunar_phrase`      |달 위상에 대한 3문자 단축 코드|
|`uv_desc`           |노출로 인한 피부 손상의 연관 위험 레벨을 제공하여 UV 인덱스 값을 보완하는 UV 인덱스 설명|
|`wx_phrase`         |보고 스테이션의 관측된 기상 조건에 대한 텍스트 설명|
|`pressure_desc`     |지난 시간 동안의 기압 읽기에서 변경사항을 설명하는 구문|
|`headline_text`     |위치에 대한 이벤트 헤드라인의 텍스트|
|`event_desc`        |이벤트의 설명|
|`cntry_name`        |이벤트가 발생한 국가 이름이며, 대소문자가 혼합됨|
*표 4. 변환된 응답 필드*

## API 응답의 널 또는 누락된 데이터 필드 처리
{: #handling_null_or_missing}

데이터가 사용 가능하지 않아서 데이터 필드가 널(NULL)인 경우 REST API가 `null` 단어와 함께 적합한 필드 태그를 반환하거나 필드를 반환하지 않습니다.

## 오류 처리
{: #handling_errors}

다음 오류 코드가 모든 API에 공통으로 적용됩니다. 

|**오류** |**설명**                                    |
|----------|---------------------------------------------------|
|400       |잘못된 요청. 잘못된 형식의 구문으로 인해 서버가 요청을 이해하지 못했습니다. 이 오류 코드는 모든 API에 대해 구현됩니다. API는 올바르지 않은 매개변수가 제공되는 경우 요청을 거부합니다.|
|401       |권한 없음. 요청에 인증이 필요합니다.|
|403       |금지됨. 서버가 요청을 이해하였으나 요청 수행을 거부하고 있습니다.|
|404       |찾을 수 없음. 필수 매개변수가 API 요청에 존재하지 않는 경우, 404 오류 코드의 MissingParameterException 오류가 리턴됩니다.|
|500       |내부 서버 오류. 서버에서 요청을 수행할 수 없게 하는 예상치 않은 조건이 발생했습니다.|
*표 5. 오류 응답 코드*

오류에 대한 응답은 항상 동일합니다. 하나의 응답에서 여러 개의 오류 코드를 리턴할 수 있습니다.
예를 들면, JSON 오류 응답은 다음과 같이 리턴될 수 있습니다.

```
{
  metadata: {
    transaction_id: "1411496413365:-1880721071"
  },
  success: false,
  errors: [
    {
      error: {
        code: "NDF-0001",
        message: "There was no data found for your product query."
      }
    }
}
```
