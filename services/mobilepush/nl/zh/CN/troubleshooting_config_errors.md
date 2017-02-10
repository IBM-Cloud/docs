---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 解决 Web 推送配置错误
{: #errors}
上次更新时间：2017 年 1 月 11 日
{: .last-updated}

使用本部分作为指南，解决经常发生的 Web 推送配置相关错误。来自 `BMSPushSDK.js` 的 Web 推送错误包含失败的相关信息。 

要解析回调中返回的错误，请考虑以下样本代码：

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


- 如果错误地配置 `applicationId`，那么对 {{site.data.keyword.mobilepushshort}} 服务的初始请求会失败，因为 statusCode 将设置为零 (0)。
- 200 或 201 的状态码表示响应成功。
- 如果 `clientSecret` 无效，那么会在 statusCode 上设置 401 响应。`response.reponse` 元素将包含错误的描述。
