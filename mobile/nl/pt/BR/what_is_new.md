---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# O que há de novo no painel Móvel
{: #what_is_new}

### Novo a partir de: dezembro de 2016
{: #dec-2016}

A atualização de dezembro de 2016 do painel do {{site.data.keyword.Bluemix}} Mobile introduziu as mudanças a seguir:

   * É possível remover um serviço conectado de um projeto para que possa ser excluído ou reutilizado com outro projeto. 
   * É possível incluir um serviço existente em um projeto.
   * É possível criar ou conectar um serviço CloudantNoSQL existente como uma origem de dados quando você usa um iniciador de código.
   * Quando for suportado, será possível criar ou conectar um serviço de Armazenamento de objetos existente como uma origem de dados para seu projeto.
   * É possível customizar o design de navegação do app que você está criando com um iniciador de UI. 
   

### Novo a partir de: novembro de 2016
{: #nov-2016}

A atualização de novembro de 2016 do painel do {{site.data.keyword.Bluemix}} Mobile introduziu as
mudanças a seguir:

   * Agora é possível gerar artefatos do SDK (kit de desenvolvimento de software) para seus projetos na página **Código**.
   * Agora o Cordova é suportado para o Iniciador de código Basic.
   * Agora é possível [relatar eventos de rede ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/sdk.html#network-requests "Ícone de link externo"){: new_window} e [monitorar solicitações de rede ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests "Ícone de link externo"){: new_window} na página **Solicitações de rede** do Console do {{site.data.keyword.mobileanalytics_short}}.
   * Agora é possível [exportar dados para o dashDB ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/mobileanalytics/app-monitoring.html#dashdb "Ícone de link externo"){: new_window} no Console do {{site.data.keyword.mobileanalytics_short}}.


### Novo a partir de outubro de 2016
{: #oct-2016}

A atualização de outubro de 2016 do painel do {{site.data.keyword.Bluemix_notm}} Mobile introduziu as mudanças a seguir:

   * Agora é possível incluir os recursos {{site.data.keyword.mobilepushshort}} e Analytics em seu projeto diretamente do painel.
   * [Iniciadores de código](starters.html#Code_Starter) agora estão disponíveis.
   * É possível incluir Autenticação nos projetos que você criou a partir de um Iniciador de código.
   * Swift agora é suportado.


#### Analytics
{: #analytics}

   * O modo demo é ativado por padrão quando você inclui o recurso de Analítica. É possível desativar o modo demo para visualizar a analítica depois de executar o app.


#### UI Builder
{: #ui_builder}

   * O recurso **{{site.data.keyword.mobilepushshort}}** é agora acessado a partir do projeto.
   * A guia **Configurações do projeto** foi renomeada para a guia **Configurações**.
   * A guia **Autenticação** foi renomeada para a guia **Acesso do usuário**.


#### Código
{: #code}

   * O código gerado Objective-C e Swift para iOS agora usa CocoaPods para gerenciar dependências. Isso significa que você precisa instalar o CocoaPods. Para instalá-lo, execute `sudo gem install cocoapods`. Após a instalação do CocoaPods, execute `pod setup` para configurá-lo (se não estiver ainda). Por último, execute `pod install` para fazer download e instalar as dependências necessárias do projeto antes de abrir o arquivo `.xcworkspace` no Xcode. Detalhes adicionais estão disponíveis no arquivo `README.md` no archive de código transferido por download. Leia sobre [Ferramentas de pré-requisito do desenvolvedor](get_code.html#prereq-dev-tools) para obter mais informações.

Verifique novamente várias vezes para se manter em dia com novas atualizações.
