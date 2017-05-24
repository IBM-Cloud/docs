---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}

O {{site.data.keyword.iot_full}} for {{site.data.keyword.Bluemix_notm}} fornece um kit de ferramentas versátil que inclui dispositivos de gateway, gerenciamento de dispositivo e acesso ao aplicativo poderoso. Usando o {{site.data.keyword.iot_short_notm}}, é possível coletar dados do dispositivo conectados e executar analítica em dados em tempo real a partir de sua organização.
{:shortdesc}

## Antes de iniciar
{: #byb}

Antes de conectar dispositivos e utilizar dados, registre uma conta {{site.data.keyword.Bluemix_notm}} e crie uma instância do serviço {{site.data.keyword.iot_short_notm}} em sua organização {{site.data.keyword.Bluemix_notm}}. É possível criar uma instância do {{site.data.keyword.iot_short_notm}} diretamente da [página do {{site.data.keyword.iot_short_notm}} no Catálogo de serviços Bluemix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/catalog/services/internet-of-things-platform/){:new_window}.  

Para obter informações detalhadas sobre como inscrever-se em conta no {{site.data.keyword.Bluemix_notm}}, configurar regiões e outras definições de gerenciamento, consulte [Gerenciando
sua conta Bluemix](https://console.ng.bluemix.net/docs/admin/account.html#signup).

É possível instalar e configurar sua instância do {{site.data.keyword.iot_short_notm}} no painel. Para abrir o painel, vá para a sua instância de serviço do {{site.data.keyword.iot_short_notm}} em
{{site.data.keyword.Bluemix_notm}} e, em seguida, clique em **Ativar painel**.

## Etapa 1: conectar seus dispositivos
{: #up_and_running}

Para colocar o serviço em funcionamento, explore as opções a seguir, dependendo de sua situação:

   |   O serviço é implementado | O serviço não é implementado
  ------------- | -------------
  **Tenho um dispositivo para conectar** | [Conecte seu dispositivo ao {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task).| Explore a conexão de dispositivo no [demo da organização Play ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}.
  **Não tenho um dispositivo para conectar** | [Crie e conecte um simulador de dispositivo Node-RED](nodereddevice_sample.html){:new_window}. | Introdução ao [Watson IoT Platform Starter](https://console.ng.bluemix.net/docs/starters/IoT/iot500.html).
Para obter mais informações sobre como conectar tipos de dispositivo específicos ao {{site.data.keyword.iot_short_notm}}, veja [Orientações do developerWorks ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}.  

Para obter a documentação para desenvolvedor de conexão de dispositivo, consulte:
- [Conectividade MQTT para dispositivos](devices/mqtt.html).
- [Conectividade MQTT para gateways](gateways/mqtt.html).

## Etapa 2: analisar os dados do dispositivo
{: #analyzing_data}

Comece explorando os dados em tempo real que os dispositivos estão enviando ao {{site.data.keyword.iot_short_notm}}.

O {{site.data.keyword.iot_short_notm}} inclui as ferramentas de análise de dados a seguir:  
- [Placas e cartões](data_visualization.html) para visualizar os dados do dispositivo de tempo real.
- [Regras e ações](analytics.html) que são acionadas por dados do dispositivo de tempo real.

Para obter um exemplo rápido de introdução, veja a orientação do developerWorks [Usando regras e ações com o IBM Watson IoT Platform Cloud Analytics ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window}.

## Etapa 3: criar aplicativos para consumir os dados do dispositivo
{: #develop_applications}

Estenda os recursos de análise de dados do {{site.data.keyword.iot_short_notm}} criando e conectando seus próprios aplicativos para consumir dados do dispositivo em tempo real e históricos.

Para obter informações adicionais, consulte os
seguintes tópicos:   
- Explore a [documentação do desenvolvedor de aplicativos](applications/api.html) e a [Documentação da API do {{site.data.keyword.iot_short_notm}}](reference/api.html).
- Explore as [Bibliotecas do cliente do {{site.data.keyword.iot_short_notm}}](iot_platform_client_lib.html) que fornecem ferramentas e arquivos para construir e desenvolver código para integração e conexão de seus dispositivos e aplicativos.
- [Conecte um serviço do {{site.data.keyword.cloudantfull}}](cloudant_connector.html) a seu {{site.data.keyword.iot_short_notm}} para armazenar dados históricos do dispositivo.
