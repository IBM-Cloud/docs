---

copyright:
  years: 2016, 2017
lastupdated: "2017 02-21"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creación y conexión de un simulador de dispositivos Node-RED
Utilice Node-RED para crear un simulador de dispositivos y enviar datos de dispositivos simulados a la organización de {{site.data.keyword.iot_full}}.  
{:shortdesc}

Node-RED es una herramienta para interconectar dispositivos de hardware, API y servicios en línea de formas nuevas e interesantes. Para obtener más información, consulte el sitio web de [Node-RED](http://nodered.org/).  

Puede ejecutar su instancia de Node-RED en su propio entorno o utilizarla como una aplicación de {{site.data.keyword.Bluemix_notm}}. El proceso siguiente incluye las instrucciones para {{site.data.keyword.Bluemix_notm}}.

Para crear y conectar el simulador de dispositivos Node-RED:

1. Crear el simulador de dispositivos Node-RED
   Utilice el simulador de dispositivos para enviar mensajes de dispositivos MQTT a {{site.data.keyword.iot_short_notm}}. El simulador de dispositivos ha simulado enviar datos para un contenedor de flete a un intermediario de MQTT como por ejemplo {{site.data.keyword.iot_short_notm}}.
    1. Inicie la sesión en {{site.data.keyword.Bluemix_notm}} en: https://console.ng.bluemix.net
    2. Seleccione el separador **Catálogo**.
    3. Localice la sección Contenedores modelo del catálogo de servicio y pulse **Node-RED Starter Community BETA**. **Consejo:** Pulse [aquí](https://console.ng.bluemix.net/catalog/starters/node-red-starter/) para ir directamente a la página Iniciador de Node-RED.
    4. En la página Iniciador de Node-RED, seleccione el espacio donde desea desplegar Node-RED, verifique las selecciones Crear una app y pulse **Crear** para añadir Node-RED a la organización de Bluemix.  
    Por ejemplo:  
     - Espacio: dev
     - Nombre: myDevice
     - Host: myDevice

    Deje el resto de las opciones con sus valores predeterminados. Una vez que se despliegue la aplicación, se le dirigirá a la página Comenzar la codificación con Node-RED.  
    **Nota:** El proceso de transferencia puede tardar algunos minutos.

    3. Pulse el enlace Rutas para abrir Node-RED.  
    Ejemplo: `http://simulatedDevice.mybluemix.net`
    4. Pulse **Ir a su editor de flujo de Node-RED** para abrir el editor.
    5. Copie los datos de flujo de Node-RED que encuentre en la sección [Datos de flujo de nodo de Node-RED](#flow_data) de este documento.
    5. En el editor de flujo de Node-RED, pulse el menú de la esquina superior derecha y seleccione **Importar > Portapapeles**.  
    6. Pegue el portapapeles al campo de entrada de los nodos de importación y pulse **Aceptar**.
    El flujo de simulador de dispositivos se importará en el editor de flujo.

2. Registrar el dispositivo con {{site.data.keyword.iot_short_notm}}
Siga estos pasos para conectar el dispositivo de ejemplo de Node-RED:
 1. En {{site.data.keyword.Bluemix_notm}}, vaya a Panel de instrumentos
 2. Seleccione el espacio en el que ha desplegado {{site.data.keyword.iot_short_notm}}.
 3. Pulse el mosaico **{{site.data.keyword.iot_short_notm}}**.
 4. Pulse **Iniciar panel de control** para abrir el panel de control de {{site.data.keyword.iot_short_notm}}.
 5. Seleccione **Dispositivos**
 6. Pulse **Añadir dispositivo**
 7. Pulse **Crear tipo de dispositivo**.
 9. Especifique un nombre descriptivo y una descripción para el tipo de dispositivo, como por ejemplo `sample_device`.
 10. Opcional: Especifique los atributos de tipo de dispositivo.
 11. Opcional: Especifique los metadatos de tipo de dispositivo.
 12. Pulse **Crear** para añadir el nuevo tipo de dispositivo.
 13. Pulse **Siguiente** para añadir el dispositivo.
 14. Especifique un ID de dispositivo como por ejemplo `Dispositivo001`.
 15. Opcional: Especifique metadatos de dispositivo.
 16. Pulse **Siguiente** para añadir una conexión de dispositivo con una señal de autenticación generada automáticamente.
 17. Verifique que la información de resumen sea correcta y, a continuación, pulse **Añadir** para añadir la conexión.
 18. En la página de información de dispositivos que se abre, copie y guarde la información de dispositivos:  
  <ul>
  <li> ID de organización
  <li> Tipo de dispositivo
  <li> ID de dispositivo
  <li> Método de autenticación
  <li> Señal de autenticación
  </ul>
  **Consejo:** Necesitará ID de organización, Señal de autenticación, Tipo de dispositivo e ID de dispositivo en los próximos pasos para finalizar la configuración de la aplicación de Node-RED para finalizar la conexión.

2. Conectar el dispositivo a {{site.data.keyword.iot_short_notm}}  
 1. Abra el editor de flujo de Node-RED.
 2. Efectúe una doble pulsación en el nodo Publicar en IoT.
 3. Verifique que la entrada del tema sea: `iot-2/evt/event_name/fmt/json` **Consejo:** La parte /event_name del tema establece el nombre de suceso para los sucesos publicados.
 4. Pulse el icono Editar que se encuentra junto al campo Servidor.
 5. Actualice el Nombre de servidor para que se corresponda a su organización de {{site.data.keyword.iot_short_notm}}.  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 Donde {organization_ID} es el *ID de organización* que ha guardado anteriormente.
 6. Actualice el ID de cliente con su ID de organización, tipo de dispositivo e ID de dispositivo:
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   Donde {organization_ID}, {device_type} y {device_ID} son los valores que ha guardado anteriormente.
 7. Pulse el separador **Seguridad**.
 8. Verifique que el campo Nombre de usuario tenga el valor `use-token-auth`.
 9. Actualice el campo Contraseña con la *Señal de autenticación* que ha guardado con anterioridad.
 10. Pulse **Actualizar** y, a continuación, **Aceptar**.
 12. En la esquina superior derecha del editor de flujo de Node-RED, pulse **Desplegar**.
 13. Verifique que el estado de conexión de Publicar en el nodo de IoT muestre *connected*.  **Consejo:** Si no se ha realizado la conexión, compruebe los valores que ha especificado. Incluso un pequeño error de cortar y pegar hará que la conexión falle.

4. Validar la conexión del dispositivo
 1. En otro separador o ventana de navegador, abra el panel de instrumentos de {{site.data.keyword.iot_short_notm}}.
 2. Seleccione **Dispositivos** y pulse **Dispositivo001** o el nombre del dispositivo que ha añadido, si es distinto.  
 Se abrirá la página de información del dispositivo. Esta vista le permite ver el estado de conexión para el dispositivo. El dispositivo debe aparecer como desconectado en esta etapa.   
 3. Atrás en el editor de flujo de Node-RED, pulse el botón en el nodo Inyectar para generar una carga útil de activos.  
 La carga útil contiene los siguientes puntos de datos:  
 ```
 {"d":
  { "name":"My Device",
    "location":
    {
      "longitude":-87.90,
      "latitude":43.03
    },
    "velocity":13,
    "type":"GPS"
  }
 }
 ```
  {:codeblock}  

 3. En el separador Depurar del panel derecho, verifique que se crean los mensajes.  
 4. Atrás en la página de información de dispositivo de {{site.data.keyword.iot_short_notm}}, el dispositivo ahora debería estar conectado. Verifique que vea los mismos puntos de datos recibidos del dispositivo.  
 ```
 Punto de datos de sucesos	 Valor	Hora Recibido
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 Ahora ha conectado el dispositivo de IoT de ejemplo a {{site.data.keyword.iot_short_notm}} y puede ver datos de dispositivo.

## Datos de flujo de nodo Node-RED
{: #flow_data}  
Copie el texto siguiente en el portapapeles y, a continuación, péguelo en el portapapeles de importación al importar nodos en el editor de flujo de Node-RED.   
**Importante:** Asegúrese de copiar todo el texto, incluidos los corchetes iniciales y finales.  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Double click the node.\n2. Click the edit icon next to the Server field.\n3. Update the Server name to correspond to your Watson IoT Platform organization.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Update the Client ID with your orgainzaiton ID, device type, and device ID:\n `d:organization_ID:device_type:device_ID`\n\n5. Click the Security tab.\n6. Verify that the Username field has the value use-auth-token.\n7. Update the Password field with the Authentication Token that you saved earlier.\n8. Click Update and then OK.\n9. In the upper right corner of the Node-RED flow editor, click Deploy. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"The Function node allows you to pass each message though a JavaScript function.\n\nThe Javascript function creates the message payload that is sent to your Watson IoT Platform organization.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.","x":75,"y":236,"wires":[]}]
```
{:codeblock}
