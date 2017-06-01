---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Convidando usuários
{: #iamuserinv}

É possível convidar usuários em serviços do {{site.data.keyword.Bluemix_notm}},
aplicativos e infraestrutura do {{site.data.keyword.Bluemix_notm}} em um único local. Para convidar usuários e gerenciar convites pendentes, deve-se ser um proprietário da conta, um
gerenciador de organização ou ter permissões de infraestrutura para incluir usuários. É possível convidar
usuários, cancelar convites e reenviar um convite pendente para um usuário convidado. É possível convidar um
único usuário ou, se fornece o mesmo acesso para todos os membros em um grupo de usuários,
é possível convidar múltiplos usuários de uma vez.
{:shortdesc}

Para convidar usuários ou gerenciar convites de usuários em sua conta, conclua as etapas a seguir:

1. Na barra de menus, clique em **Gerenciar** &gt; **Segurança** &gt; **Identidade e acesso** &gt; **Usuários**. A
janela Usuários exibe uma lista de usuários com seus endereços de e-mail e o status atual nas contas que você
gerencia. 
2. Clique em **Convidar usuários**. 
3. Especifique o endereço de e-mail ou o IBMid do usuário. Se estiver fornecendo o mesmo acesso para múltiplos
usuários, será possível selecionar **Convidar múltiplos usuários** para inserir uma lista de
usuários para convidar. Separe as entradas ID do usuário com vírgulas. 
4. Inclua uma ou mais das opções de acesso que você gerencia. Deve-se
designar pelo menos uma opção de acesso e definir as configurações para o usuário em cada opção de acesso que
você designar. Para quaisquer opções de acesso adicionais que você não incluir nem configurar, o valor padrão de
*no access* é designado. Será possível ver uma ou todas as opções de acesso a seguir, dependendo das opções que você estiver autorizado a gerenciar: **Serviços ativados para identidade e acesso**, **Acesso ao Cloud Foundry**, **Acesso à infraestrutura**. Veja [Designando acesso de usuário](/docs/iam/assignaccess.html) para obter mais informações.

Se você determinar que um usuário não precisa de acesso, será possível cancelar um convite de quaisquer usuários que forem mostrados em um estado **Processando** ou **Pendente** na coluna **Status**. Se um usuário convidado não tiver recebido um convite, será possível reenviar o convite para qualquer usuário em um estado **Pendente**.
