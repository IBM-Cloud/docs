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

#Requisitos de Serviço
{: #requirements}


##Requisitos de mensagens do dispositivo MQTT

* O message broker MQTT deve fornecer mensagens do dispositivo no formato JSON em um ou mais
tópicos do MQTT.
* As mensagens de dispositivo podem conter qualquer número de atributos, mas os três atributos a seguir sempre são necessários:
	* Um atributo que identifica exclusivamente o dispositivo.
	* Um atributo que especifica a latitude do local atual do dispositivo.
	* Um atributo que especifica a longitude do local atual do dispositivo.
* Dois modos de mensagem são suportados:
	* Uma mensagem MQTT pode conter um objeto JSON com informações sobre um único dispositivo.
	* Uma mensagem MQTT pode conter uma matriz de objetos JSON com informações sobre um conjunto de dispositivos.

##Eventos MQTT e configurando o serviço

O seu aplicativo assina mensagens MQTT e controla o {{site.data.keyword.geospatialshort_Geospatial}} por meio de sua [API REST](https://console.ng.bluemix.net/apidocs/246). As
ações a seguir estão disponíveis através de chamadas API REST:

* Configurar e iniciar o serviço.
* Incluir e remover regiões geográficas para monitorar.
* Recuperar informações sobre o status de serviço e o conjunto de regiões definido atualmente.
* Parar o serviço.
* Reiniciar um serviço já configurado.

