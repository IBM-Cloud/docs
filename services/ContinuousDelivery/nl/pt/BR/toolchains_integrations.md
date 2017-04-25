---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}    

# Configurando integrações de ferramenta
{: #integrations}

É possível configurar integrações de ferramentas que suportam tarefas de desenvolvimento, implementação e operações ao criar uma cadeia de ferramentas aberta ou é possível incluir e configurar integrações de ferramentas para customizar uma cadeia de ferramentas existente.  
{:shortdesc}

**Importante**: no {{site.data.keyword.Bluemix_notm}} Public, cadeias de ferramentas estão disponíveis somente na região sul dos EUA.

As integrações de ferramentas que estão disponíveis para incluir e configurar para a sua cadeia de ferramentas são diferentes, dependendo de você estar usando cadeias de ferramentas no {{site.data.keyword.Bluemix_notm}} Public ou no {{site.data.keyword.Bluemix_notm}} Dedicated. Se estiver usando cadeias de ferramentas no {{site.data.keyword.Bluemix_notm}} Dedicated, as integrações de ferramenta disponíveis para você dependerão de como o {{site.data.keyword.contdelivery_full}} foi configurado em seu ambiente específico.

|Integração de ferramentas |Disponível no {{site.data.keyword.Bluemix_notm}} Public	|Disponível no {{site.data.keyword.Bluemix_notm}} Dedicated (ambiente dependente)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.alertnotificationshort}}		|Sim		|no		|
|Artifactory		|Sim		|no		|
|Availability Monitoring		|Sim		|no		|
|Cloud Event Management		|Sim		|no		|
|{{site.data.keyword.deliverypipeline}} 		|Sim	   	|Sim  		|
|{{site.data.keyword.DRA_short}} 		|Sim		|no			|
|Eclipse Orion {{site.data.keyword.webide}}		|Sim		|Sim			|
|Git Repos and Issue Tracking	|Sim		|no		|
|GitHub and Issues		|Sim		|Sim		|
|Dedicated {{site.data.keyword.ghe_short}} and Issues			|no		|Sim		|
|Jenkins		|Sim		|no		|
|JIRA		|Sim		|no		|
|Nexus			|Sim		|no		|
|Outra Ferramenta			|Sim		|Sim		|
|PagerDuty			|Sim		|Sim		|
|Sauce Labs		|Sim		|no		|
|Slack			|Sim		|Sim		|
{: caption="Table 1. Tool integrations available for toolchains on {{site.data.keyword.Bluemix_notm}} Public and Dedicated" caption-side="top"}

**Dica**: se você deseja começar a desenvolver com seu código-fonte no {{site.data.keyword.Bluemix_notm}} Public, configure a integração de ferramenta GitHub ou a integração de ferramenta Git Repos and Issue Tracking antes de configurar o {{site.data.keyword.deliverypipeline}}. Se você deseja começar a desenvolver com o seu código no {{site.data.keyword.Bluemix_notm}} Dedicated, configure a integração de ferramenta {{site.data.keyword.ghe_short}} ou a integração de ferramenta GitHub antes de configurar o {{site.data.keyword.deliverypipeline}}.


