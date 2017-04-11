---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Desenvolvendo gateways no {{site.data.keyword.iot_short_notm}}
{: #gw_dev_index}

Se seus dispositivos não puderem se conectar diretamente à Internet, será possível construir um dispositivo de gateway para recuperar e enviar dados para aplicativos em sua organização do {{site.data.keyword.iot_full}}. Bibliotecas do cliente, amostras e informações são fornecidas para ajudá-lo a conectar gateways de dispositivo à sua organização e aplicativos do {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Protocolos de Conexão
Gateways se conectam ao {{site.data.keyword.iot_short_notm}} usando o protocolo de sistema de mensagens MQTT. Conectar gateways ao {{site.data.keyword.iot_short_notm}} usando o sistema de mensagens HTTP não é suportado. Apenas dispositivos podem se conectar usando o sistema de mensagens HTTP.

## Bibliotecas do cliente
Bibliotecas do cliente para desenvolver gateways que podem se conectar ao {{site.data.keyword.iot_short_notm}} estão disponíveis nos seguintes idiomas:

|Biblioteca do Cliente |Link para biblioteca e documentação adicional
|:---|:---
|C++|[https://github.com/ibm-watson-iot/iot-cpp ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-cpp){: new_window}
|C#|[https://github.com/ibm-watson-iot/iot-csharp ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-csharp){: new_window}
|C Incorporado| [https://github.com/ibm-watson-iot/iot-embeddedc ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-embeddedc){: new_window}
|Java™|[https://github.com/ibm-watson-iot/iot-java ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-java){: new_window}
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/ ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window}
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-nodered){: new_window}
|Python|[https://github.com/ibm-watson-iot/iot-python ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-python){: new_window}

Para obter mais informações e links para as bibliotecas do cliente que estão disponíveis, consulte também [Bibliotecas do cliente para desenvolvimento do {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).

## Edge Analytics
{: #eaa_community}

O recurso {{site.data.keyword.iot_short_notm}} Edge Analytics permite executar o {{site.data.keyword.iot_short_notm}} Analytics em um dispositivo de gateway. Use o Edge Analytics para gerar analítica para analisar e responder aos dados coletados na borda da rede. Também é possível enviar dados do dispositivo para o {{site.data.keyword.iot_short_notm}} para obter processamento analítico adicional, visualização de painel como entrada para outras analíticas ou para ser armazenado em um repositório histórico.

É possível fazer download do SDK do Edge Analytics na [página da comunidade do IBM Edge Analytics ![Ícone de link externo](../../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){: new_window}. O SDK inclui o arquivo JAR do SDK, o Javadoc, a amostra de código, os links de orientação e os arquivos LEIA-ME. Na comunidade, também é possível ver vídeos de como o Edge Analytics funciona e usar o fórum da comunidade para fazer perguntas.
