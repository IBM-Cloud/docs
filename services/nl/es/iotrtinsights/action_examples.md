---

copyright:
  años: 2015,2016

---

{:shortdesc: .shortdesc}

# Ejemplos de acción

Los tipos de acciones Enviar correo electrónico, IFTTT, Node-RED y webhooks abren todo un universo de opciones para ejecutar tareas, que solo están limitadas por la imaginación y los conectores utilizados por el resto de las herramientas. Por ejemplo, las acciones para publicar los mensajes de estado de dispositivo en Slack, enviar mensajes de texto al personal de servicio, crear solicitudes de servicio de dispositivo, etc.
{: shortdesc}

Todos los ejemplos que se muestran a continuación representan una acción que notifica a un ingeniero de servicio cuándo la temperatura, representada por el punto de datos temporales de un dispositivo, supera los 100 grados, utilizando la siguiente condición de regla:
`temp >= 100`

Puede desencadenar uno o varios de los siguientes tipos de acción cuando se produzca la condición de regla:  
 - [Enviar correo electrónico](#emailex "Enviar correo electrónico")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## Utilizar el envío de correo electrónico {: #emailex}
En este ejemplo, la acción está configurada para utilizar la característica de Enviar correo electrónico de Real-Time Insights para enviar un correo electrónico al ingeniero de servicio principal, y también enviar un correo electrónico de copia de seguridad a su gestor.

Para crear la acción de correo electrónico:
1. En Real-Time Insights, vaya a **Analytics > Actions**.
2. Pulse **Añadir nueva acción**.
3. Seleccione el tipo **Enviar correo electrónico**.
4. Especifique el nombre de acción `Enviar correo electrónico de solicitud de servicio`.
5. Especifique la descripción `Enviar un correo electrónico al ingeniero de servicio y a su gestor`.
6. En el campo Para, especifique `service.engineer@company.com`.
7. En el campo CC, especifique: `service.manager@company.com`.
8. En la línea de asunto, especifique: `Servicio necesario.`
9. Seleccione esta opción para anteponer con "Alerta de {{site.data.keyword.iotrtinsights_short}}" para clarificar de dónde viene el correo electrónico.
10. Para incluir los datos de dispositivo en el correo electrónico, quite la marca del **No incluya datos de dispositivo en el mensaje de correo electrónico**.
11. Pulse **Aceptar** para guardar la acción.  




## Utilice un webhook para publicar en Slack {: #webhookex}

En este ejemplo, la acción está configurada para utilizar un webhook para publicar un mensaje en nuestro canal de Slack #service-requests.

Para crear la acción publicar en slack:
1. En Slack, configure la integración de Webhooks entrantes para las #service-requests del canal. Anote el URL de webhooks. Para obtener más información, consulte la [Documentación de Slack](https://api.slack.com/incoming-webhooks).
2. En Real-Time Insights, vaya a **Analytics > Actions** y cree una nueva acción que tenga los parámetros siguientes:
 - Tipo: **Webhook**
 - Nombre: `Publicar solicitud de servicio en Slack`
 - URL: `El URL de webhooks de Slack`
 - Método: **POST**
 - Tipo de contenido: application/json
 - Seleccione **Utilizar el cuerpo del mensaje personalizado**
 - Cuerpo
 ```{"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}```  
 {: codeblock}  
 **Importante:** El webhook de Slack debe tener como mínimo el campo "text". Para obtener información, consulte [Webhooks entrantes](https://api.slack.com/incoming-webhooks "Documentación de Slack") en la documentación de Slack.
11. Pulse **Aceptar** para guardar la acción.

## Utilice Node-RED para enviar un mensaje de texto {: #noderedex}

En este ejemplo, la acción está configurada para utilizar Node-RED con un nodo Twilio para enviar un mensaje de texto al ingeniero de servicio.

Para crear la acción enviar mensaje de texto:
1. En Twilio, localice o cree un nuevo Servicio de mensajería a utilizar para enviar mensajes de texto desde la cuenta de Twilio. Para obtener información, consulte la [documentación de Twilio](https://www.twilio.com/help).
1. En Bluemix, configure y acceda a la cuenta de Node-RED con el URL de Node-RED `http://mynodered.mybluemix.net/red/`. Para obtener más información, consulte el tema [Creación de aplicaciones con el iniciador de Node-RED](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) en la documentación de Bluemix.
2. En Node-RED, cree un flujo simple de dos nodos como por ejemplo [RTI-alert]->[SMS].
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
  4. Conectar los nodos
  Conecte los nodos http y twilio arrastrando entre el puerto de salida de uno al puerto de entrada del otro.
  5. Pulse el botón **Desplegar** para desplegar el flujo para el servidor
3. En {{site.data.keyword.iotrtinsights_short}}, vaya a **Analytics > Actions** y cree una acción que tenga los parámetros siguientes:
 - Tipo: **Node-RED**
 - Nombre: `Enviar texto mediante Node-RED y Twilio`
 - Descripción: `Enviar una alerta de mensaje de texto al ingeniero de servicio.`
 - URL: `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```{"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}```  
 {: codeblock}
4. Pulse **Aceptar** para guardar la acción.

## Utilice IFTTT para publicar una tarjeta Trello {: #iftttex}

En este ejemplo, configuramos la acción para utilizar IFTTT para publicar una tarjeta en una lista de solicitudes de servicio de Trello.

Para crear la publicación de una tarjeta en la acción Trello:
1.	En IFTTT, conecte con el canal Trello.
2.	En IFTTT, conecte al canal de Maker. Tome nota de la clave IFTTT. Necesitará esto para conectarse a IFTTT desde Real-Time Insights.
5.	En IFTTT, crear una receta:
 1. Pulse **THIS**.
 2. Seleccione el canal **Maker**.  
 2. Pulse **Recibir una solicitud web**.
 3. Especifique el nombre de suceso `post-Trello-card`.
 4. Pulse **THAT**.
 5. Seleccione el canal **Trello**.
 6. Seleccione la pizarra Trello en la que se creará la tarjeta.
 7. Especifique un nombre de lista en la que se añaden las tarjetas.
 8. Edite el título y la descripción.
 9. Asigne los miembros @service.engineer y @service.manager.
 8. Pulse **Crear acción**.   
3. En {{site.data.keyword.iotrtinsights_short}}, vaya a **Analytics > Actions** y cree una acción que tenga los parámetros siguientes:
<ul>
<li>Tipo: **IFTTT**</li>
<li>Nombre: `Publicar tarjeta de solicitud de servicio`</li>
<li>Descripción: `Utilice IFTTT para publicar una tarjeta en la lista de solicitudes de servicio en Trello.`</li>
<li>Clave: Su clave IFTTT</li>
<li>Evento: `post-Trello-card`</li>
<li>Opcionalmente, añada valores para el Valor de 1 a 3. **Consejo:** Puede utilizar [sustitución de variables](actions.html#variable_substitution) para incluir de forma dinámica datos de dispositivo.</li>
</ul>
4. Pulse **Aceptar** para guardar la acción.
