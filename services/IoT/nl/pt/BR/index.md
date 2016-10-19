---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}
Última atualização: 26 de agosto de 2016
{: .last-updated}

O {{site.data.keyword.iot_full}} for {{site.data.keyword.Bluemix_notm}} fornece um kit de ferramentas versátil que inclui dispositivos de gateway, gerenciamento de dispositivo e acesso ao aplicativo poderoso. Usando o {{site.data.keyword.iot_short_notm}}, é possível coletar dados do dispositivo conectados e executar analítica em dados em tempo real a partir de sua organização.
{:shortdesc}

## Antes de iniciar
{: #byb}

Antes de conectar dispositivos e utilizar dados, uma instância do serviço do {{site.data.keyword.iot_short_notm}} deve existir em sua organização do {{site.data.keyword.Bluemix_notm}}. É possível criá-la diretamente a partir da [página do {{site.data.keyword.iot_short_notm}} no catálogo de serviços do Bluemix](https://console.{DomainName}/catalog/services/internet-of-things-platform/).  

## Etapa 1: conectar seus dispositivos
{: #up_and_running}

Para colocar o serviço em funcionamento, explore as opções a seguir, dependendo de sua situação:

   |   O serviço é implementado | O serviço não é implementado
  ------------- | -------------
  **Tenho um dispositivo para conectar** | [Conecte seu dispositivo ao {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task).| Explore conexão de dispositivo em [no demo da organização Play](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}.
  **Não tenho um dispositivo para conectar** | [Crie e conecte um simulador de dispositivo Node-RED](nodereddevice_sample.html){:new_window}. | Introdução ao [Watson IoT Platform Starter](https://new-console.stage1.ng.bluemix.net/docs/starters/IoT/iot500.html){:new_window}.
Para obter mais informações sobre como conectar tipos de dispositivo específicos ao {{site.data.keyword.iot_short_notm}}, consulte [Receitas do developerWorks](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}.  

Para obter a documentação para desenvolvedor de conexão de dispositivo, consulte:
- [Conectividade MQTT para dispositivos](devices/mqtt.html).
- [Conectividade MQTT para gateways](gateways/mqtt.html).

## Etapa 2: analisar os dados do dispositivo
{: #analyzing_data}

Comece explorando os dados em tempo real que os dispositivos estão enviando ao {{site.data.keyword.iot_short_notm}}.

O {{site.data.keyword.iot_short_notm}} inclui as ferramentas de análise de dados a seguir:  
- [Placas e cartões](data_visualization.html) para visualizar os dados do dispositivo de tempo real.
- [Regras e ações](analytics.html) que são acionadas por dados do dispositivo de tempo real.

Para um exemplo rápido de introdução, consulte a receita do developerWorks [Usando regras e ações com o IBM Watson Platform IoT Cloud Analytics](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window}.

## Etapa 3: criar aplicativos para consumir os dados do dispositivo
{: #develop_applications}

Estenda os recursos de análise de dados do {{site.data.keyword.iot_short_notm}} criando e conectando seus próprios aplicativos para consumir dados do dispositivo em tempo real e históricos.

Para obter informações adicionais, consulte os
seguintes tópicos:   
- Explore a [documentação do desenvolvedor de aplicativos](applications/api.html) e a [Documentação da API (interface de programação de aplicativos) do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}.
- Explore as [Bibliotecas do cliente do {{site.data.keyword.iot_short_notm}}](iot_platform_client_lib.html) que fornecem ferramentas e arquivos para construir e desenvolver código para integração e conexão de seus dispositivos e aplicativos.
- [Conecte um serviço do {{site.data.keyword.cloudantfull}}](cloudant_connector.html) a seu {{site.data.keyword.iot_short_notm}} para armazenar dados históricos do dispositivo.




# Links Relacionados
{: #rellinks}
## Tutoriais e amostras
{: #samples}
* [Receitas para conectar os seus dispositivos](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [Organização Play do {{site.data.keyword.iot_short_notm}}](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Conectando um Intel Galileo ao {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Conectando um ARM® mbed™ IoT Starter Kit](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Conectando um Raspberry Pi ao {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## Referência de API
{: #api}
* [Documentação da API (interface de programação de aplicativos) do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}
* [Documentação do developer](developer_doc_overview.html)
