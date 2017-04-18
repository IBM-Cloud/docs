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

# Introdução ao {{site.data.keyword.composeForRethinkDB}}
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

   Para conectar um app ao seu serviço, use as credenciais que são criadas com o
serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForRethinkDB}}.

   Faça download do app de amostra [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes de seu aplicativo no Bluemix, clique em **Visualizar APP**.

## Credenciais disponíveis

Campo de nome|Descrição
----------|-----------
`uri`|O URI a ser usado na conexão com o serviço. Inclui o esquema
(rethinkdb:), o nome do usuário administrativo e a senha, o nome do host do servidor e o
número da porta à qual se conectar.
`uri_admin`|Um URI que deve ser visitado em um navegador para acessar a
interface de administração do banco de dados. O acesso requer o nome do usuário
administrativo e a senha no campo `uri`.
`ca_certificate_base64`|Um certificado autoassinado que é usado para
confirmar se um aplicativo está se conectando ao servidor apropriado. Isso é codificado
em base64. É preciso decodificar
a chave antes de usá-la, conforme mostrado no aplicativo de amostra.
`deployment_id`|Um identificador interno para o serviço conforme criado
no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `rethink`.
`name`|O nome da implementação do banco de dados.
{: caption="Table 1. {{site.data.keyword.composeForRethinkDB}} credentials" caption-side="top"}

# Links Relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artigos do Compose](https://www.compose.com/articles/){:new_window}

## Tutoriais e amostras
{: #samples}
* [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs){:new_window}

## Links Relacionados
{: #general}
* [Ajuda do Compose](https://help.compose.com/docs){:new_window}
