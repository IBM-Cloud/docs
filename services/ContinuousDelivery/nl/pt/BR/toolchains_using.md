---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Usando cadeias de ferramentas no {{site.data.keyword.Bluemix_notm}} Public
{: #toolchains-using}

Última atualização: 9 de novembro de 2016
{: .last-updated}

É possível usar uma cadeia de ferramentas para ser produtivo em seu trabalho diário de desenvolvimento, implementação e operações. Após
configurar uma cadeia de ferramentas, é possível incluir, excluir ou configurar integrações de ferramenta e gerenciar acesso à cadeia de ferramentas. As cadeias de ferramentas estão disponíveis na região sul dos EUA somente.
{: shortdesc}

## Configurando uma integração de ferramenta
{: #configuring_a_tool_integration}

Se você adiou a configuração de uma integração de ferramenta quando criou uma cadeia de ferramentas, um botão **Configurar** será
mostrado em seu ladrilho. Se você configurou uma integração de ferramenta quando criou uma cadeia de ferramentas, será possível atualizar as definições de configuração.

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no quadrado Entrega contínua, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Visão geral**.
1. Se precisar configurar uma integração de ferramenta pela primeira vez, em seu ladrilho, clique em **Configurar**.

  ![Botão de configuração
](images/toolchain_tile_configure.png)

 Quando tiver finalizado a configuração da integração de ferramenta, clique em **Salvar integração**.
 
1. Se precisar atualizar uma configuração de integração de ferramenta, em seu ladrilho, clique no menu para acessar as opções de configuração.

  ![Menu Configuração](images/toolchain_tile_menu.png)
 
 Quando tiver finalizado a atualização das configurações, clique em **Salvar integração**.

## Incluindo uma integração de ferramenta
{: #adding_a_tool_integration}

É possível incluir e configurar integrações de ferramenta para sua cadeia de ferramentas.

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no quadrado Entrega contínua, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Visão geral**.
1. Para ver uma lista de integrações de ferramenta a serem incluídas, clique em **Incluir uma ferramenta**.
1. Clique em uma integração de ferramenta que deseja incluir.
1. Insira quaisquer informações necessárias para configurar a integração de ferramenta. 
1. Clique em **Criar integração** para incluir a integração de ferramenta em sua cadeia de ferramentas.

## Excluindo uma integração de ferramenta
{: #deleting_a_tool_integration}

Se você excluir uma integração de ferramenta a partir de sua cadeia de ferramentas, a exclusão não poderá ser desfeita. 

1. No painel do DevOps, na página **Cadeias de ferramentas**, clique em uma cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no quadrado Entrega contínua, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Visão geral**.
1. No ladrilho para a integração de ferramenta que deseja excluir, clique no menu para acessar as opções de configuração.
1. Para excluir a integração de ferramenta de sua cadeia de ferramentas, clique em **Excluir**.
1. Confirme clicando em **Excluir**.  

## Gerenciando acesso
{: #managing_access}

É possível conceder aos usuários o acesso a uma cadeia de ferramentas, incluindo-os na organização (org) à qual a cadeia de ferramentas está
associada. Cada cadeia de ferramentas é associada a uma organização específica e qualquer usuário que for um membro dessa organização poderá
acessar as cadeias de ferramentas associadas. A organização na qual você está trabalhando atualmente está exibida na barra de menus. Clique na organização e, em seguida, alterne para uma organização diferente para acessar um conjunto diferente de cadeias de ferramentas.

1. No painel DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para gerenciar e, em seguida, clique em **Gerenciar**. Como alternativa, na página Visão geral do app, no ladrilho Entrega contínua, clique em
**Visualizar cadeia de ferramentas** e, em seguida, clique em **Gerenciar**.  
1. Clique no link para sua organização. 
1. Na página Gerenciar organizações, clique em **Convidar um usuário** e digite o endereço de e-mail do usuário.
1. Se você deseja conceder permissões para gerenciar usuários em organizações do {{site.data.keyword.Bluemix_notm}}, selecione uma ou mais das
caixas de seleção **Gerenciador**, **Gerenciador
de faturamento** ou **Auditor**.
1. Clique em **CONVIDAR**.
1. Clique em **SALVAR**.

## Excluindo uma cadeia de ferramentas
{: #deleting_a_toolchain}

É possível excluir uma cadeia de ferramentas e especificar qual das integrações de ferramenta associadas deseja excluir. Quando você excluir uma cadeia de ferramentas, a exclusão não poderá ser desfeita.

1. No painel DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para excluir e, em seguida, clique em **Gerenciar**. Como alternativa, na página Visão geral do app, no ladrilho Entrega contínua, clique em
**Visualizar cadeia de ferramentas** e, em seguida, clique em **Gerenciar**.
1. Clique em **Excluir cadeia de ferramentas** e revise ou ajuste as integrações de ferramentas que você estiver excluindo.
1. Confirme a exclusão digitando o nome da cadeia de ferramentas e clicando em **Excluir**.  

 **Dica**: ao excluir uma integração de
ferramenta GitHub, o repo GitHub associado não é excluído do
GitHub. Deve-se
remover manualmente o repo do GitHub.


# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}

* [Crie e use sua primeira cadeia de ferramentas (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Crie uma cadeia de ferramentas customizada (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Crie um aplicativo com três microsserviços (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Crie uma cadeia de ferramentas a partir de um modelo em {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Crie uma cadeia de ferramentas a partir de um app em {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Links relacionados
{: #general}

* [Cadeia de ferramentas de microsserviços (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadeia de ferramentas simples (o link é aberto em uma nova janela)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (O link é aberto em uma nova janela)](https://www.ibm.com/devops/method){:new_window}
