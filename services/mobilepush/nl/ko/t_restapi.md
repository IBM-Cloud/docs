---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# REST API 사용
{: #push-api-rest}
마지막 업데이트 날짜: 2017년 2월 28일
{: .last-updated}

{{site.data.keyword.mobilepushshort}}에 REST(Representational State Transfer) API(Application Program Interface)를 사용할 수 있습니다. 또한 SDK 및 [Push API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/){: new_window}을 사용하여 클라이언트 애플리케이션을 추가 개발할 수 있습니다. 

백엔드 서버 애플리케이션과 클라이언트에서 푸시 REST API를 사용하여 {{site.data.keyword.mobilepushshort}} 기능에 액세스할 수 있습니다. 

- 디바이스 등록
- 등록
- 메시지
- 구독
- 태그
- 웹훅

REST API의 기본 URL을 얻으려면 다음 단계를 완료하십시오. 

1. MobileFirst Services Starter를 선택하여 표준 유형 섹션 Bluemix® 카탈로그에서 백엔드 애플리케이션을 작성하십시오. 이렇게 하면 {{site.data.keyword.mobilepushshort}} 서비스가 애플리케이션에 바인드됩니다. 푸시의 서비스 인스턴스를 작성하고 바인드되지 않은 상태로 둘 수도 있습니다.  
1. Bluemix 대시보드의 기본 페이지에서 **애플리케이션** 영역으로 이동한 후 앱을 선택하십시오. 
3. **모바일 옵션**을 클릭하십시오. 앱의 세부사항 페이지 시작 부분에 라우트 값과 앱 GUID 값이 표시됩니다. 신임 정보 표시 화면에 AppSecret에 관한 정보가 표시됩니다. 모바일 옵션에서 애플리케이션 시크릿을 가져올 수 있으며 일부 API의 클라이언트 시크릿을 가져올 수도 있습니다. 

또한 명령행을 사용하여 서비스 신임 정보를 가져올 수 있습니다. 

```
    cf create-service-key {push_instance_name} {key_name}
    cf service-key {push_instance_name} {key_name}
```
	{: codeblock}

## 언어 승인 헤더
{: #push-api-rest-accept}

"Accept-Language" 헤더는 [Push REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/){: new_window}에서 출력하는 오류 메시지에 사용할 언어를 지정합니다. 오류 메시지에 지원되는 언어는 중국어, 대만어, 영어(미국), 독일어, 프랑스어, 이탈리아어, 일본어, 한국어, 포르투갈어 및 스페인어입니다. 

## appSecret 
{: #push-api-rest-secret}

애플리케이션이 {{site.data.keyword.mobilepushshort}}에 바인드되는 경우 서비스에서 appSecret(고유 키)을 생성하여 응답 헤더를 통해 전달합니다. IBM {{site.data.keyword.mobilepushshort}} for Bluemix Rest API를 사용 중인 경우 보호해야 하는 API에 대한 정보를 얻으려면 REST API 참조를 사용하십시오. 자세한 정보는 [Push REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/){: new_window}을 참조하십시오. 

요청 헤더에 appSecret이 포함되어야 합니다. 그렇지 않으면 서버가 401 권한 없음 오류 코드를 리턴합니다. {{site.data.keyword.mobilepushshort}}가 애플리케이션에 추가되면 특정 AppID가 작성됩니다. 응답 과정에서 태그를 작성하거나 메시지를 전송하는 데 사용되는 appSecret 헤더를 받습니다. 카탈로그 또는 표준 유형의 서비스를 통해 오퍼레이션이 발생합니다.

appSecret 값을 가져오려면 다음을 수행하십시오. 

1. 푸시 서비스에 바인드되는 *app-name*을 클릭하십시오.
2. **신임 정보 표시** 링크를 클릭하여 appSecret(AppID)을 표시하십시오.

**신임 정보 표시** 화면에 다음과 같이 AppSecret에 대한 정보가 표시됩니다. 
```
	{
    "imfpush_Dev": [
   {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04",
       }
     }
    ]
    }
```
	{: codeblock} 


## Push REST API 필터
{: #push-api-rest-filters}

필터는 {{site.data.keyword.mobilepushshort}}의 GET API에서 리턴되는 데이터를 제한하는 검색 기준을 정의합니다. 필터링할 Get 오퍼레이션의 결과에 대해 필터를 적용하십시오. 필터가 결과에 포함되는 항목의 수를 제한합니다. 예를 들면, 필터를 사용하여 "test"로 시작하는 태그를 검색할 수 있습니다.  

다음 구문을 사용하여 필터를 생성할 수 있습니다. 

**name**: 필터가 적용되는 필드 이름입니다. 

**operator**: 사용할 필터 일치를 설명하는 ==(정확히 일치) 또는 =@(하위 문자열 포함)입니다. 

**expression**: 결과에 포함시킬 값입니다. 

표현식에 쉼표 및 백슬래시가 표시될 경우 백슬래시로 이스케이프해야 합니다. 

여러 개의 필터를 사용할 경우 AND 및 OR 논리를 사용하여 필터를 결합할 수 있습니다. 

- AND 논리의 경우 조회에서 여러 필터를 사용하십시오.
- OR 논리의 경우 필터 식 안에 쉼표(,)를 사용하십시오.
- AND 및 OR 논리를 둘 다 사용할 경우, 단일 조회에 AND 및 OR 논리를 모두 포함시킬 수 있습니다. 각 필터는 AND 표현식에서 결합되기 전에 개별적으로 평가됩니다. 

디바이스 GET API의 경우 다음 조합이 지원됩니다.
-이름은 플랫폼 필드입니다. 
- 플랫폼을 제외하고 연산자는 == 또는 =@일 수 있습니다. 
- 플랫폼의 경우 연산자는 ==여야 합니다. 연산자 =@을 사용할 경우 값이 하위 문자열이 될 수 있습니다.
- ==를 사용할 경우 값이 정확히 일치하는 문자열이어야 합니다. 

구독 GET API의 경우 다음 조합이 지원됩니다.

- 이름은 tagName 또는 deviceId 필드 중 하나일 수 있습니다. 
- 플랫폼을 제외하고 연산자는 == 또는 =@일 수 있습니다. 
- 플랫폼의 경우 연산자는 ==여야 합니다. 
- =@ 연산자를 사용하는 경우 값은 하위 문자열이 될 수 있습니다. == 연산자를 사용하는 경우 값은 정확히 일치하는 문자열이어야 합니다. 
- 태그 GET API의 경우 다음 조합이 지원됩니다.
- 이름은 "이름" 또는 "설명" 필드 중 하나일 수 있습니다.
- 연산자 =@을 사용할 경우 값이 하위 문자열이 될 수 있습니다.
- ==를 사용할 경우 값이 정확히 일치하는 문자열이어야 합니다. 


## Push Notifications 서비스 응답 코드
{: #push-api-response-codes}

상태: 405 허용되지 않은 메소드 - 적절한 메소드를 예상했습니다. 
