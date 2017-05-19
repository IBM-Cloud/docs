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

   Para conectar um aplicativo ao seu serviço, use as [credenciais](./credentials.html) que são criadas com o serviço.

   Faça download do aplicativo de amostra [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo no console do Bluemix, clique em **Visualizar app**.

   O aplicativo de amostra demonstra como usar o Node.js para se conectar a um serviço do {{site.data.keyword.composeForScyllaDB}}.
