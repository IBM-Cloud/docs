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

Para conectar um app ao seu serviço, use as credenciais que são criadas com o serviço. O aplicativo de amostra [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) demonstra como usar o Node.js para se conectar a
um serviço {{site.data.keyword.composeForPostgreSQL}} usando as credenciais.

Campo de nome|Descrição
----------|-----------
`uri`|O URI a ser usado na conexão com o serviço. Inclui o esquema (`postgres:`), o nome do usuário administrativo e a senha, o nome do host do servidor, o número da porta à qual se conectar, o nome do banco de dados e "?ssl=true" para ativar conexões SSL.
`uri_cli`|Uma linha de comando shell `psql` que se conecta à instância de banco de dados.
`ca_certificate_base64`|Um certificado autoassinado que é usado para confirmar se um aplicativo está se conectando ao servidor apropriado. Isso é codificado em base64. É preciso decodificar a chave antes de usá-la, conforme mostrado no aplicativo de amostra. `deployment_id`|Um identificador interno para o serviço conforme criado no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `postgresql`.
`name`|O nome da implementação do banco de dados.
{: caption="Tabela 1. Credenciais do Compose for PostgreSQL" caption-side="top"}
