---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Resolución de problemas
{: #errors}
Última actualización: 12 de abril de 2017
{: .last-updated}

Este tema le guía por el proceso de identificación y resolución de escenarios probables de errores con los que se puede encontrar cuando utilice el servicio de notificaciones push. 

## Resolución de problemas comunes de notificaciones push
{: #troubleshooting_notification_errors}

### Se ha producido un error de servidor interno. Póngase en contacto con el administrador. (Código de error interno: PUSHD102E)
{: #troubleshooting_notification_internal}

**Explicación**: Este error puede producirse si ha creado una instancia de push antes de noviembre de 2015.  

**Respuesta del usuario**: Para resolver el problema, suprima la instancia push y cree una nueva. Tenga en cuenta que cuando suprima la instancia de push, sus etiquetas no se conservarán.


### UnauthorizedRegistration
{: #troubleshooting_notification_unauth}

**Explicación**: Chrome Web Push no funciona con claves de Firebase Cloud Messaging (FCM). Si no puede recibir notificaciones push web en Chrome después de pasar de FCM a GCM, se debe a que el sitio web estaba configurado anteriormente para trabajar con el proyecto GCM y el nuevo proyecto se ha creado en FCM. El navegador Chrome coloca en la memoria caché las señales generadas que identifican el navegador.

**Respuesta del usuario**: Para solucionar este problema, elimine las cookies y restablezca los permisos del navegador. Este solicitará permisos para habilitar las notificaciones push. 


### No se admiten trabajadores de servicio en este navegador
{: #troubleshooting_notification_service_workers}

**Explicación**: El SDK incluido como parte de `BMSPushSDK.js` que utiliza el trabajador de servicio no está disponible. 

**Respuesta del usuario**: Se recomienda cambiar a un navegador que admita el trabajador de servicio. Las versiones admitidas de los navegadores son Firefox versión 49 o posteriores y Chrome versión 53 (64 bits) o posteriores.


### SecurityError: La operación no es segura
{: #troubleshooting_notification_insecure}

**Explicación**: Es posible que aparezca un error al habilitar la consola web en Firefox. El soporte de push de web en el servicio de notificación Push requiere que se acceda al sitio web con el protocolo `https`, no con `http`.

**Respuesta del usuario**: Se recomienda intentar conectar con el sitio web mediante `https` desde el navegador.


## Resolución de errores de configuración de push web
{: #troubleshooting_configuration_errors}

Para diagnosticar errores relacionados con la configuración de push de web, consulte el archivo `BMSPushSDK.js`. El archivo contiene información sobre el error.  

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


## Resolución de mensajes de error del servicio de notificaciones push
{: #troubleshooting_service_errors}

Se han devuelto los siguientes mensajes de error de {{site.data.keyword.mobilepushshort}} como respuesta a solicitudes de la API REST.

Ejemplo de respuesta de un error:
```
	{
		"message": "Missing APNs credentials",
     "docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
     "code":   "FPWSE0003E"
	}
```
		    {: codeblock}

Para obtener información adicional sobre un error, busque el código de error relacionado en la documentación.

### FPWSE0001E
{: #error_fpwse0001e}

**Explicación**: El recurso que está intentando consultar, como una etiqueta o suscripción, no está disponible en el servidor.

**Respuesta del usuario**: Cree el recurso que ha notificado en el mensaje. Como alternativa, proporcione el identificador correcto para consultar el recurso.


### FPWSE0002E
{: #error_fpwse0002e}

**Explicación**: El recurso que está intentado crear ya está disponible en el servidor. Puede que el recurso sea una etiqueta, una suscripción, etc.

**Respuesta del usuario**: Cree el recurso con otro identificador.


### FPWSE0003E
{: #error_fpwse0003e}

**Explicación**: La configuración de requisito previo para el servicio {{site.data.keyword.mobilepushshort}} no se ha completado. Es posible que esté intentando obtener las credenciales del servicio de notificaciones push de Apple (APNs) antes de que se hayan configurado.

**Respuesta del usuario**: Asegúrese de que el servicio {{site.data.keyword.mobilepushshort}} se ha configurado con certificados de seguridad válidos para APNs. Para obtener más información, consulte el tema sobre [Configuración de credenciales para un proveedor de notificaciones ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](t__main_push_config_provider.html){: new_window}.


### FPWSE0004E
{: #error_fpwse0004e}

**Explicación**: El cuerpo de JSON incluido en la solicitud no es válido.


**Respuesta del usuario**: Asegúrese de utilizar una sintaxis válida de JSON en la solicitud.



### FPWSE0005E
{: #error_fpwse0005e}

**Explicación**: La solicitud del servidor de {{site.data.keyword.mobilepushshort}} no es correcto o está incompleto porque el cuerpo de JSON no contiene los valores de propiedad que se necesitan para completar la solicitud de API. Por ejemplo, una contraseña no es válida o falta una señal de dispositivo.


**Respuesta del usuario**: Revise el mensaje para saber qué valor de propiedad falta o no es válido y, a continuación, proporcione la información necesaria.



### FPWSE0006E
{: #error_fpwse0006e}

**Explicación**: El cuerpo de JSON de la solicitud tiene parámetros que el servidor de {{site.data.keyword.mobilepushshort}} no conoce.


**Respuesta del usuario**: Verifique que el cuerpo de JSON en la solicitud sigue el formato de la solicitud que espera el servidor {{site.data.keyword.mobilepushshort}}. Para obtener más información, consulte las [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0007E 
{: #error_fpwse0007e}

**Explicación**: El URL de solicitud tiene una serie de consulta que tiene parámetros no reconocidos. Por ejemplo, si la solicitud para suprimir la suscripción tiene parámetros distintos de deviceId y de tagName, se puede producir este error.


**Respuesta del usuario**: Verifique que el cuerpo de JSON en la solicitud sigue el formato de la solicitud que espera el servidor {{site.data.keyword.mobilepushshort}}. Para obtener más información, consulte las [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0008E
{: #error_fpwse0008e}

**Explicación**: El URL de solicitud tiene una serie de consulta que tiene parámetros que faltan necesarios. Por ejemplo, los parámetros deviceId y tagName no se han incluido con la solicitud para suprimir la suscripción.


**Respuesta del usuario**: Verifique que el cuerpo de JSON en la solicitud sigue el formato de la solicitud que espera el servidor {{site.data.keyword.mobilepushshort}}. Para obtener más información, consulte las [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0009E
{: #error_fpwse0009e}

**Explicación**: Se ha intentado enviar notificaciones dispositivos pero no se registran dispositivos con la aplicación.

**Respuesta del usuario**: Asegúrese de que se han registrado los dispositivos con la aplicación antes de intentar enviar notificaciones.



### FPWSE0010E
{: #error_fpwse0010e}

**Explicación**: La solicitud que se ha enviado al servidor ha dado como resultado una condición de excepción. Una de las condiciones siguientes puede haber causado este error:

- Un subsistema interno que {{site.data.keyword.mobilepushshort}} utiliza no responde.
- La solicitud ha producido una condición de error que quizás no pueda manejar {{site.data.keyword.mobilepushshort}}.
- El servicio {{site.data.keyword.mobilepushshort}}
                        requiere atención por parte del administrador.

**Respuesta del usuario**: Vuelva a intentar la solicitud. Si el problema persiste, póngase en contacto con el soporte de software de IBM.



### FPWSE0011E
{: #error_fpwse0011e}

**Explicación**: La suscripción de la etiqueta ya existe en este servidor. Por ejemplo, cuando se crea una suscripción que ya existe.

**Respuesta del usuario**: Cree la suscripción con un nombre de etiqueta único.



### FPWSE0012E
{: #error_fpwse0012e}

**Explicación**: La suscripción de la etiqueta no está en el servidor. Este error se produce cuando se envía una solicitud para recuperar o suprimir una suscripción que no existe.


**Respuesta del usuario**: Utilice el nombre de etiqueta correcta y el identificador del dispositivo en la solicitud.



### FPWSE0013E
{: #error_fpwse0013e}

**Explicación**: La carga útil de JSON en la solicitud no es válida.


**Respuesta del usuario**: Asegúrese de que la carga útil de JSON es válida.


### FPWSE0025E
{: #error_fpwse0025e}

**Explicación**: El servidor no puede manejar la solicitud en este momento.

**Respuesta del usuario**: Vuelva a enviar la solicitud más tarde.


### FPWSE1007E 
{: #error_fpwse1007e}

**Explicación**: Se ha inhabilitado el servicio de {{site.data.keyword.mobilepushshort}} para esta aplicación. Esto puede ser debido a la facturación o que el administrador ha inhabilitado la app.


**Respuesta del usuario**: Consulte los temas Resolución de problemas de la documentación de Bluemix para comprobar el estado del servicio, revisar la información sobre cómo solucionar problemas y obtener ayuda.



### FPWSE1079E
{: #error_fpwse1079e}

**Explicación**: El valor de desplazamiento que se ha proporcionado para la operación de consulta no es válido.

**Respuesta del usuario**: Asegúrese de que el valor de desplazamiento es igual o mayor que cero.



### FPWSE1080E 
{: #error_fpwse1080e}

**Explicación**: El valor del tamaño que se ha proporcionado para la operación de consulta no es válido.

**Respuesta del usuario**: Asegúrese de que el valor del tamaño es mayor que cero.


