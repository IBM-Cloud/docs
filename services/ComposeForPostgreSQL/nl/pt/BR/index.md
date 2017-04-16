---

copyright:
  years: 2016
lastupdated: "2016-12-09"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao {{site.data.keyword.composeForPostgreSQL}}
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

  Para conectar um app ao seu serviço, use as credenciais que são criadas com o
serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForPostgreSQL}}.

  Faça download do app de amostra
[compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo
no Bluemix, clique em **Visualizar APP** para visualizar o conteúdo da
tabela de *exemplos*.

## Credenciais disponíveis

Campo de nome|Descrição
----------|-----------
`uri`|O URI a ser usado na conexão com o serviço. Inclui o esquema
(`postgres:`), o nome do usuário administrativo e a senha, o nome do
host do servidor, o número da porta à qual se conectar, o nome do banco de dados e
"?ssl=true" para ativar conexões SSL.
`uri_cli`|Uma linha de comando shell `psql` que se conecta à instância de banco de dados.
`ca_certificate_base64`|Um certificado autoassinado que é usado para
confirmar se um aplicativo está se conectando ao servidor apropriado. Isso é codificado
em base64. É preciso decodificar
a chave antes de usá-la, conforme mostrado no aplicativo de amostra.
`deployment_id`|Um identificador interno para o serviço conforme criado
no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse
caso, `postgresql`.
`name`|O nome da implementação do banco de dados.
{: caption="Table 1. {{site.data.keyword.composeForPostgreSQL}} credentials" caption-side="top"}

# Links Relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artigos do Compose](https://www.compose.com/articles/){:new_window}

## Tutoriais e amostras
{: #samples}
* [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs){:new_window}

## Links Relacionados
{: #general}
* [Ajuda do Compose](https://help.compose.com/docs){:new_window}