## Configurando o Alert Notification (Experimental)
{: #alertnotification}

O {{site.data.keyword.alertnotificationfull}} é uma solução híbrida baseada em nuvem que pode ser usada para centralizar e simplificar sua estratégia de notificação. Ele funciona com outros aplicativos baseados em nuvem e no local. Os alertas são encaminhados para o {{site.data.keyword.alertnotificationshort}} usando uma API RESTful segura.

Configure o {{site.data.keyword.alertnotificationshort}} para receber notificações sobre problemas durante o processo do DevOps.

### Pré-requisitos

1. Se você não tiver uma conta do {{site.data.keyword.alertnotificationshort}}, inscreva-se para uma:

 a. Abra a página [IBM {{site.data.keyword.alertnotificationshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/us-en/marketplace/alert-notification){: new_window} no IBM Marketplace.

 b. Compre uma assinatura ou inscreva-se para a avaliação grátis de 90 dias.

1. Após a configuração de sua conta do {{site.data.keyword.alertnotificationshort}}, abra o [Painel Minha IBM ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://myibm.ibm.com/dashboard/){: new_window}.
1. Próximo ao IBM {{site.data.keyword.alertnotificationshort}}, clique em **Ativar**.
1. Clique em **Gerenciar chaves API** e clique em **Criar chave API**.
1. No campo **Criar chave API**, digite uma descrição.
1. Clique em **Gerar**. As novas informações da chave API, incluindo o nome e a senha, são exibidas. Essas informações serão necessárias para a configuração da integração de ferramenta, portanto, mantenha a janela Nova chave API aberta. Para propósitos de segurança, não será possível recuperar a senha da chave API mais tarde.

### Configurando o Alert Notification

1. Se você estiver configurando essa integração de ferramenta durante a criação da cadeia de ferramentas, na seção Integrações configuráveis, clique em **{{site.data.keyword.alertnotificationshort}}**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em **Visão geral**.  

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **{{site.data.keyword.alertnotificationshort}}**.

1. Digite a URL para a API do {{site.data.keyword.alertnotificationshort}} que desejar usar. É possível localizar a URL na página Gerenciar chaves API do serviço {{site.data.keyword.alertnotificationshort}}; por exemplo, `https://ibmnotifybm.mybluemix.net/api/alerts/v1`.
1. Digite o nome da chave API do {{site.data.keyword.alertnotificationshort}}. É possível localizar o nome da chave API na janela Nova chave API.
1. Digite a senha gerada pelo {{site.data.keyword.alertnotificationshort}} para a chave API. É possível localizar a senha da chave API na janela Nova chave API.
1. Clique em **Criar integração**.
1. Na cadeia de ferramentas, clique em **{{site.data.keyword.alertnotificationshort}}**.

Para obter mais informações, veja [IBM {{site.data.keyword.alertnotificationshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/manage/tool_alert_notification/){: new_window}.


## Configurando o Artifactory
{: #artifactory}

Configure o gerenciador de repositório do Artifactory para armazenar artefatos de construção no repositório (repo) Artifactory:

1. Se você estiver configurando essa integração de ferramenta durante a criação da cadeia de ferramentas, na seção Integrações configuráveis, clique em **Artifactory**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em **Visão geral**.  

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **Artifactory**.

1. Digite a URL do repositório Artifactory que você deseja abrir ao clicar no cartão do Artifactory.
1. Selecione o tipo de repositório ao qual deseja se conectar.
1. Se estiver usando um registro npm do Artifactory, siga estas etapas:

 a. Digite o endereço de e-mail que está associado a seu registro.

 b. Digite o token de autenticação que está associado a seu registro.

 c. Digite a URL do repositório de liberação do Artifactory, que é seu registro privado no servidor Artifactory.

 d. Digite a URL do registro Espelho ou Público que você usa para combinar múltiplos registros npm públicos e privados. Por exemplo, essa URL pode ser a URL do registro virtual no servidor Artifactory que pode acessar seu registro privado e um cache do registro global npm.

1. Se estiver usando um repositório Maven do Artifactory, siga estas etapas:

 a. Digite o ID do usuário que está associado a seu repositório.

 b. Digite a senha que está associada a seu repositório.

 c. Digite a URL do repositório de liberação do Artifactory, que é seu repositório de liberação privado no servidor Artifactory.

 d. Digite a URL do repositório de captura instantânea do Artifactory, que é seu repositório de captura instantânea privado no servidor Artifactory.

 e. Digite a URL do repositório Espelho ou Público que você usa para combinar múltiplos repositórios Maven públicos e privados. Por exemplo, essa URL pode ser a URL do repositório virtual no servidor Artifactory que pode acessar seu repositório privado e um cache do repositório central Maven.

1. Clique em **Criar integração**.
1. Clique no cartão do repositório do Artifactory com o qual deseja trabalhar. O website do Artifactory é aberto, no qual é possível visualizar os conteúdos do repositório.
1. Opcional: se você estiver usando uma cadeia de ferramentas no {{site.data.keyword.Bluemix_notm}} Public e desejar construir seu app usando o Artifactory com npm, configure seu pipeline para incluir uma tarefa de construção npm. Para obter instruções para configurar a tarefa de construção, veja a seção [Configurando uma tarefa de construção npm do Artifactory em seu pipeline](#config_artifactory_npm).
1. Opcional: se você estiver usando uma cadeia de ferramentas no {{site.data.keyword.Bluemix_notm}} Public e desejar construir seu app usando o Artifactory com Maven, configure seu pipeline para incluir uma tarefa de construção Maven. Para obter instruções para configurar a tarefa de construção, veja a seção [Configurando uma tarefa de construção Maven do Artifactory em seu pipeline](#config_artifactory_maven).

### Configurando uma tarefa de construção npm do Artifactory em seu pipeline
{: #config_artifactory_npm}

Antes de configurar uma tarefa de construção npm em seu pipeline, deve-se ter um pipeline funcional que possa usar seu repositório SCM de construção como entrada e deve-se configurar o Artifactory para sua cadeia de ferramentas. Para obter instruções para configurar o Artifactory, veja a seção [Artifactory](#artifactory).

Configure o {{site.data.keyword.deliverypipeline}} para incluir uma tarefa de construção npm:

1. Crie um estágio e configure a entrada para o repositório SCM apropriado.
1. No estágio, inclua uma tarefa de construção.
1. Configure a tarefa de construção:
  ![tarefa de construção npm](images/artifactory_npm_job.png)

  a. Para o tipo de construtor, selecione **Construção NPM**.

  b. Se você tiver configurado múltiplas instâncias da integração de ferramenta Artifactory, insira o nome da integração de ferramenta Artifactory para a qual você deseja configurar a tarefa de construção npm.

  c. Para o tipo de integração de ferramenta, selecione **Artifactory**.

  d. Para o comando de construção, insira os comandos para construir seu módulo npm ou para publicá-lo em seu registro. Este exemplo mostra os comandos para construir o módulo ou publicá-lo.
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Dica**: é possível localizar a URL e as credenciais do usuário usadas para se conectar ao registro nas definições de configuração da integração de ferramenta Artifactory.

  e. Se a sua tarefa de construção publicar no registro do Artifactory e o formato de sua versão do módulo de nó for `x.y.z-SNAPSHOT.w`, marque a caixa de seleção **Incrementar versão do módulo de captura instantânea**. A tarefa de construção atualiza automaticamente a versão do módulo antes de a tarefa publicar no registro do Artifactory. A tarefa seleciona a versão mais alta do módulo do registro npm e o arquivo local `package.json` e incrementa a versão do módulo usando semver. A tarefa de construção não entrega as mudanças para o repositório SCM.

1. Clique em **SALVAR**. Sempre que o pipeline for executado, essa tarefa de construção usará as informações de configuração da integração de ferramenta Artifactory para se conectar ao registro npm.

### Configurando uma tarefa de construção Maven do Artifactory em seu pipeline
{: #config_artifactory_maven}

Antes de configurar uma tarefa de construção Maven em seu pipeline, será necessário um pipeline funcional que possa usar seu repositório SCM de construção como entrada e o Artifactory deverá ser configurado para sua cadeia de ferramentas. Para obter instruções para configurar o Artifactory, veja a seção [Artifactory](#artifactory).

Configure o {{site.data.keyword.deliverypipeline}} para incluir uma tarefa de construção Maven:

1. Crie um estágio e configure a entrada para o repositório SCM apropriado.
1. No estágio, inclua uma tarefa de construção.
1. Configure a tarefa de construção:
  ![Tarefa de construção Maven](images/artifactory_maven_job.png)

  a. Para o tipo de construtor, selecione **Construção Maven**.

  b. Se você tiver configurado múltiplas instâncias da integração de ferramenta Artifactory, insira o nome da integração de ferramenta Artifactory para a qual você deseja configurar a tarefa de construção Maven.

  c. Para o tipo de integração de ferramenta, selecione **Artifactory**.

  d. Para o comando de construção, insira os comandos para construir seu módulo Maven ou para publicá-lo em seu registro de captura instantânea. Este exemplo mostra os comandos para construir o módulo ou publicá-lo em um registro de captura instantânea.
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Dica**: é possível localizar a URL e as credenciais do usuário usadas para se conectar ao registro nas definições de configuração da integração de ferramenta Artifactory.

1. Clique em **SALVAR**. Sempre que o pipeline for executado, essa tarefa de construção usará as informações de configuração da integração de ferramenta Artifactory para se conectar ao repositório Maven.

Para saber mais, veja [Artifactory ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/code/tool_artifactory/){: new_window}.


## Incluindo monitoramento de disponibilidade
{: #availabilitymonitoring}

O {{site.data.keyword.prf_hublong}} isola problemas, identifica padrões e melhora o desempenho antes que os usuários sejam afetados. É possível testar seu app de locais ao redor do mundo, integrar com pipelines de entrega e obter insights sobre como otimizar continuamente seu código.

**Nota**: essa integração de ferramenta é pré-configurada e não requer parâmetros de configuração. Não é possível reconfigurar essa integração de ferramenta.

Para testar, monitorar e melhorar o funcionamento do app ao construí-lo, inclua a ferramenta de integração {{site.data.keyword.prf_hubshort}}:

1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página Cadeias de ferramentas, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **{{site.data.keyword.prf_hubshort}}**.

1. Clique em **Criar integração**.
1. Clique em **{{site.data.keyword.prf_hubshort}}** para abrir o painel do {{site.data.keyword.prf_hubshort}}, selecionar um app e configurar o monitoramento para o app.

Para saber mais, veja [{{site.data.keyword.prf_hublong}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/manage/tool_bluemix_availability_monitoring/){: new_window}.


## Incluindo o Cloud Event Management (Experimental)
{: #cloudeventmanagement}

O {{site.data.keyword.evtmgt_full}} fornece uma visualização consolidada de problemas que ocorrem com seus serviços, aplicativos e infraestrutura. É possível configurar o gerenciamento de incidente em tempo real para resolver os problemas de maneira mais eficiente.

**Nota**: essa integração de ferramenta é pré-configurada e não requer parâmetros de configuração. Não é possível reconfigurá-la.

Para ajudar sua equipe do DevOps a alcançar saúde operacional confiável, qualidade de serviço e objetivos de melhoria contínua, inclua o Cloud Event Management em sua cadeia de ferramentas:

1. No painel do DevOps, na página Cadeias de ferramentas, clique na cadeia de ferramentas na qual você deseja incluir o Cloud Event Management. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **Cloud Event Management**.

1. Clique em **Criar integração**.
1. Na cadeia de ferramentas, clique em qualquer um dos cartões de ferramenta a seguir:

 * **Cloud Event Management** para começar a usar o Cloud Event Management.

 * **{{site.data.keyword.alertnotificationshort}}** para criar políticas que determinem quando os usuários receberão notificações de incidente.

 * **Runbook Automation** para gerenciar seu catálogo de runbooks no Cloud Event Management.


## Configurando o Delivery Pipeline
{: #deliverypipeline}

O {{site.data.keyword.deliverypipeline}} automatiza a implementação contínua de seus projetos por meio de sequências de estágios que recuperam tarefas de entrada e de execução, como construções, testes e implementações.

Configure o {{site.data.keyword.deliverypipeline}} para automatizar a construção, o teste e a implementação contínua de seus apps:

1. Se você estiver configurando essa integração de ferramenta durante a criação da cadeia de ferramentas, na seção Integrações configuráveis, clique em **{{site.data.keyword.deliverypipeline}}**. Dependendo do modelo que usar, campos diferentes poderão estar disponíveis. Revise os valores de campo padrão e, se necessário, mude essas configurações.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **{{site.data.keyword.deliverypipeline}}**.

1. Especifique um nome para seu novo pipeline.
1. Se você planejar usar seu pipeline para implementar uma interface com o usuário, marque a caixa de seleção **Mostrar apps no menu VISUALIZAR APP**. Todos os apps que seu pipeline criar serão mostrados na lista **Visualizar app** na página Visão geral da cadeia de ferramentas.
1. Clique em **Criar integração** para incluir o {{site.data.keyword.deliverypipeline}} em sua cadeia de ferramentas.
1. Clique em **{{site.data.keyword.deliverypipeline}}** para visualizar o pipeline e configurá-lo. Para aprender os fundamentos da configuração de um pipeline, consulte [Construindo e implementando pipelines](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}.

  **Dica**: se desejar acionar o pipeline ao enviar por push mudanças para o GitHub, {{site.data.keyword.ghe_short}} ou repositório (repo) Git, deve-se configurar o GitHub, o {{site.data.keyword.ghe_short}} ou o Git Repos and Issue Tracking para sua cadeia de ferramentas antes de definir os estágios para o pipeline. Os estágios de pipeline precisam das URLs do Git para os seus repositórios. Cada estágio de pipeline pode se referir a somente um dos repositórios GitHub, {{site.data.keyword.ghe_short}} ou Git que estão associados à sua cadeia de ferramentas. Para obter instruções para configurar o GitHub, consulte a seção [GitHub](#github). Para obter instruções para configurar o Dedicated {{site.data.keyword.ghe_short}}, veja [Introdução ao {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}. Para obter instruções para configurar o Git Repos and Issue Tracking, veja a seção [Git Repos and Issue Tracking](##gitbluemix).    

  **Nota:** se você não tiver privilégios de administrador para o repositório GitHub ou GitHub Enterprise ou privilégios de Mestre ou Proprietário para o repositório Git Repos and Issue Tracking ao qual está se vinculando, sua integração será limitada porque não será possível usar um webhook. Os webhooks são necessários para acionar automaticamente um pipeline quando uma confirmação é enviada por push para o repositório. Sem um webhook, os pipelines deverão ser iniciados manualmente.

1. Opcional: se você estiver usando uma cadeia de ferramentas no {{site.data.keyword.Bluemix_notm}} Public e desejar que os Sauce Labs executem testes em seu aplicativo, configure o {{site.data.keyword.deliverypipeline}} para incluir uma tarefa de teste dos Sauce Labs. Para obter instruções para configurar a tarefa de teste, consulte a seção [Configurando uma tarefa de teste Sauce Labs em seu pipeline](#config_saucelabs).

### Configurando uma tarefa de teste Sauce Labs em seu pipeline
{: #config_saucelabs}

Antes de configurar uma tarefa de teste Sauce Labs em seu pipeline, será necessário um pipeline em funcionamento que possua estágios para construir e implementar seu app e deve-se configurar o Sauce Labs para sua cadeia de ferramentas. Para obter instruções para configurar o Sauce Labs, consulte a seção [Sauce Labs](#saucelabs).

Configure o {{site.data.keyword.deliverypipeline}} para incluir uma tarefa de teste Sauce Labs:

1. Se você não tiver um estágio que implemente uma versão de teste de seu app, crie um.
1. No estágio, inclua uma tarefa de teste após a tarefa de implementação. Ao colocar essas tarefas no mesmo estágio, elas poderão acessar o mesmo conjunto de propriedades do ambiente.   
  ![Tarefa de Teste](images/toolchain_test_job.png)

1. Configure o estágio:

  a. Na guia **PROPRIEDADES DO AMBIENTE**, crie três propriedades: CF_APP_NAME, SAUCE_USERNAME e SAUCE_ACCESS_KEY.

  b. Insira seu nome de usuário e chave de acesso do Sauce Labs. Ao fazer isso, você externaliza esses valores para que possa usá-los em seus testes.

1. Configure a tarefa de implementação. No campo **Implementar script**, inclua esse comando: `export CF_APP_NAME="$CF_APP"`. Esse comando exporta o nome do app como uma propriedade do ambiente.
1. Configure a tarefa de teste. Os valores na imagem a seguir são exemplos. Os campos **Instância de serviço**, **Destino**, **Organização** e **Espaço** são preenchidos com o nome do usuário, a região, a organização e o espaço dos Sauce Labs que você estiver usando.  
![Configurar tarefa](images/toolchain_configure_job.png)

  a. Para o tipo de testador, selecione **Sauce Labs**.

  b. Para a instância de serviço, selecione o nome de usuário Sauce Labs que usou quando configurou o Sauce Labs para sua cadeia de ferramentas.

   **Dica**: para ver o nome de usuário e chave de acesso que usou quando configurou o Sauce Labs para sua cadeia de ferramentas, clique em **Configurar**.

  c. No campo **Comando de execução de teste**, insira os comandos que instalam as dependências necessárias por seus testes e, em seguida, execute os testes. Por exemplo, para um aplicativo Node.js, você pode inserir esses comandos:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```

    d. Se desejar ver seus relatórios de teste nos logs de tarefa de teste, selecione a caixa de seleção **Ativar relatório de teste** e configure o Padrão de arquivo de resultado de teste como `test/*.xml`.

1. Clique em **SALVAR**. Sempre que a sua pipeline for executada, os seus testes dos Sauce Labs serão executados.

Para saber mais, veja [Delivery Pipeline ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/deliver/tool_delivery_pipeline/){: new_window}.


## Incluindo o DevOps Insights (Beta)
{: #dra}

{{site.data.keyword.DRA_full}} coleta e analisa os resultados dos testes de unidade, testes funcionais e ferramentas de cobertura de código para determinar se seu código atende a critérios predefinidos em gates especificados em seu processo de implementação. Se seu código não atender ou exceder os critérios, a implementação será interrompida para evitar riscos de serem liberados. É possível usar o {{site.data.keyword.DRA_short}} como uma rede de segurança para o seu ambiente de entrega contínua ou como uma forma de implementar e melhorar os padrões de qualidade.

 **Nota**: essa integração de ferramenta está disponível somente no {{site.data.keyword.Bluemix_notm}} Public. Ela é pré-configurada e não requer parâmetros de configuração. Não é possível reconfigurar essa integração de ferramenta.

Inclua o {{site.data.keyword.DRA_short}} para manter e melhorar a qualidade de seu código no {{site.data.keyword.Bluemix_notm}} monitorando as suas implementações para identificar riscos antes de serem liberadas.

1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **{{site.data.keyword.DRA_short}}**.

1. Clique em **Criar integração**.
1. Clique no **{{site.data.keyword.DRA_short}}** e, em seguida, conclua as etapas de introdução: criar critérios, conectar os critérios ao pipeline e executar o pipeline.

Para saber mais, veja [{{site.data.keyword.DRA_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window}.


## Incluindo o Eclipse Orion Web IDE
{: #webide}

O Eclipse Orion {{site.data.keyword.webide}} é um ambiente baseado na web integrado em que é possível criar, editar, executar, depurar e concluir tarefas de controle de fonte. É possível mover perfeitamente da edição para execução, do envio para implementação.

 **Nota**: esta integração de ferramenta é pré-configurada. Ela não requer nenhum parâmetro de configuração e não é possível reconfigurá-la.

Para concluir tarefas de controle de fonte, inclua a integração de ferramenta Eclipse Orion {{site.data.keyword.webide}}:

1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **Eclipse Orion Web IDE**.

1. Clique em **Criar integração**.
1. Clique em **Eclipse Orion {{site.data.keyword.webide}}**. A sua área de trabalho é previamente preenchida com seus repositórios GitHub ou do {{site.data.keyword.ghe_short}}. Os repos associados a sua cadeia de ferramentas atual são destacados.

Para saber mais, veja [Editando código com o Eclipse Orion {{site.data.keyword.webide}}](/docs/services/ContinuousDelivery/web_ide.html){: new_window} e [Eclipse Orion {{site.data.keyword.webide}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/code/tool_eclipse_orion_web_ide/){: new_window}.


## Configurando o Git Repos and Issue Tracking (Experimental)
{: #gitbluemix}

A integração de ferramenta Git Repos and Issue Tracking baseia-se no GitLab Community Edition, que é um serviço de hospedagem baseado na web para repositório Git. É possível ter ambas as cópias local e remota de seus repositórios. Para saber mais, veja [Git Repos and Issue Tracking (Experimental) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git.ng.bluemix.net/help){:new_window}.

Se estiver configurando o Git Repos and Issue Tracking durante a criação da cadeia de ferramentas, siga estas etapas:    

1. Na seção Integrações configuráveis, clique em **Git Repos and Issue Tracking**.
1. Revise os locais de destino padrão do repositório Git. Esses repos são clonados a partir dos mesmos repos de amostra. Se necessário, mude os nomes dos repos de destino.

Se você tiver uma cadeia de ferramentas e estiver incluindo o Git Repos and Issue Tracking nela, siga estas etapas:    

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.
1. Clique em **Incluir uma ferramenta**.
1. Na seção Integrações de ferramentas, clique em **Git Repos and Issue Tracking**.
1. Selecione um tipo de repositório:     

  a. Para criar um repositório vazio, para o tipo de repositório, clique em **Novo** e digite um nome de repositório.    
  b. Para bifurcar um repositório Git para que você possa contribuir com mudanças por meio de solicitações de mesclagem, para o tipo de repositório, clique em **Bifurcar**. Digite a URL para o repositório de origem.    
  c. Para criar uma cópia de um repositório Git, para o tipo de repositório, clique em **Clonar**. Digite um novo nome de repositório e a URL para o repositório de origem.     
  d. Se você tiver um repositório Git e desejar usá-lo, para o tipo de repositório, clique em **Existente**. Digite a URL.    

1. Se desejar usar o Issues para rastreamento de problemas, marque a caixa de seleção **Ativar Issues**.
1. Se desejar rastrear as mudanças de implementação de código criando tags e comentários sobre confirmações, além de rótulos e comentários sobre problemas referenciados pelas confirmações, marque a caixa de seleção **Rastrear mudanças de implementação de código**. Para obter mais informações, veja [Rastrear onde seu código é implementado com cadeias de ferramentas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Clique em **Criar integração**.
1. Clique no cartão do repositório Git com o qual deseja trabalhar. Sua página de visão geral do projeto é aberta.    

**Nota:** se você não tiver privilégios de Mestre ou Proprietário para o repositório ao qual está se vinculando, sua integração será limitada porque não será possível usar um webhook. Os webhooks são necessários para acionar automaticamente um pipeline quando uma confirmação é enviada por push para o repositório. Sem um webhook, os pipelines deverão ser iniciados manualmente.


## Configurando o GitHub e Issues
{: #github}

O GitHub é um serviço de hospedagem baseado na web para repos Git. É possível ter ambas as cópias local e remota de seus repos, o que facilita a colaboração.

O GitHub Issues é uma ferramenta de controle que mantém seu trabalho e seus planos todos em um lugar. Ele é integrado a seu repo de desenvolvimento para que possa focar em tarefas importantes.

Configure o GitHub para gerenciar o seu código-fonte na nuvem:

1. Se estiver configurando esta integração de ferramenta conforme estiver criando a cadeia de ferramentas, siga estas etapas:

 a. Na seção Integrações configuráveis, clique em **GitHub**. Se você estiver criando a cadeia de ferramentas no {{site.data.keyword.Bluemix_notm}} Public e não for autorizado {{site.data.keyword.Bluemix_notm}} a acessar o GitHub, clique em **Autorizar** para acessar o website GitHub. Se você não
tiver uma sessão GitHub ativa, será solicitado que efetue login. Clique em **Autorizar aplicativo** para permitir que o {{site.data.keyword.Bluemix_notm}} acesse sua conta GitHub. Se
você tiver uma sessão GitHub ativa, mas não tiver inserido sua senha recentemente, poderá ser solicitado que insira sua senha GitHub para
confirmar.

 b. Revise os locais de repo de destino padrão para os repos GitHub. Esses repos são clonados a partir dos mesmos repos de amostra. Se necessário, mude os nomes dos repos de destino.
 ![Locais de repo de destino padrão](images/toolchain_github_config.png)

1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **GitHub**.

1. Se você tiver um repositório GitHub e desejar usá-lo, para o tipo de repositório, clique em **Existente** e digite a URL.
1. Se desejar usar um novo repo GitHub, digite um nome para o repo GitHub, digite a URL para o repo que estiver clonando ou bifurcando e selecione o tipo de repositório:

 a. Para criar um repositório vazio, clique em **Novo**.

 b. Para criar uma cópia de um repositório GitHub, clique em **Clone**.

 c. Para bifurcar um repositório GitHub para que você possa contribuir com mudanças por meio de solicitações pull, clique em **Bifurcar**.

1. Se desejar usar o GitHub Issues para o controle de emissões, selecione a caixa de seleção **Ativar GitHub Issues**.
1. Se desejar rastrear as mudanças de implementação de código criando tags e comentários sobre confirmações, além de rótulos e comentários sobre problemas referenciados pelas confirmações, marque a caixa de seleção **Rastrear mudanças de implementação de código**. Para obter mais informações, veja [Rastrear onde seu código é implementado com cadeias de ferramentas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Clique em **Criar integração**.
1. Clique no cartão do repositório GitHub com o qual deseja trabalhar. O website do GitHub é aberto, no qual é possível visualizar os conteúdos do repositório.

  **Dica**: é possível usar as ferramentas de gerenciamento de código-fonte integradas no Eclipse Orion {{site.data.keyword.webide}} para editar o repositório GitHub e implementar um aplicativo a partir de sua área de trabalho.

1. Se você tiver ativado o GitHub Issues, clique em **GitHub Issues** para abri-lo. É possível usar essa instância do GitHub Issues para sua cadeia de ferramentas inteira, mesmo se a cadeia de ferramentas contiver múltiplos repositórios GitHub.    

**Nota:** se você não tiver privilégios de administrador para o repositório ao qual está se vinculando, sua integração será limitada porque não será possível usar um webhook. Os webhooks são necessários para acionar automaticamente um pipeline quando uma confirmação é enviada por push para o repositório. Sem um webhook, os pipelines deverão ser iniciados manualmente.

Para obter mais informações, veja [GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} e [GitHub Issues ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configurando o GitHub Enterprise and Issues no Bluemix Dedicated
{: #configghe}

 **Nota:** estas instruções se aplicam ao {{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}}. Se você estiver usando sua própria versão gerenciada do {{site.data.keyword.ghe_short}}, algumas etapas poderão ser diferentes, dependendo de seus procedimentos internos.

O {{site.data.keyword.ghe_long}} é um serviço de hospedagem no local, baseado na web para repositórios Git. O Dedicated {{site.data.keyword.ghe_short}} é para clientes {{site.data.keyword.Bluemix_notm}} Dedicated somente. O GitHub Issues é uma ferramenta de rastreamento que mantém o seu trabalho e os seus planos em um local. Ele é integrado a seu repo de desenvolvimento para que possa focar em tarefas importantes. Para obter mais informações sobre o Dedicated {{site.data.keyword.ghe_short}} e o GitHub Issues, veja [Introdução ao {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window} e [GitHub Issues ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

É possível configurar o {{site.data.keyword.ghe_short}} como uma integração de ferramenta em sua cadeia de ferramentas para que você possa gerenciar o código-fonte na instância do [{{site.data.keyword.Bluemix_notm}} Dedicated](/docs/dedicated/index.html#dedicated){: new_window} de sua empresa.

1. Se estiver configurando esta integração de ferramenta conforme estiver criando a cadeia de ferramentas, siga estas etapas:

 a. Antes de efetuar login no Dedicated {{site.data.keyword.ghe_short}} pela primeira vez, peça ao administrador de região de sua empresa para incluir seu ID de usuário na instância do {{site.data.keyword.Bluemix_notm}} Dedicated por meio do registro de usuário de sua empresa usando LDAP. Para obter informações sobre como configurar sua conta do {{site.data.keyword.ghe_short}}, consulte [Introdução ao {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}.

 b. Na seção Integrações configuráveis, clique em **{{site.data.keyword.ghe_short}}**.    

 c. Revise o nome padrão para o novo repositório do {{site.data.keyword.ghe_short}}. Se necessário, mude o nome do novo repositório. A imagem a seguir mostra um exemplo de um repositório que é clonado a partir de um repositório de amostra. É possível usar um repositório existente ou um novo repositório. Para usar um repositório novo, é possível criar um repositório vazio, clonar um repositório ou bifurcar um repositório.
 ![Locais de repositório padrão](images/toolchain_ghe_config.png)

1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **{{site.data.keyword.ghe_short}}**.

1. Se você tiver um repositório do {{site.data.keyword.ghe_short}} que deseja usar, digite a URL para o repositório. Para o tipo de repositório, clique em
**Existente**.
1. Se você deseja usar um novo repositório do {{site.data.keyword.ghe_short}}, digite um nome para o repositório, digite a URL para o repositório que você está clonando ou bifurcando e
selecione o tipo de repositório:

 a. Para criar um repositório vazio, clique em **Novo**.

 b. Para criar uma cópia de um repositório, clique em **Clonar**.

 c. Para bifurcar um repositório de maneira que você possa contribuir com mudanças por meio de solicitações pull, clique em **Bifurcar**.

1. Para usar o GitHub Issues para rastreamento de emissão, marque a caixa de seleção **Ativar o GitHub Issues**.
1. Clique em **Criar integração**.
1. Clique no cartão do repositório {{site.data.keyword.ghe_short}} com o qual deseja trabalhar. O repositório {{site.data.keyword.ghe_short}} de sua empresa é aberto.

  **Dica**: é possível usar as ferramentas de gerenciamento de código-fonte integradas no Eclipse Orion {{site.data.keyword.webide}} para editar o repositório do
{{site.data.keyword.ghe_short}} e
implementar um aplicativo a partir de sua área de trabalho.

1. Se você tiver ativado o GitHub Issues, clique em **GitHub Issues**. É possível usar essa instância do GitHub Issues para sua cadeia de ferramentas inteira, mesmo se a cadeia de ferramentas contiver múltiplos repositórios GitHub.    

**Nota:** se você não tiver privilégios de administrador para o repositório ao qual está se vinculando, sua integração será limitada porque não será possível usar um webhook. Os webhooks são necessários para acionar automaticamente um pipeline quando uma confirmação é enviada por push para o repositório. Sem um webhook, os pipelines deverão ser iniciados manualmente.


## Configurando o Jenkins
{: #jenkins}

Jenkins é uma ferramenta de software livre baseada no servidor que constrói e testa software continuamente, apoiando as práticas de integração contínua e entrega contínua.

**Importante**: antes de criar uma integração de ferramenta Jenkins, deve-se ter um servidor Jenkins.

Com a integração de ferramenta Jenkins, é possível enviar notificações de tarefas do Jenkins para outras ferramentas em sua cadeia de ferramentas, como Slack e PagerDuty. Para rastrear o código em implementações, é possível incluir mensagens de implementação nas confirmações do Git e seus problemas Git ou JIRA relacionados. É possível também visualizar suas implementações na página Conexões da cadeia de ferramentas. É possível alimentar resultados de teste para o {{site.data.keyword.DRA_short}}, incluir portas de qualidade automatizadas e rastrear seu risco de implementação.

Configure o Jenkins para automatizar a construção, o teste e a implementação contínuos de seus apps:

1. Se você estiver configurando essa integração de ferramenta durante a criação da cadeia de ferramentas, na seção Integrações configuráveis, clique em **Jenkins**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em **Visão geral**.  

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **Jenkins**.

1. Digite o nome que você deseja exibir para essa integração de ferramenta no cartão Jenkins em sua cadeia de ferramentas.
1. Digite a URL do servidor Jenkins que você deseja abrir ao clicar no cartão do Jenkins de sua cadeia de ferramentas.
1. Copie o webhook da cadeia de ferramentas gerada.
1. No servidor Jenkins, conclua estas etapas:

 a. Instale o [Cloud Foundry CLI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}.

 b. Instale o plug-in Cloud Foundry do IBM Cloud DevOps inserindo um destes comandos:

  * Mac OS: `cf install-plugin https://icd.ng.bluemix.net/icd_darwin_amd64`

  * Linux ou Docker: `cf install-plugin https://icd.ng.bluemix.net/icd_linux_amd64`

 c. Instale e configure o plug-in Jenkins do IBM Cloud DevOps para o DevOps Insights e Notifications. Para obter mais informações, veja [Instalando e configurando o plug-in](/docs/services/DevOpsInsights/insights_risk.html#integrate_jenkins){: new_window}.

 d. Em cada tarefa para a qual você deseja enviar notificações para sua cadeia de ferramentas, conclua estas etapas:

  * Marque a caixa de seleção **Este projeto é parametrizado**.

  * Inclua o parâmetro de sequência `ICD_WEBHOOK_URL`.

  * Cole o webhook da cadeia de ferramentas gerada.
 ![URL do webhook](images/jenkins_webhook_url.png)

  * Inclua uma ação de pós-construção para o IBM Cloud DevOps - Webhook Notification e marque a caixa de seleção **Tarefa concluída**.
 ![Ação de pós-construção](images/jenkins_postbuild_action.png)  

 e. Nas tarefas de implementação, conclua estas etapas:

  * Inclua os parâmetros de sequência `ICD_WEBHOOK_URL`, `CF_API`, `CF_ORG`, `CF_SPACE` e `CF_APP`. Estes exemplos mostram como incluir cada um dos parâmetros de sequência.
![Parâmetro de sequência de URL do Webhook](images/jenkins_set_webhook_url.png)
 ![Parâmetro de sequência CFI API](images/jenkins_set_cfapi.png)
 ![Parâmetro de sequência CFI ORG](images/jenkins_set_cforg.png)
 ![Parâmetro de sequência CFI SPACE](images/jenkins_set_cfspace.png)
 ![Parâmetro de sequência CFI APP](images/jenkins_set_cfapp.png)

  * Configure suas ligações do Cloud Foundry CLI usando a variável de nome do usuário `CF_CREDS_USR` e a variável de senha `CF_CREDS_PSW`.
 ![Ligações do Cloud Foundry CLI](images/jenkins_config_bindings.png)  

  * No campo **Construção**, insira esses comandos para efetuar login e use o plug-in Cloud Foundry do IBM Cloud DevOps para enviar os mapeamentos implementáveis do aplicativo, com rastreabilidade de confirmação de Git, para sua cadeia de ferramentas:
 ![Comandos de construção](images/jenkins_build_commands.png)    

  * No campo **Construção**, insira o comando `cf icd --create-connection $ICD_WEBHOOK_URL $CF_APP` para enviar os mapeamentos implementáveis do aplicativo para a cadeia de ferramentas.    

 f. Salve suas mudanças e retorne para a página Configurar a integração para a integração de ferramenta Jenkins.

1. Clique em **Criar integração**.
1. Na cadeia de ferramentas, clique em **Jenkins** para visualizar o servidor Jenkins.  

Para obter mais informações, veja [Jenkins ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/deliver/tool_jenkins/){: new_window}.


## Configurando o JIRA
{: #jira}

JIRA é uma ferramenta que rastreia problemas e erros relacionados ao software. A integração de ferramenta JIRA atualiza os problemas de seu projeto sempre que o Jenkins ou o {{site.data.keyword.deliverypipeline}} executa uma implementação. Para que a integração de ferramenta JIRA rastreie seus problemas, deve-se usar Confirmações inteligentes JIRA em suas mensagens de confirmação. Para saber mais sobre Confirmações inteligentes JIRA, veja [Usando Confirmações inteligentes ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://confluence.atlassian.com/fisheye/using-smart-commits-298976812.html){: new_window}.

Configure o JIRA para planejar, rastrear e entregar código de qualidade:

1. Se você estiver configurando essa integração de ferramenta durante a criação da cadeia de ferramentas, na seção Integrações configuráveis, clique em **JIRA**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em **Visão geral**.  

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **JIRA**.

1. Se você tiver um projeto JIRA e desejar se conectar a ele, para o tipo JIRA, clique em **Existente**:

 a. Digite a chave do projeto JIRA para o projeto JIRA. É possível localizar a chave do projeto na URL do projeto JIRA.

 b. Digite a URL da API base para a instância do JIRA. É possível localizar a URL da API do cabeçalho da instância do JIRA. Clique no ícone **Administração** e clique em **Sistema**.

 c. Opcional: Digite seu nome de usuário JIRA. Seu nome de usuário será necessário apenas se você estiver se conectando a uma instância privada do JIRA ou se estiver se conectando a uma instância pública e desejar receber informações de rastreabilidade.

 d. Opcional: Digite sua senha do JIRA. Sua senha será necessária apenas se você estiver se conectando a uma instância privada do JIRA ou se estiver se conectando a uma instância pública e desejar receber informações de rastreabilidade.

 e. Para rastrear as mudanças de implementação de código do projeto criando rótulos e comentários para problemas referenciados, marque a caixa de seleção **Rastrear mudanças de implementação de código**. Certifique-se de usar a Confirmação inteligente JIRA para referenciar os problemas do JIRA nas confirmações do GitHub. Se você não selecionar essa opção, a integração de ferramenta JIRA ignorará quaisquer confirmações.

1. Se desejar criar um projeto JIRA, para o tipo JIRA, clique em **Novo**:

 a. Digite uma chave de projeto JIRA para usar para o novo projeto. Essa chave é usada como um identificador exclusivo na URL do projeto.

 b. Digite um nome para o projeto JIRA.

 c. Digite a URL da API base para a instância do JIRA. É possível localizar a URL da API do cabeçalho da instância do JIRA. Clique no ícone **Administração** e clique em **Sistema**.

 d. Digite o nome de usuário para o líder do projeto JIRA que você deseja usar para esse projeto. Para especificar alguém como o líder do projeto JIRA, essa pessoa deve ter a permissão de líder de projeto no JIRA.

 e. Digite o nome de usuário do administrador para essa instância do JIRA.

 f. Digite a senha do administrador para essa instância do JIRA.

 g. Para rastrear as mudanças de implementação de código do projeto criando rótulos e comentários para problemas referenciados, marque a caixa de seleção **Rastrear mudanças de implementação de código**. Certifique-se de usar a Confirmação inteligente JIRA para referenciar os problemas do JIRA nas confirmações do GitHub. Se você não selecionar essa opção, a integração de ferramenta JIRA ignorará quaisquer confirmações.

1. Clique em **Criar integração**.
1. Em sua cadeia de ferramentas, clique em **JIRA** para visualizar o painel do projeto JIRA ao qual você se conectou.

Para saber mais, veja [JIRA ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/code/tool_jira/){: new_window}.


## Configurando o Nexus
{: #nexus}

Configure o Gerenciador de Repositório do Nexus para armazenar artefatos de construção no repositório (repo) Nexus:

1. Se você estiver configurando essa integração de ferramenta durante a criação da cadeia de ferramentas, na seção Integrações configuráveis, clique em **Nexus**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em **Visão geral**.  

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **Nexus**.

1. Digite um nome para essa instância da integração de ferramenta Nexus.
1. Digite a URL do repositório Nexus que você deseja abrir ao clicar no cartão do Nexus de sua cadeia de ferramentas.
1. Selecione o tipo de repositório ao qual deseja se conectar.
1. Se tiver selecionado **registro npm**, siga estas etapas:

 a. Digite o endereço de e-mail que está associado a seu registro.

 b. Digite o token de autenticação que está associado a seu registro.

 c. Digite a URL do repositório de liberação do Nexus, que é seu registro privado no servidor Nexus.

 d. Digite a URL do registro Espelho ou Público que você usa para combinar múltiplos registros npm públicos e privados. Por exemplo, essa URL pode ser a URL do registro virtual no servidor Nexus que pode acessar seu registro privado e um cache do registro global npm.

1. Se você tiver selecionado **repositório Maven**, siga estas etapas:

 a. Digite o ID do usuário que está associado a seu repositório.

 b. Digite a senha que está associada a seu repositório.

 c. Digite a URL do repositório de liberação do Nexus, que é seu repositório de liberação privado no servidor Nexus.

 d. Digite a URL do repositório de captura instantânea do Nexus, que é seu repositório de captura instantânea privado no servidor Nexus.

 e. Digite a URL do repositório Espelho ou Público que você usa para combinar múltiplos repositórios Maven públicos e privados. Por exemplo, essa URL pode ser a URL do repositório virtual no servidor Nexus que pode acessar seu repositório privado e um cache do repositório central Maven.

1. Clique em **Criar integração**.
1. Na cadeia de ferramentas, clique no cartão do repositório Nexus com o qual deseja trabalhar. O website do Nexus é aberto, no qual é possível visualizar os conteúdos do repositório.
1. Opcional: se você estiver usando uma cadeia de ferramentas no {{site.data.keyword.Bluemix_notm}} Public e desejar construir seu app usando o Nexus com npm, configure seu pipeline para incluir uma tarefa de construção npm. Para obter instruções para configurar a tarefa de construção, veja a seção [Configurando uma tarefa de construção npm do Nexus em seu pipeline](#config_nexus_npm).
1. Opcional: se você estiver usando uma cadeia de ferramentas no {{site.data.keyword.Bluemix_notm}} Public e desejar construir seu app usando o Nexus com Maven, configure seu pipeline para incluir uma tarefa de construção Maven. Para obter instruções para configurar a tarefa de construção, veja a seção [Configurando uma tarefa de construção Maven do Nexus em seu pipeline](#config_nexus_maven).

### Configurando uma tarefa de construção npm do Nexus em seu pipeline
{: #config_nexus_npm}

Antes de configurar uma tarefa de construção npm em seu pipeline, será necessário um pipeline funcional que possa usar seu repositório SCM de construção como entrada e o Nexus deverá ser configurado para sua cadeia de ferramentas. Para obter instruções para configurar o Nexus, veja a seção [Nexus](#nexus).

Configure o {{site.data.keyword.deliverypipeline}} para incluir uma tarefa de construção npm:

1. Crie um estágio e configure a entrada para o repositório SCM apropriado.
1. No estágio, inclua uma tarefa de construção.
1. Configure a tarefa de construção:
  ![tarefa de construção npm](images/nexus_npm_job.png)

  a. Para o tipo de construtor, selecione **Construção NPM**.

  b. Se você tiver configurado múltiplas instâncias da integração de ferramenta Nexus, insira o nome da integração de ferramenta Nexus para a qual você deseja configurar a tarefa de construção npm.

  c. Para o tipo de integração de ferramenta, selecione **Nexus**.

  d. Para o comando de construção, insira os comandos para construir seu módulo npm ou para publicá-lo em seu registro. Este exemplo mostra os comandos para construir o módulo ou publicá-lo.
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Dica**: é possível localizar a URL e as credenciais do usuário usadas para se conectar ao registro nas definições de configuração da integração de ferramenta Nexus.

  e. Se a sua tarefa de construção publicar no registro do Nexus e o formato de sua versão do módulo de nó for `x.y.z-SNAPSHOT.w`, marque a caixa de seleção **Incrementar versão do módulo de captura instantânea**. A tarefa de construção atualiza automaticamente a versão do módulo antes da publicação no registro do Nexus. A tarefa de construção seleciona a versão mais alta do módulo do registro npm e o arquivo local `package.json` e incrementa a versão do módulo usando semver. A tarefa de construção não entrega as mudanças para o repositório SCM.

1. Clique em **SALVAR**. Sempre que o pipeline for executado, essa tarefa de construção usará as informações de configuração da integração de ferramenta Nexus para se conectar ao registro npm.

### Configurando uma tarefa de construção Maven do Nexus em seu pipeline
{: #config_nexus_maven}

Antes de configurar uma tarefa de construção Maven em seu pipeline, será necessário um pipeline funcional que possa usar seu repositório SCM de construção como entrada e o Nexus deverá ser configurado para sua cadeia de ferramentas. Para obter instruções para configurar o Nexus, veja a seção [Nexus](#nexus).

Configure o {{site.data.keyword.deliverypipeline}} para incluir uma tarefa de construção Maven:

1. Crie um estágio e configure a entrada para o repositório SCM apropriado.
1. No estágio, inclua uma tarefa de construção.
1. Configure a tarefa de construção:
  ![Tarefa de construção Maven](images/nexus_maven_job.png)

  a. Para o tipo de construtor, selecione **Construção Maven**.

  b. Se você tiver configurado múltiplas instâncias da integração de ferramenta Nexus, insira o nome da integração de ferramenta Nexus para a qual você deseja configurar a tarefa de construção Maven.

  c. Para o tipo de integração de ferramenta, selecione **Nexus**.

  d. Para o comando de construção, insira os comandos para construir seu módulo Maven ou para publicá-lo em seu registro de captura instantânea. Este exemplo mostra os comandos para construir o módulo ou publicá-lo.
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Dica**: é possível localizar a URL e as credenciais do usuário usadas para se conectar ao registro nas definições de configuração da integração de ferramenta Nexus.

1. Clique em **SALVAR**. Sempre que o pipeline for executado, essa tarefa de construção usará as informações de configuração da integração de ferramenta Nexus para se conectar ao repositório Maven.

Para obter mais informações, veja [Nexus ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/code/tool_nexus/){: new_window}.


## Configurando uma ferramenta customizada (Outra Ferramenta)
{: #othertool}

Se a sua equipe usar uma ferramenta que não está incluída na lista de integrações de cadeias de ferramentas, será possível integrar uma ferramenta customizada.

Configure uma ferramenta customizada para que ela trabalhe com outras ferramentas em sua cadeia de ferramentas e esteja disponível para a sua equipe:

1. Se você estiver configurando essa integração de ferramenta conforme cria a cadeia de ferramentas, na seção Integrações configuráveis, clique em **Outra ferramenta**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **Outra ferramenta**.

1. Digite o nome da ferramenta.
1. Selecione a fase de ciclo de vida que for mais estreitamente associada à ferramenta. Essa seleção determina em qual categoria sua ferramenta está listada na página Visão geral.
1. Inclua uma URL de ícone. O ícone será mostrado no cartão da integração de ferramenta.
1. Inclua uma URL de documentação.
1. Especifique um nome da instância da ferramenta. Por exemplo: Minha Ferramenta de Equipe.
1. Inclua uma URL da instância da ferramenta. Essa URL é aberta sempre que o cartão da integração de ferramenta é clicado.
1. Inclua uma descrição da sua ferramenta.
1. (Avançado) Inclua propriedades adicionais, se necessário. Por exemplo, liste quaisquer informações ou atributos que forem necessários para integrar sua ferramenta a outras ferramentas na cadeia de ferramentas.  
1. Clique em **Criar integração**.

Para saber mais, veja [Introduzindo a integração de ferramenta customizada para as cadeias de ferramentas do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/blogs/bluemix/2016/10/custom-tool-integration-with-bluemix-toolchains/){: new_window}.


## Configurando o PagerDuty
{: #pagerduty}

O PagerDuty integra dados de diversos sistemas de monitoramento em uma única visualização. Quando um problema ocorre, o PagerDuty
assegura que o membro da equipe que melhor se adapta para corrigi-lo no momento seja notificado. Se o membro da equipe não responder ao problema, as escaladas poderão ser configuradas para roteá-lo para engenheiros secundários ou gerenciadores de operações.

Configure o PagerDuty para enviar notificações quando as falhas de estágio de pipeline ocorrerem para que você possa corrigir problemas mais rapidamente e reduzir o tempo de inatividade:

1. Se você estiver configurando esta integração de ferramenta conforme estiver criando a cadeia de ferramentas, na seção Integrações configuráveis, clique em **PagerDuty**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **PagerDuty**.

1. Digite a chave de acesso API para sua conta PagerDuty. Se você não tiver uma conta PagerDuty, [registre-se para uma ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://signup.pagerduty.com/accounts/new){: new_window}. Para obter instruções para localizar a chave, veja [Gerando uma chave API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.pagerduty.com/hc/en-us/articles/202829310-Generating-an-API-Key){: new_window}.
1. Digite o nome de seu serviço PagerDuty.
1. Digite o endereço de e-mail para o contato PagerDuty primário.
1. Digite o número do telefone para o contato PagerDuty primário.
1. Clique em **Criar integração**.
1. Clique em **PagerDuty** para acessar pagerduty.com. É possível visualizar os eventos associados ao serviço PagerDuty
que você especificou quando configurou esta integração de ferramenta para sua cadeia de ferramentas.

Para saber mais, veja [PagerDuty ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configurando o Sauce Labs
{: #saucelabs}

O Sauce Labs executa testes de unidade funcional. Quando o suíte de testes do Sauce Labs é configurado como uma tarefa de teste no
{{site.data.keyword.deliverypipeline}}, o suíte de testes pode executar testes em relação a seu app da web ou móvel como parte de seu
processo de entrega contínua. Esses testes podem fornecer um controle de fluxo valioso para seus projetos, atuando como gates para impedir a
implementação de um código ruim.

 **Nota**: essa integração de ferramenta está disponível somente no {{site.data.keyword.Bluemix_notm}} Public. 

Configure o Sauce Labs para executar testes funcionais automatizados em múltiplos sistemas operacionais e navegadores para que possa emular a
forma que um usuário pode usar um website ou um aplicativo:

1. Se você estiver configurando esta integração de ferramenta conforme estiver criando a cadeia de ferramentas, na seção Integrações configuráveis, clique em **Sauce Labs**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **Sauce Labs**.

1. Digite o nome de usuário associado à sua conta Sauce Labs. É possível [localizar seu nome de usuário na mensagem de boas-vindas na parte superior da página da sua conta Sauce Labs ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://saucelabs.com/account){: new_window}.
1. Digite a chave de acesso para sua conta Sauce Labs. É possível [localizar a chave na página da sua conta Sauce Labs ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://saucelabs.com/account){: new_window}.
1. Clique em **Criar integração**.
1. Clique em **Sauce Labs** para acessar saucelabs.com e visualizar a atividade de teste da cadeia de ferramentas.

 **Dica**: se você incluiu uma tarefa de teste Sauce Labs no {{site.data.keyword.deliverypipeline}}, é possível selecionar a instância de serviço.

Para saber mais, veja [Sauce Labs ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configurando o Slack
{: #slack}

**Importante**: as notificações que são postadas nos canais públicos Slack estão visíveis a todos na equipe. Lembre-se
que você é responsável pelo conteúdo que postar.

O Slack é um sistema de mensagens e um sistema de notificação tempo real baseados na nuvem. O Slack fornece o bate-papo persistente, que é uma alternativa interativa ao e-mail para a colaboração da equipe. É
possível se comunicar com sua equipe em um canal dedicado ou em um conjunto de canais diretamente relacionado ao seu trabalho. Também é possível
compartilhar arquivos e imagens por meio dos canais ou em mensagens diretas entre duas ou mais pessoas. As comunicações nas mensagens diretas e nos
canais são retidas para que seja possível procurá-las.

Configure o Slack para recuperar notificações sobre sua cadeia de ferramentas a partir das integrações de ferramenta, como atividades de
teste e de implementação:

1. Se você estiver configurando esta integração de ferramenta conforme estiver criando a cadeia de ferramentas, na seção Integrações
configuráveis, clique em **Slack**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, em **Visão geral**.

 a. Clique em **Incluir uma ferramenta**.

 b. Na seção Integrações de ferramentas, clique em **Slack**.

1. Digite a URL de webhook do Slack, que é gerada pelo Slack como um webhook recebido. É necessária uma URL do webhook do Slack para que um canal Slack receba notificações sobre sua cadeia de ferramentas das integrações de ferramentas. Para obter instruções para criar ou localizar seu webhook, veja [Webhooks recebidos ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://api.slack.com/incoming-webhooks){: new_window}.

 **Dica**: se você estiver usando uma chave API para que seu canal Slack receba notificações sobre sua cadeia de ferramentas das integrações de ferramentas, sua configuração deverá ser atualizada para usar um webhook, como alternativa.

1. Digite o nome do canal Slack para o qual deseja que as notificações sejam enviadas. O canal já deverá existir e estar ativo em sua equipe do Slack.
1. Digite o nome do host da URL para sua equipe do Slack, que é a palavra ou a frase antes de `.slack.com` na URL de sua equipe. Por exemplo, se a URL de sua equipe for `https://team.slack.com`, o nome do host será `team`.
1. Clique em **Criar integração**.

 **Dica**: se o canal e a equipe do Slack especificados não puderem ser atingidos, o erro `Falha na configuração` será exibido no cartão do Slack. Passe o mouse sobre a mensagem `Falha na configuração` e clique em **Reconfigurar**. Certifique-se de que esteja usando parâmetros de configuração válidos para a URL do webhook do Slack, o canal Slack e o nome do host da URL para sua equipe do Slack. Atualize as configurações conforme necessário e clique em **Salvar integração**.

1. Clique em **Slack**. É possível visualizar todas as atividades para sua cadeia de ferramentas no canal Slack configurado.

Para saber mais, veja [Slack ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
