---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Resolvendo erros de configuração Push da web
{: #errors}
Última atualização: 11 de janeiro de 2017
{: .last-updated}

Use esta seção como um guia para resolver erros relacionados à configuração Push da web que normalmente ocorrem. Os erros de push da web do `BMSPushSDK.js` contêm informações sobre a falha. 

Para analisar um erro retornado no retorno de chamada, considere o código de amostra a seguir:

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


- Se o `applicationId` estiver configurado incorretamente, a solicitação inicial para o serviço {{site.data.keyword.mobilepushshort}} falhará, por conseguinte o statusCode será configurado como zero (0).
- Um código de status de 200 ou 201 denota uma resposta bem-sucedida.
- No caso de o `clientSecret` ser inválido, uma resposta 401 será configurada no statusCode. O elemento `response.reponse` conterá uma descrição do erro.
