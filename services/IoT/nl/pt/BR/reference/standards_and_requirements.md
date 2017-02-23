---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-28"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# Padrões e requisitos
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} suporta vários padrões e requisitos para o sistema de mensagens e o desenvolvimento geral de aplicativos e dispositivos.
{:shortdesc}


<!-- ## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} supports the following versions of the Hyperledger fabric:
- 0.5

## Python
{: #python}

Support for MQTT over SSL requires at least Python v2.7.9 or v3.4, and OpenSSL v1.0.1.
-->

## MQTT
{: #mqtt}

O {{site.data.keyword.iot_short_notm}} suporta as versões a seguir do protocolo de sistema de mensagens MQTT:

Versão de MQTT | Notas
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1) (recomendada)  | <ul><li>OASIS Standard.<li>Norma ISO (organização internacional para normatização) (ISO/IEC PRF 20922) <li>Interoperabilidade melhorada entre vários clientes e servidores por causa de uma definição mais precisa do protocolo em comparação com a V3.1.   <li>O comprimento máximo do identificador de cliente MQTT (ClientId) aumentou para 256 do limite de 23 caracteres imposto pela V3.1. </br>O serviço {{site.data.keyword.iot_short_notm}} frequentemente requer IDs de cliente mais longos. </br>IDs de cliente longos são suportados independentemente da versão de protocolo MQTT. No entanto, algumas bibliotecas de cliente V3.1 verificam o comprimento do valor ClientId e reforçam o limite de 23 caracteres.</ul>
3.1 | O MQTT V3.1 é a versão do protocolo que está em uso mais amplo hoje.

O {{site.data.keyword.iot_short_notm}} suporta qualquer conteúdo permitido pelo padrão MQTT. MQTT é agnóstico com relação a dados, portanto, é possível enviar imagens, textos que estão em qualquer codificação, dados criptografados e praticamente todo tipo de dado em formato binário. Para obter mais informações sobre o padrão MQTT, consulte os recursos a seguir:
- [MQTT.org](http://mqtt.org/)
- [HiveMQ: introdução a MQTT](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

Para obter informações sobre limites de tamanho de carga útil da mensagem e restrições de formato para casos de uso específicos para {{site.data.keyword.iot_short_notm}}, consulte [Sistema de mensagens MQTT](mqtt/index.html).
