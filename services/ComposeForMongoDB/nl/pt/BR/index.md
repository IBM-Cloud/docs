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

# Introdução ao Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

O {{site.data.keyword.composeForMongoDB_full}} usa indexação e
consulta poderosas, agregação e amplo suporte a driver do MongoDB que fizeram dele
o melhor armazenamento de dados JSON para muitas startups e empresas. O
{{site.data.keyword.composeForMongoDB}} oferece um sistema de implementação
fácil de auto-scaling. Ele entrega alta disponibilidade e redundância, backups contínuos
automatizados e sob demanda, ferramentas de monitoramento, integração em sistemas de
alerta, visualizações de análise de desempenho e muito mais, tudo isso em uma interface
com o usuário limpa e simples.
{:shortdesc}

**Nota:** todas as instâncias de serviço do Compose que foram
provisionadas antes de 14 de setembro de 2016 que ainda estiverem ativas poderão ser
usadas e acessadas diretamente em
[https://www.compose.com/](https://www.compose.com). Qualquer instância
de serviço do Compose que for provisionada desse ponto em diante será diretamente
acessada e usada dentro de sua conta do Bluemix.

Conclua estas etapas para obter uma introdução ao
{{site.data.keyword.composeForMongoDB}}:

1. [Crie
uma instância do {{site.data.keyword.composeForMongoDB}}](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/).

   Ao criar uma instância do serviço, assegure-se de escolher um nome para seu
serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado.  Os diversos valores de credenciais são listados na seção
*Credenciais disponíveis*.

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForMongoDB}}.

   Para conectar um app ao seu serviço, use as [credenciais](./credentials.html) que são criadas com o serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForMongoDB}}.

   Faça download do app de amostra
[compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes de seu aplicativo
no Bluemix, clique em **Visualizar APP**.
