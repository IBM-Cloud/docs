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

# Introdução ao Compose for Redis
{: #getting-started-with-compose-for-redis}

O Redis é um armazenamento de valores de chave de software livre, na memória. Os valores no Redis podem ser sequências simples, hashes, listas e conjuntos ou bitmaps poderosos, hyperloglogs e índices geoespaciais. O Redis é ideal como um cache do aplicativo ou armazenamento de dados de resposta rápida. O {{site.data.keyword.composeForRedis_full}} dá a você uma configuração pré-ajustada para alta disponibilidade e persistência no disco, tudo bloqueado com recursos de segurança extras.
{:shortdesc}

**Nota:** todas as instâncias de serviço do Compose que foram
provisionadas antes de 14 de setembro de 2016 que ainda estiverem ativas poderão ser
usadas e acessadas diretamente em
[https://www.compose.com/](https://www.compose.com). Qualquer instância
de serviço do Compose que for provisionada desse ponto em diante será diretamente
acessada e usada dentro de sua conta do Bluemix.

Conclua estas etapas para obter uma introdução ao
{{site.data.keyword.composeForRedis}}.

1. [Crie
uma instância do {{site.data.keyword.composeForRedis}}](https://console.ng.bluemix.net/catalog/services/compose-for-redis/).

  Ao criar uma instância do serviço, assegure-se de escolher um nome para seu
serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado. Os diversos valores de credenciais são listados na seção
*Credenciais disponíveis*.

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForRedis}}.

  Para conectar um app ao seu serviço, use as [credenciais](./credentials.html) que são criadas com o serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForRedis}}.

  Faça download do app de amostra
[compose-redis-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-redis-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes de seu
aplicativo no Bluemix, clique em **Visualizar APP**.
