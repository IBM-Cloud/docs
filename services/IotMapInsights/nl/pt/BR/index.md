---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Introdução ao {{site.data.keyword.iotmapinsights_short}}
{: #iotdriverinsights_index}
Última atualização: 22 de junho de 2016
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} é um serviço no {{site.data.keyword.Bluemix}} que pode ser usado para ativar funções geoespaciais,
tais como correspondência de mapa e procura de caminho mais curto para redes viárias em todo
o mundo com seus aplicativos.  
{:shortdesc}

Os recursos a seguir estão disponíveis por meio da API REST do {{site.data.keyword.iotmapinsights_short}}:

|Feature|Utilize para...|
|:---|:---|
|Correspondência de mapa altamente precisa|Corresponda sua localização via GPS com a rede viária mapeada real|
|Recuperação dos dados de geometria viária|Recuperar a rede viária mapeada para desenhar formas viárias em um mapa|
|Procura dinâmica de caminho mais curto|Procurar a rota mais curta que incorpore eventos em tempo real, tal como tráfego|
|Manipulação de evento de tráfego em tempo real|Incluir eventos correspondidos no mapa em tempo real,
por exemplo, condições de tráfego para melhorar os resultados do planejamento de rota|

## Antes
de Começar
{: #byb}

1. Ao incluir uma instância do serviço a partir do [{{site.data.keyword.Bluemix_notm}} catálogo](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}, assegure-se de que ela não esteja vinculada a um aplicativo e de anotar os valores de ID, nome de usuário e senha do locatário gerados automaticamente. Estes valores serão necessários posteriormente para acessar o serviço por meio da API do {{site.data.keyword.iotmapinsights_short}}.

2. Familiarize-se com o [OpenStreetMap](http://www.openstreetmap.org/){: new_window}.  

 O serviço {{site.data.keyword.iotmapinsights_short}} usa os dados da rede viária, em coordenadas WGS84, que são extraídos do [OpenStreetMap](http://www.openstreetmap.org/){: new_window}. Somente as estradas nas quais um veículo pode percorrer são usadas para análise.  

 As regiões de mapa a seguir são suportadas:

|Região|ID do Mapa|
|:---|:---|
|Europe|map_id=1|
|África|map_id=2|
|Asia|map_id=3|
|Austrália e Oceania|map_id=4|
|North America|map_id=5|
|América Central|map_id=6|
|América
do Sul|map_id=7|

## Correspondência de mapa
{: #map_matching}
Para mapear coordenadas brutas de GPS para mapear coordenadas correspondidas no mapa,
conclua as etapas a seguir:

1. Prepare um conjunto de coordenadas brutas de GPS a serem analisadas.
2. Envie as coordenadas brutas de GPS usando o comando de API `mapMatching`. Opcionalmente, configure um ângulo de curso de cada posição em graus para especificar a direção da viagem.
 - Solicitação: dados brutos de GPS
 - Resposta: dados de GPS correspondidos no mapa, ID do link
3. Opcional: obtenha os dados de tipo de estrada usando o comando de API
`getLinkInformation`. É possível recuperar os dados de forma da estrada correspondidos como uma série de coordenadas
com a API REST `getLinkInformation`.
 - Solicitação: ID do link
 - Resposta: tipo de estrada

## Procura de rota
{: #route_searching}

Localize as informações de caminho de rota mais curto entre as coordenadas de origem
e destino especificadas usando as etapas a seguir:

1. Determine uma posição inicial e final para o caminho mais curto.
2. Envie as coordenadas inicial e final com a API REST `routeSearch`.
Opcionalmente, configure um ângulo de curso para cada posição, em graus, para especificar
a direção da viagem.
 - Solicitação: coordenadas de origem e destino
 - Resposta: rota mais curta correspondida no mapa

Use os dados de forma do link retornados para desenhar uma forma do caminho localizado em um mapa.

## Incluindo Ocorrências de Tráfego
{: #traffic_events}

Para incluir informações de evento de tráfego no serviço {{site.data.keyword.iotmapinsights_short}}, conclua as etapas a seguir:

1. Escolha o tipo e a posição do evento de tráfego que deseja criar.
2. Injete o evento usando o comando de API `createEvent`.
Envie as informações de evento de tráfego para o serviço {{site.data.keyword.iotmapinsights_short}}.
 - Solicitação: informações do evento
 - Resposta: ID de evento
3. Localize eventos usando o comando de API REST `queryEvent`.
Procure eventos de tráfego que estão em uma área retangular específica e, opcionalmente, um
tipo de evento de tráfego específico.
 - Solicitação: informações da área.
 - Resposta: informações do evento.  
4. Opcional: remova um evento de tráfego que não seja mais válido usando o comando
de API `deleteEvent`.
5. Opcional: recupere uma área na estrada que é afetada por um evento de tráfego usando
o comando de API `getAffectedLinksInformation`.

# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Tutorial do {{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Parte1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [Tutorial do {{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Parte2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [Aplicativo IoT for Automotive Starter](https://iot-automotive-starter.mybluemix.net){:new_window}

## Referência à API
{: #api}

* [Docs API](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## Links relacionados
{: #general}

* [Introdução ao {{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window}
* [Introdução ao {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [dW Answers no IBM developerWorks](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Estouro da capacidade](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [O que há de novo em Serviços do Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap
](http://www.openstreetmap.org/){:new_window}
* [&copy; Contribuidores do OpenStreetMap](http://www.openstreetmap.org/copyright){:new_window}
* [Open Data Commons Open Database License (ODbL)](http://opendatacommons.org/licenses/odbl/){:new_window}
