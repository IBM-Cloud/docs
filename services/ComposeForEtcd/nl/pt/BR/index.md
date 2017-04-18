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

# Introdução ao {{site.data.keyword.composeForEtcd}}
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

Para conectar um app ao seu serviço, use as credenciais que são criadas com o
serviço. O app de amostra demonstra como usar o Node.js para se conectar a um serviço do
{{site.data.keyword.composeForEtcd}}.

Faça download do app de amostra
[compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs)
e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo
no Bluemix, clique em **Visualizar APP** para visualizar o conteúdo
dos *exemplos*.

## Credenciais disponíveis

Campo de nome|Descrição
----------|-----------
`ca_certificate_base64`|Um certificado autoassinado que é usado para
confirmar se um app está se conectando ao servidor apropriado. O certificado é codificado
em base64. Deve-se decodificar a chave antes de usá-la, conforme mostrado no aplicativo de amostra.
`deployment_id`|Um identificador interno para o serviço conforme criado
no Compose.
`db_type`|O tipo de banco de dados que é oferecido pelo serviço; nesse caso, `etcd`.
`name`|O nome da implementação do banco de dados.
`uri`|O URI a ser usado na conexão com o serviço. `uri`
inclui o esquema (`amqps:), o nome do usuário administrativo e a senha, o nome do
host do servidor, o número da porta à qual se conectar e o `nome do vhost.
{: caption="Table 1. {{site.data.keyword.composeForEtcd}} credentials" caption-side="top"}

# Links Relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artigos do Compose](https://www.compose.com/articles/){:new_window}

## Tutoriais e amostras
{: #samples}
* [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs){:new_window}

## Links Relacionados
{: #general}
* [Ajuda do Compose](https://help.compose.com/docs){:new_window}
