---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# O que há de novo no {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}
{: #what-is-new}


## Novo a partir de março de 2017
{: #mar-2017}

A atualização de março de 2017 do {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} introduziu as mudanças a seguir:

   * O painel do {{site.data.keyword.Bluemix_notm}} Mobile é agora o {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}.
   * A criação do projeto foi projetada novamente para incluir tipos padrão de servidor de Web App, BFF e Microservice com suporte para Node.js, Java e Swift.
   * A integração com o serviço {{site.data.keyword.appid_full}} novo e melhorado fornece autenticação para projetos Móveis e da Web.
   * Agora também é possível gerar SDKs para seus projetos usando o [plug-in do SDK Generator](sdk_cli.html). A geração de SDK no {{site.data.keyword.dev_console}} está disponível apenas para projetos móveis.
   * Agora também é possível criar projetos usando a [{{site.data.keyword.dev_cli_short}}](dev_cli.html).


## Novo a partir de janeiro de 2017
{: #jan-2017}

A atualização de janeiro de 2017 do painel do {{site.data.keyword.Bluemix_notm}} Mobile introduziu as mudanças a seguir:

   * A partir de 31 de janeiro, os Iniciadores de UI foram descontinuados. Os projetos existentes que foram criados por meio de um Iniciador de UI podem ser usados até 30 de abril de 2017. Para obter mais informações sobre as etapas de migração e as datas de remoção, veja a [postagem do blog de anúncio de descontinuação ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-mobile-dashboard-update/).
{: deprecated}
   * Agora é possível atualizar seu tipo de iniciador de projeto, em vez de excluir o projeto e criar um novo.
   * Agora é possível criar seu projeto com um Iniciador de código [Watson Conversation](tutorial_conversation.html).
   * Quando for suportado, agora será possível gerar um SDK para seu projeto.
   * Agora é possível incluir suas instâncias de [Cálculo](sdk_compute.html) existentes e gerar SDKs do cliente para incluir em seu projeto.


## Novo a partir de dezembro de 2016
{: #dec-2016}

A atualização de dezembro de 2016 do painel do {{site.data.keyword.Bluemix_notm}} Mobile introduziu as mudanças a seguir:

   * Agora é possível remover um serviço conectado de um projeto para que ele possa ser excluído ou reutilizado com outro projeto. 
   * Agora é possível incluir um serviço existente em um projeto.
   * Agora é possível criar ou conectar um serviço CloudantNoSQL existente como uma origem de dados quando você usa um Iniciador de código.
   * Quando for suportado, agora será possível criar ou conectar um serviço Object Storage existente como uma origem de dados para seu projeto.
   * Agora é possível customizar o design de navegação do app que você está criando com um Iniciador de UI. 
   

## Novo a partir de novembro de 2016
{: #nov-2016}

A atualização de novembro de 2016 do painel do {{site.data.keyword.Bluemix_notm}} Mobile introduziu as
mudanças a seguir:

   * Agora é possível gerar artefatos do SDK (kit de desenvolvimento de software) para seus projetos na página **Código**.
   * Agora o Cordova é suportado para o Iniciador de código Basic.
   * Agora é possível [relatar eventos de rede ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} e [monitorar solicitações de rede ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window} na página **Solicitações de rede** do console do {{site.data.keyword.mobileanalytics_short}}.
   * Agora é possível [exportar dados para o dashDB ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window} no console do {{site.data.keyword.mobileanalytics_short}}.


## Novo a partir de outubro de 2016
{: #oct-2016}

A atualização de outubro de 2016 do painel do {{site.data.keyword.Bluemix_notm}} Mobile introduziu as mudanças a seguir:

   * Agora é possível incluir os recursos {{site.data.keyword.mobilepushshort}} e Analytics em seu projeto diretamente do painel.
   * [Iniciadores de código](starters.html#Code_Starter) agora estão disponíveis.
   * É possível incluir Autenticação nos projetos que você criou a partir de um Iniciador de código.
   * Swift agora é suportado.


### Analytics
{: #analytics notoc}

   * O modo demo é ativado por padrão quando você inclui o recurso de Analítica. É possível desativar o modo demo para visualizar a analítica depois de executar o app.


### UI Builder
{: #ui_builder notoc}

   * O recurso **{{site.data.keyword.mobilepushshort}}** é agora acessado a partir do projeto.
   * A guia **Configurações do projeto** foi renomeada para a guia **Configurações**.
   * A guia **Autenticação** foi renomeada para a guia **Acesso do usuário**.


### Código
{: #code notoc}

   * O código gerado Objective-C e Swift para iOS agora usa CocoaPods para gerenciar dependências. Isso significa que você precisa instalar o CocoaPods. Para instalá-lo, execute `sudo gem install cocoapods`. Após a instalação do CocoaPods, execute `pod setup` para configurá-lo (se não estiver ainda). Por último, execute `pod install` para fazer download e instalar as dependências necessárias do projeto antes de abrir o arquivo `.xcworkspace` no Xcode. Detalhes adicionais estão disponíveis no arquivo `README.md` no archive de código transferido por download. Leia sobre [Ferramentas de pré-requisito do desenvolvedor](get_code.html#prereq-dev-tools) para obter mais informações.

Verifique novamente várias vezes para se manter em dia com novas atualizações.
