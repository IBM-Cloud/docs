----

copyright:
  years: 2015, 2016, 2017

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Desenvolvendo dispositivos no {{site.data.keyword.iot_short_notm}}
{: #device_dev_index}

Última atualização: 26 de novembro de 2016
{: .last-updated}

Um dispositivo é qualquer coisa que tenha uma conexão com a Internet e tenha dados para enviar ou receber da nuvem. É possível usar dispositivos para enviar informações de eventos como leituras do sensor para a nuvem e para aceitar comandos de aplicativos na nuvem.

Os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}} usando eventos. O dispositivo controla o conteúdo do evento e designa um nome para cada evento enviado. Quando um evento é recebido pelo {{site.data.keyword.iot_short_notm}} de um dispositivo, as credenciais da conexão na qual o evento foi recebido são usadas para determinar de qual dispositivo o evento foi enviado. Essa arquitetura evita que um dispositivo personifique outro dispositivo.

Para obter mais informações sobre conceitos-chave, incluindo dispositivos, veja [Sobre o Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts).


# Conectando seu dispositivo ao {{site.data.keyword.iot_short_notm}}
{: #device_connect}
É possível conectar seu dispositivo ao {{site.data.keyword.iot_short_notm}} usando os protocolos HTTP ou MQTT. Use HTTP se desejar um cenário de configuração de solicitação-resposta, como quando alguém faz uma compra e recebe uma confirmação. Use MQTT se desejar configurar um cenário de evento, como quando alguém toca uma campainha e faz com que um alerta seja acionado em um dispositivo móvel.

Um dispositivo deve ser registrado com uma organização antes que possa se conectar ao {{site.data.keyword.iot_full}}. Para se conectar com segurança ao {{site.data.keyword.iot_short_notm}}, deve-se registrar para uma conta do Bluemix e criar sua própria organização do {{site.data.keyword.iot_short_notm}}. Será possível então registrar seu dispositivo usando o ID dessa organização. Os dispositivos registrados identificam-se para o {{site.data.keyword.iot_short_notm}} com um identificador de dispositivo exclusivo, por exemplo, o endereço de Controle de Acesso à Mídia e um token de autenticação que é aceito somente para esse dispositivo. Depois de ter se conectado com segurança, use o Bluemix para construir seus próprios aplicativos. Tente usar o Node-RED para conectar seus aplicativos juntos.

Se desejar conectar seu dispositivo sem registrá-lo, por exemplo, para executar uma prova de conceito, isso poderá ser feito usando o ID de organização especial `QuickStart`. `QuickStart` é uma instância pública de ambiente de simulação do {{site.data.keyword.iot_short_notm}} que é executada na nuvem. Se não for necessário se conectar com segurança, será possível usar `QuickStart` para testar a conectividade de seu dispositivo e experimentar com o {{site.data.keyword.iot_short_notm}}. Quando você tiver concluído o experimento, reconecte o dispositivo com segurança à sua própria instância de ID de organização específica usando TLS e o token de autenticação.

Para obter mais informações sobre como conectar seu dispositivo ao {{site.data.keyword.iot_short_notm}} usando o protocolo HTTP, veja [API de REST HTTP para dispositivos](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html).
Para obter mais informações sobre como conectar seu dispositivo ao {{site.data.keyword.iot_short_notm}} usando o protocolo MQTT, veja [Conectividade MQTT para dispositivos](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html).

# Introdução ao desenvolvimento de dispositivos
{: #get_started}
Se você tiver um dispositivo que já esteja ativado para o {{site.data.keyword.iot_short_notm}}, bastará começar a usá-lo.

Se o seu dispositivo ainda não estiver ativado, verifique as orientações que estão disponíveis no [developerWorks](https://developer.ibm.com/recipes/). Procure nas orientações existentes se há uma para seu dispositivo e use-a para ajudá-lo a iniciar o desenvolvimento. Será possível até mesmo publicar suas próprias orientações se desejar.

Se não for possível localizar uma orientação para seu dispositivo específico, a IBM fornecerá vários guias de programação e APIs que poderão ser usadas para a introdução. Esses guias contêm bibliotecas do cliente, amostras e informações que podem ajudá-lo a construir e desenvolver código para integrar e conectar seus dispositivos e aplicativos ao {{site.data.keyword.iot_short_notm}}. Os guias de programação a seguir estão disponíveis atualmente:

- Java
- Node.js
- C Incorporado
- ARM mBed C++
- Python
- C#
- Node-RED

Para obter mais informações e links para os guias de programação que estão disponíveis, veja [Bibliotecas do cliente para desenvolvimento do {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).

Se não for possível localizar um guia de programação adequado do {{site.data.keyword.iot_short_notm}}, será possível gravar seu próprio programa e usar o protocolo MQTT ou HTTP para conectar seu dispositivo ao {{site.data.keyword.iot_short_notm}}.

MQTT é um padrão aberto gerenciado pela organização de padronização OASIS e reconhecido internacionalmente pela ISO. Para obter mais informações, veja [OASIS Message Queuing Telemetry Transport](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt).

Uma ampla variedade de bibliotecas do cliente MQTT está disponível para vários sistemas diferentes, incluindo os ambientes a seguir:
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

Para obter mais informações sobre MQTT, veja [Sistema de mensagens MQTT](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3).
