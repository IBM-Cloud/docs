---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 解析 Web 推送配置錯誤
{: #errors}
前次更新：2017 年 1 月 11 日
{: .last-updated}

使用本節作為指引來解析一般發生的 Web 推送配置相關錯誤。`BMSPushSDK.js` 的 Web 推送錯誤包含失敗的資訊。 

若要剖析在回呼時傳回的錯誤，請考量下列範例程式碼：

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


- 如果未正確配置 `applicationId`，{{site.data.keyword.mobilepushshort}} 服務的起始要求將會失敗，因此 statusCode 將設為零 (0)。
- 狀態碼 200 或 201 表示順利回應。
- 案例 `clientSecret` 無效，將在 statusCode 上設定 401 回應。`response.reponse` 元件將包含錯誤說明。
