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

# Introdução ao Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB é uma substituição no local para o banco de dados distribuído de coluna ampla do Cassandra. O ScyllaDB é escrito em C++, em vez de Java do Cassandra, para um melhor uso dos recursos, o que pode resultar em um desempenho 10 vezes melhor em avaliações de desempenho. Além disso, para retenção de compatibilidade com a ferramenta Cassandra e os arquivos de dados, o ScyllaDB inclui recursos de autoajuste. O {{site.data.keyword.composeForScyllaDB_full}} amplia os recursos do ScyllaDB gerenciando-o para você, oferecendo um sistema de implementação fácil e de escala automática que oferece alta
disponibilidade e redundância, além de backups automatizados.
{:shortdesc}

**Observação:** o {{site.data.keyword.composeForScyllaDB_full}} não concede acesso à interface com o usuário do Compose. Consulte [Suporte ao Compose no Bluemix](https://help.compose.com/docs/bluemix-compose-support) para obter mais detalhes.

Conclua estas etapas para obter uma introdução ao {{site.data.keyword.composeForScyllaDB}}:

1. [Crie uma instância do {{site.data.keyword.composeForScyllaDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   Ao criar uma instância do serviço, escolha um nome para seu serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado. Os vários valores de credencial são listados na seção "Credenciais disponíveis".

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForScyllaDB}}.

   Para conectar um aplicativo ao seu serviço, use as credenciais que são criadas com o serviço. 

   Faça download do aplicativo de amostra [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo no console do Bluemix, clique em **Visualizar app**.

   O aplicativo de amostra demonstra como usar o Node.js para se conectar a um serviço do {{site.data.keyword.composeForScyllaDB}}.


## Credenciais disponíveis

Campo de nome|Descrição
----------|-----------
`db_type`|O tipo de banco de dados que é oferecido pelo serviço, nesse caso `scylla`.
`uri_cli_1`|Uma linha de comandos shell `cqlsh` alternativa que se conecta à instância de banco de dados.
`maps`|Um mapa de conexão do ScyllaDB que fornece as informações que são necessárias por vários drivers para associar endereços IP internos aos nomes DNS externos de um banco de dados ScyllaDB.
`name`|O nome da implementação do banco de dados.
`uri_cli`|Uma linha de comandos shell `cqlsh` que se conecta à instância de banco de dados.
`uri_direct_2`|Um URI alternativo que pode ser usado para se conectar ao serviço. Formatado como para `uri`.
`uri_direct_1`|Um URI alternativo que pode ser usado para se conectar ao serviço. Formatado como para `uri`.
`ca_certificate_base64`|Um certificado autoassinado que é usado para confirmar se um aplicativo está se conectando ao servidor apropriado. O certificado é codificado em base64.
`deployment_id`|Um identificador interno para o serviço conforme criado
no Compose.
`uri_cli_2`|Uma linha de comandos shell `cqlsh` alternativa que se conecta à instância de banco de dados.
`uri`|O URI que é usado ao se conectar ao serviço, que inclui o esquema (`scylla:`), a senha, o nome do host do servidor, o número da porta à qual se conectar e o nome do banco de dados.
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} credentials" caption-side="top"}


# Links Relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artigos do Compose](https://www.compose.com/articles/){:new_window}

## Tutoriais e amostras
{: #samples}
* [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs){:new_window}

## Links Relacionados
{: #general}
* [Ajuda do Compose](https://help.compose.com/docs){:new_window}
