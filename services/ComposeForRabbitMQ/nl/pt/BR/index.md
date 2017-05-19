---

copyright:
  years: 2016,2017
lastupdated: "2017-04-027"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao Compose for RabbitMQ
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

  Para conectar um app ao seu serviço, use as [credenciais](./credentials.html) que são criadas com o serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForRabbitMQ}}.

  Faça download do app de amostra
[compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes de seu
aplicativo no Bluemix, clique em **Visualizar APP**.
