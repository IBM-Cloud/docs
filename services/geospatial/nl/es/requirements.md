---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Requisitos del servicio
{: #requirements}


##Requisitos de mensajes de dispositivo MQTT

* El intermediario de mensajes MQTT debe proporcionar los mensajes de dispositivo en formato JSON en uno o varios temas MQTT.
* Los mensajes de dispositivo pueden contener cualquier serie de atributos, pero los tres atributos siguientes son siempre obligatorios:
	* Un atributo que identifica de forma exclusiva el dispositivo.
	* Un atributo que especifica la latitud de la ubicación actual del dispositivo.
	* Un atributo que especifica la longitud de la ubicación actual del dispositivo.
* Se da soporte a dos modalidades de mensajes:
	* Un mensaje MQTT puede contener un objeto JSON con información sobre un único dispositivo.
	* Un mensaje MQTT puede obtener una matriz de objetos JSON con información sobre un conjunto de dispositivos.

##Sucesos MQTT y configuración del servicio

La aplicación se suscribe a los mensajes MQTT y controla {{site.data.keyword.geospatialshort_Geospatial}} a través de su [API REST](https://console.ng.bluemix.net/apidocs/246). Las siguientes opciones están disponibles mediante las llamadas de API REST:

* Configurar e iniciar el servicio.
* Añadir y eliminar regiones geográficas que desea supervisar.
* Recuperar información sobre el estado del servicio y sobre el conjunto de regiones definidas actualmente.
* Detener el servicio.
* Reiniciar un servicio ya configurado.

