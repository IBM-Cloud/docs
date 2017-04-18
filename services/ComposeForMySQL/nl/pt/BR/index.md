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

# Introdução ao Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Com um subconjunto amplo de ANSI SQL 99 e um vasto conjunto de suas próprias extensões, incluindo o documento JSON, a procura de texto completa e as visualizações atualizáveis, o MySQL oferece uma paleta rica para desenvolvedores usarem em seus aplicativos. Os administradores também podem localizar uma ampla seleção de ferramentas de gerenciamento de banco de dados que podem funcionar com o MySQL. O {{site.data.keyword.composeForMySQL_full}} faz o MySQL ampliar os recursos de MySQL, gerenciando-o para você, oferecendo um sistema de implementação fácil e de escala automática que oferece alta
disponibilidade e redundância, além de backups automatizados.
{:shortdesc}

**Observação:** o {{site.data.keyword.composeForMySQL_full}} não concede acesso à interface com o usuário do Compose. Consulte [Suporte ao Compose no Bluemix](https://help.compose.com/docs/bluemix-compose-support) para obter mais detalhes.

Conclua estas etapas para obter uma introdução ao {{site.data.keyword.composeForMySQL}}:

1. [Crie uma instância do {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

   Ao criar uma instância do serviço, escolha um nome para seu serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado.  Os vários valores de credencial são listados na seção "Credenciais disponíveis".

2. Conecte-se ao seu serviço do {{site.data.keyword.composeForMySQL}}.

  Para conectar um aplicativo ao seu serviço, use as credenciais que são criadas com o serviço. 

  Faça download do aplicativo de amostra [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) e siga as instruções no arquivo leia-me. Em seguida, na página de detalhes do aplicativo no console do Bluemix, clique em **Visualizar app**.

  O aplicativo de amostra demonstra como usar o Node.js para se conectar a um serviço do {{site.data.keyword.composeForMySQL}}.


## Credenciais disponíveis

Campo de nome|Descrição
----------|-----------
`db_type`|O tipo de banco de dados que é oferecido pelo serviço, nesse caso `mysql`.
`name`|O nome da implementação do banco de dados.
`uri_cli`|Uma linha de comandos shell `mysql` que se conecta à instância de banco de dados.
`ca_certificate_base64`|Um certificado autoassinado que é usado para confirmar se um aplicativo está se conectando ao servidor apropriado. O certificado é codificado em base64.
`deployment_id`|Um identificador interno para o serviço conforme criado
no Compose.
`uri`|O URI que é usado ao se conectar ao serviço, que inclui o esquema (`mysql:`), o nome do usuário administrativo e a senha, o nome do host do servidor, o número da porta à qual se conectar e o nome do vhost.
{: caption="Table 1. {{site.data.keyword.composeForMySQL}} credentials" caption-side="top"}


# Links Relacionados
{: #rellinks}

* [Compose](https://www.compose.com){:new_window}
* [Artigos do Compose](https://www.compose.com/articles/){:new_window}

## Tutoriais e amostras
{: #samples}
* [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs){:new_window}

## Links Relacionados
{: #general}
* [Ajuda do Compose](https://help.compose.com/docs){:new_window}
