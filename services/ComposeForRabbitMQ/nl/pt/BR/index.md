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

# Introdução ao {{site.data.keyword.composeForRabbitMQ}}
{: #getting-started-with-compose-for-rabbitmq}

O RabbitMQ manipula de forma assíncrona as mensagens entre aplicativos e
bancos de dados, permitindo a separação das camadas de dados e aplicativos. O RabbitMQ
permite aos desenvolvedores rotear, rastrear e enfileirar mensagens com níveis de
persistência, configurações de entrega e publicação confirmada customizáveis. Usando o
{{site.data.keyword.composeForRabbitMQ_full}}, você obtém acesso à interface
administrativa fácil de usar com um host de recursos de gerenciamento, como monitoramento
de implementação, ajuste de escala com um clique de um botão, configuração do usuário e
acesso ao arquivo de log.
{:shortdesc}

**Nota:** todas as instâncias de serviço do Compose que foram
provisionadas antes de 14 de setembro de 2016 que ainda estiverem ativas poderão ser
usadas e acessadas diretamente em
[https://www.compose.com/](https://www.compose.com). Qualquer instância
de serviço do Compose que for provisionada desse ponto em diante será diretamente
acessada e usada dentro de sua conta do Bluemix.

Conclua estas etapas para obter uma introdução ao
{{site.data.keyword.composeForRabbitMQ}}.

1. [Crie
uma instância do {{site.data.keyword.composeForRabbitMQ}}](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  Ao criar uma instância do serviço, assegure-se de escolher um nome para seu
serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado.  Os diversos valores de credenciais são listados na seção
*Credenciais disponíveis*.

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForRabbitMQ}}.

  Para conectar um app ao seu serviço, use as credenciais que são criadas com o
serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForRabbitMQ}}.

  Faça download do app de amostra
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes de seu
aplicativo no Bluemix, clique em **Visualizar APP**.

## Credenciais disponíveis

Campo de nome|Descrição
----------|-----------
``uri``|O URI a ser usado na conexão com o serviço. Inclui o esquema (`amqps:), o nome do usuário administrativo e a senha, o nome do host do servidor, o número da porta à qual se conectar e o nome do vhost.
`uri_direct_1`|Um URI alternativo que pode ser usado na conexão com o serviço. Formatado conforme `uri`.
`uri_admin`|Um URI que deve ser visitado em um navegador para acessar a interface de administração do banco de dados. O acesso requer o nome do usuário administrativo e a senha no campo `uri`.
`uri_admin_1`|Um URI de administração alternativo - consulte `uri_admin`.
`uri_admin_2`|Um URI de administração alternativo - consulte `uri_admin`.
`uri_admin_3`|Um URI de administração alternativo - consulte `uri_admin`.
`uri_admin_4`|Um URI de administração alternativo - consulte `uri_admin`.
`ca_certificate_base64`|Um certificado autoassinado que é usado para
confirmar se um aplicativo está se conectando ao servidor apropriado. Isso é codificado
em base64. É preciso decodificar
a chave antes de usá-la, conforme mostrado no aplicativo de amostra.
`deployment_id`|Um identificador interno para o serviço conforme criado no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `rabbitmq`.
`name`|O nome da implementação do banco de dados.
{: caption="Table 1. {{site.data.keyword.composeForRabbitMQ}} credentials" caption-side="top"}

# Links Relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artigos do Compose](https://www.compose.com/articles/){:new_window}

## Tutoriais e amostras
{: #samples}
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs){:new_window}

## Links Relacionados
{: #general}
* [Ajuda do Compose](https://help.compose.com/docs){:new_window}
