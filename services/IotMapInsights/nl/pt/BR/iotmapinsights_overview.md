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
Última atualização: 20 de julho de 2016
{: .last-updated}

O {{site.data.keyword.iotmapinsights_full}} é um serviço no {{site.data.keyword.Bluemix_notm}} que pode ser usado para obter acesso rápido aos dados estáticos da rede viária e aos dados dinâmicos do evento. O {{site.data.keyword.iotmapinsights_short}} também fornece ferramentas geoespaciais para redes viárias, que podem ser usadas para integrar recursos geoespaciais com seus aplicativos.
{:shortdesc}

O serviço {{site.data.keyword.iotmapinsights_short}} fornece os recursos a seguir:

- Dados estáticos do mapa
- Dados dinâmicos do evento
- Ferramentas geoespaciais

O serviço {{site.data.keyword.iotmapinsights_short}} coleta e usa dados da
rede viária do [OpenStreetMap](http://www.openstreetmap.org/){: new_window}
que são armazenados no cache de memória de serviço para processamento.

Os dados do OpenStreetMap são disponibilizados sob o Open Data Common Open Database License (ODbL) pela OpenStreetMap Foundation (OSMF). Para obter mais informações, veja as informações de [Copyright e Licença do OpenStreetMap](http://www.openstreetmap.org/copyright){: new_window}.

## Dados estáticos do mapa
{: #static_map_data_query}

Um dos principais recursos do produto é a capacidade de recuperar informações detalhadas
da estrada para uso com seus aplicativos. Use a interface de API REST Consulta de link para consultar dados estáticos do atributo do mapa de estradas por ID do link. Use a função [função de correspondência de mapa](#map_matching) do {{site.data.keyword.iotmapinsights_short}} para identificar o parâmetro do ID do link necessário.

Os dados que são retornados incluem as informações a seguir sobre o ID do link solicitado:

- Tipo de estrada
- Comprimento da estrada
- Uma matriz de pontos de forma detalhados
- Informações sobre nós adjacentes e links adjacentes

Ao consultar informações detalhadas de link de estrada, seu aplicativo pode atravessar
uma rede de link de estrada de forma inteligente usando as informações de link adjacentes que são retornadas.

## Dados dinâmicos do evento
{: #dynamic_event_data}

Além dos dados estáticos do mapa, a condição de mundo real das estradas por necessidades
inclui eventos dinâmicos, tais como congestionamento de tráfego e obras viárias. Use o {{site.data.keyword.iotmapinsights_short}} para criar, gerenciar e incorporar eventos
de tráfego com [procuras de link afetadas](#link_search) para propósitos de planejamento de rota.

### Injetando e excluindo eventos
{: #inject_event}

Use a API REST de injeção de evento de serviço do {{site.data.keyword.iotmapinsights_short}}
para injetar e remover dinamicamente os eventos de tráfego na forma de modelos de objeto de mapa
que são colocados em links de estrada específicos. Cada evento inclui atributos básicos, tais
como coordenadas de GPS, horário de início, tipo de evento, duração do evento e o comprimento afetado da estrada.

Use a interface da API REST de exclusão de evento para remover eventos do mapa quando
eles estão obsoletos.

### Consulta de evento
{: #query_event}

Use a API REST de consulta de evento para obter informações detalhadas sobre todos os eventos dinâmicos em uma determinada área geográfica. É possível consultar por área com um intervalo de
longitude e latitude, além de poder incluir atributos de evento para limitar o número de eventos de destino que são retornados.

## Ferramentas geoespaciais
{: #geospatial_tools}

Aprimore o seu aplicativo com as funções de procura de correspondência de mapa e rotas que são fornecidas pelas ferramentas geoespaciais do {{site.data.keyword.iotmapinsights_short}}.

### Correspondência de mapa
{: #map_matching}

Use a interface da API REST de correspondência de mapa com o seu aplicativo para mapear coordenadas de GPS do dispositivo real para dados da rede viária do[OpenStreetMap](http://www.openstreetmap.org/){: new_window} para aumentar
a precisão de localização para dados de GPS imprecisos. Também é possível receber informações
sobre os atributos de estrada com base no local. A API REST de correspondência de mapa permite que o seu aplicativo ajuste o ponto de dados brutos do GPS para um ponto correspondido no link
de estrada.

A interface de API REST de correspondência de mapa recebe um ponto de dados de coordenadas de GPS de longitude e latitude e retorna um ponto correspondido do mapa. O ponto correspondido no mapa
é analisado ao considerar dados históricos para cada carro dentro de um determinado período
de tempo para localizar o ponto mais provável em tempo real. Para os pontos que não têm dados históricos de localização, a interface de correspondência do mapa retorna o ponto mais próximo
no link de estrada a partir do ponto de GPS solicitado.

### Procura de rota
{: #route_search}

Um dos recursos básicos de um aplicativo com funções geoespaciais é a capacidade de
localizar o caminho mais curto entre dois pontos.  

A interface da API REST de procura de rota do serviço do {{site.data.keyword.iotmapinsights_short}}
calcula o caminho mais curto entre as coordenadas de GPS do ponto de início e do ponto final. As coordenadas recebidas são correspondidas com o link mais próximo do mapa usando a função de correspondência de mapa e o caminho mais curto entre esses pontos correspondidos do mapa é calculado.

### Procura de link afetado
{: #link_search}

Quando um evento ocorre em uma estrada, vários links de estrada podem ser afetados. É
possível usar as APIs REST para procurar links afetados e também localizar links de estrada
nos quais os veículos podem atingir o evento. A procura considera a topologia da rede de
links de estrada, não apenas a distância dos veículos até o evento.
