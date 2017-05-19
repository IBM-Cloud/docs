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

# Introdução ao Compose for PostgreSQL
{: #getting-started-with-compose-for-postgreSQL}

O {{site.data.keyword.composeForPostgreSQL}} fornece um poderoso banco
de dados objeto-relacional de software livre que é altamente customizável. Com Postgres, o
desenvolvimento é rápido e facilmente escalável. É possível desenvolver em uma linguagem
com a qual você está acostumado, como C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP,
ASP e Java. Você obtém um banco de dados corporativo rico em recursos com suporte JSON,
proporcionando a você o melhor dos mundos SQL e NoSQL.
{:shortdesc}

**Nota:** todas as instâncias de serviço do Compose que foram
provisionadas antes de 14 de setembro de 2016 que ainda estiverem ativas poderão ser
usadas e acessadas diretamente em
[https://www.compose.com/](https://www.compose.com). Qualquer instância
de serviço do Compose que for provisionada desse ponto em diante será diretamente
acessada e usada dentro de sua conta do Bluemix.

Conclua estas etapas para obter uma introdução ao Compose for PostgreSQL:

1. [Crie
uma instância do {{site.data.keyword.composeForPostgreSQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/).

  Ao criar uma instância do serviço, assegure-se de escolher um nome para seu
serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado. Os diversos valores de credenciais são listados na seção
*Credenciais disponíveis*.

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForPostgreSQL}}.

  Para conectar um app ao seu serviço, use as [credenciais](./credentials.html) que são criadas com o serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForPostgreSQL}}.

  Faça download do app de amostra
[compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo
no Bluemix, clique em **Visualizar APP** para visualizar o conteúdo da
tabela de *exemplos*.
