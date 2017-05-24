---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloud Analytics
{: #cloud_analytics}

Al utilizar cloud analytics de {{site.data.keyword.iot_short}}, especifique condiciones de reglas basadas en datos de dispositivos en tiempo real y que activen alertas y acciones opcionales cuando se cumplan.    
{: shortdesc}

Por ejemplo, puede crear una regla para asegurarse de que cuando el dispositivo se ha eliminado o cuando se dispara la temperatura del dispositivo, se envíe una alerta al panel de control del dispositivo de un usuario, y se envíe un correo electrónico al administrador.

## Antes de empezar
{: #byb}
Asegúrese de que las propiedades de dispositivos que desea utilizar como condiciones en las reglas se hayan correlacionado con esquemas. Consulte [Conexión de dispositivos](iotplatform_task.html) y [Creación de esquemas](im_schemas.html) para obtener más información.

Consulte también la receta [Utilización de reglas y acciones con {{site.data.keyword.iot_short}} Cloud Analytics ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window} para comprender las reglas y acciones que se utilizan en Cloud Analytics.

## Gestión de reglas y acciones  
{: #managing_rules}

Utilice el panel de control **Reglas** para crear y gestionar reglas y acciones para su organización.

Para obtener una visión general de las reglas y las alertas que se han desencadenado para los dispositivos, utilice los paneles siguientes:

 |Nombre del tablero | Descripción |  
 |:---|:---|  
  |Analítica centrada en las reglas | Muestra las reglas para su organización. Las alertas desencadenadas de lista de tarjetas adicionales, los dispositivos asociados, las propiedades de dispositivos y la información de alertas. |  
 |Analítica centradas en los dispositivos | Muestra los dispositivos conectados a su organización. Las tarjetas adicionales muestran alertas para un dispositivo seleccionado, información para un dispositivo seleccionado, propiedades de dispositivos e información de alerta. |

 Para obtener más información sobre los paneles de analítica predeterminados, consulte [Visualización de datos en tiempo real utilizando paneles y tarjetas](data_visualization.html#default_boards).


## Creación de reglas
{: #rules}

Las reglas son puntos de decisión basadas en condiciones que coinciden con los datos de dispositivos en tiempo real con valores de umbral predefinidos u otros datos de propiedades para desencadenar una alerta si se cumple una condición. Además de la alerta que se muestra en el panel de control de {{site.data.keyword.iot_short}}, puede añadir una o varias acciones para ejecutar la lógica empresarial cuando se desencadena una regla.

**Importante:** Para poder crear reglas para un tipo de dispositivo, debe crear un esquema para el tipo de dispositivo. Para obtener más información, consulte [Crear esquemas de tipo de dispositivo](im_schemas.html).

Para crear una regla:
1. En el panel de control de {{site.data.keyword.iot_short}}, vaya a **Reglas**.
2. Pulse **Crear una regla**, dé un nombre a la regla, proporcione una descripción, seleccione un tipo de dispositivo al que se aplique la regla y, a continuación, pulse **Siguiente**.  
3. Para configurar la lógica de la regla, añada una o varias condiciones IF para utilizarlas como desencadenantes para la regla.  
Puede añadir condiciones en filas paralelas para aplicarlas como condiciones OR, o puede añadir condiciones en columnas secuenciales para aplicarlas como condiciones AND.  
**Importante:** Para desencadenar una condición que compara dos propiedades o para desencadenar dos o más condiciones de propiedades que se combinan secuencialmente utilizando AND, deben incluirse los puntos de datos desencadenantes en el mismo mensaje de dispositivos. Si los datos se reciben en más de un mensaje, la condición o las condiciones secuenciales no se desencadenarán.  
**Ejemplos:**   
Una regla sencilla puede desencadenar una alerta si un valor de parámetro es mayor que un valor especificado:
Condición = `temp_cpu>80`  
Una regla más compleja puede desencadenarse cuando se cumple una combinación de umbrales:
Condición = `temp_cpu>60 AND cpu_load>90`   

4. Configure requisitos desencadenantes condicionales para la regla.  
Para controlar el número de alertas desencadenadas para una regla durante un periodo de tiempo, puede configurar requisitos desencadenantes condicionales para la regla.  
**Importante:** El desencadenante condicional actúa en cualquier condición de la regla. Por ejemplo, si una regla tiene cinco conjuntos de condiciones paralelas distintas utilizando OR, cada condición que sea true cuenta hacia el recuento desencadenante condicional.
Para establecer el desencadenante condicional para una regla:
 1. En el editor de reglas, pulse el enlace predeterminado **Desencadenar cada vez que se cumplan las condiciones** para abrir el recuadro de diálogo de requisitos de frecuencia establecido.
 2. Seleccione y configure el desencadenante condicional que desea utilizar en la regla.
 <ul>
 <li>Desencadenar cada vez que se cumplan las condiciones</li>
 <li>Desencadenar si las condiciones se cumplen N veces en la *Unidad de tiempo* M</li>
 </ul>  
 Para obtener una descripción más detallada de los desencadenantes condicionales, consulte [Desencadenante de reglas condicionales](#conditional "Visión general de desencadenante condicional").
5. Cree o seleccione una o varias acciones que se producen si se cumplen las condiciones de la regla.  
Para obtener más información sobre las acciones, consulte [Utilización de acciones con las reglas](#shared "Crear acciones").   
 Por ejemplo: Una acción puede ser enviar un correo electrónico o publicar un webhook.
3. **Opcional:** Seleccionar una prioridad de alerta para la regla.  
 La prioridad se utiliza para clasificar las alertas que se muestran en el tablero **Herramientas de análisis basadas en reglas**. La prioridad predeterminada es Low.
6. Cuando esté satisfecho con la regla, pulse **Guardar** para guardar sin activar o pulse **Activar** para guardar y activar la regla.

Su regla se ha creado. Si activa la regla, cuando se cumplan las condiciones de la regla, se añadirá una alerta al tablero **Paneles > Herramientas de análisis basadas en reglas**, y se ejecutará cualquier acción de regla.

## Desencadenante de reglas condicionales
{: #conditional}

Para controlar el número de alertas desencadenadas para una regla durante un periodo de tiempo, puede configurar requisitos desencadenantes condicionales para la regla.

En función de la frecuencia de mensajes y de las condiciones de las reglas, una regla puede desencadenarse un gran número de veces una vez que se cumpla una condición de desencadenante. Por ejemplo, si la condición es `temp >= 90` y la temperatura aumenta y se estabiliza en 91, la regla se desencadena con cada mensaje entrante. En función de la frecuencia de los mensajes de dispositivos y de las acciones que la regla tenga establecido ejecutar, es posible que este volumen de alertas llene rápidamente su bandeja de entrada de correo electrónico o desborde un canal de información de Twitter con mensajes que no proporcionan ningún valor adicional.

**Importante:** El desencadenante condicional actúa en cualquier condición de la regla. Por ejemplo, si una regla tiene cinco conjuntos de condiciones paralelas distintas utilizando OR, cada condición que se cumpla cuenta hacia el recuento desencadenante condicional.

Condición | Descripción
------------- | -------------
Desencadenar cada vez que se cumplan las condiciones | La regla se desencadena cada vez que se cumplen las condiciones de reglas.
Desencadenar si se cumplen las condiciones *N* veces en *M* *días/horas/minutos/personalizado* | La regla se desencadena cuando se cumplen las condiciones *N* veces en el intervalo de tiempo seleccionado y no se desencadenará de nuevo hasta que haya pasado el periodo de tiempo configurado. </br>Ejemplo: El requisito desencadenante condicional =`Desencadenar solo una vez si las condiciones se cumplen cuatro veces en 30 minutos`. El dispositivo envía un mensaje nuevo cada cinco minutos. A las 12:00, la temperatura supera inicialmente los 90 grados, lo que cumple la condición. Se inicia el contador desencadenante condicional, pero la regla no se ha desencadenado todavía.  Tras 15 minutos y después de que se hayan recibido tres mensajes más que indican que `temp > 90`, se desencadenará la regla. La regla no se desencadenará durante otros 15 minutos, independientemente de la temperatura.
Desencadenar sólo la primera vez que se cumplan las condiciones y restablecer cuando ya no se cumplan las condiciones. | La regla se desencadena cuando se cumplen las condiciones, pero no se desencadenará para mensajes consecutivos que también cumplen las condiciones. Los criterios desencadenantes los restablece el primer mensaje que no cumple las condiciones de reglas.
Desencadenar si las condiciones persisten para *M* *days/hours/minutes/custom*. | La regla se desencadena después del intervalo de tiempo seleccionado si todos los puntos de datos recibidos durante el intervalo de tiempo cumplen las condiciones o si no se reciben puntos de datos adicionales. El intervalo de tiempo se inicia cuando se cumplen inicialmente las condiciones.



## Utilización de acciones en las reglas
{: #shared}

Además de visualizar alertas en el panel de control de alertas, {{site.data.keyword.iot_short}} da soporte a varios tipos de acciones desencadenadas por reglas, como el envío de correos electrónicos y la publicación de webhooks.

Puede crear acciones directamente en el editor de reglas o crear las acciones en el separador Acciones y, a continuación, seleccionar las acciones al crear las reglas.

Para crear una acción en el separador Acciones:
1. En el panel de control de {{site.data.keyword.iot_short}}, vaya a **Reglas**.
2. En el panel de control Reglas, seleccione el separador **Acciones**.
2. Pulse **Crear una acción**, dé un nombre y una descripción a la acción y seleccione un tipo de acción y, a continuación, pulse **Siguiente**.
3. Proporcione los parámetros necesarios para el tipo de acción que está creando.  
Tipos de acciones:  
 - [Enviar correo electrónico](#email "Enviar correo electrónico")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. Pulse **Aceptar** para crear la acción nueva.

La acción ahora está disponible en el editor de reglas.

**Nota:** Los ejemplos siguientes representan una acción que notifica a un ingeniero de servicio cuándo la temperatura, representada por la propiedad `temp_cpu` de un dispositivo, supera los 80 grados, utilizando la siguiente condición de regla: `temp_cpu >= 80`

### Enviar correo electrónico  
{: #email}
Utilice la acción send email para enviar un correo electrónico a uno o varios destinatarios cuando se desencadena una regla.

Ejemplo: [Enviar correo electrónico](#emailex).

Los parámetros siguientes se utilizan para configurar la acción send email:

Parámetro | Descripción
---|---
Nombre | El nombre de la acción, que se utiliza en el panel de instrumentos Alertas.
Descripción | Una breve descripción de la acción.
Asunto | Línea de asunto del correo electrónico. La línea de asunto predeterminada es "IBM Watson IoT Alert: Mail action".
Para | Seleccione esta opción para enviar la alerta sólo a usted mismo o a una lista separada por comas de direcciones de correo electrónico. Si selecciona enviarlo a sí mismo, el correo electrónico se envía a la dirección de correo electrónico del {{site.data.keyword.iot_short}} como ha iniciado sesión en ella.
Cc | Ninguno, o una lista separada por comas de direcciones de correo electrónico.
El cuerpo del correo electrónico se crea automáticamente desde el mensaje del dispositivo en el momento en que se desencadenó la regla.  
**Importante:** De forma predeterminada, los mensajes de correo electrónico no incluyen datos de dispositivo que puedan incluir información confidencial. Cambie el valor **Incluir datos** para que incluya datos de dispositivo.

#### Ejemplo: Utilizar send email
{: #emailex}

En este ejemplo, la acción está configurada para utilizar la característica send email para enviar un correo electrónico al ingeniero de servicio principal y enviar también un correo electrónico de copia de seguridad a su gestor.

Para crear la acción de correo electrónico:
1. En el panel de control de {{site.data.keyword.iot_short}}, vaya a **Reglas**.
2. Pulse **Crear una acción**.
4. Especifique el nombre de acción `Enviar correo electrónico de solicitud de servicio`.
5. Especifique la descripción `Enviar un correo electrónico al ingeniero de servicio y a su gestor`.
3. Seleccione el tipo **Correo electrónico**.
6. En el campo Para, seleccione **Personas específicas** y especifique `service.engineer@company.com`.
7. En el campo CC, seleccione **Personas específicas** y especifique: `service.manager@company.com`.
8. En la línea de asunto, especifique: `Servicio necesario.`
10. Seleccione **Incluir datos** para incluir los datos de dispositivo en el correo electrónico.
11. Pulse **Finalizar** para guardar la acción.  


### IFTTT  
{: #ifttt}

Utilice la acción IFTTT para desencadenar una receta IFTTT cuando se desencadene una regla. Para obtener más información sobre el desencadenamiento de acciones como recetas IFTTT, consulte [Canal de Maker ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://ifttt.com/maker){: new_window} en el sitio IFTTT.

Ejemplo: [Utilice IFTTT para publicar una tarjeta Trello](#iftttex).

Los parámetros siguientes se utilizan para configurar una acción IFTTT:

Parámetro | Descripción
---|---
Nombre | El nombre de la acción, que se utiliza en el panel de instrumentos Alertas.
Descripción | Una breve descripción de la acción.
Clave | La clave Canal de Maker a utilizar para desencadenar el suceso.
Suceso | El nombre de suceso que ha configurado como desencadenante para el Suceso de Maker. Puede crear varias recetas con desencadenantes distintos, cada uno de ellos con un nombre de suceso distinto.
Valor 1-3 | Puede pasar cualquier contenido en estos parámetros, que se pasan a la acción en la receta IFTTT. **Consejo:** Puede utilizar [sustitución de variables](#variable_substitution) para incluir de forma dinámica datos adicionales en la cabecera.

#### Ejemplo: Utilice IFTTT para publicar una tarjeta Trello {: #iftttex}

En este ejemplo, la acción está configurada para utilizar IFTTT para publicar una tarjeta a una lista de solicitudes de servicio en Trello.

Para crear la publicación de una tarjeta en la acción Trello:
1.	En IFTTT, conecte con el canal Trello.
2.	En IFTTT, conecte al canal de Maker. Tome nota de la clave IFTTT. Necesita esta clave para conectarse a IFTTT desde {{site.data.keyword.iot_short_notm}}.
5.	En IFTTT, crear una receta:
 1. Pulse **THIS**.
 2. Seleccione el canal **Maker**.  
 2. Pulse **Recibir una solicitud web**.
 3. Especifique el nombre de suceso `post-Trello-card`.
 4. Pulse **THAT**.
 5. Seleccione el canal **Trello**.
 6. Seleccione el tablero Trello en el que se creará la tarjeta.
 7. Especifique un nombre de lista en la que se añaden las tarjetas.
 8. Edite el título y la descripción.
 9. Asigne los miembros @service.engineer y @service.manager.
 8. Pulse **Crear acción**.   
3. En el panel de instrumentos {{site.data.keyword.iot_short}}, vaya a **Reglas > Acciones** y cree una acción nueva que tenga los parámetros siguientes:
<ul>
<li>Tipo: **IFTTT**</li>
<li>Nombre: `Publicar tarjeta de solicitud de servicio`</li>
<li>Descripción: `Utilice IFTTT para publicar una tarjeta en la lista de solicitudes de servicio en Trello.`</li>
<li>Clave: Su clave IFTTT</li>
<li>Suceso: `post-Trello-card`</li>
<li>Opcionalmente, añada valores para el Valor 1-3. **Consejo:** Puede utilizar [sustitución de variables](#variable_substitution) para incluir de forma dinámica datos de dispositivo.</li>
</ul>
4. Pulse **Aceptar** para guardar la acción.


### Node-RED
{: #nodered}

Utilice la acción Node-RED para conectarse a una aplicación Node-RED cuando se desencadene una regla. Para obtener más información sobre cómo utilizar Node-RED, consulte [Creación de apps con la aplicación de inicio Internet of Things](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html).

Ejemplo: [Utilice Node-RED para enviar un mensaje de texto](#noderedex).

Los parámetros siguientes se utilizan para configurar una acción Node-RED:

Parámetro | Descripción
---|---
Nombre | El nombre de la acción, que se utiliza en el panel de instrumentos Alertas.
Descripción | Una breve descripción de la acción.
URL | El URL del nodo de entrada HTTP de Node-RED de destino.
Nombre de usuario | Lo incluye si es necesario el servicio Node-RED.
Contraseña | Lo incluye si es necesario el servicio Node-RED. **Importante:** La contraseña se envía en texto sin cifrar.
Cuerpo | De forma predeterminada, el campo de cuerpo se prerrellena con todas las variables listadas en [sustitución de variables](#variable_substitution).

#### Ejemplo: Utilice Node-RED para enviar un mensaje de texto
{: #noderedex}

En este ejemplo, la acción está configurada para utilizar Node-RED con un nodo Twilio para enviar un mensaje de texto al ingeniero de servicio.

Para crear la acción enviar mensaje de texto:
1. En Twilio, localice o cree un nuevo Servicio de mensajería a utilizar para enviar mensajes de texto desde la cuenta de Twilio. Para obtener información, consulte la [documentación de Twilio ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.twilio.com/help){: new_window}.
2. En Bluemix, configure y acceda a la cuenta de Node-RED con el URL de Node-RED `http://mynodered.mybluemix.net/red/`. Para obtener más información, consulte el tema [Creación de apps con el iniciador de Node-RED](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) en la documentación de Bluemix.
3. En Node-RED, cree un flujo simple de dos nodos, como por ejemplo [RTI-alert]->[SMS].  
Donde el primer nodo es un nodo http, y el segundo es un nodo twilio.
 1. Añada el nodo de entrada "http" y configúrelo con los atributos siguientes:
  <ul>
  <li>Método: POST</li>
  <li>URL: `RTI-alert`</li>
  <li>Nombre: RTI Action</li>
  </ul>
  2. Añada un nodo de salida "http response" y conéctelo a los de entrada "http" arrastrando entre el puerto de salida de uno y el puerto de entrada del otro.
  3. Añada un nodo de salida "twilio" y configúrelo con los atributos siguientes:
  <ul>
  <li>Servicio: **Servicio externo**</li>
  <li>Twilio: Añadir una nueva twilio-api</li>
  <li>SMS para: `Número de teléfono para el ingeniero de servicio`</li>
  <li>Nombre: **SMS**</li>
  </ul>
  4. Conecte los nodos entre sí  
  Conecte los nodos http y twilio entre sí arrastrando entre el puerto de salida de uno y el puerto de entrada del otro.
  5. Pulse el botón **Desplegar** para desplegar el flujo para el servidor
4. En el panel de instrumentos {{site.data.keyword.iot_short}}, vaya a **Reglas > Acciones** y cree una acción nueva que tenga los parámetros siguientes:
 - Tipo: **Node-RED**
 - Nombre: `Enviar texto mediante Node-RED y Twilio`
 - Descripción: `Enviar una alerta de mensaje de texto al ingeniero de servicio.`
 - URL: `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```json
 {"text":"*Un dispositivo necesita su atención*\n Hora: {{timestamp}}\n {{site.data.keyword.iot_short}} instancia: {{tenantId}}\n Dispositivo: {{deviceId}}\n Regla: {{ruleName}}\n Descripción: {{ruleDescription}}\n Condición: {{ruleCondition}}\n Mensaje de dispositivo en bruto: \n{{message}}"}
 ```  
5. Pulse **Finalizar** para guardar la acción.



### Webhook
{: #webhook}

Utilice la acción webhook para realizar una solicitud HTTP en un servicio web habilitado por webhook cuando se activa una alerta. Por ejemplo, un webhook podría utilizarse para abrir una solicitud de servicio para un activo si un sensor del dispositivo informa de una lectura anormal.

Ejemplo: [Utilice webhook para publicar en Slack](#webhookex).

Los parámetros siguientes se utilizan para configurar una acción webhook:

Parámetro | Descripción
---|---
Nombre | El nombre de la acción, que se utiliza en el panel de instrumentos Alertas.
Descripción | Una breve descripción de la acción.
URL | El URL del servidor de destino habilitado por webhook. **Consejo:** Puede utilizar [sustitución de variables](#variable_substitution) para incluir de forma dinámica datos adicionales en el URL.
Método | El tipo de llamada webhook a ejecutar. Seleccione uno de los tipos siguientes: GET, HEAD, OPTIONS, PATCH, PUT, POST o DELETE.
Nombre de usuario | Lo incluirá el servicio web si es necesario.
Contraseña | Lo incluirá el servicio web si es necesario. **Importante:** La contraseña se envía en texto sin cifrar.
Cabecera | Las cabeceras se componen de la clave y de los pares de valores. **Consejo:** Puede utilizar [sustitución de variables](#variable_substitution) para incluir de forma dinámica datos adicionales en la cabecera.
Tipo de contenido | El tipo de contenido del cuerpo: JSON, XML, formulario WWW URL codificado, o texto sin formato.  Disponible para los métodos OPTIONS, PATCH, PUT, POST y DELETE.
Cuerpo | El cuerpo de la llamada webhook.  Disponible para los métodos OPTIONS, PATCH, PUT, POST y DELETE. De forma predeterminada, el campo de cuerpo se prerrellena con todas las variables listadas en [sustitución de variables](#variable_substitution). **Importante:** El servidor de webhook puede necesitar que determinados campos específicos se incluyan en el cuerpo. Por ejemplo, un webhook Slack debe contener el campo "text".   

#### Ejemplo: Utilice un webhook para publicar en Slack
{: #webhookex}

En este ejemplo, la acción está configurada para utilizar un webhook para poder publicar un mensaje en el canal de Slack #service-requests.

Para crear la acción publicar en slack:
1. En Slack, configure la integración de Webhooks entrantes para las #service-requests del canal. Anote el URL de webhooks. Para obtener información, consulte la [documentación de Slack ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://api.slack.com/incoming-webhooks){: new_window}.
2. En el panel de instrumentos {{site.data.keyword.iot_short}}, vaya a **Reglas > Acciones** y cree una acción nueva que tenga los parámetros siguientes:
 - Nombre: `Publicar solicitud de servicio en Slack`
 - Tipo: **Webhook**
 - URL: `El URL de webhooks de Slack`
 - Método: **POST**
 - Tipo de contenido: `application/json`
 - Cuerpo   
 ```json
 {"text":"*Un dispositivo necesita su atención*\n Hora: {{timestamp}}\n {{site.data.keyword.iot_short}} instancia: {{tenantId}}\n Dispositivo: {{deviceId}}\n Regla: {{ruleName}}\n Descripción: {{ruleDescription}}\n Condición: {{ruleCondition}}\n Mensaje de dispositivo en bruto: \n{{message}}"}
 ```  
  **Importante:** El webhook de Slack debe tener como mínimo el campo "text". Para obtener información, consulte [Webhooks entrantes ![Icono de enlace externo](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks "Documentación de Slack"){: new_window} en la documentación de Slack.
11. Pulse **Finalizar** para guardar la acción.


### Sustitución de variables  
{: #variable_substitution}

Incluir las siguientes sustituciones de variables para incluir de forma dinámica datos de dispositivo. La variable debe estar entre llaves dobles.

Variable | Descripción
---|---
**URL, cabecera y cuerpo** |
`{{timestamp}}` | La indicación de fecha y hora del mensaje.
`{{orgId}}` | El ID de organización del servicio de {{site.data.keyword.iot_short_notm}}.
`{{tenantId}}` | En desuso: El ID del servicio de {{site.data.keyword.iotrtinsights_full}}.
`{{deviceId}}` | El ID del dispositivo.
`{{ruleName}}` | El nombre de la regla que incluye la acción.
`{{ruleID}}` | El ID de la regla que incluye la acción.
**Sólo cuerpo** |
`{{ruleDescription}}`| La descripción de la regla que incluye la acción.
`{{ruleCondition}}` | La condición de la regla que ha desencadenado la acción.
`{{message}}` | El mensaje de dispositivo en bruto que incluía el valor de punto de datos que ha desencadenado la regla.

## Recetas sobre Cloud Analytics

En las siguientes recetas se describe cómo utilizar las características de Cloud Analytics para distintos casos de uso:

- [Análisis de datos en tiempo real utilizando IBM Watson™ IoT Platform Analytics ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [Análisis predictivo sobre datos de ejemplo de IOT ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [La tarjeta de lista de dispositivos SIMPLIFICA la supervisión de dispositivos en tiempo real en el panel de control de WIoTP ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [Realizar acciones en IBM Watson IoT Platform Cloud Analytics ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [Utilizar IBM Data Science Experience para detectar anomalías en series temporales ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
