---

copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Convidando usuários e designando e gerenciando o acesso
{: #iamuserinv}

É possível convidar usuários em serviços do {{site.data.keyword.Bluemix_notm}},
aplicativos e infraestrutura do {{site.data.keyword.Bluemix_notm}} em um único local. Você
designa o acesso aos usuários conforme eles são convidados, atribuindo funções, políticas e as contas ou
as organizações, ou ambos, que eles possam acessar. Dependendo das opções de acesso que você estiver autorizado
a gerenciar, é possível convidar e fornecer acesso para usuários na conta ou na organização. Como
um proprietário da conta, é possível designar opções de acesso à sua conta para um usuário quando você e o
usuário são membros, independentemente da função.{:shortdesc}

Para convidar usuários ou gerenciar convites de usuários em sua conta, na barra de menus, clique em
**Gerenciar** &gt; **Conta** &gt; **Usuários**. A
janela Usuários exibe uma lista de usuários com seus endereços de e-mail e o status atual nas contas que você
gerencia. 

Para convidar usuários e gerenciar convites pendentes, deve-se ser um proprietário da conta, um
gerenciador de organização ou ter permissões de infraestrutura para incluir usuários. É possível convidar
usuários, cancelar convites e reenviar um convite pendente para um usuário convidado. É possível convidar um
único usuário ou, se fornece o mesmo acesso para todos os membros em um grupo de usuários,
é possível convidar múltiplos usuários de uma vez.

Para convidar usuários, clique em **Convidar usuários**, especifique o endereço de
e-mail ou IBMid do usuário e, em seguida, inclua-os em uma ou mais das opções de acesso que você gerencia. Deve-se
designar pelo menos uma opção de acesso e definir as configurações para o usuário em cada opção de acesso que
você designar. Para quaisquer opções de acesso adicionais que você não incluir nem configurar, o valor padrão de
*no access* é designado. É possível ver uma ou todas as seguintes opções de acesso, dependendo
das opções que você estiver autorizado a gerenciar:

**Serviços ativados para identidade e acesso** Selecione para
designar os serviços, regiões, instâncias de serviço e funções para os usuários que você convidar.
**Nota**: se selecionar a opção **Conceder acesso automaticamente quando novos
serviços forem incluídos**, você não será notificado para cancelar a seleção de cada novo
serviço do {{site.data.keyword.Bluemix_notm}} para esse usuário quando os serviços forem
incluídos posteriormente.

**Acesso do Cloud Foundry** Selecione para designar os serviços, regiões,
espaços e funções de espaço para os usuários que você convidar. Consulte
[Funções de usuário](/docs/admin/users_roles.html#userrolesinfo) para obter informações mais
específicas sobre essas configurações. É possível incluir múltiplas funções, uma por vez.

**Acesso de infraestrutura** Designe a permissão de infraestrutura a seguir
para o usuário: 
<dl>
<dt>Visualização Apenas</dt>
<dd>Os usuários com essa permissão podem visualizar somente os itens dentro do sistema.</dd>
<dt>Usuário Básico</dt>
<dd>Os usuários com essa permissão podem executar ações básicas dentro do sistema, como incluir um chamado e
gerenciar dispositivos.</dd>
<dt>Super usuário</dt>
<dd>Os usuários com essa permissão podem executar todas as ações disponíveis no sistema.</dd>
</dl>
**Nota**: as permissões reais designadas serão limitadas automaticamente ao
subconjunto de permissões que você possuir.Se estiver fornecendo o mesmo acesso para múltiplos
usuários, será possível selecionar **Convidar múltiplos usuários** para inserir uma lista de
usuários para convidar. Separe as entradas ID do usuário com vírgulas.  

Se determinar que um usuário não precisa de acesso, também será possível cancelar um convite para
quaisquer usuários que possuírem um estado **Processando** ou
**Pendente** na coluna **Status**. Se um usuário convidado não recebeu
convite, também será possível enviar novamente o convite para qualquer usuário que estiver em um estado
**Pendente**.  Essas opções estão disponíveis para usuários no estado apropriado do
menu **Ações** na janela Usuários.

Para obter informações específicas sobre como configurar o acesso para usuários, incluindo funções e
políticas, consulte [Gerenciando contas e acesso do usuário](/docs/admin/iamusermanage.html).
