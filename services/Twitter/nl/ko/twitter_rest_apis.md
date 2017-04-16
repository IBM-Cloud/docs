---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Twitter REST API 사용
{: #rest_apis}

{{site.data.keyword.twittershort}} 서비스는 Twitter 컨텐츠를 검색하고 소비하는 RESTful API로 구성되어 있습니다. [쿼리 언어](twitter_rest_apis.html#querylanguage){: new.window} 표에는 서비스 API에서 지원하는 쿼리 용어가 나열되어 있습니다. 쿼리를 구성할 수 있는 방법을 보여주는 예제가 제공됩니다.
{:shortdesc}

## REST API 문서 {: #rest_api}
REST API 문서는 Swagger를 사용하여 빌드되어, API 조작을 테스트하고 결과를 즉각 볼 수 있으므로 애플리케이션을 더 빠르게 빌드할 수 있습니다.
현재 다음 API 조작이 사용 가능합니다. 

* 검색: Decahose 또는 필터링된 PowerTrack 스트림에서 트윗을 찾습니다.
* 개수: 지정된 쿼리를 토대로 트윗의 수를 리턴합니다. 
* 검사: 메시지 목록이 Twitter 정책과 Twitter 사용자에 부합하는지 판별합니다. 
* 추적: Entry Plan 사용자에게 엔드포인트 모음을 제공하여 PowerTrack 필터를 관리합니다.

지원되는 REST API와 이의 자원에 대한 자세한 정보는  [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window} 참조를 보십시오.애플리케이션이 존재하는 지역을 선택하십시오. 각 지역은 독립적입니다. 한 지역에서 프로비저닝되는 서비스 신임 정보를 사용하여 다른 지역의 서비스를 인증할 수 없습니다. 

참조 문서에서 각 조작의 상세 정보를 보려면 **조작 목록**을 클릭하십시오. **실행** 단추를 클릭한 후 신임 정보를 제공해야 할 수 있습니다. **VCAP_SERVICES** 환경 변수의 사용자 이름과 비밀번호를 제공해야 합니다. 사용자의 애플리케이션을 열고 목차의 **환경 변수**를 클릭하면 이 정보를 찾을 수 있습니다. 

**참고**: 적합한 신임 정보를 입력하지 않으면 응답 본문에 "권한 없음" 메시지가 표시됩니다.

**중요**: **실행** 기능을 사용하여 작성된 활성 트랙은 Twitter에서 트윗을 수집하며 월별 허용량에 대하여 계산됩니다. 추적이 이제 필요하지 않으면 해당 상태를 **비활성**으로 변경하거나 추적을 삭제하면 됩니다.


## 쿼리 언어 {: #querylanguage}

{{site.data.keyword.twittershort}}에서 풍부한 쿼리 매개변수 세트와 필터를 사용하여 Twitter 컨텐츠를 검색하여 좀 더 정확한 결과를 생성할 수 있습니다. 

다음의 부울 연산자가 쿼리에서 지원됩니다.  

| **연산자**        | **설명**                                                                                                                   | **예**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| term1 **AND** term2 | term1과 term2를 포함하는 트윗을 리턴합니다. 두 용어 사이의 공백은 AND로 처리되므로 연산자를 생략할 수 있습니다.  | `#ibm twitter`      |
| term1 **OR** term2  | term1 또는 term2를 포함하는 트윗을 리턴합니다.     | `#money OR revenue` |
| -term1              | term1을 포함하지 않은 트윗을 리턴합니다.   |`ibm -apple`  |

*표 1. 부울 연산자*

연산자 우선순위: "-"이 "AND"보다 우선하며 "AND"가 "OR"보다 우선합니다. 연산자의 우선순위를 명확히 하려면 소괄호를 사용해야 합니다. 예를 들어 `large animals` -(`giraffes` OR `bears`)의 경우 "large" 및 "animals"를 포함하는 트윗을 검색하지만 "giraffes" 및 "bears"를 포함하는 트윗은 제외합니다. 

현재 지원되는 쿼리 용어가 다음 테이블에 나열되어 있습니다. 

| **용어** 	| **설명** 	| **예** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| 키워드 	| 본문에 "키워드"가 있는 트윗을 일치로 판별합니다. 검색은 대소문자를 구분하지 않습니다.  	| analytics 	|
| "정확한 문구 일치" 	| 정확히 일치하는 키워드 시퀀스가 포함된 트윗을 일치로 판별합니다.  	| "IBM and analytics" 	|
| `#hashtag` 	| *#hashtag* 해시태그가 있는 트윗을 일치로 판별합니다.  	| `#insight2015` 	|
| `bio_lang:language` 	| 프로파일 언어 설정이 지정된 언어 코드와 일치하는 사용자의 트윗을 일치로 판별합니다. 지원되는 언어 목록은 `lang:`에서 확인하십시오.  	| `bio_lang:en` 	|
| `bio_location:"location"` 	| 지정된 `location` 참조가 프로파일 위치 설정에 포함되어 있는 사용자의 트윗을 일치로 판별합니다.  	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| 태그된 장소나 위치가 지정된 국가 코드와 일치하는 사용자의 트윗을 일치로 판별합니다. </br>**지원되는 국가 코드 목록은 **http://en.wikipedia.org/wiki/ISO_3166-1 에서 확인하십시오. 	| `country_code:us` 	|
| `followers_count: lowerLimit,upperLimit` 	| 지정된 범위 내의 팔로워 수를 갖는 사용자의 트윗을 일치로 판별합니다. upperLimit는 선택사항이며 두 한도 모두 끝 수를 포함합니다. 	| `followers_count:500` 	|
| `friends_count: lowerLimit,upperLimit` 	| 지정된 범위 내의 사용자 수를 팔로우하는 사용자의 트윗을 일치로 판별합니다. upperLimit는 선택사항이며 두 한도 모두 끝 수를 포함합니다. 	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| preferredUsername *twitterHandle*인 사용자의 트윗을 일치로 판별합니다. &commat; 기호를 포함하면 안 됩니다. 	| `from:alexlang11` 	|
| `has:children` 	| 하위가 있는 사용자의 트윗을 일치로 판별합니다.  	| `has:children` 	|
| `is:married` 	| 결혼한 사용자의 트윗을 일치로 판별합니다.  	| `is:married` 	|
| `is:verified` 	| 작성자가 Twitter에서 확인된 트윗을 일치로 판별합니다.  	| `analytics is:verified` 	|
| `lang:language-code` 	| 특정 언어의 트윗을 일치로 판별합니다. 지원되는 언어 코드 목록은 다음과 같습니다. <ul><li>`ar` (아랍어)</li><li>`zh` (중국어)</li><li>`da` (덴마크어)</li><li>`dl` (네덜란드어)</li><li>`en` (영어)</li><li>`fi` (핀란드어)</li><li>`fr` (프랑스어)</li><li>`de` (독일어)</li><li>`el` (그리스어)</li><li>`he` (히브리어)</li><li>`id` (인도네시아어)</li><li>`it` (이탈리아어)</li><li>`ja` (일본어)</li><li>`ko` (한국어)</li><li>`no` (노르웨이어)</li><li>`fa` (페르시아어)</li><li>`pl` (폴란드어)</li><li>`pt` (포르투갈어)</li><li>`ru` (러시아어)</li><li>`es` (스페인어)</li><li>`sv` (스웨덴어)</li><li>`th` (태국어)</li><li>`tr` (터키어)</li><li>`uk` (우크라이나어)</li></ul>    | `lang:de` (독일어 트윗을 일치로 판별) 	|
| `listed_count: lowerLimit,upperLimit` 	| Twitter의 작성자 목록이 지정된 범위 내에 있는 트윗을 일치로 판별합니다. upperLimit는 선택사항이며 두 한도 모두 끝 수를 포함합니다. 	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| 경도와 위도 및 반경으로 지정된 지역의 트윗을 일치로 판별합니다. </br></br>모든 좌표는 10진수로 표시됩니다. `longitude`는 -180 ~ +180 사이의 값이어야 하고 `latitude`는 -90 ~ +90 사이의 값이어야 합니다. 지원되는 범위 밖의 값을 지정하면 오류가 리턴됩니다. 값을 부동 소수점 수로 입력해야 하며 정수는 지원되지 않습니다.</br></br>주변 영역의 반경은 마일(mi) 또는 킬로미터(km)로 지정해야 합니다.  	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| "startTime"에 또는 그 이후에 게시된 트윗을 일치로 판별합니다. "endTime"은 선택사항이며 두 한도의 끝 수는 포함됩니다. 시간 소인은 다음 형식 중 하나를 따라야 합니다. </br>"yyyy-mm-dd" 또는 "yyyy-mm-ddTHH:MM:SSZ" </br>  시간대는 협정 세계시(UTC)에 기반합니다. 시간, 분 및 초를 지정할 때 시간은 규정된 형식에 따라 "T" 및 "Z"로 둘러싸야 합니다. 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| 특정 감정 상태의 트윗을 일치로 판별합니다. 지원되는 값은 다음과 같습니다. </br><dl>긍정</dl> <dlentry>트윗에 부정 감정 구문보다 긍정 구문이 더 많이 포함되어 있습니다. </dlentry></br></br><dl>부정</dl> <dlentry>트윗에 긍정 감정 구문보다 부정 구문이 더 많이 포함되어 있습니다. </dlentry></br></br><dl>중립</dl>  <dlentry>트윗에 어떤 감정도 포함되어 있지 않거나 감정 표현을 제공하지 않는 언어로 되어 있습니다. </dlentry></br></br><dl>양면성</dl>  <dlentry>긍정과 부정의 감정 구문이 동일하게 트윗에 포함되어 있습니다.</dlentry> 	| `sentiment:positive` 	|
| `statuses_count: lowerLimit,upperLimit` 	| 지정된 범위 내의 상태 수를 게시한 사용자의 트윗을 일치로 판별합니다. upperLimit는 선택사항이며 두 한도 모두 끝 수를 포함합니다. 	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| 프로파일 설정이 지정된 시간대와 일치하는 사용자의 트윗을 일치로 판별합니다.  	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| 프로파일 설정이 지정된 도시와 일치하는 사용자의 트윗과 일치합니다. 	| `time_zone:"Dublin"` 	|
*표 2. 쿼리 용어*

지원되는 모든 쿼리 용어를 이전에 설명한 부울 연산자를 사용하여 결합할 수 있습니다. 예를 들면 다음과 같습니다.

`ibm -apple followers_count:500`
