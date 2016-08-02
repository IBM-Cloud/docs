---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando integrações de ferramenta
{: #integrations}

*Última atualização: 17 de junho de 2016*
{: .last-updated}

É possível configurar integrações de ferramenta que suportam tarefas de desenvolvimento, implementação e operações ao criar uma cadeia de ferramentas ou é possível incluir e configurar integrações de ferramenta para customizar uma cadeia de ferramentas existente.  
{:shortdesc}

**Importante**: este recurso é experimental. As cadeias de ferramentas podem não ser estáveis e podem mudar de formas que
não sejam compatíveis com versões anteriores. Elas não são recomendadas para uso em ambientes de produção. Para usar cadeias de ferramentas,
deve-se fazer uma
[solicitação
para acesso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} única. As cadeias de ferramentas estão disponíveis na região sul dos EUA somente.

**Dica**: se desejar iniciar o desenvolvimento com seu código de origem, assegure-se de configurar o GitHub e as
integrações de ferramenta GitHub Issues antes de configurar o {{site.data.keyword.deliverypipeline}}.

## Configurando o pipeline de entrega
{: #deliverypipeline}

O {{site.data.keyword.deliverypipeline}} automatiza a implementação contínua de seus projetos por meio de sequências de estágios que
recuperam tarefas de entrada e de execução, como construções, testes e implementações. 

Configure o {{site.data.keyword.deliverypipeline}} para automatizar a construção, o teste e a implementação contínuos de seus apps: 

1. Se estiver configurando essa integração de ferramenta conforme estiver criando a cadeia de ferramentas, na seção Integrações
configuráveis, clique em **Pipeline de entrega**. Dependendo do modelo que usar, campos diferentes poderão estar disponíveis. Revise
os valores de campo padrão e, se necessário, mude essas configurações.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel DevOps, na guia
**Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Integrações de ferramenta. Como
alternativa, na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em
seguida, clique em **Integrações de ferramenta**. 
1. Clique no botão de inclusão (+).
1. Na seção Integrações de ferramenta, clique em **Pipeline de entrega**.
1. Especifique um nome para seu novo pipeline.
1. Se planejar usar seu pipeline para implementar uma interface com o usuário, selecione a caixa de seleção **App
visualizável**. Todos os apps que seu pipeline criar serão mostrados na lista **VISUALIZAR APP** na página Integrações
de ferramenta da cadeia de ferramentas.
1. Clique em **Criar integração** para incluir o {{site.data.keyword.deliverypipeline}} em sua cadeia de
ferramentas.
1. Clique no ladrilho para {{site.data.keyword.deliverypipeline}} para visualizar o pipeline e configurá-lo. Para aprender os fundamentos da configuração de um pipeline, consulte [Construindo e implementando pipelines](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Dica**: se desejar acionar o pipeline ao enviar por push as mudanças em seu repositório (repo) GitHub, deverá
configurar o GitHub para sua cadeia de ferramentas antes de definir os estágios para seu pipeline. Os estágios do pipeline precisam das URLs Git
para seus repos GitHub. Cada estágio de pipeline pode se
referir a somente um dos repos GitHub associado a sua cadeia de
ferramentas. Para obter
instruções para configurar o GitHub, consulte a seção [GitHub e GitHub Issues](#github).
  
1. Opcional: se desejar que o Sauce Labs execute testes em seu app, configure o {{site.data.keyword.deliverypipeline}} para
incluir uma tarefa de teste de Sauce Labs. Para obter instruções para configurar a tarefa de teste, consulte a seção
[Configurando uma tarefa de teste Sauce Labs em seu pipeline](#config_saucelabs).

### Configurando uma tarefa de teste Sauce Labs em seu pipeline
{: #config_saucelabs}

Antes de configurar uma tarefa de teste Sauce Labs em seu pipeline, será necessário um pipeline em funcionamento que possua estágios para
construir e implementar seu app e deve-se configurar o Sauce Labs para sua cadeia de ferramentas. Para obter instruções para configurar o Sauce
Labs, consulte a seção [Sauce Labs](#saucelabs).

Configure o {{site.data.keyword.deliverypipeline}} para incluir uma tarefa de teste Sauce Labs:

1. Se você não tiver um estágio que implemente uma versão de teste de seu app, crie um.
1. No estágio, inclua uma tarefa de teste após a tarefa de implementação. Ao colocar essas tarefas no mesmo estágio, elas poderão acessar o
mesmo conjunto de propriedades do ambiente.
  ![Tarefa de Teste
](images/toolchain_test_job.png) 

1. Configure o estágio: 

  a. Na guia **PROPRIEDADES DO AMBIENTE**, crie três propriedades: CF_APP_NAME, SAUCE_USERNAME e SAUCE_ACCESS_KEY.
  
  b. Insira seu nome de usuário e chave de acesso do Sauce Labs. Ao fazer isso, você externaliza esses valores para que possa usá-los em
seus testes.
  
1. Configure a tarefa de implementação. No campo **Implementar script**, inclua este comando: export CF_APP_NAME="$CF_APP". Esse
comando exporta o nome do app como uma propriedade do ambiente.
1. Configure a tarefa de teste. Os valores na imagem a seguir são exemplos. Os campos **Instância de serviço**,
**Destino**, **Organização** e **Espaço** serão preenchidos com o nome de usuário, região,
organização e espaço do Sauce Labs que estiver usando atualmente.
![Configurar tarefa](images/toolchain_configure_job.png)

  a. Para o tipo de testador, selecione **Sauce Labs**.
  
  b. Para a instância de serviço, selecione o nome de usuário Sauce Labs que usou quando configurou o Sauce Labs para sua cadeia de ferramentas. 
  
   **Dica**: para ver o nome de usuário e chave de acesso que usou quando configurou o Sauce Labs para sua cadeia de
ferramentas, clique em **Configurar**. 
  
  c. No campo **Comando de execução de teste**, insira os comandos que instalam as dependências necessárias por
seus testes e, em seguida, execute os testes. Por exemplo, para um app Node.js hipotético, é possível inserir:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Se desejar ver seus relatórios de teste nos logs de tarefa de teste, selecione a caixa de seleção **Ativar
relatório de teste** e configure o Padrão de arquivo de resultado de teste como `test/*.xml`.
  
1. Clique em **SALVAR**. Agora, sempre que seu pipeline for executado, seus testes Sauce Labs serão executados.

Para aprender mais, consulte [Pipeline
de entrega](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.

## Incluindo o Deployment Risk Analytics
{: #dra}

{{site.data.keyword.DRA_full}} coleta e analisa os resultados dos testes de unidade, testes funcionais e ferramentas de
cobertura de código para determinar se seu código atende a critérios predefinidos em gates especificados em seu processo de implementação. Se seu
código não atender ou exceder os critérios, a implementação será interrompida para evitar riscos de serem liberados. É possível usar o Deployment
Risk Analytics como uma rede de segurança para seu ambiente de entrega contínua ou como uma forma de implementar e melhorar os padrões de
qualidade. 

 **Dica**: esta integração de ferramenta é pré-configurada. Ela não requer nenhum parâmetro de configuração e não é
possível reconfigurá-la.
 
Inclua o Deployment Risk Analytics para manter e melhorar a qualidade de seu código no Bluemix monitorando suas implementações para
identificar riscos antes de serem liberadas:

1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel DevOps, na guia
**Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Integrações de ferramenta. Como alternativa,
na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**. 
1. Clique no botão de inclusão (+).
1. Na seção Integrações de ferramenta, clique em **Deployment Risk Analytics**. 
1. Clique em
**Criar integração**.
1. Clique no ladrilho para o Deployment Risk Analytics e, em seguida, conclua as etapas de introdução: criar critérios, conectar os
critérios ao pipeline e executar o pipeline. Para obter mais informações, consulte [Deployment Risk Analytics](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.

## Incluindo o Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

O Eclipse Orion {{site.data.keyword.webide}} é um ambiente baseado na web integrado em que é possível criar, editar, executar,
depurar e concluir tarefas de controle de fonte. É possível mover perfeitamente da edição para execução, do envio para implementação. 

 **Dica**: esta integração de ferramenta é pré-configurada. Ela não requer nenhum parâmetro de configuração e não é
possível reconfigurá-la.
 
Inclua a integração de ferramenta Eclipse Orion {{site.data.keyword.webide}} para concluir as tarefas de controle de fonte:

1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel DevOps, na guia
**Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Integrações de ferramenta. Como alternativa,
na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**. 
1. Clique no botão de inclusão (+).
1. Na seção Integrações de ferramenta, clique em **Eclipse Orion Web IDE**. 
1. Clique em
**Criar integração**.
1. Clique no ladrilho para o novo Eclipse Orion Web IDE. Sua
área de trabalho é pré-preenchida com seus repos GitHub. Os
repos associados a
sua cadeia de ferramentas atual são destacados.

Para aprender mais, consulte [Web
IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}.


## Configurando GitHub e GitHub Issues
{: #github}

O GitHub é um serviço de hospedagem baseado na web para
repos Git. É possível ter ambas as cópias local e remota de
seus repos, o que
facilita a colaboração. 

O GitHub Issues é uma ferramenta de controle que mantém seu trabalho e seus planos todos em um lugar. Ele
é integrado a seu repo de
desenvolvimento para que possa focar em tarefas importantes.

Configure o GitHub e o GitHub Issues para gerenciar seu código de fonte na nuvem:

1. Se estiver configurando esta integração de ferramenta conforme estiver criando a cadeia de ferramentas, siga estas etapas:

 a. Na seção Integrações configuráveis, clique em **GitHub**. Se você não tiver autorizado o
{{site.data.keyword.Bluemix}} para acessar o GitHub, clique em **Autorizar** para acessar o website GitHub. Se você não
tiver uma sessão GitHub ativa, será solicitado que efetue login. Clique em **Autorizar aplicativo** para permitir que o {{site.data.keyword.Bluemix}} acesse sua conta GitHub. Se
você tiver uma sessão GitHub ativa, mas não tiver inserido sua senha recentemente, poderá ser solicitado que insira sua senha GitHub para
confirmar.
 
 b. Revise os locais de repo de destino padrão para os
repos GitHub. Esses repos são clonados a partir dos mesmos
repos de amostra. Se
necessário, mude os nomes dos repos de destino.
 ![Locais de repo de destino padrão](images/toolchain_github_config.png)
   
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel DevOps, na guia
**Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Integrações de ferramenta. Como alternativa,
na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**. 
1. Clique no botão de inclusão (+).
1. Na seção Integrações de ferramenta, clique em **GitHub**.
1. Se você tiver um repo GitHub e desejar usá-lo, digite
a
URL. Para o tipo de repositório, clique em **Link**.
1. Se desejar usar um novo repo GitHub, digite um nome
para o repo GitHub, digite a URL para o repo que estiver
clonando ou bifurcando e
selecione o tipo de repositório: 

 a. Para criar um repo vazio, selecione
**Novo**. 
 
 b. Para criar uma cópia de um repo GitHub, selecione
**Clonar**.
 
 c. Para bifurcar um repo GitHub para que possa contribuir
com as mudanças por meio das solicitações de pull, selecione
**Bifurcar**.
 
1. Se desejar usar o GitHub Issues para o controle de emissões, selecione a caixa de seleção **Ativar GitHub Issues**.
1. Clique em
**Criar integração**.
1. Clique no ladrilho para o repo GitHub com que deseja
trabalhar para acessar o github.com e visualize o conteúdo do repo.
 
  **Dica**: é possível usar as ferramentas de gerenciamento de código fonte integradas no Eclipse Orion Web IDE para
editar o repo GitHub e implementar um app a partir de sua área de
trabalho.

1. Se você ativou o GitHub Issues, clique no ladrilho para o GitHub Issues para acessar o GitHub Issues.

Para aprender mais, consulte [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} e [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.    

##Usando o Dedicated {{site.data.keyword.ghe_short}}
{: #ghe}

{{site.data.keyword.ghe_long}} é a versão hospedada pela nuvem IBM e totalmente gerenciada do
{{site.data.keyword.ghe_short}}, disponível para ambientes Dedicated Bluemix. O GitHub fornece a experiência de codificação social que os desenvolvedores amam. O
[{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window} fornece um ambiente de computação em nuvem em hardware isolado fisicamente, integrado à sua rede.

O Dedicated {{site.data.keyword.ghe_short}} é para clientes {{site.data.keyword.Bluemix_notm}} Dedicated somente.

### Configurando sua conta 

O {{site.data.keyword.ghe_short}} inclui a conexão única com o {{site.data.keyword.Bluemix_notm}} Dedicated. Para efetuar
login no {{site.data.keyword.ghe_short}}, cole a URL de seu administrador de região ou e-mail de boas-vindas em um navegador. Sua URL
seguirá este padrão: `github.your-company-dedicated-name.bluemix.net`. Conecte-se a seu ID do usuário e senha do {{site.data.keyword.Bluemix_notm}} Dedicated e a sua conta do {{site.data.keyword.ghe_short}} será criada
automaticamente.

**Nota:** se uma mensagem declarar que seu ID do usuário não existe, solicite ao seu administrador de região que inclua seu ID do usuário no registro do usuário do {{site.data.keyword.Bluemix_notm}} Dedicated. Se você for o administrador de região, consulte [Gerenciando usuários e permissões do {{site.data.keyword.Bluemix_notm}} Dedicated](https://new-console.stage1.ng.bluemix.net/docs/admin/index.html#oc_useradmin){: new_window}.

Na maioria dos casos, seu nome de usuário GitHub é seu nome abreviado de e-mail, a menos que seu nome abreviado inclua caracteres que o
GitHub não suporte, como pontos. Se seu nome abreviado incluir caracteres que o GitHub não suportar, os caracteres serão substituídos por traços.     

### Incluindo um endereço de e-mail em sua conta

Deve-se incluir seu endereço de e-mail em suas configurações de conta do {{site.data.keyword.ghe_short}} para receber
notificações. Após incluir seu endereço de e-mail, você aproveita os recursos de codificação social do {{site.data.keyword.ghe_short}}.    
 
Para incluir seu endereço de e-mail em sua conta do Dedicated {{site.data.keyword.ghe_short}}, conclua estas etapas:    
1. No canto superior direito de qualquer página do GitHub, clique em seu ícone de perfil e, em seguida, clique em
**Configurações**.    
2. Na barra lateral, clique em **E-mails**.    
3. Inclua seu endereço de e-mail e clique em **Incluir**.     

{: #ghe_auth}
### Criando um token de acesso pessoal ou chave SSH para autenticação

Para executar operações Git remotas como
`clonar` ou `enviar por push` do
seu repositório Git local,
deve-se usar um token de acesso pessoal ou chave SSH para se autenticar com o {{site.data.keyword.ghe_short}}. A autenticação por
meio de HTTPS é suportada usando um token de acesso somente; não é possível usar seu ID do usuário e senha para clonar ou enviar por push de um
repositório local. As solicitações de API também requerem um token de acesso pessoal.

**Nota:** para usar um token de acesso pessoal ou chave SSH para autenticação, deve-se configurar o Git localmente. Para
obter instruções, consulte [Configurando o Git](https://help.github.com/enterprise/2.6/user/articles/set-up-git/){: new_window}.    

Para criar um token de acesso pessoal, conclua estas etapas:    
   1. No canto superior direito de qualquer página do GitHub, clique em seu ícone de perfil e, em seguida, clique em
**Configurações**.    
   2. Na barra lateral, clique em **Tokens de acesso pessoal**.   
   3. Clique em **Gerar novo token**.
   4. Inclua uma descrição de token e clique em **Gerar token**.
   5. Copie o token em um local seguro ou app de gerenciamento de senha.
     **Nota:** por motivos de segurança, após deixar a página, não será mais possível ver o token novamente.    

Use seu token de acesso pessoal em vez de uma senha para o acesso da linha de comandos por HTTPS. 


Para criar uma chave SSH, conclua estas etapas:
   1. Abra o Git Bash (Windows) ou uma nova janela do Terminal (Linux e Mac).    
   2. Cole o texto a seguir, substituindo o endereço de e-mail que incluiu em sua conta {{site.data.keyword.ghe_short}}:
   
     ``
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     # Cria uma nova chave SSH, usando o e-mail fornecido como um rótulo
     Gerando par de chaves rsa pública/privada.
     ``

   3. Quando for solicitado que especifique um arquivo para salvar a chave, pressione Enter para aceitar o local padrão.
   4. No prompt, digite um passphrase seguro. Para obter mais informações, consulte [Trabalhando com passphrases de chave SSH](https://help.github.com/enterprise/2.6/user/articles/working-with-ssh-key-passphrases/){: new_window}.   

Inclua sua chave SSH no ssh-agent:    
   1. Assegure-se de que o ssh-agent esteja ativado. Usando o Git Bash, insira este comando para ativar o ssh-agent:
      ``
      # inicie o ssh-agent no plano de fundo
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ``    
  
   2. Inclua sua chave SSH no ssh-agent inserindo este comando:
      ``
      $ ssh-add ~/.ssh/id_rsa
      ``    
   3. Inclua a chave SSH em sua conta GitHub. Para obter mais informações, consulte
[Incluindo uma nova chave SSH em sua
conta GitHub](https://help.github.com/enterprise/2.6/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}.
   

### Configurando organizações, equipes e repos GitHub    

Configurar organizações GitHub é útil porque você cria grupos distintos de usuários que trabalham em projetos ou tarefas semelhantes. Organizar
equipes em uma organização tem o benefício agregado de controlar o acesso a repos. Para obter mais informações, consulte [Organizações e equipes](https://help.github.com/enterprise/2.6/admin/guides/user-management/organizations-and-teams/){: new_window}.

**Nota:** as organizações GitHub não são as mesmas que as organizações Bluemix.

Configure o projeto de sua equipe concluindo estas etapas:

   1. [Criar uma
organização (org)](https://help.github.com/enterprise/2.6/user/articles/creating-a-new-organization-account/){: new_window}.
   2. [Criar
um repo para sua organização](https://help.github.com/enterprise/2.6/user/articles/create-a-repo/){: new_window}.
   3. [Convidar usuários a se unirem em sua organização](https://help.github.com/enterprise/2.6/user/articles/inviting-users-to-join-your-organization/){: new_window}.
   4. [Selecione cuidadosamente
pelo menos um membro de equipe para ter permissões de proprietário em sua organização](https://help.github.com/enterprise/2.6/user/articles/changing-a-person-s-role-to-owner/){: new_window}.
   
  **Nota:** antes de convidar usuários para sua organização, eles devem efetuar login no
{{site.data.keyword.ghe_short}} pelo menos uma vez ou suas contas {{site.data.keyword.ghe_short}} não estarão disponíveis para
convite.
   
### Obtendo Suporte
Para obter respostas agora, envie questões a [Estouro de pilha](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}. 

Para obter mais suporte, use estes recursos:    
   1. Conclua o formulário em https://ibm.biz/bluemixsupport.   
   2. Envie um novo chamado por meio do Client Success Portal em https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix.    


## Configurando o PagerDuty
{: #pagerduty}

O PagerDuty integra dados de diversos sistemas de monitoramento em uma única visualização. Quando um problema ocorre, o PagerDuty
assegura que o membro da equipe que melhor se adapta para corrigi-lo no momento seja notificado. Se o membro da equipe não responder ao problema, as escaladas poderão ser configuradas para roteá-lo para engenheiros secundários ou gerenciadores de operações.

Configure o PagerDuty para enviar notificações quando as falhas de estágio de pipeline ocorrerem para que você possa corrigir problemas mais rapidamente e reduzir o tempo de inatividade:

1. Se você estiver configurando esta integração de ferramenta conforme estiver criando a cadeia de ferramentas, na seção Integrações configuráveis, clique em **PagerDuty**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel DevOps, na guia
**Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Integrações de ferramenta. Como alternativa,
na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**. 
1. Clique no botão de inclusão (+).
1. Na seção Integrações de ferramenta, clique em **PagerDuty**
1. Digite o nome do site PagerDuty associado à sua conta PagerDuty. Se você não tiver uma conta PagerDuty,
[registre uma](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Digite a chave de acesso API para sua conta PagerDuty. Para obter instruções para localizar a chave, consulte
[Autenticação de API](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Digite o nome de seu serviço PagerDuty.
1. Digite o endereço de e-mail para o contato PagerDuty primário.
1. Digite o número do telefone para o contato PagerDuty primário.
1. Clique em
**Criar integração**.
1. Clique no ladrilho para o PagerDuty para acessar o pagerduty.com. É possível visualizar os eventos associados ao serviço PagerDuty
que você especificou quando configurou esta integração de ferramenta para sua cadeia de ferramentas. 

Para aprender mais, consulte [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configurando o Sauce Labs
{: #saucelabs}

O Sauce Labs executa testes de unidade funcional. Quando o suíte de testes do Sauce Labs é configurado como uma tarefa de teste no
{{site.data.keyword.deliverypipeline}}, o suíte de testes pode executar testes em relação a seu app da web ou móvel como parte de seu
processo de entrega contínua. Esses testes podem fornecer um controle de fluxo valioso para seus projetos, atuando como gates para impedir a
implementação de um código ruim.

Configure o Sauce Labs para executar testes funcionais automatizados em múltiplos sistemas operacionais e navegadores para que possa emular a
forma que um usuário pode usar um website ou um aplicativo:

1. Se você estiver configurando esta integração de ferramenta conforme estiver criando a cadeia de ferramentas, na seção Integrações configuráveis, clique em **Sauce Labs**.
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel DevOps, na guia
**Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Integrações de ferramenta. Como alternativa,
na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**. 
1. Clique no botão de inclusão (+).
1. Na seção Integrações de ferramenta, clique em **Sauce Labs**.
1. Digite o nome de usuário associado à sua conta Sauce Labs. É possível [localizar seu nome de
usuário na mensagem de boas-vindas na parte superior da página da sua conta Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Digite a chave de acesso para sua conta Sauce Labs. É possível [localizar a chave no
canto inferior esquerdo da página da sua conta Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Clique em
**Criar integração**.
1. Clique no ladrilho para o Sauce Labs para acessar saucelabs.com e visualizar a atividade de teste para a cadeia de ferramentas.

 **Dica**: se você incluiu uma tarefa de teste Sauce Labs no {{site.data.keyword.deliverypipeline}}, é possível selecionar a instância de serviço.

Para aprender mais, consulte [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


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
1. Se você tiver uma cadeia de ferramentas e estiver incluindo essa integração de ferramenta nela, no painel DevOps, na guia
**Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Integrações de ferramenta. Como alternativa,
na página Visão geral do app, no ladrilho Entrega contínua, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**.
1. Clique no botão de inclusão (+).
1. Na seção Integrações de ferramenta, clique em **Slack**.
1. Digite o token de autenticação API para sua conta Slack. Deve-se usar um token de acesso total gerado para se autenticar com o Slack. Para
obter instruções para localizar o token, consulte [Autenticação de Slack](https://api.slack.com/web#authentication){: new_window}.
1. Digite o nome do canal Slack para o qual deseja que as notificações sejam enviadas. Se o canal que especificar não existir, ele será criado. Se o canal foi arquivado, ele será reativado.
1. Clique em
**Criar integração**.
1. Clique no ladrilho para o Slack. É possível visualizar todas as atividades para sua cadeia de ferramentas no canal Slack configurado.

Para aprender mais, consulte [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
