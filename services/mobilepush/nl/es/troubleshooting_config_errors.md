---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Resolución de errores de configuración de push web
{: #errors}
Última actualización: 11 de enero de 2017
{: .last-updated}

Utilice esta sección como guía para la resolución de errores frecuentes relacionados con la configuración de push web. Los errores de push web procedentes de `BMSPushSDK.js` contienen información sobre el error.  

Para analizar un error devuelto en callback, observe el siguiente código de ejemplo: 

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


- Si `applicationId` no está correctamente configurado, la solicitud inicial al servicio {{site.data.keyword.mobilepushshort}} fallará, por lo que statusCode se establecerá en cero (0).
- El código de estado 200 ó 201 indica una respuesta satisfactoria. 
- En el caso de que `clientSecret` no sea válido, se establecerá la respuesta 401 en statusCode. El elemento `response.reponse` contendrá la descripción del error. 
