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

# Introdução ao Compose for RethinkDB
{: #getting-started-with-compose-for-rethinkdb}

O {{site.data.keyword.composeForRethinkDB}} dá a você um banco de dados distribuído, baseado em documento JSON, com um console integrado de administração e exploração. O RethinkDB usa a linguagem de consulta ReQL, que é construída com encadeamento de funções e está disponível nas bibliotecas do cliente para Java, JavaScript, Python e Ruby. Com a ReQL, é possível usar os recursos no lado do servidor RethinkDB, como junções e subconsultas distribuídas entre os nós do cluster. O RethinkDB também suporta índices secundários para melhor desempenho de consulta de leitura. O mais poderoso recurso do RethinkDB, changefeeds, permite que muitas consultas ReQL sejam convertidas em feeds em tempo real.
{:shortdesc}

**Nota:** todas as instâncias de serviço do Compose que foram
provisionadas antes de 14 de setembro de 2016 que ainda estiverem ativas poderão ser
usadas e acessadas diretamente em
[https://www.compose.com/](https://www.compose.com). Qualquer instância
de serviço do Compose que for provisionada desse ponto em diante será diretamente
acessada e usada dentro de sua conta do Bluemix.

Conclua estas etapas para obter uma introdução ao
{{site.data.keyword.composeForRethinkDB}}.

1. [Crie
uma instância do {{site.data.keyword.composeForRethinkDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/).

  Ao criar uma instância do serviço, assegure-se de escolher um nome para seu
serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado. Os diversos valores de credenciais são listados na seção
*Credenciais disponíveis*.

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForRethinkDB}}.

   Para conectar um app ao seu serviço, use as [credenciais](./credentials.html) que são criadas com o serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForRethinkDB}}.

   Faça download do app de amostra [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes de seu aplicativo no Bluemix, clique em **Visualizar APP**.
