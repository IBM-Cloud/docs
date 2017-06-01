---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Designando Acesso do Usuário
{: #assignaccess}

Você
designa o acesso aos usuários conforme eles são convidados, atribuindo funções, políticas e as contas ou
as organizações, ou ambos, que eles possam acessar. Dependendo das opções de acesso que você estiver autorizado a gerenciar, será possível convidar e fornecer acesso para usuários na conta, na organização, no espaço e nas instâncias de serviço. Como
um proprietário da conta, é possível designar opções de acesso à sua conta para um usuário quando você e o
usuário são membros, independentemente da função. As seções a seguir descrevem os três tipos de acesso que podem ser designados a um usuário convidado.
{:shortdesc}

## Serviços ativados para identidade e acesso

É possível designar uma única política de serviço ao convidar um novo usuário. Quando o usuário aceitar o convite, será possível incluir políticas de serviço adicionais.

1. Na tela **Convidar usuários**, expanda a seção **Serviços ativados para identidade e acesso**.
2. Selecione **Todos os serviços ativados para identidade e acesso** ou selecione um serviço individual. **Nota**: se selecionar a opção **Conceder acesso automaticamente quando novos
serviços forem incluídos**, você não será notificado para cancelar a seleção de cada novo
serviço do {{site.data.keyword.Bluemix_notm}} para esse usuário quando os serviços forem
incluídos posteriormente.
3. Selecione **Todas as regiões atuais** ou uma região específica.
4. Selecione **Todas as instâncias de serviço atuais** ou selecione uma instância de serviço específica.
5. Selecione uma função para definir o escopo de acesso da política.
6. Opcional: selecione **Incluir função** para especificar uma função adicional para a política.

Veja [Políticas e funções de gerenciamento de identidade e acesso](/docs/iam/users_roles.html#iamusermanpol) para obter informações mais específicas sobre a configuração de políticas de serviço.

## Acesso ao Cloud Foundry

Todos os usuários são concedidos à função de organização de auditor por padrão. É possível atualizar essa função para gerente de faturamento, gerenciador de organização ou nenhuma função de organização depois que o usuário aceita o convite. Durante o processo de convite, é possível incluir múltiplas funções de espaço, uma de cada vez.

1. Na tela **Convidar usuários**, expanda a seção **Acesso do Cloud Foundry**.
2. Selecione uma organização na qual incluir o usuário.
3. Selecione **Todas as regiões atuais** ou uma região específica.
4. Selecione **Todos os espaços atuais** ou um espaço específico.
5. Selecione uma função para definir o escopo de acesso.
6. Opcional: selecione **Incluir função** para especificar uma função adicional para a política.

Veja [Funções do Cloud Foundry](/docs/iam/users_roles.html#cfroles) para obter informações mais específicas sobre essas funções.

## Acesso ao Infrastructure

Se você tiver permissão, verá a opção para designar permissões de infraestrutura. As permissões reais designadas são limitadas automaticamente ao subconjunto de permissões que você tem. Para obter mais informações sobre as permissões e quais ações o usuário pode executar com cada uma, veja [Permissões de infraestrutura](/docs/iam/users_roles.html#infrapermissions).

1. Na tela **Convidar usuários**, expanda a seção **Acesso à infraestrutura**. 
2. Selecione uma permissão para definir o escopo de acesso.

Para obter informações sobre como configurar o acesso para usuários depois de eles terem sido incluídos em sua conta, veja [Gerenciando contas do usuário e o acesso](/docs/iam/iamusermanage.html).
