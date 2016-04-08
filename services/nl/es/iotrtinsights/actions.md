---

copyright:
  años: 2015,2016

---

{:shortdesc: .shortdesc}

# Tipos de acciones{: #actions}

Además de visualizar alertas en el panel de instrumentos de alertas, {{site.data.keyword.iotrtinsights_short}} soporta varios tipos de acciones desencadenadas por las reglas, como el envío de correos electrónicos y el envío de webhooks.
{: shortdesc}

## Creación de acciones {: #shared}
Puede [crear acciones directamente desde el editor de reglas](rules.html "Crear reglas"), o crear las acciones en el panel Actions y, a continuación, seleccionar las acciones al crear las reglas.

Para crear una acción en el panel Actions:
1. En la consola {{site.data.keyword.iotrtinsights_short}}, vaya a **Analytics > Actions**.
2. Pulse **Añadir nueva acción**, seleccione un tipo de acción, dé un nombre a la acción y proporcione una descripción.
3. Proporcione los parámetros necesarios para el tipo de acción que va a crear.
Tipos de acciones:  
 - [Enviar correo electrónico](#email "Enviar correo electrónico")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#ifttt "IFTTT")
4. Pulse **Aceptar** para crear la acción nueva.

La acción ahora está disponible en el [editor de reglas](rules.html#rules "Editor de reglas").



## Enviar correo electrónico{: #email}
Utilice la acción de enviar correo electrónico para enviar un correo electrónico a uno o varios destinatarios cuando se desencadena una regla.

Ejemplo: [Enviar correo electrónico](action_examples.html#emailex).

Los parámetros siguientes se utilizan para configurar la acción de envío de correo electrónico:

Parámetro | Descripción
---|---
Nombre | El nombre de la acción, que se utiliza en el panel de instrumentos Alertas.
Descripción | Una breve descripción de la acción.
Para | Una o varias direcciones de correo electrónico, separadas por comas.
Cc | Una o varias direcciones de correo electrónico, separadas por comas.
Asunto | Línea de asunto del correo electrónico. Opcionalmente, puede iniciar automáticamente el asunto con "IoT Real-Time Insight alert".

El cuerpo del correo electrónico se crea automáticamente desde el mensaje del dispositivo en el momento en que se ha desencadenado la regla.  
**Importante:** Si los datos del dispositivo contienen información confidencial, puede optar por no incluir los datos del dispositivo en el mensaje de correo electrónico y para mostrar los datos confidenciales solo en el panel de alertas.


## Webhook {: #webhook}
Utilice la acción webhook para realizar una solicitud HTTP en un servicio web habilitado por webhook cuando se activa una alerta. Por ejemplo, un webhook podría utilizarse para abrir una solicitud de servicio para un activo si un sensor del dispositivo informa de una lectura anormal.

Ejemplo: [Utilice webhook para publicar en Slack](action_examples.html#webhookex).

Los parámetros siguientes se utilizan para configurar una acción webhook:

Parámetro | Descripción
---|---
Nombre | El nombre de la acción, que se utiliza en el panel de instrumentos Alertas.
Descripción | Una breve descripción de la acción.
URL | El URL del servidor de destino habilitado por webhook. **Consejo:** Puede utilizar [sustitución de variables](#variable_substitution) para incluir de forma dinámica datos adicionales en el URL.
Método | El tipo de llamada webhook que se ejecutará. Seleccione uno de los tipos siguientes: GET, HEAD, OPTIONS, PATCH, PUT, POST o DELETE.
Nombre de usuario | Lo incluirá el servicio web si es necesario.
Contraseña | Lo incluirá el servicio web si es necesario. **Importante:** La contraseña se envía en texto simple.
Cabecera | Las cabeceras se componen de la clave y de los pares de valores. **Consejo:** Puede utilizar [sustitución de variables](#variable_substitution) para incluir de forma dinámica datos adicionales en la cabecera.
Tipo de contenido | El tipo de contenido del cuerpo: JSON, XML, formulario WWW URL codificado, o texto sin formato. Disponible para los métodos OPTIONS, PATCH, PUT, POST y DELETE.
Cuerpo | El cuerpo de la llamada webhook. Disponible para los métodos OPTIONS, PATCH, PUT, POST y DELETE. De forma predeterminada, el campo de cuerpo se prerrellena con todas las variables listadas en [sustitución de variables](#variable_substitution). Seleccione **Utilizar cuerpo de mensaje personalizado** para editar el contenido del campo de cuerpo. **Importante:** El servidor de webhook puede necesitar que determinados campos específicos se incluyan en el cuerpo. Por ejemplo, un webhook Slack debe contener el campo "text".   



## Node-RED {: #nodered}
Utilice la acción Node-RED para conectarse a una aplicación Node-RED cuando se desencadene una regla. Para obtener más información sobre el uso de Node-RED, consulte [Creación de aplicaciones con la aplicación de inicio Internet of Things](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500).

Ejemplo: [Utilice Node-RED para enviar un mensaje de texto](action_examples.html#noderedex).

Los parámetros siguientes se utilizan para configurar una acción Node-RED:

Parámetro | Descripción
---|---
Nombre | El nombre de la acción, que se utiliza en el panel de instrumentos Alertas.
Descripción | Una breve descripción de la acción.
URL | El URL del nodo de entrada HTTP Node-RED de destino.
Nombre de usuario | Lo incluye si es necesario el servicio Node-RED.
Contraseña | Lo incluye si es necesario el servicio Node-RED. **Importante:** La contraseña se envía en texto simple.
Cuerpo | De forma predeterminada, el campo de cuerpo se prerrellena con todas las variables listadas en [sustitución de variables](#variable_substitution). Seleccione **Utilizar cuerpo de mensaje personalizado** para editar el contenido del campo de cuerpo.

## IFTTT {: #ifttt}
Utilice la acción IFTTT para que se desencadene una receta IFTTT cuando se desencadene una regla. Para obtener más información sobre el desencadenamiento de acciones Real-Time Insights como recetas IFTTT, consulte [Canal de Maker](https://ifttt.com/maker) en el sitio IFTTT.

Ejemplo: [Utilice IFTTT para publicar una tarjeta Trello](action_examples.html#iftttex).

Los parámetros siguientes se utilizan para configurar una acción IFTTT:

Parámetro | Descripción
---|---
Nombre | El nombre de la acción, que se utiliza en el panel de instrumentos Alertas.
Descripción | Una breve descripción de la acción.
Clave | La clave Canal de Maker a utilizar para desencadenar el suceso.
Suceso | El nombre de suceso que ha configurado como desencadenante para el Suceso de Maker. Puede crear varias recetas con desencadenantes distintos, cada uno de ellos con un nombre de suceso distinto.
Valor 1-3 | Puede pasar cualquier contenido en estos parámetros, que se pasan a la acción en la receta IFTTT. **Consejo:** Puede utilizar [sustitución de variables](#variable_substitution) para incluir de forma dinámica datos adicionales con la cabecera.
## Sustitución de variables{: #variable_substitution}
Incluir las siguientes sustituciones de variables para incluir de forma dinámica datos de dispositivo. La variable se debe envolver entre llaves dobles.

Variable | Descripción
---|---
**URL, cabecera y cuerpo** |
`{{timestamp}}` | La indicación de fecha y hora del mensaje
`{{tenantId}}` | El ID del servicio de Real-Time Insights
`{{deviceId}}` | El ID del dispositivo
`{{ruleName}}` | El nombre de la regla que incluye la acción
**Solo el cuerpo** |
`{{ruleDescription}}`| La descripción de la regla que incluye la acción
`{{ruleCondition}}` | La condición de la regla que ha desencadenado la acción
`{{message}}` | El mensaje de dispositivo en bruto que incluía el valor de punto de datos que ha desencadenado la regla
