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
{: #gettingstartedtemplate}
*Última atualização: 13 de maio de 2016*

O {{site.data.keyword.iotmapinsights_full}} torna fácil para os desenvolvedores permitir que seus aplicativos usem funções geoespaciais, como correspondência de mapa e procura de caminho mais curto com base nas redes viárias no globo.
{:shortdesc}

É possível usar as funções a seguir por meio da API REST do {{site.data.keyword.iotmapinsights_short}}:

- Correspondência de mapa altamente precisa que usa a geometria de rede viária.
- Manipulação de eventos em tempo real em um mapa, como tráfego.
- Procura dinâmica de caminho mais curto (procura de rota) considerando eventos em tempo real, como tráfego.
- Recuperação dos dados de geometria de estrada que podem ser usados para desenhar formas de estrada em um mapa.

O serviço {{site.data.keyword.iotmapinsights_short}} usa os dados da rede viária, em coordenadas WGS84, que são extraídos do OpenStreetMap. Somente as estradas que um veículo pode percorrer são usadas para análise.

As regiões do mapa suportadas são:

- Europa (map_id=1)
- África (map_id=2)
- Ásia (map_id=3)
- Austrália Oceania (map_id=4)
- América do Norte (map_id=5)
- América Central (map_id=6)
- América do Sul (map_id=7)


Siga estas etapas para usar as funções de análise do serviço {{site.data.keyword.iotmapinsights_short}}.

## Usando o {{site.data.keyword.iotmapinsights_short}} para correspondência de mapa

1. Prepare um conjunto de dados brutos de coordenadas de GPS a serem analisados.
2. Envie os dados brutos de coordenadas de GPS na ordem de série temporal para o serviço {{site.data.keyword.iotmapinsights_short}} usando a API REST `mapMatching`. Opcionalmente, configure um ângulo de curso de cada posição em graus (Norte é 0, ângulo no sentido horário) para especificar a direção da viagem.
3. Receba as coordenadas correspondidas do mapa e informações de link de estrada em resposta à chamada API REST `mapMatching`.
4. Opcionalmente, recupere os dados de forma de estrada do link de estrada correspondido do mapa usando a API REST `getLinkInformation`. Chame a API REST `getLinkInformation` com um ID do link para obter uma série de coordenadas que consistem em uma forma de estrada.

## Usando o {{site.data.keyword.iotmapinsights_short}} para procura de rota

1. Determine uma posição de início e de término para a qual você deseja obter um caminho mais curto.
2. Envie as coordenadas de início e de término para o serviço {{site.data.keyword.iotmapinsights_short}} usando a API REST `routeSearch`. Opcionalmente, configure um ângulo de curso de cada posição em graus (Norte é 0, ângulo no sentido horário) para especificar a direção de viagem.
3. Receba uma lista de links de estrada em resposta à chamada API REST `routeSearch`. É possível desenhar a forma do caminho localizado em um mapa quando os dados de forma que estão incluídos nos dados de resultado.

## Usando o {{site.data.keyword.iotmapinsights_short}} para manipulação de evento de tráfego

1. Determine um tipo e posição de um evento de tráfego que você deseja criar.
2. Envie as informações de evento de tráfego para o serviço {{site.data.keyword.iotmapinsights_short}} usando a API REST `createEvent`.
3. Receba um ID de evento do evento de tráfego criado em resposta à chamada API REST `createEvent`.
4. Procure os eventos de tráfego dentro de uma área retangular específica e, opcionalmente, com um tipo de evento de tráfego específico, usando a API REST `queryEvent`.

- Opcionalmente, remova um evento de tráfego que não seja mais válido usando a API REST `deleteEvent`.
- Opcionalmente, recupere uma área na estrada que seja afetada por um evento de tráfego usando a API REST `getAffectedLinksInformation`.


# Links relacionados
{: #rellinks}
## Tutoriais e amostras
{: #samples}
* [Tutorial do {{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Parte1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [Tutorial do {{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} Parte2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

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

