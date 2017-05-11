---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Minhas APIs
{: #manage_api}

Use a guia **Visualizar APIs Gerenciadas** para ver o status geral das APIs que você gerencia e daquelas que gerenciou anteriormente, mas que não estão atualmente expostas. Na guia **APIs Compartilhadas**, é possível ver todas as APIs que foram compartilhadas com sua organização do {{site.data.keyword.Bluemix_notm}} por meio do gerenciamento de API ou por meio do serviço do {{site.data.keyword.apiconnect_short}}.

É possível visualizar todas as APIs que você gerencia em conjunto com o gerenciamento de API usando o painel APIs. 

## Visualizando APIs gerenciadas
{: #view_api}

Aqui é possível visualizar APIs criadas para ações do {{site.data.keyword.openwhisk_short}} e outras origens externas.

1. No Painel do {{site.data.keyword.Bluemix_notm}}, selecione o ícone **Menu** > **Serviços** > **APIs**.
2. Para selecionar sua origem, clique em **Gerenciar APIs**. Uma lista das APIs que são gerenciadas atualmente é exibida. Os tipos de APIs incluem os tipos a seguir:
    * Terminais definidos pelo usuário - Essas entradas são APIs que estão fora do ambiente do {{site.data.keyword.Bluemix_notm}} e são rastreadas por seu terminal de URL. 
    * Apps do {{site.data.keyword.openwhisk_short}} - Essas entradas são ações do {{site.data.keyword.openwhisk_short}} que foram agrupadas dentro de uma API.

Selecione o nome de uma API para visualizar mais detalhes sobre ela.

## Criando APIs gerenciadas
{: #create_mgd_api}

É possível incluir uma API na lista sem sair da lista de APIs gerenciadas selecionando **Criar API gerenciada**.

Depois de selecionar se você deseja criar uma API do {{site.data.keyword.openwhisk_short}} ou do Proxy de API (externo), insira as informações para sua nova API.  

Esse é o único local onde é possível incluir um Proxy de API ou API externa. Uma API externa é aquela que não é criada ou armazenada no espaço da organização do {{site.data.keyword.Bluemix_notm}}. É possível gerenciar uma API externa especificando a URL de seu terminal externo. Isso é útil quando você está testando o gerenciamento de API para ver se ele atende às suas necessidades ou quando já possui APIs que estão em execução com URLs existentes que você não deseja interromper. 

Consulte [Gerenciar APIs](manage_apis.html) para obter informações adicionais sobre as configurações necessárias para criar APIs.

## Trabalhando com APIs compartilhadas
{: #share_api}

Na guia **Explorar APIs Compartilhadas** é possível visualizar APIs que foram criadas por outros e compartilhadas com você. Também é possível criar chaves API para as APIs associadas às ações do {{site.data.keyword.openwhisk_short}} e ao serviço do {{site.data.keyword.appconserviceshort}}.

1. No Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Menu** > **Serviços** > **APIs**.
2. Selecione **Explorar APIs Compartilhadas** na navegação. Todas as APIs que você pode consumir são exibidas aqui.
3. Para consumir uma API, selecione-a para abrir seu Portal do desenvolvedor, no qual é possível assinar um plano para usá-la. 
4. Depois de selecionar uma API para gerenciar, consulte [Gerenciar APIs](manage_apis.html) para obter mais informações sobre como concluir as tarefas a seguir: 
    * Visualizar uso da API
    * Criar chaves API
    * Usar o Explorador de API para visualizar a documentação e testar a API.
