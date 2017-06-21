---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Resolución de problemas de {{site.data.keyword.contdelivery_short}}
{: #ts_cd}

Aquí encontrará respuestas a preguntas comunes sobre la resolución de problemas al utilizar {{site.data.keyword.contdelivery_full}}.
{:shortdesc}


## No se puede autorizar con GitHub
{: #cannot_authorize_github}

No está autorizado con GitHub.
{:shortdesc}

Si tiene está autorizado por {{site.data.keyword.Bluemix_notm}} para acceder a la cuenta de GitHub, puede producirse uno de estos problemas:
{: tsSymptoms}

 * Cuando intente añadir la integración de herramientas de GitHub a la cadena de herramientas, la integración de herramientas no se añade.
 * El conducto no se ejecuta automáticamente cuando se envían cambios en el repositorio de GitHub o GitHub Enterprise.

{{site.data.keyword.Bluemix_notm}} no está autorizado para acceder a GitHub.  
{: tsCauses}
 
Si configura la integración de esta herramienta de GitHub mientras crea la cadena de herramientas, siga estos pasos:
{: tsResolve}
 
  1. En la sección Integraciones configurables, pulse **GitHub**. 
  1. Si está creando la cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y no ha autorizado a {{site.data.keyword.Bluemix_notm}} acceso a GitHub, pulse **Autorizar** para ir al sitio web de GitHub. 
  1. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Autorizar aplicación** para permitir que {{site.data.keyword.Bluemix_notm}} acceda a su cuenta de GitHub. Si tiene una sesión activa de GitHub pero no ha introducido recientemente su contraseña, es posible que se le solicite que introduzca la contraseña de GitHub para confirmarla.
  
Si ya tiene una cadena de herramientas, actualice la configuración de la integración de herramientas de GitHub:

 1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse sobre la cadena de herramientas para abrir la página Visión general correspondiente. Si lo prefiere, en la página Visión general de la app, tarjeta Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Visión general**.
 1. En la tarjeta GitHub, pulse el menú y pulse **Configurar**.
 1. Actualice los valores de configuración para autorizar a {{site.data.keyword.Bluemix_notm}} para acceder a GitHub. Pulse **Autorizar** para ir al sitio web de GitHub. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Autorizar aplicación** para permitir que {{site.data.keyword.Bluemix_notm}} acceda a su cuenta de GitHub. Si tiene una sesión activa de GitHub pero no ha introducido recientemente su contraseña, es posible que se le solicite que introduzca la contraseña de GitHub para confirmarla.
 1. Cuando haya terminado de configurar los ajustes, pulse **Guardar integración**.


## La integración de herramientas no está configurada
{: #tool_integration_error}

Después de configurar una integración de herramientas para su cadena de herramientas, se muestra el error `Error de configuración` en su tarjeta de la herramienta.
{:shortdesc}

Después de configurar una integración de herramientas, puede ver su tarjeta de herramienta en la página Visión general de la cadena de herramientas y ver que la configuración ha fallado.
{: tsSymptoms}

 ![Error de configuración](images/tool_setup_failed.png)
 
Cuando añade una integración de herramientas, la cadena de herramientas se comunica con la herramienta representada mediante la integración de herramientas para suministrar los recursos necesarios y asociarlos con la cadena de herramientas. Si se produce un error durante el proceso de configuración o si la comunicación entre la cadena de herramientas y la herramienta no se establece correctamente, la integración de herramientas se coloca en un estado de error.
{: tsCauses}

Vuelva a configurar la integración de herramientas:
{: tsResolve}

1. En su tarjeta de herramienta, mueva el cursor sobre el mensaje `Error de configuración` y pulse **Volver a configurar**.

 ![Botón Volver a configurar](images/tool_reconfigure.png)
 
1. Asegúrese de utilizar parámetros de configuración válidos. Si el error está causado por una configuración no válida, se muestra un mensaje de error; por ejemplo, `La integración se ha podido configurar. Compruebe la configuración y vuelva a intentarlo. Razón: api_key:fakeKey no válido`. Actualice los valores de la integración de herramientas y pulse **Guardar integración**.
1. Si el error está causado por un problema de comunicación, pulse **Guardar integración** para intentarlo de nuevo.
