---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Usando uma cadeia de ferramentas
{: #toolchains-using}

As cadeias de ferramentas abertas estão disponíveis nos ambientes Public e Dedicated no {{site.data.keyword.Bluemix}}. É possível usar uma cadeia de ferramentas para ser produtivo em seu trabalho diário de desenvolvimento, implementação e operações. Após
configurar uma cadeia de ferramentas, é possível incluir, excluir ou configurar integrações de ferramenta e gerenciar acesso à cadeia de ferramentas. No {{site.data.keyword.Bluemix_notm}} Public, cadeias de ferramentas estão disponíveis somente na região sul dos EUA.
{: shortdesc}

## Configurando uma integração de ferramenta
{: #configuring_a_tool_integration}

Se você tiver adiado a configuração de uma integração de ferramenta quando criou uma cadeia de ferramentas, um botão **Configurar** será mostrado em seu cartão. Se você configurou uma integração de ferramenta quando criou uma cadeia de ferramentas, será possível atualizar as definições de configuração.

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Visão geral**.
1. Se precisar configurar uma integração de ferramenta pela primeira vez, em seu cartão, clique em **Configurar**.

  ![Botão de configuração
](images/toolchain_tile_configure.png)

 Quando tiver finalizado a configuração da integração de ferramenta, clique em **Salvar integração**.

1. Se precisar atualizar a configuração de uma integração de ferramenta, em seu cartão, clique no menu para acessar as opções de configuração.

  ![Menu Configuração](images/toolchain_tile_menu.png)

 **Dica**: algumas das integrações de ferramenta são pré-configuradas e não requerem parâmetros de configuração. É possível atualizar as definições de configuração para apenas as integrações de ferramenta configuradas.

 Quando tiver finalizado a atualização das configurações, clique em **Salvar integração**.

## Incluindo uma integração de ferramenta
{: #adding_a_tool_integration}

É possível incluir e configurar integrações de ferramenta para sua cadeia de ferramentas. As integrações de ferramentas disponíveis são diferentes, dependendo de se você usa o {{site.data.keyword.Bluemix_notm}} Public ou o {{site.data.keyword.Bluemix_notm}} Dedicated.

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Visão geral**.
1. Para ver uma lista de integrações de ferramenta a serem incluídas, clique em **Incluir uma ferramenta**.
1. Clique em uma integração de ferramenta que deseja incluir.
1. Insira quaisquer informações necessárias para configurar a integração de ferramenta.
1. Clique em **Criar integração** para incluir a integração de ferramenta em sua cadeia de ferramentas.

## Excluindo uma integração de ferramenta
{: #deleting_a_tool_integration}

Se você excluir uma integração de ferramenta a partir de sua cadeia de ferramentas, a exclusão não poderá ser desfeita.

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Visão geral**.
1. No cartão da integração de ferramenta que desejar excluir, clique no menu para acessar as opções de configuração.
1. Para excluir a integração de ferramenta de sua cadeia de ferramentas, clique em **Excluir**.
1. Confirme clicando em **Excluir**.  

## Gerenciando acesso
{: #managing_access}

É possível conceder aos usuários acesso a uma cadeia de ferramentas, incluindo-os na organização (org) à qual a cadeia de ferramentas está associada e à lista de controle de acesso da cadeia de ferramentas. Cada cadeia de ferramentas é associada a uma organização específica e qualquer usuário que seja membro dessa organização poderá ser incluído na lista de controle de acesso de qualquer uma das cadeias de ferramentas associadas. A organização na qual você está trabalhando atualmente é exibida na barra de menus. Para acessar um conjunto diferente de cadeias de ferramentas, alterne para uma organização diferente.

Se você estiver usando o {{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}}, ao incluir usuários em sua organização e espaços do {{site.data.keyword.Bluemix_notm}}, os usuários poderão efetuar login no {{site.data.keyword.ghe_short}} usando seus IDs e senhas do {{site.data.keyword.Bluemix_notm}}. Quando os usuários efetuarem login, as contas serão criadas para eles. Quando você incluir usuários em sua organização e espaços do {{site.data.keyword.Bluemix_notm}}, eles não serão incluídos automaticamente no repositório {{site.data.keyword.ghe_short}}. Alguém com privilégio do administrador para o repositório deverá inclui-los. Para obter mais informações, consulte [Usando o Dedicated GitHub Enterprise](/docs/services/ghededicated/index.html){: new_window}. Se você estiver usando sua própria versão gerenciada do {{site.data.keyword.ghe_short}}, siga seus procedimentos internos.

###Dicas para gerenciar o acesso a uma cadeia de ferramentas

* Para gerenciar o acesso à cadeia de ferramentas, no painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas a ser gerenciada e, em seguida, clique em **Gerenciar**. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Gerenciar**.

* Para conceder acesso a todos os membros da organização da cadeia de ferramentas, clique em **Incluir organização**. Todos os membros dessa organização poderão visualizar a cadeia de ferramentas.

* É possível conceder privilégios de administrador para uma organização ou um usuário. Os administradores podem modificar e excluir a cadeia de ferramentas. Para conceder privilégios de administrador, marque a caixa de seleção **ADMINISTRADOR** da organização ou do usuário.

* Se você marcar a caixa de seleção **ADMINISTRADOR** de uma organização, todos os membros dessa organização se tornarão administradores. Se você incluir membros na organização depois de conceder privilégios de administrador para a organização, esses membros receberão o mesmo acesso que o resto da organização.

* Para conceder acesso a um usuário que é um membro da organização da cadeia de ferramentas, insira o ID do usuário e clique em **Incluir usuário**. O usuário pode visualizar a cadeia de ferramentas.

* Para conceder acesso a um usuário que não é um membro da organização da cadeia de ferramentas, siga estas etapas:

   a. Na barra de menus, clique em **Gerenciar > Conta > Organizações**.

   b. Clique em **Convidar membros da equipe**.
   
   c. Selecione a organização para a qual você deseja convidar o usuário e clique em **Avançar**.
   
   d. Selecione os espaços os quais você deseja permitir que o usuário acesse.
   
   e. Selecione a função a ser designada aos espaços selecionados na organização. 
   
     **Nota**: por padrão, os gerenciadores da organização têm privilégios completos de administrador a todas as cadeias de ferramentas que estão associadas à organização. Para conceder privilégios completos de administrador ao usuário, selecione a função **Gerenciador**. As funções Gerente de faturamento e Auditor não afetam o acesso da cadeia de ferramentas. É possível mudar as funções posteriormente, na página Diretório da Equipe. Para obter mais informações, veja [Gerenciando membros da equipe e funções](/docs/admin/users_roles.html){: new_window}.
   
   f. Selecione a opção para confirmar que você assume a responsabilidade financeira por todos os encargos incorridos na conta.
   
   g. Insira o endereço de e-mail do usuário que você deseja convidar e clique em **Enviar**.

   h. Depois que o usuário for um membro da organização, retorne à página Gerenciar da cadeia de ferramentas e inclua o usuário na cadeia de ferramentas.  


## Excluindo uma cadeia de ferramentas
{: #deleting_a_toolchain}

É possível excluir uma cadeia de ferramentas e especificar qual das integrações de ferramenta associadas deseja excluir. Quando você excluir uma cadeia de ferramentas, a exclusão não poderá ser desfeita.

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas a ser excluída. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas**. 
1. Clique no menu **Mais ações**, que está próximo a **Visualizar app**.
1. Clique em **Excluir** e revise ou ajuste as integrações de ferramentas que você estiver excluindo.
1. Confirme a exclusão digitando o nome da cadeia de ferramentas e clicando em **Excluir**.  

 **Dica**: ao excluir uma integração de ferramenta GitHub, {{site.data.keyword.ghe_short}} ou Git Repos and Issue Tracking, o repositório associado não será excluído do GitHub, do {{site.data.keyword.ghe_short}} ou do Git Repos and Issue Tracking. Deve-se remover manualmente o repositório.
