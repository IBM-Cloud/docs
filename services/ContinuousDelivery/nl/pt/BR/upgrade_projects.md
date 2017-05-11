---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Fazer upgrade do projeto {{site.data.keyword.jazzhub_short}} para uma cadeia de ferramentas
{: #upgrade_projects}

O {{site.data.keyword.jazzhub}} está sendo desenvolvido para o {{site.data.keyword.contdelivery_full}}. Como parte dessa mudança, será feito upgrade dos projetos para cadeias de ferramentas. 

É possível fazer upgrade de seu projeto ou esperar que seja submetido a upgrade automaticamente. Para obter a melhor experiência, faça upgrade de seu projeto assim que possível para que você possa controlar qual é o nome da sua cadeia de ferramentas e em qual organização ela foi criada.  
{: shortdesc}

## Cadeias de ferramentas
{: #compare_toolchains}

As cadeias de ferramentas são como projetos, com algumas diferenças importantes:

- Os projetos podem ter apenas um repositório (repo) e pipeline. As cadeias de ferramentas podem ter tantos repositórios e pipelines quantos forem necessários.
- As cadeias de ferramentas podem incluir ferramentas que não estão disponíveis em projetos, como Slack, Sauce Labs, PagerDuty e {{site.data.keyword.DRA_full}}.
- O acesso às cadeias de ferramentas é gerenciado por meio de organizações padrão do Bluemix. A associação é mantida no nível de organização, ao contrário dos projetos, nos quais a associação era mantida no nível do projeto.

É possível saber mais sobre cadeias de ferramentas no [YouTube![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://youtu.be/2SIPE1e7NJ4){: new_window} ou em [Introdução ao {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![Link externo para o YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}    

## Pré-requisitos
{: #upgrade_prereqs}    

- Para acessar a cadeia de ferramentas de seu projeto submetido a upgrade, você precisará de um ID do Bluemix. Antes de fazer upgrade, deve-se verificar se você tem um ID ativo do Bluemix. Se você não tiver um, [inscreva-se](https://console.ng.bluemix.net/registration/).
- Certifique-se de que o proprietário do projeto DevOps Services esteja correto. A cadeia de ferramentas criada de seu projeto fará parte da organização do Bluemix desse proprietário.

**Importante:** o Eclipse Orion {{site.data.keyword.webide}} na cadeia de ferramentas é separado do {{site.data.keyword.webide}} que está associado ao seu projeto. Se você usar o {{site.data.keyword.webide}} e houver mudanças não confirmadas, confirme-as antes de fazer upgrade.  


## Fazendo upgrade de um projeto para uma cadeia de ferramentas
{: #project_to_toolchain}

Quando seu projeto estiver pronto para ser submetido a upgrade, uma mensagem será exibida no cartão do projeto e na página Visão geral.

![Imagem do cartão com a etiqueta Pronto para upgrade](images/card-project-to-upgrade.png)

![Mensagem Hora de fazer upgrade](images/banner-ready-to-upgrade.png)

**Dica:** é possível localizar projetos que estão prontos para upgrade no menu na página Meus projetos: 

![Imagem do item de menu Projetos para upgrade](images/menu-projects-to-upgrade.png)

## Iniciando o Processo de Upgrade
{: #start_upgrade}

Antes de iniciar o processo de upgrade, é possível vê-lo em ação no [YouTube![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://youtu.be/oaZVGveVxBg){: new_window}.
[![Link externo para o YouTube](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window}    
Para fazer upgrade de seu projeto para uma cadeia de ferramentas, siga estas etapas:

1. Para iniciar o processo de upgrade, na mensagem do banner, clique em **fazer upgrade agora**. A página "Cadeia de ferramentas de upgrade do projeto" é aberta. 

   ![Exemplo de uma página de upgrade](images/project-upgrade-toolchain.png)

   Para obter uma visão geral do processo de upgrade, leia a descrição nessa página. Nesse caso, como o projeto usou um repositório em GitHub.com, a cadeia de ferramentas será conectada ao mesmo repositório GitHub. A cadeia de ferramentas incluirá um novo pipeline que contém os mesmos estágios e tarefas que o pipeline do projeto. Além disso, a cadeia de ferramentas conterá um ponteiro para o Eclipse Orion {{site.data.keyword.webide}}, que é executado no {{site.data.keyword.contdelivery_short}}.

2. Para customizar a cadeia de ferramentas, é possível configurar algumas definições:

   - Para mudar o nome da cadeia de ferramentas, edite o campo **Nome**.

      ![Campo Nome](images/name-change.png)

   - Para mudar em qual organização do {{site.data.keyword.Bluemix_notm}} criar a cadeia de ferramentas, selecione a organização no menu de sua conta:

      ![Selecionador de organização do Bluemix](images/bluemix-organization-chooser.png)

   Como as cadeias de ferramentas são gerenciadas no nível de organização, certifique-se de selecionar uma organização na qual os membros do projeto que precisam acessar as cadeias de ferramentas já existam ou possam ser incluídos. 
  
3. Clique em **Criar**. A nova cadeia de ferramentas é criada e sua página Visão geral é exibida.

   ![Visão geral da cadeia de ferramentas submetida a upgrade](images/new-toolchain-page.png)

   - Para acessar seu repositório GitHub ou o rastreador de problemas associado, clique em **GitHub** ou **Problemas**.
   
   - Para acessar seu pipeline, clique em **Delivery Pipeline**.  
   
   - Para acessar o {{site.data.keyword.webide}}, que contém o conteúdo de seu repositório que foi retirado para a área de trabalho, clique em **Eclipse Orion {{site.data.keyword.webide}}**. 

## Revisitando seu projeto
{: #revisit_projects}

Você está pronto para usar sua nova cadeia de ferramentas. Seu projeto agora está identificado como "Submetido a upgrade" e, na página Visão geral, é exibida uma mensagem de confirmação.

![Imagem do cartão do projeto com a etiqueta Submetido a upgrade](images/card-upgraded-project.png)

![Projeto submetido a upgrade](images/banner-upgraded.png)

É possível ver quais projetos foram submetidos a upgrade selecionando **Projetos submetidos a upgrade** no menu na página Meus projetos:

![Imagem do item de menu Projetos submetidos a upgrade](images/menu-upgraded-projects.png)

Se for necessário reverter o upgrade, exclua sua cadeia de ferramentas. Em seguida, ao retornar para a página Visão geral do projeto, a mensagem de upgrade será exibida novamente e será possível fazer upgrade novamente quando você estiver pronto.

## Próximas Etapas
{: #upgrade_next_steps}   

1. Confirme se o upgrade está completo, verificando a mensagem na página Visão geral do projeto:    

   ![Projeto submetido a upgrade](images/banner-upgraded.png)    

2. Dê aos membros da equipe acesso à cadeia de ferramentas.    
    - Cada membro da equipe deve ter uma conta válida do Bluemix. Os membros da equipe que não tiverem contas deverão [inscrever-se ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/registration){:new_window}.
    - Inclua membros da equipe na organização (org) à qual a cadeia de ferramentas pertence.
3. Use as ferramentas de sua cadeia de ferramentas no lugar das ferramentas de seu projeto {{site.data.keyword.jazzhub_short}}. Por exemplo, para editar código usando um navegador, use o Web IDE de sua cadeia de ferramentas.    

## Solucionando problemas
{: #upgrade_troubleshoot}    

Se você tiver perguntas ou problemas, envie um e-mail para [hub@jazz.net](mailto:hub@jazz.net). No e-mail, inclua as URLs para o projeto {{site.data.keyword.jazzhub_short}} e a cadeia de ferramentas do {{site.data.keyword.contdelivery_short}}.

