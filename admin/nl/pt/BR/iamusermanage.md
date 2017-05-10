---

copyright:

  years: 2015, 2017

lastupdated: "2017-04-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando a conta e o acesso do usuário
{: #iamusermanage}

Dependendo das opções de acesso que você estiver autorizado a gerenciar, é possível visualizar e
gerenciar usuários na conta ou na organização. Como um proprietário da conta, é possível gerenciar usuários em
qualquer uma das opções de acesso que você administrar e às quais o usuário tiver acesso designado,
independentemente da função, na conta atual. É possível designar, editar e remover o acesso para usuários em
qualquer das opções de acesso que você gerenciar. 
{:shortdesc}

Para gerenciar usuários em sua conta, na barra de menus, clique em **Gerenciar** &gt;
**Conta** &gt; **Usuários**. A janela Usuários exibe uma lista de
usuários com seus endereços de e-mail e o status atual das contas que você gerencia. Na janela Usuários,
selecione o usuário que deseja gerenciar ou clique em **Gerenciar usuário** no
menu **Ações**. Serão exibidas tabelas de política para as opções de acesso que podem
ser gerenciadas para esse usuário.

## Gerenciando serviços ativados para identidade e acesso
{: #iammanidaccser}

Se o usuário tiver acesso designado a um **Serviço ativado para identidade e acesso**,
será possível ver informações sobre as políticas designadas na janela Gerenciar usuário.  O que é exibido para esse usuário ou grupo depende das políticas que tiverem sido designadas. Se nenhuma
política estiver designada, será exibida uma mensagem perguntando se deseja designar uma política. Se
políticas já estiverem designadas, então, uma lista das políticas será mostrada com a função do usuário ou
do grupo e com uma descrição dos atributos de recurso para cada política. É possível designar políticas na
página Designar políticas clicando em **Designar políticas de serviço**. A opção
**Designar políticas de serviço** será ativada você estiver autorizado a criar
políticas. É possível gerenciar políticas existentes clicando na política na lista ou clicando em
**Editar política** em **Ações** na linha da política que deseja
editar.

## Gerenciando acesso a serviços do Cloud Foundry
{: #iammancfser}

Se o usuário tiver acesso designado ao **Cloud Foundry**, será possível ver as
organizações e os espaços aos quais o usuário estiver designado na janela Gerenciar usuário. É possível remover o usuário de
uma organização ou mudar a função que é designada para uma organização ou espaço. Será possível incluir um
usuário em outra organização clicando em **Designar organização** se você for o gerente de
uma organização da qual o usuário ainda não é membro. É possível gerenciar funções de espaço e
de organização existentes clicando em **Editar função de espaço** ou **Editar
função de organização** na linha da função que deseja editar.

## Gerenciando políticas
{: #iamusermanpol}

É possível designar e gerenciar políticas para um usuário que tenha acesso aos
**Serviços ativados para identidade e acesso**. Uma política designa a um usuário uma ou
mais funções para um conjunto de recursos usando uma combinação de atributos para definir o conjunto
de recursos aplicável.

Ao designar uma política a um usuário, primeiro você especifica o serviço que deseja designar. A lista
**Serviço** fornece a opção para serviços específicos, incluindo uma opção para
designar todos os serviços disponíveis. Você também seleciona uma ou mais funções que deseja designar.

Opções de configuração adicionais estão disponíveis, dependendo do serviço que você seleciona. É possível
selecionar um serviço para ver as opções para esse serviço.

É possível limitar a lista de opções de serviço que são exibidas. Clique em **Especificar
contexto do serviço opcional** para especificar opções adicionais, como regiões e instâncias
de serviço.  Talvez você não queira especificar todas as opções que são exibidas, mas é possível escolher qual
deseja configurar.

Será possível designar e gerenciar políticas se você possuir a função adequada. A tabela a seguir mostra
as tarefas de gerenciamento de política e a função necessária para cada uma.


{: #iamui_table1}

| Ações | Atribuição necessária |
|----------|---------|
| Criar uma política em uma conta | Administrador na conta |
| Criar uma política em todos os serviços em uma conta | Administrador na conta |
| Criar uma política em todas as instâncias de serviço em uma conta | Administrador na conta |
| Criar uma política em um serviço em uma conta | Administrador da conta ou administrador no serviço na conta |
| Criar uma instância de serviço | Administrador ou editor na conta ou administrador ou editor no serviço na
conta |
| Criar uma política em uma instância de serviço | Administrador na conta ou administrador no serviço na conta
ou administrador na instância de serviço |
{: caption="Tabela 1. Tarefas administrativas para gerenciar políticas de **Serviços ativados para identidade e acesso**" caption-side="top"}

## Designando e gerenciando funções
{: #iamusermanrol}

Funções são uma coleção de ações; as ações que são mapeadas para essas funções são específicas de
serviço. 
Como as ações são agrupadas como funções, é possível usar um pequeno conjunto de funções definidas para suportar
quaisquer ações para quaisquer serviços e qualquer recurso. Por exemplo, se precisar de um administrador
para máquinas virtuais, armazenamento e rede, será possível configurar o usuário como o administrador para todos
os três itens mudando o destino da política. Portanto, você configuraria a política para incluir o administrador
de máquinas virtuais, o administrador de armazenamento e o administrador de rede.

Os recursos não são construídos para as funções para que novos nomes de função não sejam criados para
cada tipo de recurso que for introduzido no sistema. Por exemplo, não são necessárias uma função de administrador
de máquina virtual, uma função de administrador de armazenamento e uma função de administrador da rede para
cobrir a administração de recursos de máquinas virtuais, armazenamento e rede.

Além das descrições das funções fornecidas na interface com o usuário, a tabela a seguir fornece
exemplos de algumas das tarefas que os usuários designados a cada função podem executar.

{: #iamui_table2}

| Função | Descrição das ações | Exemplo de ações|
|:-----------------|:-----------------|:-----------------|
| Viewer | Executa ações que não mudam o estado; ações somente leitura | <ul><li>Listar dispositivos</li><li>Ler objeto de armazenamento</li><li>Executar consultas</li><li>Executar procuras</li></ul>|
| Aplicativos | Executa ações que modificam o estado e criam ou excluem sub-recursos |<ul><li>Criar ou excluir
máquinas virtuais</li><li>Anexar armazenamento</li><li>Reinicializar</li><li>Iniciar ou parar</li><li>Renomear</li></ul> |
| Administrator | Executa todas as ações, incluindo a capacidade de gerenciar o controle de acesso |<ul><li>Convidar usuários</li><li>Criar ou excluir
máquinas virtuais</li><li>Atualizar políticas de acesso de usuário</li><li>Listar dispositivos</li><li>Anexar armazenamento</li><li>Reinicializar</li><li>Iniciar ou parar</li><li>Renomear</li><li>Fazer backup e restaurar</li></ul>|
{: caption="Tabela 2. Tarefas administrativas para gerenciar políticas de **Serviços ativados para identidade e acesso**" caption-side="top"}

Para obter informações mais específicas sobre funções de usuários que tiverem acesso designado ao Cloud
Foundry, consulte [Funções de usuário](/docs/admin/users_roles.html#userrolesinfo).

Ao incluir usuários, deve-se selecionar pelo menos uma função e é possível incluir múltiplas
funções. Ao selecionar uma função, é exibida uma definição para ela para que seja possível determinar
uma ou mais funções que deseja fornecer.  As funções que você designar possuem opções de acesso diferentes, mas
para os mesmos atributos de recursos que forem especificados.

Se o serviço **Cloud Foundry** foi selecionado, então, as funções que forem
designadas serão associadas às organizações e espaços que você selecionar.
