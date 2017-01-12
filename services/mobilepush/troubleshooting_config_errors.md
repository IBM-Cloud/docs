---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Resolving web push configuration errors
{: #errors}
Last updated: 11 January 2017
{: .last-updated}

Use this section as a guide to resolve commonly occurring web push configuration related errors. Web push errors from the `BMSPushSDK.js` contain information on the failure. 

To parse an error returned in the callback, consider the following sample code:

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


- If the `applicationId` is incorrectly configured, the initial request to {{site.data.keyword.mobilepushshort}} service will fail, hence the statusCode will be set to zero (0).
- A status code of 200 or 201 denotes a successful response.
- In case the `clientSecret` is invalid, a 401 response will be set on the statusCode. The `response.reponse` element will contain description of the error.
