---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 웹 푸시 구성 오류 해결
{: #errors}
마지막 업데이트 날짜: 2017년 1월 11일
{: .last-updated}

이 섹션을 참조하여 일반적으로 발생하는 웹 푸시 구성 관련 오류를 해결하십시오. `BMSPushSDK.js`의 웹 푸시 오류에는 실패에 대한 정보가 포함되어 있습니다. 

콜백에 리턴된 오류를 구문 분석하려면 다음 샘플 코드를 살펴보십시오.

```
function showStatus(response) {
 if(response.statusCode == 200 || response.statusCode == 201) {
   		document.getElementById("status").innerHTML = "Response is " + response.response;
   	}
   	else if(response.statusCode == 0) {
  		if(response.response) {
  			document.getElementById("status").innerHTML = response.response;	
    		}
    		else {
    			document.getElementById("status").innerHTML = "There is a possible CORS or access issue while attempting the request.";	
   		}   		
   	}
   	else {
   		document.getElementById("status").innerHTML = "Response is " + response.response + " with the error " 
		+ response.error + " and the status code " + response.statusCode;
   	}
 	}
```
	{: codeblock}


- `applicationId`가 잘못 구성되면 {{site.data.keyword.mobilepushshort}} 서비스에 대한 초기 요청에 실패하므로 statusCode가 영(0)으로 설정됩니다.
- 상태 코드가 200 또는 201이면 성공적인 응답을 나타냅니다.
- `clientSecret`가 올바르지 않으면 401 응답이 statusCode에 설정됩니다. `response.reponse` 요소에 오류의 설명이 포함됩니다.
