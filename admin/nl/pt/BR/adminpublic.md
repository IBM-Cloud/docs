---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Administração
{: #administer}
*Última atualização: 29 de fevereiro de 2016*

Gerencie suas organizações, espaços e usuários designados clicando no ícone **Conta e suporte** ![Conta e suporte](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**. Se você for um usuário do {{site.data.keyword.Bluemix_notm}} Local ou {{site.data.keyword.Bluemix_notm}} Dedicated, veja [Gerenciando o {{site.data.keyword.Bluemix_notm}} Local e {{site.data.keyword.Bluemix_notm}} Dedicated](../admin/index.html#mng) para obter mais informações sobre como administrar a sua instância local ou dedicada.
{:shortdesc}

## Gerenciando o {{site.data.keyword.Bluemix_notm}} Public
{: #mngacct}

No {{site.data.keyword.Bluemix}} Public, é possível gerenciar organizações e espaços, incluindo acesso de usuário Todos a partir do painel na interface com o usuário. É possível também monitorar seu uso e faturamento.
{:shortdesc}

### Organizações e espaços
{: #orgsandspaces}

Como gerenciador de organização ou proprietário da conta, é possível usar a página Gerenciar organizações para visualizar e gerenciar as configurações da organização ou do espaço, incluindo acesso de usuário. Para abrir a página Gerenciar organizações, clique no ícone **Conta e suporte** ![Conta e suporte](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**.

#### Organizações

Uma organização é definida pelos itens a seguir:

<dl>
<dt>Usuários</dt>
<dd>A função com permissão básica em organizações e espaços. Você deve estar designado a
uma organização para poder receber permissões para os espaços dentro da organização. Para
obter informações detalhadas, veja
[Usuários e funções](adminpublic.html#userroles).</dd>
<dt>Domínios</dt>
<dd>Fornecem a rota na Internet que é alocada para a organização. Uma rota tem um subdomínio e um domínio. Um subdomínio normalmente é o nome do aplicativo. Um domínio pode ser um domínio do sistema ou um domínio customizado que você registrou para seu aplicativo.<br/>
<p>**Nota**: Se um domínio customizado for incluído, deve-se configurar seu servidor DNS para resolver seu domínio customizado para apontar para o domínio de sistema {{site.data.keyword.Bluemix_notm}}. Dessa
maneira, quando o
{{site.data.keyword.Bluemix_notm}}
receber uma solicitação para o domínio customizado, ele poderá roteá-lo corretamente
para o aplicativo.</p></dd>
<dt>Cota</dt>
<dd>Representa os limites de recurso para a organização, incluindo o número de serviços e a quantia de memória
que pode ser alocada para uso pela organização. As cotas são designadas quando as organizações são criadas. Qualquer
aplicativo ou serviço em um espaço da organização contribui para o uso da cota. Com planos de Assinatura ou de
Pagamento conforme o uso, é possível ajustar a sua conta para contêineres e aplicativos
do Cloud Foundry conforme as necessidades de mudança da sua organização.</dd>
</dl>

No
{{site.data.keyword.Bluemix_notm}},
é possível usar organizações para permitir a colaboração entre usuários e para facilitar
o agrupamento lógico de recursos de projetos nas maneiras a seguir:

<ul>
<li>É possível agrupar um conjunto de espaços, aplicativos, serviços, domínios, rotas e
usuários juntos em organizações.</li>
<li>É possível gerenciar o acesso aos espaços e organizações por usuário.</li>
</ul>

Ao
criar uma organização, o nome da organização deve ser exclusivo no {{site.data.keyword.Bluemix_notm}}. Depois de criar a organização, você será designado automaticamente à permissão *Gerenciador de organização*, que permite editar o nome da organização, excluir a organização e criar espaços na organização.

Ao excluir uma organização, todos os espaços, aplicativos e serviços
dentro da organização são excluídos.

O
{{site.data.keyword.Bluemix_notm}}
permite a colaboração em projetos, designando usuários dentro de uma organização e dentro
dos espaços na organização. É possível usar a guia **Usuários** para
exibir e gerenciar usuários da organização. Também é possível convidar usuários em sua organização clicando no link **Convidar um novo usuário** na guia **Usuários**. As permissões a seguir podem ser designadas
aos usuários em uma organização:

<ul>
<li>Usuário da organização</li>
<li>Gerente da organização</li>
<li>Gerente de faturamento da organização</li>
<li>Auditor da organização</li>
</ul>

#### Espaços

Dentro de uma organização, é possível usar espaços para
agrupar um conjunto de aplicativos, serviços e usuários.

Após a inclusão de
usuários em uma organização, é possível conceder a eles permissões para os espaços
dentro da organização. Semelhantes às organizações, os espaços também têm um conjunto de
permissões que podem ser designadas aos usuários:

<ul>
<li>Gerente de espaço</li>
<li>Desenvolvedor de espaço</li>
<li>Auditor de espaço</li>
</ul>

**Nota**: Um usuário deve ser designado a pelo menos uma das permissões no espaço.

A guia **Domínios** para um espaço é uma lista
somente leitura dos domínios designados ao espaço. O domínio do sistema está sempre disponível a um espaço e domínios customizados também
podem ser alocados para o espaço. Os aplicativos que foram criados no espaço podem usar
qualquer um dos domínios listados para o espaço.

### Usuários e funções
{: #userroles}

Os proprietários de contas executam todas as operações nas organizações e
nos espaços.

####Tipos de usuário

É possível ser membro ou colaborador de
uma conta.

<dl>
<dt>Membro</dt>
<dd>Você será membro de uma conta do
{{site.data.keyword.Bluemix_notm}}
se for seu criador ou caso tenha sido convidado para conta e se inscrito nela a partir do
convite, como sua primeira experiência com o
{{site.data.keyword.Bluemix_notm}}. </dd>
<dt>Colaborador</dt>
<dd>Você será colaborador de uma conta do
{{site.data.keyword.Bluemix_notm}}
se tiver usado anteriormente o
{{site.data.keyword.Bluemix_notm}}
 com uma conta diferente e, depois de convidado, aceito o convite para conta.</dd>
</dl>

#### Funções de usuário

Usuários podem ser designados às permissões a seguir para assumir
diferentes funções de usuário em uma organização ou espaço:

<dl>
<dt>Gerentes de organização</dt>
<dd>Os gerenciadores de organização têm as seguintes permissões:
<ul>
<li>Criar ou excluir espaços dentro da organização.</li>
<li>Convidam usuários para a organização, caso sejam membros da organização ou proprietários da
conta.</li>
<li>Gerenciam usuários existentes que já estão na organização.</li>
<li>Gerenciar domínios da organização.</li>
</ul>
<p>**Nota**: Se você tiver o tipo de usuário de colaborador e usou anteriormente o {{site.data.keyword.Bluemix_notm}} com uma conta diferente, não é possível convidar usuários na organização mesmo se estiver designado à função de gerenciador de organização. É necessário ter o tipo de usuário
membro para convidar usuários. Consulte  <a href="../troubleshoot/index.html#ts_adduser">Não é
possível incluir usuários em uma organização</a> para obter informações sobre como trabalhar
com esse problema.</p>
</dd>
<dt>Gerentes de faturamento</dt>
<dd>Os gerenciadores de faturamento têm permissões para visualizar as informações de uso do
serviço e tempo de execução da organização.</dd>
<dt>Auditores de organização</dt>
<dd>Os auditores da organização têm permissões para visualizar o conteúdo do aplicativo e do
serviço no espaço.</dd>
<dt>Gerentes de espaço</dt>
<dd>Os gerenciadores de espaçamento têm as permissões a seguir:
<ul>
<li>Incluem usuários no espaço e gerenciam usuários.</li>
<li>Ativar recursos para o espaço</li>
</ul>
</dd>
<dt>Desenvolvedores de espaço</dt>
<dd>Os desenvolvedores de espaço têm as seguintes permissões:
<ul>
<li>Criar, excluir e gerenciar aplicativos e serviços dentro do espaço.</li>
<li>Ter acesso a logs dentro do espaço</li>
</ul>
</dd>
<dt>Auditores de espaço</dt>
<dd>Os auditores de espaço têm permissões de acesso somente leitura a todas as informações
sobre o espaço, por exemplo, informações sobre aplicativos e serviços, configurações,
relatórios e logs.</dd>
</dl>

**Nota**: os usuários designados à função de gerente ou desenvolvedor podem acessar a variável de ambiente VCAP_SERVICES. No entanto, um usuário designado à função de auditor não pode acessar VCAP_SERVICES. 

### Gerenciando suas organizações
{: #orgmng}

Como gerenciador de organização ou proprietário da conta, é possível gerenciar
suas organizações. As tarefas de gerenciamento incluem criar uma organização, renomear uma organização, criar um espaço, convidar usuários para um espaço, mudar funções de usuário e excluir uma organização existente.

#### Criando uma organização

Somente usuários com
contas a pagar podem criar uma organização. Com uma conta a pagar, é possível
criar uma organização executando as etapas a seguir:

<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone  **Conta e suporte**  ![Conta e suporte](../support/images/account_support.svg) e, em seguida,  selecione **Gerenciar organizações**.</li>
<li>Clique em **Criar uma organização** e
siga os prompts para criar sua organização.</li>
</ol>

#### Renomeando uma organização

Execute as etapas
a seguir para renomear sua organização:

<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte** ![Conta e suporte](images/account_support.svg) e selecione **Gerenciar organizações**.</li>
<li>Selecione a organização que você deseja renomear.</li>
<li>Digite um novo nome no campo **Organização**
e clique em **Salvar**.</li>
</ol>

#### Listando membros 

Execute as etapas a seguir
para listar os membros de sua organização ou espaço:

<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte**  ![Conta e suporte](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**. É
possível ver os membros de sua organização e suas funções na guia **Usuários**.</li>
<li>Clique no nome de espaço em sua organização para ver os
membros desse espaço e suas funções.</li>
</ol>

#### Criando um espaço

É possível criar espaços em
sua organização, por exemplo, um espaço *dev* como
um ambiente de desenvolvimento, um espaço *test* como um ambiente
de teste e um espaço *production* como um ambiente de
produção. Em seguida, é possível associar seus apps aos espaços. Execute as
etapas a seguir para criar um espaço:

<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte** ![Conta e suporte](images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**.</li>
<li>Clique em **Criar um espaço** sob o nome da organização e siga os prompts para criar seu espaço.</li>
</ol>

#### Convidando usuários para um espaço

É possível convidar usuários para suas organizações e espaços por endereço de e-mail. Os usuários só podem acessar
o espaço no qual foram incluídos. 

Dependendo de se o convidado tem um ID IBM ou não, esse usuário é designado como tendo uma função de `membro` ou de `colaborador` para a conta. A tabela a seguir detalha como as funções de conta são designadas por tipo de convite.

*Tabela 1. Designações de funções de conta*

| **Tipo de e-mail convidado** | **Função de conta designada** | 
|----------------|------------------|
|O usuário tem uma conta de ID IBM vinculada ao endereço de e-mail convidado  | Membro  | 
|O usuário não tem um ID IBM | Um ID IBM é criado correspondendo ao endereço de e-mail enviado e o usuário é incluído como um Membro. | 
|Um endereço de e-mail para um usuário atual do {{site.data.keyword.Bluemix_notm}} | Colaborador | 

Conclua as etapas a seguir para incluir usuários com funções designadas a espaços específicos para uma organização escolhida:

<ol>
<li>Acesse **Conta e suporte** &gt; **Conta** &gt; **Gerenciar organizações**.</li>
<li>Selecione **Convidar
Usuários**.</li>
<li>Insira o endereço de e-mail da pessoa que deseja convidar.</li>
<li>Selecione a função da organização para a qual planeja convidar o novo usuário.</li>
<li>Selecione a função do espaço para o qual planeja convidar o novo usuário.</li>
<li>Selecione **Convidar**.</li>
<li>Na seção **Pendente**, visualize a confirmação de que o convite foi enviado. Selecione **Reenviar e-mail** ou **Cancelar convite** para agir em um convite pendente.</li>
</ol>

#### Mudando funções de usuário

Execute as etapas a seguir para mudar as funções de usuário:

<ol>
<li>Na interface com o usuário do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte** ![Conta e suporte](images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**.</li>
<li>Marque a caixa de seleção **GERENTE**, **GERENTE DE FATURAMENTO** ou **AUDITOR** na guia **USUÁRIOS** para mudar as funções de usuários em sua organização. Ou selecione um espaço na área de janela de navegação e, em seguida, marque a caixa de seleção **GERENTE**, **DESENVOLVEDOR** ou **AUDITOR** na guia **USUÁRIOS** para mudar as funções de usuários no espaço. </li>
<li>Clique em **SALVAR**.</li>
</ol>

#### Excluindo uma organização existente

Entre em contato com o suporte de registro e ID do {{site.data.keyword.Bluemix_notm}} para excluir a sua organização.

**Nota**: Não é possível inverter operações de exclusão. Você perderá todos os aplicativos e
serviços que estiverem associados à organização.

