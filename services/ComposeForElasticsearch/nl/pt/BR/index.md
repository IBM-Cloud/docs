---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

O {{site.data.keyword.composeForElasticsearch_full}} combina o poder de um
mecanismo de procura de texto completa com os potenciais de indexação de um banco de
dados de documento JSON. Juntos, eles criam uma ferramenta poderosa para análise de dados
ricos em grandes volumes de dados. Com o Elasticsearch, sua procura pode ser pontuada
para fins de exatidão, permitindo que você pesquise a fundo seu conjunto de dados em busca de
correspondências próximas e quase perdas que você possa estar deixando passar.
{:shortdesc}

**Nota:** todas as instâncias de serviço do Compose que foram
provisionadas antes de 14 de setembro de 2016 que ainda estiverem ativas poderão ser
usadas e acessadas diretamente em
[https://www.compose.com/](https://www.compose.com). Qualquer instância
de serviço do Compose que for provisionada desse ponto em diante será diretamente
acessada e usada dentro de sua conta do Bluemix.

Conclua estas etapas para obter uma introdução ao {{site.data.keyword.composeForElasticsearch}}:

1. [Crie uma instância do {{site.data.keyword.composeForElasticsearch}}](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/).

  Ao criar uma instância do serviço, assegure-se de escolher um nome para seu
serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado. Os diversos valores de credenciais são listados na seção
*Credenciais disponíveis*.

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForElasticsearch}}.

  Para conectar um app ao seu serviço, use as [credenciais](./credentials.html) que são criadas com o serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForElasticsearch}}.

  Faça download do app de amostra
[compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo
no Bluemix, clique em **Visualizar APP** para visualizar o conteúdo do
índice de *exemplos*.
