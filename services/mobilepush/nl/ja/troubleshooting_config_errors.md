---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Web プッシュ構成エラーの解決
{: #errors}
最終更新日: 2017 年 1 月 11 日
{: .last-updated}

このセクションは、一般的に発生する Web プッシュ構成に関連したエラーを解決するためのガイドとして使用してください。`BMSPushSDK.js` からの Web プッシュ・エラーには、障害に関する情報が含まれています。 

コールバックで返されたエラーを解析するには、以下のサンプル・コードを検討してください。

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


- `applicationId` が誤って構成されていると {{site.data.keyword.mobilepushshort}} サービスへの初期要求が失敗し、それにより statusCode はゼロ (0) に設定されます。
- 状況コード 200 または 201 は、正常な応答を示しています。
- `clientSecret` が無効な場合、statusCode に 401 応答が設定されます。`response.reponse` エレメントには、エラーの説明が含まれます。
