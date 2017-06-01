---

copyright:

  years: 2015, 2016
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Funções e Permissões do Usuário
{: #userroles}

É possível gerenciar usuários nos serviços Platform and Infrastructure do {{site.data.keyword.Bluemix_notm}} na página **Usuários** de sua conta. Um link para a página Diretório da equipe também estará disponível na página Usuários, se você quiser gerenciar apenas o acesso do Cloud Foundry dos usuários da plataforma a organizações e espaços. No entanto, não será necessário sair da página Usuários para gerenciar o acesso ao Cloud Foundry.
{:shortdesc}

Para acessar a página Usuários, no menu do {{site.data.keyword.Bluemix_notm}}, clique
em **Gerenciar** &gt; **Conta** &gt; **Usuários**. Os proprietários da conta executam todas as operações nas organizações e nos espaços, incluindo o gerenciamento de usuários e suas funções designadas. Os gerenciadores de organização e de espaço também têm acesso para gerenciar funções. 

Se você for um usuário incluído na conta de outra pessoa e desejar visualizar suas funções e permissões designadas, acesse **Gerenciar** &gt; **Segurança** &gt; **Identidade e acesso** &gt; **Usuários** e clique em seu nome.

## Funções da conta
{: #userrolesinfo}

No nível de conta, há duas funções que permitem o acesso a diferentes recursos de gerenciamento de conta:

| Função da conta | Permissões |
|----------------|---------|
|Proprietário | Um proprietário para a conta tem acesso ao seu perfil, diretório da equipe, às suas informações de faturamento, notificações de gastos e ao seu painel de uso. Na página de diretório da equipe ou de usuários, o proprietário pode convidar novos membros da equipe e ajustar as funções. O proprietário também pode incluir créditos promocionais, configurar ou mudar o limite de faturamento, configurar o acesso de
serviço e gerenciar organizações e espaços. |
|Membro | Um membro tem acesso ao seu perfil, diretório da equipe, ao seus créditos da conta e limites de faturamento no cabeçalho do {{site.data.keyword.Bluemix_notm}}. No entanto, na página de
diretório da equipe, um membro pode apenas visualizar os membros da equipe dentro da conta. |
{:caption="Tabela 1. Funções e permissões de conta" caption-side="top"}

Todos os novos usuários são incluídos como um membro da conta. É possível designar funções de organização e espaço para convidados, a fim de ativar visualizações e permissões específicas no
{{site.data.keyword.Bluemix_notm}}. Novos membros da equipe incluídos em uma organização, exceto em um ambiente local ou dedicado, são designados à função de organização de auditor por padrão. Para um espaço específico, é possível optar por
designar a função de desenvolvedor ou auditor para convidados. Quando seus convidados aceitarem o convite e se associarem ao {{site.data.keyword.Bluemix_notm}}, será possível editar suas funções na página Usuários ou Diretório da equipe.

## Funções do Cloud Foundry
{: #cfroles}

As funções do Cloud Foundry incluem as permissões de acesso para organizações e espaços definidos na conta. As funções a seguir podem ser designadas no nível de organização:

| Função organizacional | Permissões |
|-------------------|-------------|
|Gerente | Gerenciadores de organização podem criar, visualizar, editar ou excluir espaços dentro da organização, visualizar o uso e a cota da organização, convidar membros da equipe para a organização,
gerenciar quem tem acesso à organização e às suas funções na organização e gerenciar domínios customizados para a organização. |
|Gerenciador de faturamento | Gerenciadores de faturamento podem visualizar informações de uso de tempo de execução e serviço para a organização na página de Painel de uso.  |
|Auditor | Auditores da organização podem visualizar o conteúdo do aplicativo e do serviço na organização. Os auditores também podem visualizar os usuários na organização e suas funções designadas, além da cota da organização. Essa função é designada a todos os convidados, exceto em ambientes locais ou dedicados, por padrão. |
{:caption="Tabela 2. Funções e permissões de organização" caption-side="top"}

As funções a seguir podem ser designadas no nível de espaço:

| Função de espaço | Permissões |
|------------|-------------|
|Gerente | Os gerenciadores de espaço podem incluir usuários existentes e gerenciar funções dentro do espaço. O gerenciador de espaço também pode visualizar o número de instâncias, ligações de serviço e
o uso recurso para cada aplicativo no espaço. |
|Desenvolvedor | Desenvolvedores de espaço podem criar, excluir e gerenciar aplicativos e serviços dentro do espaço. Algumas das tarefas de gerenciamento incluem implementar aplicativos, iniciar ou parar
aplicativos, renomear um aplicativo, excluir um aplicativo, renomear um espaço, ligar ou desvincular um serviço para um aplicativo, visualizar o número ou as instâncias, ligações de serviço e uso de recurso
para cada aplicativo no espaço. Além disso, o desenvolvedor de espaço pode associar uma URL interna ou externa com um aplicativo no espaço.   |
|Auditor | Auditores de espaço têm acesso somente leitura a todas as informações sobre o espaço, como informações sobre o número de instâncias, ligações de serviço e uso de recurso para cada aplicativo no
espaço. |
{:caption="Tabela 3. Funções e permissões de espaço" caption-side="top"}

**Nota**: os usuários designados à função de espaço de gerenciador ou desenvolvedor podem acessar a variável de ambiente VCAP_SERVICES. No entanto, um usuário designado à função de auditor não pode acessar VCAP_SERVICES.

## Políticas e funções de Identidade e gerenciamento de acesso
{: #iamusermanpol}

Os proprietários da conta são designados automaticamente à função de administrador de acesso da conta para Identidade e gerenciamento de acesso que permite designar e gerenciar políticas de serviço. Esse tipo de controle de acesso permite a designação de políticas por serviço ou instância de serviço para permitir níveis de acesso para gerenciar recursos e usuários dentro do contexto designado.

### Políticas de serviço

Uma política designa a um usuário uma ou
mais funções para um conjunto de recursos usando uma combinação de atributos para definir o conjunto
de recursos aplicável. Ao designar uma política a um usuário, você primeiramente especifica o serviço a ser designado, incluindo uma opção para designar todos os serviços disponíveis. Em seguida, também será possível selecionar uma função ou funções, para designar. Opções de configuração adicionais poderão estar disponíveis, dependendo do serviço selecionado.

Será possível designar e gerenciar políticas se você possuir a função adequada. A tabela a seguir mostra
as tarefas de gerenciamento de política e a função necessária para cada uma.

{: #iamui_table1}

| Ações | Atribuição necessária |
|----------|---------|
| Criar uma política em uma conta | Administrador de acesso à conta |
| Criar uma política em todos os serviços em uma conta | Administrador de acesso à conta |
| Criar uma política em todas as instâncias de serviço em uma conta | Administrador de acesso à conta |
| Criar uma política em um serviço em uma conta | Administrador de acesso à conta ou administrador no serviço na conta |
| Criar uma instância de serviço | Administrador de acesso à conta, editor, administrador ou editor no serviço na conta |
| Criar uma política em uma instância de serviço | Administrador de acesso à conta, administrador no serviço na conta ou administrador na instância de serviço |
{: caption="Tabela 4. Tarefas administrativas para gerenciar políticas de serviços ativadas para Identidade e acesso" caption-side="top"}

### Funções de política de serviço
{: #iamusermanrol}

Funções são uma coleção de ações; as ações que são mapeadas para essas funções são específicas de
serviço. Consulte a documentação do serviço selecionado para obter detalhes adicionais sobre os tipos de ações que cada função permite.

Além das descrições das funções fornecidas no console, a tabela a seguir fornece exemplos de algumas das tarefas que os usuários designados a cada função podem executar, dependendo do serviço selecionado. 

{: #iamui_table2}

| Função | Descrição das ações | Exemplo de ações|
|:-----------------|:-----------------|:-----------------|
| Viewer | Executa ações que não mudam o estado; ações somente leitura | <ul><li>Listar dispositivos</li><li>Ler objeto de armazenamento</li><li>Executar consultas</li><li>Executar procuras</li></ul>|
| Aplicativos | Executa ações que modificam o estado e criam ou excluem sub-recursos |<ul><li>Criar ou excluir
máquinas virtuais</li><li>Anexar armazenamento</li><li>Reinicializar</li><li>Iniciar ou parar</li><li>Renomear</li></ul> |
| Administrator | Executa todas as ações, incluindo a capacidade de gerenciar o controle de acesso |<ul><li>Convidar usuários</li><li>Criar ou excluir
máquinas virtuais</li><li>Atualizar políticas de acesso de usuário</li><li>Listar dispositivos</li><li>Anexar armazenamento</li><li>Reinicializar</li><li>Iniciar ou parar</li><li>Renomear</li><li>Fazer backup e restaurar</li></ul>|
{: caption="Tabela 5. Tarefas administrativas para gerenciar políticas de serviços ativados para Identidade e acesso" caption-side="top"}

## Permissões de infraestrutura
{: #infrapermissions}

Se você tiver acesso para designar funções de infraestrutura, será possível configurar as permissões a seguir para o usuário: 

| Permissão de infraestrutura | Descrição das ações |
|---------------------------|------------------------|
|Visualização Apenas | Os usuários com essa permissão podem visualizar somente os itens dentro do sistema.|
|Usuário Básico | Os usuários com essa permissão podem executar ações básicas dentro do sistema, como incluir um chamado e
gerenciar dispositivos. |
|Super usuário | Os usuários com essa permissão podem executar todas as ações disponíveis no sistema. |
{:caption="Tabela 6. Permissões de infraestrutura" caption-side="top"}

