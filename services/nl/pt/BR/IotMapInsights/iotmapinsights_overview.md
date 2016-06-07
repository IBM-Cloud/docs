---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Sobre {{site.data.keyword.iotmapinsights_short}}
{: #iotmapinsights_overview}

O serviço {{site.data.keyword.iotmapinsights_short}} é baseado nos dados da rede viária que estão armazenados no cache de memória. O serviço fornece acesso de alta velocidade para dados estáticos da rede viária, dados dinâmicos do evento e ferramentas geoespaciais baseadas na rede viária, que permitem que o aplicativo integre recursos geoespaciais.
{:shortdesc}

## Consulta de dados estáticos do mapa
{: #static_map_data_query}

Para acessar os dados do atributo de link de estrada, o serviço {{site.data.keyword.iotmapinsights_short}} fornece uma interface de API REST de Consulta de link. A interface recebe um ID do link como um parâmetro que pode ser identificado por uma função correspondente do mapa e retorna informações detalhadas para o link solicitado, como tipo de estrada, comprimento, matriz de pontos de forma de detalhe, nós adjacentes e links adjacentes. Usando as informações do link de detalhe consultadas, o aplicativo pode atravessar uma rede de link de estrada observando informações do link adjacente.

## Dados dinâmicos do evento
{: #dynamic_event_data}

Um evento no serviço {{site.data.keyword.iotmapinsights_short}} é um modelo de objeto para um evento de tráfego colocado dinamicamente em um link de estrada específico. O evento tem atributos básicos de um evento de tráfego, como coordenadas de GPS, horário, tipo, duração do evento e comprimento afetado. É possível injetar e excluir eventos dinamicamente.

## Injeção e exclusão de evento
{: #inject_event}

Com a interface de API REST de injeção de evento, é possível armazenar um evento em um mapa. Para injetar um evento, é possível postar as informações do evento na interface com um tipo de evento definido para classificar os eventos e seus atributos de acordo com o uso desejado do aplicativo. Com a interface de API REST de exclusão de evento, é possível remover eventos do mapa para que os eventos desatualizados possam ser gerenciados.

## Consulta de evento
{: #query_event}

Com a interface de API REST de consulta de evento, é possível consultar eventos sob as condições especificadas que estão configurados como parâmetros de solicitação. Para uma condição de consulta, é possível configurar a área com um intervalo de longitude e latitude, além de atributos do evento para limitar os eventos de destino que são retornados como uma resposta da solicitação.

## Ferramentas geoespaciais
{: #geospatial_tools}

Para ferramentas geoespaciais, o serviço {{site.data.keyword.iotmapinsights_short}} fornece uma interface de API REST para as funções de correspondência de mapa e de procura de rota.

## Correspondência de mapa
{: #map_matching}

Se os dados de GPS dos dispositivos não forem suficientemente exatos para usar análise ou visualização, ou se os atributos da rede de link de estrada forem necessários para seu aplicativo, será possível usar a interface de API REST de correspondência de mapa. A API REST de correspondência de mapa permite que o aplicativo ajuste o ponto de dados brutos do GPS para um ponto correspondido no link de estrada. A interface de API REST de correspondência de mapa recebe um ponto de dados de coordenadas de GPS de longitude e latitude e retorna um ponto correspondido do mapa. O ponto é analisado considerando os dados históricos para cada veículo dentro de um período de tempo específico para localizar o ponto mais provável em tempo real. Para pontos que não têm dados históricos da localização, a interface de correspondência de mapa retorna o ponto mais próximo no link de estrada a partir do ponto solicitado do GPS.

## Procura de rota
{: #route_search}

Se for necessário implementar um aplicativo com funções geoespaciais, será necessário procurar o caminho mais curto entre dois pontos.  A interface de API REST de procura de rota do serviço {{site.data.keyword.iotmapinsights_short}} calcula o caminho mais curto entre as coordenadas de GPS do ponto de início ao ponto de término. As coordenadas recebidas são correspondidas com o link mais próximo do mapa usando a função de correspondência de mapa e o caminho mais curto entre esses pontos correspondidos do mapa é calculado.

## Procura de link afetado
{: #link_search}

Quando um evento ocorre em uma estrada, vários links de estrada podem ser afetados. É possível usar as APIs REST para procurar os links afetados e para localizar os links de estrada nos quais os veículos podem atingir o evento. A procura leva em consideração a topologia da rede de link de estrada, não apenas a distância dos veículos até o evento.

