---

copyright:

  years: 2015, 2016
lastupdated: "2017-03-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando usuários e funções de acesso a serviços do Cloud Foundry no Diretório da equipe
{: #userroles}

É possível gerenciar o acesso a serviços do Cloud Foundry designado aos usuários da plataforma
na página Diretório da equipe para sua conta. É possível gerenciar membros da equipe existentes e suas funções
em sua organização e espaços.{:shortdesc}

É possível acessar o Diretório da equipe para sua conta de um link na parte superior da nova página
Usuários. Para acessar a página Usuários, no menu do {{site.data.keyword.Bluemix_notm}}, clique
em **Gerenciar** &gt; **Conta** &gt; **Usuários**.

Os proprietários da conta executam todas as operações nas organizações e espaços, incluindo o
gerenciamento de membros da equipe e de suas funções designadas. Os gerenciadores de organização têm acesso
para gerenciar funções. Gerenciadores de
espaço podem usar a página **Gerenciar organizações** para incluir membros da conta existente no espaço e ajustar as suas
funções. Verifique as informações a seguir, para saber mais sobre funções.

## Funções de usuário
{: #userrolesinfo}

No nível de conta, há duas funções que permitem o acesso a diferentes recursos de gerenciamento de conta:

| Função da conta | Permissões |
|----------------|---------|
|Proprietário | Um proprietário para a conta tem acesso ao seu perfil, diretório da equipe, às suas informações de faturamento, notificações de gastos e ao seu painel de uso. A partir da página de diretório da
equipe, o proprietário pode convidar novos membros da equipe e ajustar funções. O proprietário também pode incluir créditos promocionais, configurar ou mudar o limite de faturamento, configurar o acesso de
serviço e gerenciar organizações e espaços. |
|Membro | Um membro tem acesso ao seu perfil, diretório da equipe, ao seus créditos da conta e limites de faturamento no cabeçalho do {{site.data.keyword.Bluemix_notm}}. No entanto, na página de
diretório da equipe, um membro pode apenas visualizar os membros da equipe dentro da conta. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

Todos os novos membros da equipe são incluídos como um membro da conta. É possível designar funções de organização e espaço para convidados, a fim de ativar visualizações e permissões específicas no
{{site.data.keyword.Bluemix_notm}}. Novos membros da equipe incluídos em uma organização, exceto em um ambiente local ou dedicado, são designados à função de organização de auditor por padrão. Para um espaço específico, é possível optar por
designar a função de desenvolvedor ou auditor para convidados. Quando os seus convidados aceitam o
convite e se associam ao {{site.data.keyword.Bluemix_notm}}, é possível editar suas funções na página
Diretório da equipe.

As funções a seguir podem ser designadas no nível de organização:

| Função organizacional | Permissões |
|-------------------|-------------|
|Gerente | Gerenciadores de organização podem criar, visualizar, editar ou excluir espaços dentro da organização, visualizar o uso e a cota da organização, convidar membros da equipe para a organização,
gerenciar quem tem acesso à organização e às suas funções na organização e gerenciar domínios customizados para a organização. |
|Gerenciador de faturamento | Gerenciadores de faturamento podem visualizar informações de uso de tempo de execução e serviço para a organização na página de Painel de uso.  |
|Auditor | Auditores da organização podem visualizar o conteúdo do aplicativo e do serviço na organização. Auditores também podem visualizar os membros da equipe na organização e as suas funções designadas e a
cota para a organização. Essa função é designada a todos os convidados, exceto em ambientes locais ou dedicados, por padrão. |
{:caption="Table 2. Organization roles and permissions" caption-side="top"}

As funções a seguir podem ser designadas no nível de espaço:

| Função de espaço | Permissões |
|------------|-------------|
|Gerente | Gerenciadores de espaço podem incluir membros da equipe existentes e gerenciar funções dentro do espaço. O gerenciador de espaço também pode visualizar o número de instâncias, ligações de serviço e
o uso recurso para cada aplicativo no espaço. |
|Desenvolvedor | Desenvolvedores de espaço podem criar, excluir e gerenciar aplicativos e serviços dentro do espaço. Algumas das tarefas de gerenciamento incluem implementar aplicativos, iniciar ou parar
aplicativos, renomear um aplicativo, excluir um aplicativo, renomear um espaço, ligar ou desvincular um serviço para um aplicativo, visualizar o número ou as instâncias, ligações de serviço e uso de recurso
para cada aplicativo no espaço. Além disso, o desenvolvedor de espaço pode associar uma URL interna ou externa com um aplicativo no espaço.   |
|Auditor | Auditores de espaço têm acesso somente leitura a todas as informações sobre o espaço, como informações sobre o número de instâncias, ligações de serviço e uso de recurso para cada aplicativo no
espaço. |
{:caption="Table 3. Space roles and permissions" caption-side="top"}

**Nota**: membros da equipe que são designados com a função de espaço de gerenciador ou desenvolvedor podem acessar a variável de ambiente VCAP_SERVICES. No entanto, um membro da
equipe designado com a função de auditor não pode acessar VCAP_SERVICES.

## Editando Funções
{: #editinguserroles}

Os proprietários da conta e os gerenciadores de organização podem editar funções de organização e de espaço
para membros da equipe existentes na página Diretório da equipe.

1. Localize e selecione o membro da equipe cujas funções deseja editar. 
2. Clique em **Visualizar funções**.
3. Selecione ou limpe as seleções de função de espaço, para modificar o acesso ao espaço para o membro da equipe.
4. Clique **Salvar.**

Os gerenciadores de espaço podem editar funções para os membros da equipe em seu espaço.

1. Localize e selecione o membro da equipe cujas funções deseja editar. 
2. Clique em **Visualizar funções**.
3. Clique em **Visualizar espaços**.
4. Selecione ou limpe a opção de função de espaço para a função que você deseja incluir ou remover para o membro da equipe.
5. Então clique em **Salvar**.

## Convidando membros da equipe
{: #inviteteammembers}

Será possível incluir um usuário usando a janela Diretório da equipe se o ID do usuário não for uma conta
vinculada e se você for um proprietário da conta ou um gerenciador de organização. Quando você inclui novos membros da equipe, exceto em um ambiente local ou dedicado, eles são designados às funções de auditor automaticamente. É possível mudar as funções posteriormente, na página Diretório da equipe. Para convidar um membro da equipe, conclua estas etapas:

<ol>
<li>Clique em **Convidar um usuário**.</li>
<li>Insira o endereço de e-mail do usuário que deseja convidar.</li>
<li>Selecione a função a ser designada para a organização.</li>
<li>Selecione a função a ser designada para um ou mais espaços selecionados na organização.</li>
<li>Selecione a opção para confirmar que você assume a responsabilidade financeira por todos os encargos incorridos na conta.</li>
<li>Clique em **Convidar**.</li>
</ol>

O usuário é incluído na lista de membros da equipe exibida para a conta.

## Removendo membros da equipe
{: #removingteammembers}

Se o usuário foi incluído no Diretório da equipe e não for uma conta vinculada, os proprietários
da conta e os gerenciadores de organização poderão remover membros da equipe de uma conta na página Diretório da equipe. Para remover um membro da equipe, conclua as etapas a seguir:

1. Localize o usuário que deseja remover e clique no ícone **Remover usuário**
![ícone Remover](../icons/icon_remove_teamuser.svg).
2. Clique em **Remover** para
confirmar que você deseja remover o usuário especificado da conta.

O usuário é removido da lista de membros da equipe exibida para a conta.
