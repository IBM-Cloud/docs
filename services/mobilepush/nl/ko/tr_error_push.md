---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}} 서비스 오류 메시지
{: #errors}
마지막 업데이트 날짜: 2017년 2월 13일
{: .last-updated}


다음과 같은 {{site.data.keyword.mobilepushshort}} 오류 메시지는
REST API 요청에 대한 응답으로 리턴됩니다. 

샘플 오류 응답:
```
	{
		"message": "Missing APNs credentials",
		"docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
		"code":   "FPWSE0003E"
	}
```
		    {: codeblock}

오류에 대한 추가 정보를 얻으려면 문서에서 관련 오류 코드를 검색하십시오. 

## FPWSE0001E
{: #error_fpwse0001e}

**설명**: 조회하려는 자원(예: 태그 또는 구독)이 서버에 없습니다. 

**사용자 응답**: 메시지에서 보고된 리소스를 작성하십시오. 또는 올바른 ID를 제공하여 리소스를 조회할 수 있습니다. 


## FPWSE0002E
{: #error_fpwse0002e}

**설명**: 작성하려는 자원이 서버에 이미 있습니다. 자원은 태그, 구독 등일 수 있습니다. 

**사용자 응답**: 다른 ID를 사용하여 리소스를 작성하십시오. 


## FPWSE0003E
{: #error_fpwse0003e}

**설명**: {{site.data.keyword.mobilepushshort}} 서비스에 대한 전제조건 구성이 완료되지 않았습니다. Apple Push Notification 서비스(APNs) 신임 정보가 구성되기 전에 해당 신임 정보를 가져오려고 했을 수 있습니다. 

**사용자 응답**: {{site.data.keyword.mobilepushshort}} 서비스가 APNs에 대한 올바른 보안 인증서를 사용하여 구성되었는지 확인하십시오. 자세한 정보는 [APNs에 대한 신임 정보 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](t_push_provider_ios.html){: new_window}을 참조하십시오. 


## FPWSE0004E
{: #error_fpwse0004e}

**설명**: 요청에 포함된 JSON 본문이 올바르지 않습니다. 


**사용자 응답**: 요청에서 올바른 JSON 구문을 사용하는지 확인하십시오. 



## FPWSE0005E
{: #error_fpwse0005e}

**설명**: API 요청을 완료하는 데 필요한 특성이 JSON 본문에 포함되어 있지 않기 때문에 {{site.data.keyword.mobilepushshort}} 서버에 대한 요청이 올바르지 않거나 완전하지 않습니다. 예를 들어, 비밀번호가 올바르지 않거나 디바이스 토큰이 누락되었습니다. 


**사용자 응답**: 메시지를 검토하여 올바르지 않거나 누락된 특성 값을 확인한 후 필수 정보를 제공하십시오. 



## FPWSE0006E
{: #error_fpwse0006e}

**설명**: 요청의 JSON 본문에 {{site.data.keyword.mobilepushshort}} 서버에서 이해할 수 없는 매개변수가 있습니다. 


**사용자 응답**: 요청의 JSON 본문이 {{site.data.keyword.mobilepushshort}} 서버에서 예상하는 요청의 형식을 따르는지 확인하십시오. 자세한 정보는 [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/){: new_window}을 참조하십시오. 



## FPWSE0007E 
{: #error_fpwse0007e}

**설명**: 요청 URL에 인식되지 않는 매개변수가 포함된 조회 문자열이 있습니다. 예를 들어, 구독을 삭제하기 위한 요청에 deviceId 및 tagName 이외의 매개변수가 있는 경우 이 오류가 발생할 수 있습니다. 


**사용자 응답**: 요청의 JSON 본문이 {{site.data.keyword.mobilepushshort}} 서버에서 예상하는 요청의 형식을 따르는지 확인하십시오. 자세한 정보는 [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/){: new_window}을 참조하십시오. 



## FPWSE0008E
{: #error_fpwse0008e}

**설명**: 요청 URL에 필수 매개변수가 누락된 조회 문자열이 있습니다. 예를 들어, 구독을 삭제하기 위한 요청에서 deviceId 및 tagName 매개변수가 누락되었을 수 있습니다. 


**사용자 응답**: 요청의 JSON 본문이 {{site.data.keyword.mobilepushshort}} 서버에서 예상하는 요청의 형식을 따르는지 확인하십시오. 자세한 정보는 [REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/){: new_window}을 참조하십시오. 



## FPWSE0009E
{: #error_fpwse0009e}

**설명**: 알림 전송이 시도되었지만 애플리케이션에 등록된 디바이스가 없습니다. 

**사용자 응답**: 알림 전송을 시도하기 전에 디바이스가 애플리케이션에 등록되었는지 확인하십시오. 



## FPWSE0010E
{: #error_fpwse0010e}

**설명**: 서버에 제출된 요청이 예외 조건을 생성했습니다. 다음 조건 중 하나가 이 오류를 일으켰을 수 있습니다. 

- {{site.data.keyword.mobilepushshort}}가 사용하는 내부 시스템이 응답하지 않습니다. 
- 요청이 {{site.data.keyword.mobilepushshort}}에서 처리할 수 없는 오류 조건을 생성했습니다. 
- {{site.data.keyword.mobilepushshort}} 서비스가 관리자의 조치가 필요한 상태입니다. 

**사용자 응답**: 요청을 재시도하십시오. 문제가 계속되면 IBM 소프트웨어 지원 부서에 문의하십시오. 



## FPWSE0011E
{: #error_fpwse0011e}

**설명**: 태그에 대한 구독이 이미 서버에 있습니다. 예를 들어, 이미 존재하는 구독을 작성하려고 했습니다. 

**사용자 응답**: 고유한 태그 이름을 사용하여 구독을 작성하십시오. 



## FPWSE0012E
{: #error_fpwse0012e}

**설명**: 태그에 대한 구독이 이미 서버에 없습니다. 이 오류는 존재하지 않는 구독을 검색하거나 삭제하는 요청이 제출되는 경우에 발생합니다. 


**사용자 응답**: 요청에 올바른 태그 이름 및 디바이스 ID를 사용하십시오. 



## FPWSE0013E
{: #error_fpwse0013e}

**설명**: 요청에 포함된 JSON 페이로드가 올바르지 않습니다. 


**사용자 응답**: JSON 페이로드가 올바른지 확인하십시오. 


## FPWSE0025E
{: #error_fpwse0025e}

**설명**: 현재 서버는 요청을 처리할 수 없습니다. 

**사용자 응답**: 나중에 요청을 다시 제출하십시오. 


## FPWSE1007E 
{: #error_fpwse1007e}

**설명**: {{site.data.keyword.mobilepushshort}} 서비스가 이 애플리케이션에 대해 사용되지 않도록 설정되었습니다. 요금 청구 관련 문제이거나 관리자가 앱을 사용하지 않음으로 설정했을 수 있습니다. 


**사용자 응답**: Bluemix 문서의 문제점 해결 주제에서 서비스 상태를 확인하고 문제점 해결 정보 또는 지원을 받는 방법에 대한 정보를 검토하십시오. 



## FPWSE1079E
{: #error_fpwse1079e}

**설명**: 조회 오퍼레이션에 제공된 오프셋 값이 올바르지 않습니다. 

**사용자 응답**: 오프셋 값이 0보다 크거나 같은지 확인하십시오. 



## FPWSE1080E 
{: #error_fpwse1080e}

**설명**: 조회 오퍼레이션에 제공된 크기 값이 올바르지 않습니다. 

**사용자 응답**: 크기 값이 0보다 큰지 확인하십시오. 



