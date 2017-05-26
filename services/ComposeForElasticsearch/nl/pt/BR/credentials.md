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

# Credenciais Disponíveis
{: #available-credentials}

Para conectar um app ao seu serviço, use as credenciais que são criadas com o serviço. O aplicativo de amostra [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) demonstra como usar o Node.js para se conectar ao serviço {{site.data.keyword.composeForElasticsearch}} usando as credenciais.

Campo de nome|Descrição
----------|-----------
`uri`|O URI a ser usado na conexão com o serviço. Inclui o esquema (`https:`), o nome do usuário administrativo e a senha, o nome do host do servidor e o número da porta à qual se conectar.
`uri_direct_1`|Um URI alternativo que pode ser usado na conexão com o serviço. Formatado como para `uri`.
`uri_health`|Um comando `curl` que solicita o funcionamento do cluster do primeiro haproxy.
`uri_health_1`|Um comando `curl` que solicita o funcionamento do cluster do segundo haproxy.
`ca_certificate_base64`|Um certificado autoassinado que é usado para confirmar se um aplicativo está se conectando ao servidor apropriado. Isso é codificado em base64. É preciso decodificar a chave antes de usá-la, conforme mostrado no aplicativo de amostra.
`deployment_id`|Um identificador interno para o serviço conforme criado no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `elastic_search`.
`name`|O nome da implementação do banco de dados.
{: caption="Tabela 1. Credenciais do Compose for Elasticsearch" caption-side="top"}

**Nota:** dois portais `haproxy` fornecem acesso ao cluster do Elasticsearch. `uri` e `uri_direct_1` podem ser usados para conexão com o cluster. Em seus aplicativos, alterne entre `uri` e `uri_direct_1` para gerenciar respostas às falhas de conexão.
