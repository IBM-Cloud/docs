---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Fazer upgrade do projeto {{site.data.keyword.jazzhub_short}} para uma cadeia de ferramentas
{: #upgrade_projects}

O {{site.data.keyword.jazzhub}} está sendo desenvolvido para o {{site.data.keyword.contdelivery_full}}. Como parte dessa mudança, será feito upgrade dos projetos para cadeias de ferramentas.

É possível fazer upgrade de seu projeto ou esperar que seja submetido a upgrade automaticamente. Para obter a melhor experiência, certifique-se de atender aos [pré-requisitos](#upgrade_prereqs) e fazer upgrade de seu projeto assim que possível para que possa controlar o nome da sua cadeia de ferramentas e a organização na qual ela foi criada.
{: shortdesc}

## Cadeias de ferramentas
{: #compare_toolchains}

As cadeias de ferramentas são como projetos, com algumas diferenças importantes:

- Os projetos podem ter apenas um repositório (repo) e pipeline. As cadeias de ferramentas podem ter tantos repositórios e pipelines quantos forem necessários.
- As cadeias de ferramentas podem incluir ferramentas que não estão disponíveis em projetos, como Slack, Sauce Labs, PagerDuty e {{site.data.keyword.DRA_full}}.
- O acesso às cadeias de ferramentas é gerenciado pelas organizações {{site.data.keyword.Bluemix_notm}} padrão. A associação é mantida no nível de organização, ao contrário dos projetos, nos quais a associação era mantida no nível do projeto.

É possível saber mais sobre cadeias de ferramentas no [YouTube ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://youtu.be/2SIPE1e7NJ4){: new_window} ou em [Introdução ao {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![Link externo para o YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}

## Pré-requisitos
{: #upgrade_prereqs}

- Para acessar a cadeia de ferramentas de seu projeto atualizado, você precisa de um ID do {{site.data.keyword.Bluemix_notm}}. Antes de fazer upgrade, deve-se verificar se você tem um ID do {{site.data.keyword.Bluemix_notm}} ativo. Se você não tiver um, [inscreva-se](https://console.ng.bluemix.net/registration/).
- Certifique-se de que o proprietário do projeto {{site.data.keyword.jazzhub_short}} esteja correto. A cadeia de ferramentas criada no seu projeto fará parte da organização {{site.data.keyword.Bluemix_notm}} desse proprietário.
- Se você estiver planejando iniciar o upgrade, certifique-se de que seja membro de cada organização e espaço nos quais o pipeline é implementado. Qualquer administrador de projeto pode iniciar o upgrade. No entanto, se o administrador que inicia o upgrade não for membro de cada organização e espaço nos quais o pipeline é implementado, o pipeline não poderá ser criado. A pessoa que inicia o upgrade se torna o proprietário do repositório na cadeia de ferramentas.
- O Eclipse Orion {{site.data.keyword.webide}} na cadeia de ferramentas é separado do {{site.data.keyword.webide}} que está associado ao projeto. Se você usar o {{site.data.keyword.webide}} e houver mudanças não confirmadas, confirme-as antes de fazer upgrade.


## Fazendo upgrade de um projeto para uma cadeia de ferramentas
{: #project_to_toolchain}

**Importante:** Os projetos no hub.jazz.net e nas cadeias de ferramentas são hospedados na região sul dos EUA. Se seu projeto foi configurado para implementar apps em uma região diferente, ele ainda implementará apps nessa região após o upgrade para uma cadeia de ferramentas.

Quando seu projeto estiver pronto para ser submetido a upgrade, uma mensagem será exibida no cartão do projeto e na página Visão geral.

![Imagem do cartão com a etiqueta Pronto para upgrade](images/card-project-to-upgrade.png)

![Mensagem Hora de fazer upgrade](images/banner-ready-to-upgrade.png)

**Dica:** é possível localizar projetos que estão prontos para upgrade no menu na página Meus projetos:

![Imagem do item de menu Projetos para upgrade](images/menu-projects-to-upgrade.png)

Ao iniciar o upgrade, os estágios do pipeline em seu projeto serão bloqueados. Você não conseguirá executá-los ou modificá-los. Se você reverter o upgrade excluindo a cadeia de ferramentas, o pipeline será desbloqueado.

Se seu projeto usar um repositório Git hospedado no JazzHub, depois de iniciar o upgrade, o repositório será bloqueado para garantir a integridade dos dados que são movidos para a cadeia de ferramentas. Se você reverter o upgrade excluindo a cadeia de ferramentas, o repo no JazzHub será desbloqueado.

## Iniciando o Processo de Upgrade
{: #start_upgrade}

Antes de iniciar o processo de upgrade, é possível vê-lo em ação no [YouTube![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://youtu.be/LSr2e3uvyLs){: new_window}.
[![Link externo para o YouTube](images/migration-video2.png)](https://youtu.be/LSr2e3uvyLs){: new_window}

Para fazer upgrade de seu projeto para uma cadeia de ferramentas, siga estas etapas:

1. Para iniciar o processo de upgrade, na mensagem do banner, clique em **fazer upgrade agora**. A página "Cadeia de ferramentas de upgrade do projeto" é aberta.

   ![Exemplo de uma página de upgrade](images/project-upgrade-toolchain.png)

   Para obter uma visão geral do processo de upgrade, leia a descrição nessa página. A cadeia de ferramentas incluirá um novo pipeline que contém os mesmos estágios e tarefas que o pipeline do projeto. Além disso, a cadeia de ferramentas conterá um ponteiro para o Eclipse Orion {{site.data.keyword.webide}}, que é executado no {{site.data.keyword.contdelivery_short}}.

   Neste exemplo, como o projeto usa um repositório público no github.com, a cadeia de ferramentas será conectada ao mesmo repositório GitHub. Se seu projeto usar um repositório Git hospedado no JazzHub, o conteúdo desse repositório será clonado em um novo repositório no {{site.data.keyword.gitrepos}}, que faz parte do {{site.data.keyword.contdelivery_short}}. Para obter detalhes completos sobre como cada tipo de repositório é tratado, consulte a tabela a seguir.

|Repositório de projetos |Tipo de projeto	|Repositório de cadeias de ferramentas |
|:----------|:------------------------------|:------------------|
|github.com 		|Privado ou público 		|O mesmo repositório github.com com o {{site.data.keyword.Bluemix_notm}} Public.	|
|hub.jazz.net/git		|Privado ou público 		|Um novo repositório no {{site.data.keyword.gitrepos}} com o {{site.data.keyword.Bluemix_notm}} Public.	|
{: caption="Tabela 1. Repositórios de projeto mapeados para repositórios de cadeia de ferramentas" caption-side="top"}

2. Para customizar a cadeia de ferramentas, é possível configurar algumas definições:

   - Para mudar o nome da cadeia de ferramentas, edite o campo **Nome**.

      ![Campo Nome](images/name-change.png)

   - Para mudar em qual organização do {{site.data.keyword.Bluemix_notm}} criar a cadeia de ferramentas, selecione a organização no menu de sua conta:

      ![Selecionador de organização do Bluemix](images/bluemix-organization-chooser.png)

   Como as cadeias de ferramentas são gerenciadas no nível de organização, certifique-se de selecionar uma organização na qual os membros do projeto que precisam acessar as cadeias de ferramentas já existam ou possam ser incluídos.

3. Se você usou Track & Plan em seu projeto, é possível transferir os dados do Track & Plan para o GitHub Issues.

   ![Opções do Track and Plan](images/upgrade-tutorial-track-and-plan.png)

   - Indique se você deseja migrar seus dados do Track & Plan.
   - Por padrão, todos os dados do Track & Plan são migrados. Se você preferir migrar apenas os itens de trabalho que fazem parte de uma consulta específica, especifique essa consulta.
   - Selecione qualquer atributo de item de trabalho que você deseja mapear para rótulos no GitHub Issues.

4. Clique em **Criar**. A nova cadeia de ferramentas é criada e sua página Visão geral é exibida.

   ![Visão geral da cadeia de ferramentas submetida a upgrade](images/new-toolchain-page.png)

   - Para acessar seu repositório GitHub ou o rastreador de problemas associado, clique em **GitHub** ou **Problemas**.
   - Para acessar seu pipeline, clique em **Delivery Pipeline**.
   - Para acessar o {{site.data.keyword.webide}}, que contém o conteúdo de seu repositório que foi retirado para a área de trabalho, clique em **Eclipse Orion {{site.data.keyword.webide}}**.

   Se você retornar para seu projeto durante o upgrade, a mensagem do banner poderá declarar que o upgrade está em andamento, especialmente se o processo de upgrade envolve a importação de código-fonte para um novo repositório ou a importação de itens de trabalho do Track &amp; Plan como problemas.

   ![Mensagem sobre projeto sendo atualizado para uma cadeia de ferramentas](images/project-being-upgraded-banner.png)

## Revisitando seu projeto
{: #revisit_projects}

Você está pronto para usar sua nova cadeia de ferramentas. Seu projeto agora está identificado como "Submetido a upgrade" e, na página Visão geral, é exibida uma mensagem de confirmação.

![Imagem do cartão do projeto com a etiqueta Submetido a upgrade](images/card-upgraded-project.png)

![Projeto submetido a upgrade](images/banner-upgraded.png)

É possível ver quais projetos foram submetidos a upgrade selecionando **Projetos submetidos a upgrade** no menu na página Meus projetos:

![Imagem do item de menu Projetos submetidos a upgrade](images/menu-upgraded-projects.png)

Se for necessário reverter o upgrade, exclua sua cadeia de ferramentas. É possível excluir sua cadeia de ferramentas do menu **Mais ações** na página Visão geral da cadeia de ferramentas:

![imagem da ação Excluir, no menu Mais ações](images/upgrade-tutorial-delete-toolchain.png)

Quando você retornar ao seu projeto, a mensagem de upgrade será exibida novamente e um novo upgrade poderá ser feito quando você estiver pronto.

## Próximas Etapas
{: #upgrade_next_steps}

1. Confirme se o upgrade está completo atualizando seu navegador e verificando a mensagem de que seu projeto foi "atualizado para essa cadeia de ferramentas" na página Visão geral do projeto:

   ![Mensagem no banner indicando que o projeto foi atualizado](images/banner-upgraded.png)

   **Nota:** Se a mensagem disser "upgrade agora", seu upgrade falhou. Clique no link **upgrade agora** para tentar novamente.

   ![Mensagem no banner indicando que o projeto está pronto para upgrade](images/banner-ready-to-upgrade.png)

2. Dê aos membros da equipe acesso à cadeia de ferramentas.
    - Cada membro da equipe deve ter uma conta do {{site.data.keyword.Bluemix_notm}} válida. Os membros da equipe que não tiverem contas deverão [inscrever-se ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/registration){:new_window}.
    - Conceda aos membros da organização (org) acesso à cadeia de ferramentas na página Gerenciar da cadeia de ferramentas. Para obter mais informações sobre o controle de acesso de cadeias de ferramentas, consulte [Gerenciando o acesso ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){:new_window}.
    - Se um usuário não for membro da organização à qual a cadeia de ferramentas pertence, inclua-o na organização na página Gerenciar organizações.
      Para obter mais informações sobre como gerenciar organizações, consulte [Gerenciando organizações e espaços ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](/docs/admin/orgs_spaces.html#orgsspacesusers){:new_window}.

3. Use as ferramentas de sua cadeia de ferramentas no lugar das ferramentas de seu projeto {{site.data.keyword.jazzhub_short}}. Por exemplo, para editar código usando um navegador, use o Web IDE de sua cadeia de ferramentas.

4. Se você estiver usando o {{site.data.keyword.gitrepos}}, autentique usando um token de acesso pessoal ou uma chave SSH. Para obter mais informações sobre chaves SSH, consulte [Criando um token de acesso pessoal ou uma chave SSH para autenticação](/docs/services/ContinuousDelivery/git_working.html#git_authentication). Para autenticar de um cliente Git externo através de https, siga estas etapas:
    1. Acesse a [página Tokens de acesso ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git.ng.bluemix.net/profile/personal_access_tokens){:new_window} das configurações de usuário do {{site.data.keyword.gitrepos}}.
    2. Crie um token de acesso pessoal que use **api** como escopo.
    3. Acesse a [página Conta ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git.ng.bluemix.net/profile/account){:new_window} e localize seu nome de usuário para o {{site.data.keyword.gitrepos}}. Seu nome de usuário é listado na seção "Mudar nome do usuário" e mostrado como a primeira parte da URL de qualquer repositório pessoal que você criar.
    4. Para autenticar com o {{site.data.keyword.gitrepos}} de um cliente Git externo por meio de https, use seu nome de usuário e seu token de acesso pessoal.
    5. Se você desejar reutilizar o repositório local de seu repositório Git JazzHub, aponte o repositório para o novo repositório no {{site.data.keyword.gitrepos}}. Em um shell em um terminal, mude para o diretório no qual o repositório Git JazzHub é clonado. Insira o comando `git remote set-url`: `git remote set-url origin https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

        **Dica:** Para verificar quais URLs remotas estão configuradas para quais nomes remotos, use o comando `git remote -v`. O nome remoto padrão é `origin`. Se você tiver uma configuração mais avançada, o formato do comando será este: `git remote set-url <remote-name-that-uses-jazzhub-repo> https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

5. Quando sua cadeia de ferramentas estiver configurada e você tiver começado a usá-la, considere executar todas ou qualquer uma dessas etapas para assegurar que ninguém use seu projeto:
    - Inclua um sufixo no nome do projeto para indicar que ele não deve ser usado. Você poderá incluir `_DO_NOT_USE` no final do nome do projeto.
    - Atualize a descrição do projeto para mencionar que ele não é mais usado e inclua um ponteiro na cadeia de ferramentas.
    - Remova os membros do projeto.
    - Quando você não precisar mais do projeto, exclua-o.

6. Opcional: para explorar a maturidade de desenvolvimento do projeto, as práticas da equipe e a qualidade do código base, inclua o IBM Cloud {{site.data.keyword.DRA_short}} na sua cadeia de ferramentas. O {{site.data.keyword.DRA_short}} aplica a análise de desenvolvedor, equipe e implementação aos projetos do DevOps. Para obter mais informações, consulte [Introdução ao {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).


## Solucionando problemas
{: #upgrade_troubleshoot}

Se você tiver perguntas ou problemas, acesse o [fórum de suporte](https://developer.ibm.com/answers/questions/ask/?smartspace=devops-services). No post do fórum, inclua as URLs em seu projeto {{site.data.keyword.jazzhub_short}} e na cadeia de ferramentas do {{site.data.keyword.contdelivery_short}} e identifique seu post com a tag `devops-services`.
