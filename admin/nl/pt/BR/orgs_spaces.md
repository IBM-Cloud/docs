---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Criando organizações e espaços
{: #orgsspacesusers}

Como um proprietário da conta, é possível gerenciar suas organizações usando a página
Gerenciar organizações. Gerenciadores de organização também podem usar a página Gerenciar Organizações,
para gerenciar quaisquer organizações na qual eles estão configurados como o gerente.
{:shortdesc}

Para gerenciar usuários em sua conta, na barra de menus do {{site.data.keyword.Bluemix_notm}},
clique em **Gerenciar** &gt; **Conta** &gt;
**Usuários**. 

**Observação**: deve-se ser o proprietário de uma conta pay-as-you-go para criar uma organização.

## Criando Organizações
{: #createorg}

As organizações podem abranger múltiplas regiões e elas são definidas pelos itens a seguir:

<dl>
<dt>Os membros da equipe</dt>
<dd>A função com permissão básica em organizações e espaços. Você deve estar designado a
uma organização para poder receber permissões para os espaços dentro da organização. Para
obter informações detalhadas, veja
[Usuários e funções](/docs/iam/users_roles.html#userrolesinfo).</dd>
<dt>Domínios</dt>
<dd>Fornecem a rota na Internet que é alocada para a organização. Uma rota tem um subdomínio e um domínio. Um subdomínio normalmente é o nome do aplicativo. Um
domínio pode ser um domínio do sistema ou um domínio customizado que você registrou para
seu aplicativo. Veja [Gerenciando domínios customizados](/docs/admin/manageorg.html#managedomains).<br/>
<p>**Nota:** se um domínio customizado é incluído, deve-se configurar seu servidor DNS para resolver seu domínio customizado para apontar para o domínio de sistema {{site.data.keyword.Bluemix_notm}}. Dessa
maneira, quando o
{{site.data.keyword.Bluemix_notm}}
receber uma solicitação para o domínio customizado, ele poderá roteá-lo corretamente
para o aplicativo.</p></dd>
<dt>Cota</dt>
<dd>Representa os recursos que estão disponíveis para uma organização, incluindo o número de serviços e a quantia de memória que pode ser alocada para uso pela organização. As cotas são designadas quando as organizações são criadas. Qualquer aplicativo ou serviço em um espaço dentro de uma organização contribui para o uso da cota. Com planos de Pagamento por uso ou de Assinatura, é possível ajustar a sua cota para aplicativos e contêineres do Cloud Foundry
conforme as necessidades de mudança da sua organização. Consulte [Gerenciando cota](/docs/admin/manageorg.html#managequota).
<p>**Nota:** em uma conta da Assinatura, a cota é um limite definido pelo usuário que aciona notificações de gasto.</p></dd>
</dl>

No {{site.data.keyword.Bluemix_notm}}, é possível usar organizações para permitir a colaboração entre membros da equipe e para facilitar o agrupamento lógico de recursos do projeto das
seguintes maneiras:

<ul>
<li>É possível agrupar um conjunto de espaços, aplicativos, serviços, domínios, rotas e membros da equipe juntos em organizações.</li>
<li>É possível gerenciar o acesso aos espaços e organizações por usuário.</li>
</ul>

Ao
criar uma organização, o nome da organização deve ser exclusivo no {{site.data.keyword.Bluemix_notm}}. Se o nome da organização já estiver em uso por outro usuário do
{{site.data.keyword.Bluemix_notm}} Public, Dedicated ou
Local, então, deverá especificar um novo nome. Depois de criar a organização, você será designado automaticamente com a permissão de
*Gerenciador de organização*, que permite editar o nome da organização, incluir membros da equipe e criar ou excluir espaços na organização.

É possível usar o comando [`bx iam org-delete`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_org_delete) para excluir organizações. Ao excluir uma organização, todos os espaços, aplicativos e serviços
dentro da organização são excluídos.

As [funções de usuário](/docs/iam/users_roles.html#userrolesinfo) a seguir podem ser designadas para membros da equipe em uma organização:

<ul>
<li>Gerente da organização</li>
<li>Gerente de faturamento da organização</li>
<li>Auditor da organização</li>
</ul>

Somente proprietários da conta com contas de Pagamento por uso podem criar uma organização. É possível criar uma organização concluindo as etapas a seguir:

1. Clique em **Gerenciar** &gt; **Conta** &gt;
**Organizações**.
2. Clique em **Incluir uma nova organização**.
3. Insira o nome da organização.
4. Clique em ** Adicionar**.

<!-- Add info on Manage infrastructure option under a space -->

## Criando Espaços
{: #spaceinfo}

Dentro de uma organização, é possível usar espaços para agrupar um conjunto de aplicativos, serviços e membros da equipe. Espaços são ligados a uma região específica no
{{site.data.keyword.Bluemix_notm}}.

Após incluir membros da equipe em uma organização, é possível conceder a eles permissões para os espaços. Semelhantes às organizações, os espaços também têm um conjunto de
[funções de usuário](/docs/iam/users_roles.html#userrolesinfo) com permissões específicas que são designadas a membros da equipe:

<ul>
<li>Gerente de espaço</li>
<li>Desenvolvedor de espaço</li>
<li>Auditor de espaço</li>
</ul>

**Nota**: um membro da equipe deve ser designado a pelo menos uma das permissões no espaço.

É possível criar espaços em
sua organização, por exemplo, um espaço *dev* como
um ambiente de desenvolvimento, um espaço *test* como um ambiente
de teste e um espaço *production* como um ambiente de
produção. Em seguida, é possível associar os apps aos espaços. Conclua as etapas a seguir para criar um espaço:

1. Clique em **Gerenciar** &gt; **Conta** &gt;
**Organizações**.
2. Identifique a organização na qual você deseja incluir um espaço e selecione **Visualizar
detalhes**.
4. Clique em **Incluir um espaço**.
5. Insira o nome de espaço.
6. Clique em ** Adicionar**.
