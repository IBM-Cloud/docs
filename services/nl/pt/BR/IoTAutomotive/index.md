---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao {{site.data.keyword.iot4auto_short}} (Beta)
{: #getting_started_iotautomotive}

Última atualização: 29 de julho de 2016
{: .last-updated}

O {{site.data.keyword.iot4auto_full}} é um serviço do {{site.data.keyword.Bluemix_notm}} que pode ser usado para recuperar, gerenciar e analisar big data de veículos conectados. A análise de dados do {{site.data.keyword.iot4auto_short}} fornece insights poderosos e práticos no comportamento de direção, localização do veículo, outras atividades automotivas relacionadas e eventos de interesse.

{:shortdesc}

Usando o {{site.data.keyword.iot4auto_short}}, é possível executar as tarefas a seguir:

- Enviar dados de análise do veículo e dados normalizados para o armazenamento de dados para análise
- Injetar eventos no mapa de contexto e recuperar os eventos pelos quais veículos específicos são afetados
- Identificar novos eventos a partir dos dados de análise do veículo
- Recuperar informações sobre os veículos conectados
- Gerenciar dados de ativo para motoristas, veículos, regras de eventos, tipos de eventos e fornecedores


O serviço do {{site.data.keyword.iot4auto_short}} inclui os serviços do {{site.data.keyword.Bluemix_notm}} a seguir, que também estão disponíveis separadamente no catálogo do {{site.data.keyword.Bluemix_notm}}:

|Serviço|Descrição|
|:---|:---|
|[Comportamento do motorista](../IotDriverInsights/index.html){:new_window}| Um serviço que pode analisar o comportamento do motorista e identificar padrões de trajetória de uma viagem a partir dos dados de análise e contexto do veículo que são recuperados de um veículo conectado.
|[Mapeamento de contexto](../IotMapInsights/index.html){:new_window}| Um serviço que fornece funções geoespaciais, tais como a correspondência de mapa e
a busca do caminho mais curto por redes viárias.
*Tabela 1. Serviços do {{site.data.keyword.iot4auto_short}}*

Antes de iniciar a integração de seus dispositivos e aplicativos automotivos com o serviço,assegure-se de concluir as tarefas a seguir:

1. Revise o tópico [Sobre o {{site.data.keyword.iot4auto_short}}](iotautomotive_overview.html) para familiarizar-se com os recursos e a
análise de dados
que estão disponíveis e são suportados pelo serviço.
2. Ao incluir uma instância do serviço a partir do [{{site.data.keyword.Bluemix_notm}} catálogo](https://console.ng.bluemix.net/catalog/labs/){:new_window}, assegure-se de que ela não esteja vinculada a um aplicativo e de anotar os valores de ID, nome de usuário e senha do locatário gerados automaticamente. Estes valores serão necessários posteriormente para acessar o serviço por meio da API do {{site.data.keyword.iot4auto_short}}.
3. Usando o console no painel, configure as portas, os nomes de host de destino e as outras configurações para o seu {{site.data.keyword.iot4auto_short}}. Para obter mais informações, veja [Administrando](iotautomotive_admin.html).

É possível integrar seus dispositivos e aplicativos automotivos com este serviço usando comandos de API REST do {{site.data.keyword.iot4auto_short}}.

Para que o serviço funcione rapidamente, conclua as etapas a seguir:

1. Injete eventos usando o comando de solicitação de API `sendEvent` para enviar eventos para serem analisados.
  - Solicitação: dados do evento com posição
2. Confirme se os dados do evento estão armazenados com Correspondência de Mapa usando o comando de solicitação de API `getEvent` para recuperar o evento.
  - Solicitação: dados da área (longitude e latitude dos pontos iniciais ou finais)
  - Resposta: dados do evento com o ID do link de estrada
3.  Envie dados de análise do veículo a serem analisados usando o comando de solicitação de API `sendCarProbe`.
  - Solicitação: dados de análise do veículo com posição
4. Confirme se os dados de análise do veículo estão armazenados com Correspondência de Mapa usando o comando de solicitação de API `getCarProbe` para recuperar os dados.
  - Solicitação: dados da área (longitude e latitude dos pontos iniciais ou finais)
  - Resposta: dados de análise do veículo com o ID do link de estrada
5. Analise os dados do motorista. Para obter mais informações, veja [Comportamento do motorista](../IotDriverInsights/index.html){:new_window}.

# Links Relacionados
{: #rellinks}

## Referência de API
{: #api}
* [{{site.data.keyword.iot4auto_short}}Docs API](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [APIs de serviço do Mapa Contextual](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [APIs de serviço de Comportamento do Motorista]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## Links Relacionados
{: #general}
* [Introdução ao {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Introdução ao {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Introdução ao {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [O que há de novo em Serviços do Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [dW Answers no IBM developerWorks](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Estouro da capacidade](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
