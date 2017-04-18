---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Usando cadeias de ferramentas no {{site.data.keyword.Bluemix_notm}} Dedicated
{: #toolchains-using_dedicated}

Última atualização: 13 de setembro de 2016
{: .last-updated}

É possível usar uma cadeia de ferramentas para ser produtivo em seu trabalho diário de desenvolvimento, implementação e operações. Após
configurar uma cadeia de ferramentas, é possível incluir, excluir ou configurar integrações de ferramenta e gerenciar acesso à cadeia de ferramentas.
{: shortdesc}

## Configurando uma integração de ferramenta
{: #configuring_a_tool_integration_dedicated}

Se você adiou a configuração de uma integração de ferramenta quando criou uma cadeia de ferramentas, um botão **Configurar** será mostrado em seu ladrilho. Se você configurou uma
integração de ferramenta quando criou uma cadeia de ferramentas, será possível atualizar as definições de configuração.

1. No Painel, na guia **DEVOPS**, clique na cadeia de ferramentas para abrir a sua página Integrações de ferramentas. Como alternativa, no canto superior direito da página Visão
geral do aplicativo, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**.
1. Se precisar configurar uma integração de ferramenta pela primeira vez, em seu ladrilho, clique em **Configurar**.

  ![Botão de configuração
](images/toolchain_tile_configure.png)

 Quando tiver finalizado a configuração da integração de ferramenta, clique em **Salvar integração**.
 
1. Se precisar atualizar uma configuração de integração de ferramenta, em seu ladrilho, clique no menu para acessar as opções de configuração.

  ![Menu Configuração](images/toolchain_tile_menu.png)
 
 Quando tiver finalizado a atualização das configurações, clique em **Salvar integração**.

## Incluindo uma integração de ferramenta
{: #adding_a_tool_integration_dedicated}

É possível incluir e configurar integrações de ferramenta para sua cadeia de ferramentas.

1. No Painel, na guia **DEVOPS**, clique na cadeia de ferramentas para abrir a sua página Integrações de ferramentas. Como alternativa, no canto superior direito da página Visão
geral do aplicativo, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**.
1. Para ver uma lista de integrações de ferramenta para incluir, clique no botão de inclusão (+).
1. Clique na integração de ferramenta a ser incluída.
1. Insira quaisquer informações necessárias para configurar a integração de ferramenta. 
1. Clique em **Criar integração** para incluir a integração de ferramenta em sua cadeia de ferramentas.

## Excluindo uma integração de ferramenta
{: #deleting_a_tool_integration}

Se você excluir uma integração de ferramenta a partir de sua cadeia de ferramentas, a exclusão não poderá ser desfeita. 

1. No Painel, na guia **DEVOPS**, clique na cadeia de ferramentas para abrir a sua página Integrações de ferramentas. Como alternativa, no canto superior direito da página Visão
geral do aplicativo, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique
em **Integrações de ferramenta**.
1. No ladrilho para a integração de ferramenta a ser excluída, clique no menu para acessar as opções de configuração.
1. Para excluir a integração de ferramenta de sua cadeia de ferramentas, clique em **Excluir**.
1. Confirme clicando em **Excluir**. 

## Gerenciando acesso
{: #managing_access_dedicated}

É possível conceder aos usuários o acesso a uma cadeia de ferramentas, incluindo-os na organização (org) à qual a cadeia de ferramentas está
associada. Cada cadeia de ferramentas é associada a uma organização específica e qualquer usuário que for um membro dessa organização poderá
acessar as cadeias de ferramentas associadas. Para visualizar a organização na qual você está trabalhando atualmente, clique no ícone
**{{site.data.keyword.avatar}}**
![Avatar icon](../icons/i-avatar-icon.svg) na barra de menus. Para acessar um conjunto diferente de cadeias de ferramentas, alterne para uma organização diferente.

Quando você incluir usuários em sua organização e nos espaços do {{site.data.keyword.Bluemix}}, os usuários poderão efetuar login no GitHub Enterprise usando o seu ID e senha do
{{site.data.keyword.Bluemix_notm}}. Quando os usuários efetuarem login, as contas serão criadas para eles. Quando você incluir usuários em sua organização e nos espaços do
{{site.data.keyword.Bluemix_notm}}, eles não serão incluídos automaticamente no repositório GitHub Enterprise. Alguém com privilégio do administrador para o repositório deverá inclui-los. Para
obter mais informações, consulte [Usando o Dedicated GitHub Enterprise (O link é aberto em uma nova janela)](../services/ghededicated/index.html){: new_window}.

Para incluir um usuário, siga estas etapas: 

1. No Painel, na guia **DEVOPS**, clique na cadeia de ferramentas para abrir a sua página Integrações de ferramentas. Em seguida, clique
em **Gerenciar**. Como alternativa, no canto superior direito da página Visão geral do aplicativo, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em
**Gerenciar**.  
1. Clique no link para a sua organização. 
1. Na página Gerenciar organizações, clique em **Convidar um usuário** e digite o endereço de e-mail do usuário.
1. Se você deseja conceder permissões para gerenciar usuários em organizações do {{site.data.keyword.Bluemix_notm}}, selecione uma ou mais das caixas de seleção
**Gerenciador**, **Gerenciador de faturamento** ou **Auditor**.
1. Clique em **CONVIDAR**.
1. Clique em **SALVAR**.

## Excluindo uma cadeia de ferramentas
{: #deleting_a_toolchain_dedicated}

É possível excluir uma cadeia de ferramentas e especificar qual de suas integrações de ferramenta associadas você deseja excluir. Quando você excluir uma cadeia de ferramentas, a exclusão não poderá ser
desfeita.

1. No Painel, na guia **DEVOPS**, clique na cadeia de ferramentas para abrir a sua página Integrações de ferramentas. Em seguida, clique em **Gerenciar**. Como
alternativa, no canto superior direito da página Visão geral do aplicativo, clique em **Visualizar cadeia de ferramentas**. Em seguida, clique em **Gerenciar**.
1. Clique em **Excluir cadeia de ferramentas** e revise ou ajuste as integrações de ferramentas que você estiver excluindo.
1. Confirme a exclusão digitando o nome da cadeia de ferramentas e clicando em **Excluir**.

 **Dica**: quando você excluir uma integração de ferramenta do GitHub Enterprise, o repositório GitHub Enterprise associado não será excluído do GitHub Enterprise. Deve-se
remover manualmente o repositório a partir do GitHub Enterprise.
