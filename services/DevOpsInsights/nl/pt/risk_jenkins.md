---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrando a projetos Jenkins de formato livre

Depois de incluir o {{site.data.keyword.DRA_full}} em uma cadeia de ferramentas aberta e definir as políticas que ele monitora, será possível integrá-lo a seu projeto Jenkins de formato livre. Projetos Jenkins de formato livre são configurados e administrados por meio da interface da web do Jenkins. 

O plug-in IBM Cloud DevOps para Jenkins integra projetos Jenkins a cadeias de ferramentas. Uma *cadeia de ferramentas* é um conjunto de integrações de ferramentas que suporta tarefas de desenvolvimento, de implementação e de operações. O
poder coletivo de uma cadeia de ferramentas é maior que a soma de suas integrações de ferramentas individuais. As cadeias de ferramentas abertas são parte do serviço {{site.data.keyword.contdelivery_full}}. Para saber mais sobre o serviço {{site.data.keyword.contdelivery_short}}, veja [sua documentação](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Depois de instalar o plug-in IBM Cloud DevOps, será possível publicar os resultados de teste no {{site.data.keyword.DRA_short}}, incluir portas de qualidade automatizadas e controlar o risco de implementação. Também é possível enviar notificações de tarefa para outras ferramentas em sua cadeia de ferramentas, como Slack e PagerDuty. Para ajudá-lo a controlar as implementações, a cadeia de ferramentas poderá incluir mensagens de implementação nas confirmações do Git e seus problemas Git ou JIRA relacionados. Também será possível visualizar suas implementações na página Conexões da cadeia de ferramentas. 

O plug-in fornece ações pós-construção e CLIs para suportar a integração. O {{site.data.keyword.DRA_short}} agrega e analisa os resultados de testes de unidade, testes funcionais, ferramentas de cobertura de código, varreduras de código de segurança estática e varreduras de código de segurança dinâmica para determinar se seu código atende às políticas predefinidas nas portas em seu processo de implementação. Se o seu código não atender nem exceder uma
política, a implementação será interrompida, impedindo que as mudanças de risco sejam liberadas. É possível usar o {{site.data.keyword.DRA_short}} como uma
rede de segurança para o seu ambiente de entrega contínua, uma forma de implementar e melhorar padrões de qualidade ao longo do tempo e uma ferramenta de visualização
de dados para ajudá-lo a entender o funcionamento do seu projeto.

## Pré-Requisitos
{: #jenkins_prerequisites}

Deve-se ter acesso a um servidor que esteja executando um projeto Jenkins.

## Criando uma cadeia de ferramentas
{: #jenkins_create}

Antes de ser possível integrar o {{site.data.keyword.DRA_short}} a um projeto Jenkins, deve-se criar uma cadeia de ferramentas. 

1. Para criar uma cadeia de ferramentas, acesse a [página Criar uma cadeia de ferramentas](https://console.ng.bluemix.net/devops/create) e siga as instruções nessa página. 

2. Depois de criar a cadeia de ferramentas, inclua o {{site.data.keyword.DRA_short}} nela. Para obter instruções, veja a [documentação do {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html). 

## Instalando o Plug-in
{: #jenkins_install}

Primeiro, faça download do plug-in do {{site.data.keyword.DRA_short}}.  

1. Na página Visão geral da cadeia de ferramentas, clique em **DevOps Insights**.
2. Clique em **Configurações** e, em seguida, em **Configuração do plug-in do Jenkins**.
3. Siga as instruções na página para fazer download do plug-in.

Em seguida, no servidor Jenkins, instale o plug-in.

1. Clique em **Gerenciar Jenkins &gt; Gerenciar plug-ins** e clique na guia **Avançado**.
2. Clique em **Escolher arquivo** e selecione o arquivo de instalação do plug-in IBM Cloud DevOps. 
3. Clique em **Carregar**.
4. Reinicie o Jenkins e verifique se o plug-in foi instalado.

## Configurando tarefas do Jenkins para o painel Deployment Risk
{: #jenkins_configure}

Após a instalação do plug-in, é possível integrar o {{site.data.keyword.DRA_short}} ao projeto Jenkins. 

Siga estas etapas para usar as portas e o painel do Deployment Risk com seu projeto.

1. Abra a configuração de quaisquer tarefas que você tenha, como construção, teste ou implementação.

2. Inclua uma ação pós-construção para o tipo correspondente:

   * Para tarefas de construção, use **Publicar informações de construção no IBM Cloud DevOps**.
   
   * Para tarefas de teste, use **Publicar o resultado do teste no IBM Cloud DevOps**.
   
   * Para tarefas de implementação, use **Publicar informações de implementação no IBM Cloud DevOps**.
   
3. Preencha os campos requeridos. Eles variarão, dependendo do tipo de tarefa. 

   * Na lista **Credenciais**, selecione o ID e a senha do {{site.data.keyword.Bluemix_notm}}. Se eles não estiverem salvos no Jenkins, clique em **Incluir** para incluí-los e salvá-los. Teste sua conexão com o {{site.data.keyword.Bluemix_notm}} clicando em **Conexão de teste**.
   
   * No campo **Nome da tarefa de construção**, especifique o nome de sua tarefa de construção exatamente como está no Jenkins. Se a construção ocorrer com a tarefa de teste, deixe esse campo vazio. Se a tarefa de construção ocorrer fora do Jenkins, marque a caixa de seleção **As construções estão sendo feitas fora do Jenkins** e especifique o número e a URL da construção.
   
   * Para o ambiente, se os testes estiverem em execução no estágio de construção, selecione apenas o ambiente de construção. Se os testes estiverem em execução no estágio de implementação, selecione o ambiente de implementação e especifique o nome do ambiente. Dois valores são suportados: `STAGING` e `PRODUCTION`.
   
   * Para o campo **Local do arquivo de resultado**, especifique o local do arquivo de resultado. Se o teste não gerar um arquivo de resultado, deixe esse campo vazio. O plug-in fará upload de um arquivo de resultado padrão com base no status da tarefa de teste atual.

   Estas imagens mostram configurações de exemplo:
   
   ![Fazer upload de informações de construção](images/Upload-Build-Info.png "Publicar informações de construção no DRA")
   *Publicar informações de construção*
   
   ![Fazer upload de resultado de teste](images/Upload-Test-Result.png "Publicar resultado de teste no DRA")
   *Publicar resultado de teste*
   
   ![Fazer upload de informações de implementação](images/Upload-Deployment-Info.png "Publicar informações de implementação no DRA")
   *Publicar informações de implementação*

4. Se desejar usar as portas de política do {{site.data.keyword.DRA_short}} para controlar uma tarefa de implementação de recebimento de dados, inclua uma ação pós-construção, **Porta do IBM Cloud DevOps**. Escolha uma política e especifique o escopo dos resultados de teste. Para permitir que as portas de política evitem implementações de recebimento de dados, marque a caixa de seleção **Falhar a construção com base nas regras de política**. A imagem a seguir mostra uma configuração de exemplo:

    ![Porta do DevOps Insights](images/DRA-Gate.png "Porta do DevOps Insights")

5. Execute a tarefa de construção do Jenkins.

6. Visualize o painel Deployment Risk acessando o [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops), selecionando sua cadeia de ferramentas e clicando em **DevOps Insights**.

O painel Deployment Risk depende da presença de uma porta após uma tarefa de implementação temporária. Se desejar usar o painel, certifique-se de que tenha uma porta depois de implementar no ambiente temporário, mas antes de implementar em um ambiente de produção.
    
## Configurando as Notificações
{: #jenkins_notifications}

É possível configurar as tarefas do Jenkins para enviar notificações para ferramentas, como Slack ou PagerDuty, seguindo as instruções nos [Bluemix Docs](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).

Este exemplo mostra como configurar o `ICD_WEBHOOK_URL` para configurações de tarefa:
![Configurar o parâmetro ICD_WEBHOOK_URL](images/Set-Parameterized-Webhook.png "Configurar WebHook parametrizado")

Este exemplo mostra como configurar ações pós-construção para notificações de tarefa:
![Ações pós-construção para notificação de WebHook](images/PostBuild-WebHookNotification.png "Configurar notificação de WebHook em ações pós-construção")
