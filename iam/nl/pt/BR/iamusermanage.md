---

copyright:

  years: 2015, 2017

lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando usuários e o acesso
{: #iamusermanage}

Dependendo das opções de acesso que você estiver autorizado a gerenciar, é possível visualizar e
gerenciar usuários na conta ou na organização. Como um proprietário da conta, será possível gerenciar usuários em qualquer uma das opções de acesso que você administrar e às quais o usuário tem acesso designado na conta atual.
{:shortdesc}

Para gerenciar usuários em sua conta, conclua as etapas a seguir:

1. Na barra de menus, clique em **Gerenciar** &gt; **Conta** &gt; **Usuários**. A janela Usuários exibe uma lista de
usuários com seus endereços de e-mail e o status atual das contas que você gerencia. 
2. Selecione o nome do usuário ou clique em **Gerenciar usuários** no menu **Ações**. 
3. Em seguida, dependendo do acesso que você pode gerenciar, atualize o acesso para o usuário nas seções Políticas de serviço ou Funções do Cloud Foundry ou clique no link para acessar a página Designar acesso à infraestrutura.

Revise as seções a seguir para obter informações adicionais sobre como gerenciar cada tipo de acesso e informações sobre o uso do Diretório da equipe.

Se for necessário revisar seu acesso designado em uma conta à qual tenha sido incluído, conclua as etapas a seguir:

1. Na barra de menus, clique em **Gerenciar** &gt; **Segurança** &gt; **Identidade e acesso** &gt; **Usuários**. 
2. Selecione seu nome. 
3. Revise suas funções designadas.

Se for necessário mudar sua função ou política de serviço, deverá entrar em contato com o gerenciador de organização ou com o proprietário da conta para atualizar a função do Cloud Foundry ou com o administrador do serviço ou instância de serviço para atualizar a política de serviço.

## Acesso ao Cloud Foundry
{: #iammancfser}

Para gerenciar o acesso a organizações e espaços da conta, deve-se ser o proprietário da conta, o gerenciador de organização ou o gerenciador de espaço:

1. Na barra de menus, clique em **Gerenciar** &gt; **Segurança** &gt; **Identidade e acesso** &gt; **Usuários**. 
2. Selecione o nome de usuário para o qual você deseja editar funções.
3. No menu **Ações** na seção Cloud Foundry, é possível:

  * Remover o usuário da organização
  * Editar a função de organização
  * Editar a função de espaço

Também será possível incluir um usuário em outra organização clicando em **Designar organização**, se você for o gerenciador de uma organização da qual o usuário ainda não for membro. 


## Serviços ativados para identidade e acesso
{: #iammanidaccser}

Para gerenciar políticas de serviço ou designar novas políticas de serviço aos usuários, deve-se ser o administrador de acesso da conta ou o administrador designado para o serviço ou para a instância de serviço específicos.

1. Na barra de menus, clique em **Gerenciar** &gt; **Segurança** &gt; **Identidade e acesso** &gt; **Usuários**. 
2. Selecione o nome de usuário para o qual você deseja designar políticas de serviço.
3. Selecione **Designar políticas de serviço** para criar uma nova política de serviço ou no menu **Ações**, na seção Políticas de serviço, será possível:
  
  * Editar a política
  * Remover a política

Para obter mais informações sobre políticas de serviço e funções, veja [Políticas e funções de gerenciamento de identidade e acesso](/docs/iam/users_roles.html#iamusermanpol).

## Serviços de Infraestrutura

Se você tiver acesso para designar permissões de infraestrutura, será possível configurar as funções a seguir para o usuário: Visualizar apenas, Usuário básico ou Superusuário. Clique no link **Designar acesso à infraestrutura** para atualizar ou designar novas permissões.

Para obter mais informações sobre as permissões, veja [Permissões de infraestrutura](/docs/iam/users_roles.html#infrapermissions).

## Gerenciando funções do Cloud Foundry no diretório da equipe
{: #editinguserroles}

Na página Diretório da equipe, os proprietários de contas podem gerenciar usuários somente da plataforma. No entanto, se você puder acessar a página **Gerenciar** &gt; **Conta** &gt; **Usuários**, será possível gerenciar todos os usuários de serviços de plataforma e de infraestrutura em um lugar.

Os gerenciadores de organização podem editar funções de organização e de espaço para usuários existentes na página Diretório da equipe.

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
