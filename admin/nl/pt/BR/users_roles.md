---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando membros da equipe e funções
{: #userroles}
*Última atualização: 16 de maio de 2016*

A partir da página de **Diretório da equipe** para a sua conta, é possível gerenciar membros da equipe existentes e suas funções em sua organização e espaços, bem como convidar novos
membros da equipe. Para acessar o diretório da equipe para a sua conta, acesse o ícone **Conta e suporte** ![ícone Conta e suporte](../admin/images/account_support.svg) &gt; **Conta** &gt; *nome_de_sua_conta* &gt; **Diretório da equipe**.
{:shortdesc}

Proprietários da conta executam todas as operações nas organizações e espaços, incluindo o gerenciamento de membros da equipe e de suas funções designadas. Gerenciadores de organização têm acesso para
convidar membros da equipe e gerenciar funções. Gerenciadores de
espaço podem usar a página **Gerenciar organizações** para incluir membros da conta existente no espaço e ajustar as suas
funções. Verifique as informações a seguir, para saber mais sobre funções.

## Funções
{: #userrolesinfo}

No nível de conta, há duas funções que permitem o acesso a diferentes recursos de gerenciamento de conta:

*Tabela 1. Funções e permissões da conta*

| Função da conta | Permissões |    
|----------------|---------|
|Proprietário | Um proprietário para a conta tem acesso ao seu perfil, diretório da equipe, às suas informações de faturamento, notificações de gastos e ao seu painel de uso. A partir da página de diretório da
equipe, o proprietário pode convidar novos membros da equipe e ajustar funções. O proprietário também pode incluir créditos promocionais, configurar ou mudar o limite de faturamento, configurar o acesso de
serviço e gerenciar organizações e espaços. |
|Membro | Um membro tem acesso ao seu perfil, diretório da equipe, ao seus créditos da conta e limites de faturamento no cabeçalho do {{site.data.keyword.Bluemix_notm}}. No entanto, na página de
diretório da equipe, um membro pode apenas visualizar os membros da equipe dentro da conta. |

 Todos os novos membros da equipe são incluídos como um membro da conta. É possível designar funções de organização e espaço para convidados, a fim de ativar visualizações e permissões específicas no
{{site.data.keyword.Bluemix_notm}}. Novos membros da equipe incluídos em uma organização são designados com a função de organização de auditor por padrão. Para um espaço específico, é possível optar por
designar a função de desenvolvedor ou auditor para convidados. Logo que os seus convidados aceitarem o convite e se associarem ao {{site.data.keyword.Bluemix_notm}}, será possível editar as suas
funções na página **Diretório da equipe**.

As funções a seguir podem ser designadas no nível de organização:

*Tabela 2. Funções e permissões de organização*

| Função organizacional | Permissões |    
|-------------------|-------------|
|Gerente | Gerenciadores de organização podem criar, visualizar, editar ou excluir espaços dentro da organização, visualizar o uso e a cota da organização, convidar membros da equipe para a organização,
gerenciar quem tem acesso à organização e às suas funções na organização e gerenciar domínios customizados para a organização. |
|Gerenciador de faturamento | Gerenciadores de faturamento podem visualizar informações de uso de tempo de execução e serviço para a organização na página de Painel de uso.  |
|Auditor | Auditores da organização podem visualizar o conteúdo do aplicativo e do serviço na organização. Auditores também podem visualizar os membros da equipe na organização e as suas funções designadas e a
cota para a organização. Essa função é designada para todos os convidados por padrão.|

As funções a seguir podem ser designadas no nível de espaço:

*Tabela 3. Funções e permissões de espaço*

| Função de espaço | Permissões |    
|------------|-------------|
|Gerente | Gerenciadores de espaço podem incluir membros da equipe existentes e gerenciar funções dentro do espaço. O gerenciador de espaço também pode visualizar o número de instâncias, ligações de serviço e
o uso recurso para cada aplicativo no espaço. |
|Desenvolvedor | Desenvolvedores de espaço podem criar, excluir e gerenciar aplicativos e serviços dentro do espaço. Algumas das tarefas de gerenciamento incluem implementar aplicativos, iniciar ou parar
aplicativos, renomear um aplicativo, excluir um aplicativo, renomear um espaço, ligar ou desvincular um serviço para um aplicativo, visualizar o número ou as instâncias, ligações de serviço e uso de recurso
para cada aplicativo no espaço. Além disso, o desenvolvedor de espaço pode associar uma URL interna ou externa com um aplicativo no espaço.   |
|Auditor | Auditores de espaço têm acesso somente leitura a todas as informações sobre o espaço, como informações sobre o número de instâncias, ligações de serviço e uso de recurso para cada aplicativo no
espaço. |

**Nota**: membros da equipe que são designados com a função de espaço de gerenciador ou desenvolvedor podem acessar a variável de ambiente VCAP_SERVICES. No entanto, um membro da
equipe designado com a função de auditor não pode acessar VCAP_SERVICES.

## Convidando membros da equipe
{: #inviteteammembers}

Proprietários da conta e gerenciadores de organização podem convidar membros da equipe para as organizações a partir da página Convidar Membros da Equipe. Quando você inclui novos membros da equipe,
eles são designados com a função de auditor automaticamente. É possível mudar as funções posteriormente, na página Diretório da Equipe. Para convidar um membro da equipe, conclua estas etapas:

<ol>
<li>Acesse o ícone **Conta e suporte**
![ícone Conta e suporte](../admin/images/account_support.svg) &gt; **Conta** &gt;
*nome_de_sua_conta* &gt; **Convidar membro da equipe**.</li>
<li>Selecione a organização para a qual deseja convidar membros da equipe.</li>
<li>Clique em **Avançar**.</li>
<li>Selecione os espaços para os quais deseja permitir acesso aos seus membros da equipe.</li>
<li>Selecione a função a ser designada para os espaços selecionados na organização.</li>
<li>Selecione a opção para confirmar que você assume a responsabilidade financeira por todos os encargos incorridos na conta.</li>
<li>Insira o endereço de e-mail para um membro da equipe individual ou endereços de e-mail para múltiplos membros da equipe:<ul>
<li>Para incluir um membro da equipe único, insira o endereço de e-mail e clique em **Enviar**.</li>
<li>Para incluir mais de um membro da equipe, clique em **Convidar todos eles de uma vez**. Insira os endereços de e-mail usando uma lista separada por vírgula, espaços ou quebras de linha. 
Em seguida, clique em **Avançar**, para verificar os endereços de e-mail ao quais o convite deve ser enviado e clique em **Enviar**.</li>
</ul>
</li>
</ol>

Clique em **Visualizar pendente**, para verificar se os convites estão pendentes ou aceitos. É possível optar por reenviar o e-mail de convite ou cancelar o convite para um convite
pendente a qualquer momento.

## Editando Funções
{: #editinguserroles}

Proprietários da conta e gerenciadores de organização podem editar funções de organização e espaço para membros da equipe existentes na página **Diretório da equipe**. 

1. Acesse o ícone **Conta e suporte** ![ícone Conta e suporte](../admin/images/account_support.svg) &gt; **Conta** &gt; *nome_de_sua_conta* &gt; **Diretório da equipe**.
2. Localize o membro da equipe cujas funções você deseja editar.
3. Clique em **Visualizar funções**.
4. Selecione ou limpe as seleções de função de organização, para modificar o acesso à organização para o membro da equipe.
5. Clique em **Visualizar espaços**, para incluir ou remover funções de espaço.
6. Selecione ou limpe as seleções de função de espaço, para modificar o acesso ao espaço para o membro da equipe.
7. Clique em **Fechar espaços**.
8. Clique em **Salvar** no final da página.

Gerenciadores de espaço podem editar funções para os membros da equipe em seu espaço na página **Gerenciar organizações**.

1. Acesse o ícone **Conta e suporte**
![ícone Conta e suporte](../admin/images/account_support.svg) &gt; **Conta** &gt;
*nome_de_sua_conta* &gt; **Gerenciar organizações**.
2. Localize a organização na qual o seu espaço está.
3. Clique em **Visualizar Detalhes**.
4. Localize o seu espaço e clique em **Editar espaço**.
5. Selecione a guia **Usuários**.
6. Selecione ou limpe a opção de função de espaço para a função que você deseja incluir ou remover para o membro da equipe.
7. Clique **Salvar.**
