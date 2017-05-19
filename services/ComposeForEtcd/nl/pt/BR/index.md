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

# Introdução ao Compose for etcd
{: #getting-started-with-compose-for-etcd}

etcd é um armazenamento de valores de chave que contém os dados sempre corretos necessários para coordenar e gerenciar seu cluster de servidores para gerenciamento de
configuração de servidor distribuído. O etcd usa o algoritmo RAFT de consenso para
assegurar a consistência de dados no cluster. Ele impõe a ordem na qual as operações
ocorrem nos dados para que cada nó no cluster chegue ao mesmo resultado da mesma maneira. O
{{site.data.keyword.composeForEtcd_full}} inclui backups automáticos dos dados de
configuração que estão armazenados no etcd. Uma interface administrativa intuitiva
permite que você monitore, escale e administre sua implementação com facilidade.
{:shortdesc}

**Nota:** todas as instâncias de serviço do Compose que foram
provisionadas antes de 14 de setembro de 2016 que ainda estiverem ativas poderão ser
usadas e acessadas diretamente em
[https://www.compose.com/](https://www.compose.com). Qualquer instância
de serviço do Compose que for provisionada desse ponto em diante será diretamente
acessada e usada dentro de sua conta do Bluemix.

Conclua estas etapas para obter uma introdução ao {{site.data.keyword.composeForEtcd}}.

1. [Crie
uma instância do {{site.data.keyword.composeForEtcd}}](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/).

  Ao criar uma instância do serviço, assegure-se de escolher um nome para seu
serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado. Os diversos valores de credenciais são listados na seção
*Credenciais disponíveis*.

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForEtcd}}.

Para conectar um app ao seu serviço, use as [credenciais](./credentials.html) que são criadas com o serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForEtcd}}.

Faça download do app de amostra
[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo
no Bluemix, clique em **Visualizar APP** para visualizar o conteúdo
dos *exemplos*.
