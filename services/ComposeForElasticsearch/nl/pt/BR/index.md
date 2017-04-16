---

copyright:
  years: 2016
lastupdated: "2016-12-09"
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

  Para conectar um app ao seu serviço, use as credenciais que são criadas com o
serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForElasticsearch}}.

  Faça download do app de amostra
[compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo
no Bluemix, clique em **Visualizar APP** para visualizar o conteúdo do
índice de *exemplos*.

## Credenciais disponíveis

Campo de nome|Descrição
----------|-----------
`uri`|O URI a ser usado na conexão com o serviço. Inclui o esquema (`https:`), o nome do usuário administrativo e a senha, o nome do host do servidor e o número da porta à qual se conectar.
`uri_direct_1`|Um URI alternativo que pode ser usado na conexão com o serviço. Formatado como para `uri`.
`uri_health`|Um comando `curl` que solicita o funcionamento do cluster do primeiro haproxy.
`uri_health_1`|Um comando `curl` que solicita o funcionamento do cluster do segundo haproxy.
`ca_certificate_base64`|Um certificado autoassinado que é usado para confirmar se um aplicativo está se conectando ao servidor apropriado. Isso é codificado em base64. É preciso decodificar
a chave antes de usá-la, conforme mostrado no aplicativo de amostra.
`deployment_id`|Um identificador interno para o serviço conforme criado no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `elastic_search`.
`name`|O nome da implementação do banco de dados.
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**Nota:** dois portais `haproxy` fornecem
acesso ao cluster do Elasticsearch. `uri` e
`uri_direct_1` podem ser usados para conexão com o cluster. Em seus
aplicativos, alterne entre `uri` e `uri_direct_1` para
gerenciar respostas às falhas de conexão.

# Links Relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artigos do Compose](https://www.compose.com/articles/){:new_window}

## Tutoriais e amostras
{: #samples}
* [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs){:new_window}

## Links Relacionados
{: #general}
* [Ajuda do Compose](https://help.compose.com/docs){:new_window}
