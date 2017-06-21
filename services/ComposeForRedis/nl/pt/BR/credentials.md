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

Para conectar um app ao seu serviço, use as credenciais que são criadas com o
serviço. O aplicativo de amostra [compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs) demonstra como usar o Node.js para se conectar a um serviço {{site.data.keyword.composeForRedis}} usando as credenciais.

Campo de nome|Descrição
----------|-----------
`uri`|O URI a ser usado na conexão com o serviço, que inclui o esquema (redis:), o nome do usuário administrativo e a senha, o nome do host do servidor e o número da porta à qual se conectar.
`uri_cli`|Uma linha de comando `redis-cli` que se conecta à instância de banco de dados.
`deployment_id`|Um identificador interno para o serviço conforme criado no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `redis`.
`name`|O nome da implementação do banco de dados.
{: caption="Tabela 1. Credenciais do Compose for Redis" caption-side="top"}
