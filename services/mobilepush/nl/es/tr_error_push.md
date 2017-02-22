---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Mensajes de error del servicio {{site.data.keyword.mobilepushshort}}
{: #errors}
Última actualización: 16 de enero de 2017
{: .last-updated}


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

## FPWSE0001E
{: #error_fpwse0001e}

**Explicación**: El recurso que está intentando consultar, como una etiqueta o suscripción, no está disponible en el servidor.

**Respuesta del usuario**: Cree el recurso que ha notificado en el mensaje. Como alternativa, proporcione el identificador correcto para consultar el recurso.


## FPWSE0002E
{: #error_fpwse0002e}

**Explicación**: El recurso que está intentado crear ya está disponible en el servidor. Puede que el recurso sea una etiqueta, una suscripción, etc.

**Respuesta del usuario**: Cree el recurso con otro identificador.


## FPWSE0003E
{: #error_fpwse0003e}

**Explicación**: La configuración de requisito previo para el servicio {{site.data.keyword.mobilepushshort}} no se ha completado. Es posible que esté intentando obtener las credenciales del servicio de notificaciones push de Apple (APN) antes de que se hayan configurado.

**Respuesta del usuario**: Asegúrese de que el servicio {{site.data.keyword.mobilepushshort}} se ha configurado con certificados de seguridad válidos para los APN. Para obtener más información, consulte el tema sobre [Configuración de credenciales para APN ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](t_push_provider_ios.html "icono de enlace externo"){: new_window}.


## FPWSE0004E
{: #error_fpwse0004e}

**Explicación**: El cuerpo de JSON incluido en la solicitud no es válido.


**Respuesta del usuario**: Asegúrese de utilizar una sintaxis válida de JSON en la solicitud.



## FPWSE0005E
{: #error_fpwse0005e}

**Explicación**: La solicitud del servidor de {{site.data.keyword.mobilepushshort}} no es correcto o está incompleto porque el cuerpo de JSON no contiene los valores de propiedad que se necesitan para completar la solicitud de API. Por ejemplo, una contraseña no es válida o falta una señal de dispositivo.


**Respuesta del usuario**: Revise el mensaje para saber qué valor de propiedad falta o no es válido y, a continuación, proporcione la información necesaria.



## FPWSE0006E
{: #error_fpwse0006e}

**Explicación**: El cuerpo de JSON de la solicitud tiene parámetros que el servidor de {{site.data.keyword.mobilepushshort}} no conoce.


**Respuesta del usuario**: Verifique que el cuerpo de JSON en la solicitud sigue el formato de la solicitud que espera el servidor {{site.data.keyword.mobilepushshort}}. Para obtener más información, consulte las [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/ "icono de enlace externo"){: new_window}.



## FPWSE0007E 
{: #error_fpwse0007e}

**Explicación**: El URL de solicitud tiene una serie de consulta que tiene parámetros no reconocidos. Por ejemplo, si la solicitud para suprimir la suscripción tiene parámetros distintos de deviceId y de tagName, se puede producir este error.


**Respuesta del usuario**: Verifique que el cuerpo de JSON en la solicitud sigue el formato de la solicitud que espera el servidor {{site.data.keyword.mobilepushshort}}. Para obtener más información, consulte las [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/ "icono de enlace externo"){: new_window}.



## FPWSE0008E
{: #error_fpwse0008e}

**Explicación**: El URL de solicitud tiene una serie de consulta que tiene parámetros que faltan necesarios. Por ejemplo, los parámetros deviceId y tagName no se han incluido con la solicitud para suprimir la suscripción.


**Respuesta del usuario**: Verifique que el cuerpo de JSON en la solicitud sigue el formato de la solicitud que espera el servidor {{site.data.keyword.mobilepushshort}}. Para obtener más información, consulte las [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/ "icono de enlace externo"){: new_window}.



## FPWSE0009E
{: #error_fpwse0009e}

**Explicación**: Se ha intentado enviar notificaciones dispositivos pero no se registran dispositivos con la aplicación.

**Respuesta del usuario**: Asegúrese de que se han registrado los dispositivos con la aplicación antes de intentar enviar notificaciones.



## FPWSE0010E
{: #error_fpwse0010e}

**Explicación**: La solicitud que se ha enviado al servidor ha dado como resultado una condición de excepción. Una de las condiciones siguientes puede haber causado este error:

- Un subsistema interno que {{site.data.keyword.mobilepushshort}} utiliza no responde.
- La solicitud ha producido una condición de error que quizás no pueda manejar {{site.data.keyword.mobilepushshort}}.
- El servicio {{site.data.keyword.mobilepushshort}}
                        requiere atención por parte del administrador.

**Respuesta del usuario**: Vuelva a intentar la solicitud. Si el problema persiste, póngase en contacto con el soporte de software de IBM.



## FPWSE0011E
{: #error_fpwse0011e}

**Explicación**: La suscripción de la etiqueta ya existe en este servidor. Por ejemplo, cuando se crea una suscripción que ya existe.

**Respuesta del usuario**: Cree la suscripción con un nombre de etiqueta único.



## FPWSE0012E
{: #error_fpwse0012e}

**Explicación**: La suscripción de la etiqueta no está en el servidor. Este error se produce cuando se envía una solicitud para recuperar o suprimir una suscripción que no existe.


**Respuesta del usuario**: Utilice el nombre de etiqueta correcta y el identificador del dispositivo en la solicitud.



## FPWSE0013E
{: #error_fpwse0013e}

**Explicación**: La carga útil de JSON en la solicitud no es válida.


**Respuesta del usuario**: Asegúrese de que la carga útil de JSON es válida.



## FPWSE1007E 
{: #error_fpwse1007e}

**Explicación**: Se ha inhabilitado el servicio de {{site.data.keyword.mobilepushshort}} para esta aplicación. Esto puede ser debido a la facturación o que el administrador ha inhabilitado la app.


**Respuesta del usuario**: Consulte los temas Resolución de problemas de la documentación de Bluemix para comprobar el estado del servicio, revisar la información sobre cómo solucionar problemas y obtener ayuda.



## FPWSE1079E
{: #error_fpwse1079e}

**Explicación**: El valor de desplazamiento que se ha proporcionado para la operación de consulta no es válido.

**Respuesta del usuario**: Asegúrese de que el valor de desplazamiento es igual o mayor que cero.



## FPWSE1080E 
{: #error_fpwse1080e}

**Explicación**: El valor del tamaño que se ha proporcionado para la operación de consulta no es válido.

**Respuesta del usuario**: Asegúrese de que el valor del tamaño es mayor que cero.



