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


Para conectar um app ao seu serviço, use as credenciais que são criadas com o serviço. O aplicativo de amostra [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) demonstra como usar o Node.js para se conectar a um serviço {{site.data.keyword.composeForEtcd}} usando as credenciais.

Campo de nome|Descrição
----------|-----------
`ca_certificate_base64`|Um certificado autoassinado que é usado para confirmar se um app está se conectando ao servidor apropriado. O certificado é codificado em base64. Deve-se decodificar a chave antes de usá-la, conforme mostrado no app de amostra. `deployment_id`|Um identificador interno para o serviço conforme criado no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `etcd`.
`name`|O nome da implementação do banco de dados.
`uri`|O URI a ser usado na conexão com o serviço. `uri` inclui o esquema (`amqps:), o nome do usuário administrativo e a senha, o nome do host do servidor, o número da porta à qual se conectar e o `nome do vhost.
{: caption="Tabela 1. Credenciais do Compose for etcd" caption-side="top"}
