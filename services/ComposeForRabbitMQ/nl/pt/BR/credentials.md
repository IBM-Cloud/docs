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
serviço. O aplicativo de amostra [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) demonstra como usar o Node.js para se conectar a um serviço
{{site.data.keyword.composeForRabbitMQ}} usando as credenciais.

Campo de nome|Descrição
----------|-----------
`uri`|O URI a ser usado na conexão com o serviço. Inclui o esquema (`amqps:), o nome do usuário administrativo e a senha, o nome do host do servidor, o número da porta à qual se conectar e o nome do vhost.
`uri_direct_1`|Um URI alternativo que pode ser usado na conexão com o serviço. Formatado conforme `uri`.
`uri_admin`|Um URI que deve ser visitado em um navegador para acessar a interface de administração do banco de dados. O acesso requer o nome do usuário administrativo e a senha no campo `uri`.
`uri_admin_1`|Um URI de administração alternativo - consulte `uri_admin`.
`uri_admin_2`|Um URI de administração alternativo - consulte `uri_admin`.
`uri_admin_3`|Um URI de administração alternativo - consulte `uri_admin`.
`uri_admin_4`|Um URI de administração alternativo - consulte `uri_admin`.
`ca_certificate_base64`|Um certificado autoassinado que é usado para confirmar se um aplicativo está se conectando ao servidor apropriado. Isso é codificado em base64. É preciso decodificar
a chave antes de usá-la, conforme mostrado no aplicativo de amostra.
`deployment_id`|Um identificador interno para o serviço conforme criado no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `rabbitmq`.
`name`|O nome da implementação do banco de dados.
{: caption="Tabela 1. Credenciais do Compose for RabbitMQ" caption-side="top"}
