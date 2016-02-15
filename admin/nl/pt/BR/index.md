{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Administrando o {{site.data.keyword.Bluemix_notm}}
{: #administer}
*Última atualização: 20 de janeiro de 2016*

Gerencie suas organizações, espaços e usuários designados clicando no ícone **Conta e suporte** ![Conta e suporte](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**. Se você for um usuário do {{site.data.keyword.Bluemix_notm}} Local ou {{site.data.keyword.Bluemix_notm}} Dedicated, veja [Gerenciando o {{site.data.keyword.Bluemix_notm}} Local e {{site.data.keyword.Bluemix_notm}} Dedicated](index.html#mng) para obter mais informações sobre como administrar a sua instância local ou dedicada.
{:shortdesc}

##Gerenciando sua conta
{: #mngacct}

No {{site.data.keyword.Bluemix}} Public, é possível gerenciar organizações e espaços, incluindo acesso de usuário Todos a partir do painel na interface com o usuário. É possível também monitorar seu uso e faturamento.
{:shortdesc}

###Organizações e espaços
{: #orgsandspaces}

Como gerenciador de organização ou proprietário da conta, é possível usar a página Gerenciar organizações para visualizar e gerenciar as configurações da organização ou do espaço, incluindo acesso de usuário. Para abrir a página Gerenciar organizações, clique no ícone **Conta e suporte** ![Conta e suporte](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**.

####Organizações

Uma organização é definida pelos itens a seguir:

<dl>
<dt>Usuários</dt>
<dd>A função com permissão básica em organizações e espaços. Você deve estar designado a
uma organização para poder receber permissões para os espaços dentro da organização. Para
obter informações detalhadas, veja
[Usuários e funções](index.html#userroles).</dd>
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

####Espaços

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

###Usuários e funções
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

####Funções de usuário

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

###Gerenciando sua organização
{: #orgmng}

Como gerenciador de organização ou proprietário da conta, é possível gerenciar
suas organizações. As tarefas de gerenciamento incluem criar uma organização, renomear uma organização, criar um espaço, convidar usuários para um espaço, mudar funções de usuário e excluir uma organização existente.

<ul>
<li>Criando uma organização
<p>Somente usuários com
contas a pagar podem criar uma organização. Com uma conta a pagar, é possível
criar uma organização executando as etapas a seguir:</p>
<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone  **Conta e suporte**  ![Conta e suporte](../support/images/account_support.svg) e, em seguida,  selecione **Gerenciar organizações**.</li>
<li>Clique em **Criar uma organização** e
siga os prompts para criar sua organização.</li>
</ol>
</li>
<li>Renomeando uma organização
<p>Execute as etapas
a seguir para renomear sua organização:</p>
<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte** ![Conta e suporte](images/account_support.svg) e selecione **Gerenciar organizações**.</li>
<li>Selecione a organização que você deseja renomear.</li>
<li>Digite um novo nome no campo **Organização**
e clique em **Salvar**.</li>
</ol>
</li>
<li>Listando membros
<p>Execute as etapas a seguir
para listar os membros de sua organização ou espaço:</p>
<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte**  ![Conta e suporte](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**. É
possível ver os membros de sua organização e suas funções na guia **Usuários**.</li>
<li>Clique no nome de espaço em sua organização para ver os
membros desse espaço e suas funções.</li>
</ol>
</li>
<li>Criando um espaço
<p>É possível criar espaços em
sua organização, por exemplo, um espaço *dev* como
um ambiente de desenvolvimento, um espaço *test* como um ambiente
de teste e um espaço *production* como um ambiente de
produção. Em seguida, é possível associar seus apps aos espaços. Execute as
etapas a seguir para criar um espaço:</p>
<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte** ![Conta e suporte](images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**. </li>
<li>Clique em **Criar um espaço** sob o nome da organização e siga os prompts para criar seu espaço.</li>
</ol>
</li>
<li>Convidando usuários para um espaço
<p>É possível convidar
usuários para sua organização como colaboradores. Também é possível incluir usuários
de sua organização em espaços diferentes. Os usuários só podem acessar
o espaço no qual foram incluídos. Execute as etapas a seguir para incluir
um usuário em um espaço:</p>
<ol>
<li>Acesse o Painel do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte** ![Conta e suporte](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**. Em seguida, clique em **Incluir usuário** em sua organização e siga os prompts para incluir o usuário em sua organização.</li>
<li>Inclua o usuário em um espaço. Selecione o espaço na área de janela de navegação, clique em **Incluir usuário** e siga os prompts para incluir o usuário no espaço.</li>
</ol>
</li>
<li>Mudando funções de usuário
<p>Execute as etapas a seguir para mudar as funções de usuário:</p>
<ol>
<li>Na interface com o usuário do {{site.data.keyword.Bluemix_notm}}, clique no ícone **Conta e suporte** ![Conta e suporte](images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**.</li>
<li>Marque a caixa de seleção **GERENTE**, **GERENTE DE FATURAMENTO** ou **AUDITOR** na guia **USUÁRIOS** para mudar as funções de usuários em sua organização. Ou selecione um espaço na área de janela de navegação e, em seguida, marque a caixa de seleção **GERENTE**, **DESENVOLVEDOR** ou **AUDITOR** na guia **USUÁRIOS** para mudar as funções de usuários no espaço. </li>
<li>Clique em **SALVAR**.</li>
</ol>
</li>
<li>Excluindo uma organização existente
<p>Entre em contato com o suporte de registro e ID do {{site.data.keyword.Bluemix_notm}} para excluir a sua organização.</p>
<p>**Nota**: Não é possível inverter operações de exclusão. Você perderá todos os aplicativos e
serviços que estiverem associados à organização.</p>
</li>
</ul>

## Gerenciando o {{site.data.keyword.Bluemix_notm}} Local e {{site.data.keyword.Bluemix_notm}} Dedicated
{: #mng}

Se você tiver acesso de administrador para o {{site.data.keyword.Bluemix_notm}} Local ou o {{site.data.keyword.Bluemix_notm}} Dedicated, acesse a página **Administração** para gerenciar recursos, monitorar o uso de cotas, administrar permissões de usuário, planejar notificações de upgrade, visualizar relatórios e logs de segurança e mais. É possível gerenciar suas organizações criando espaços e configurando funções e permissões de usuário; veja [Gerenciando suas organizações](index.html#orgmng).
{:shortdesc}

*Tabela 1. Tarefas administrativas para gerenciar a instância local ou dedicada do {{site.data.keyword.Bluemix_notm}}*

| O que fazer? | Detalhes |    
|----------------|---------|
|Monitorar o uso do sistema | Clique em **ADMINISTRAÇÃO &gt; USO**. Visualize as informações do sistema, monitore o uso da CPU e o uso do plano para tomar as melhores decisões para seus negócios.|
|Gerenciar seu catálogo | Clique em **ADMINISTRAÇÃO &gt; GERENCIAMENTO DO CATÁLOGO**. Gerencie quais serviços estão visíveis para seus usuários.|
|Administrar organizações | Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DA ORGANIZAÇÃO**. Crie organizações, monitore cotas para organizações e tome decisões baseadas nas necessidades com rapidez.|
|Criar espaços e designar funções de usuário | Clique no ícone **Conta e suporte** ![Conta e suporte](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações**. Crie espaços dentro de suas organizações. Inclua usuários e designe funções de organização e espaço para os usuários. |
|Gerenciar permissões de usuário administrativo | Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DE USUÁRIO**. Inclua usuários, remova usuários e ajuste permissões de usuários. |
|Revisar relatórios e logs | Clique em **ADMINISTRAÇÃO &gt; RELATÓRIOS E LOGS**. Visualize relatórios de segurança e logs de auditoria de sua instância.|
|Visualizar Informações do Sistema | Clique em **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA**. Visualize informações do sistema, tais como atualizações pendentes, nome e versão de sua instância, região, URL da API, URL da CLI, detalhes da configuração de LDAP, mapeamentos de grupos e de usuários, estatísticas e domínios compartilhados.  |

### Visualizando as informações do sistema
{: #oc_system}

Para visualizar informações do sistema, clique em
**ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA**.

É possível expandir e visualizar várias seções sobre
atualizações pendentes, informações gerais do sistema e detalhes de
configuração de LDAP.

* Na seção Atualizações, você pode visualizar quaisquer
atualizações pendentes que requeiram ação de sua parte. É possível
também controlar facilmente suas atualizações utilizando o
link de calendário para importar suas atualizações planejadas para um
app de calendário.

<ol>
<li>Para tomar ação para uma atualização específica, conclua as seguintes etapas:
<ol type="a">
<li>Clique em <strong><em>Number</em> atualizações pendentes</strong>
para visualizar todas as atualizações pendentes.</li>
<li>Selecione uma atualização para tomar uma ação ou visualizar os detalhes da atualização, que incluem a janela de atualização, data planejada ou status de interrupção.</li>
<li>Clique em <strong>CONFIGURAR DATAS INDISPONÍVEIS</strong> para
configurar dias específicos na janela de atualização que não são
convenientes para a aplicação da atualização. Se você configurar
datas indisponíveis, a IBM aprova e planeja sua atualização com base em suas seleções. Você
recebe uma notificação quando a atualização é aprovada e planejada.</li>
<li>Clique em <strong>APROVAR</strong> para aprovar a atualização,
se não tiver datas indisponíveis. Se você aprovar, a atualização será
aplicada durante a janela de atualização planejada. A IBM envia uma notificação quando a implementação de atualização começa e termina.</li>
</ol>
</li>
<li>Para importar suas atualizações planejadas para um app de
calendário de sua escolha, conclua as seguintes etapas:
<ol type="a">
<li>Abra seu app de calendário.</li>
<li>Importe o calendário de atualizações colando a **URL
de calendário** listada na página Informações do
sistema em seu app. Ou, faça o download do arquivo de calendário
clicando na URL de calendário e, em seguida, importando-o em seu
app de calendário usando o arquivo `.ics`.</li>
<li>Insira suas credenciais.</li>
<li>Visualize suas atualizações planejadas.</li>
</ol>
</li>
</ol>

* Na seção Informações gerais, é possível visualizar as informações a seguir:
    * Informações básicas sobre a construção do {{site.data.keyword.Bluemix_notm}}.
    * Informações de API incluindo a versão, a URL, a região e um link para a documentação de CLI.
    * Informações de domínio compartilhadas sobre seu sistema e serviço.
    * Estatísticas sobre o número total de aplicativos, usuários e organizações.
* Na seção Detalhes de configuração LDAP, é possível selecionar o servidor
LDAP e visualizar informações sobre os mapeamentos de usuários e de grupos. Se
você estiver usando o {{site.data.keyword.IBM}} WebID, isso é
indicado na seção Detalhes de configuração de LDAP.

### Visualizando informações de uso
{: #oc_resource}

Para visualizar informações de recursos, clique em
**ADMINISTRAÇÃO &gt; USO**.

Na seção Monitoramento de recurso, é possível visualizar as
informações a seguir:

* Informações de uso do recurso, tais como quantos GB de memória e quantos GB de espaço em disco são
usados. É possível visualizar o uso de CPU médio em todos os Droplet Execution Agents (DEAs). Clique no quadrado de
**CPU** e poderá ver o uso de CPU para cada DEA. O DEA com o mais alto uso é listado primeiro e cada
um é identificado por suas tarefas e endereço IP. O uso de CPU é separado em três categorias que incluem a quantia de
CPU gasto em processos do sistema, quantia de CPU gasta em processos do usuário e quantia de
CPU gasta em processos em espera.
* As informações de uso da rede para entrada de largura da banda e saída da largura da banda, durante o último dia, durante a última semana ou
durante o último mês.
Os dados exibidos são baseados na soma do tráfego de entrada e de saída para as redes públicas e privadas.
* Tempo médio de resposta para {{site.data.keyword.Bluemix_notm}} nos últimos 10 minutos, hora e dia.
* Transações médias por segundo para {{site.data.keyword.Bluemix_notm}} nos últimos 10 minutos, hora e dia.

### Visualizando relatórios
{: #oc_report}

É possível visualizar os logs e relatórios de segurança, como
DataPower&trade;, firewall, e auditoria de login, para a instância
do {{site.data.keyword.Bluemix_notm}}.

Para visualizar relatórios e logs, clique em
**ADMINISTRAÇÃO &gt; RELATÓRIOS E LOGS**.

Selecione a partir das opções a seguir:

* É possível selecionar as datas de início e de encerramento nos campos para filtrar quais relatórios e logs são
exibidos.
* É possível expandir e visualizar vários relatórios na área de janela de navegação.
* É possível procurar em sua coleção de relatórios e logs. A procura se aplica aos nomes de relatório
bem como ao conteúdo de texto contido nos logs e relatórios. Também é possível escolher filtrar sua procura por
**Eventos de administração**, **Relatórios do DataPower**,
**Firewall** e **Auditoria de login**.
* Ao exibir um relatório ou log, é possível clicar no ícone ![Download](images/icon_download.svg)
para fazer download do relatório.

### Visualizando o status
{: #oc_status}

É possível monitorar o status de sua instância do {{site.data.keyword.Bluemix_notm}} usando a página Status do {{site.data.keyword.Bluemix_notm}}. A página Status é o local central para localizar notificações e anúncios sobre os eventos principais que estão afetando a plataforma do {{site.data.keyword.Bluemix_notm}} e os serviços principais no {{site.data.keyword.Bluemix_notm}}.

É possível assinar um feed RSS para notificações de modo que não seja necessário verificá-las. Para obter mais informações sobre a página Status e a configuração do feed RSS, veja [Visualizando o {{site.data.keyword.Bluemix_notm}}](../troubleshoot/getting_customer_support.html#status).

### Gerenciando seu catálogo
{: #oc_catalog}

É possível gerenciar quais serviços e iniciadores do
{{site.data.keyword.Bluemix_notm}} ficarão visíveis
para usuários no catálogo do {{site.data.keyword.Bluemix_notm}}. Clique em **ADMINISTRAÇÃO &gt; GERENCIAMENTO DO CATÁLOGO**. 

Selecione um título de iniciador ou serviço para editar a visibilidade do plano do iniciador ou serviço. Para
editar a visibilidade, selecione dentre as opções a seguir:
* Para mostrar o serviço ou o iniciador oculto para que
ele fique visível para seus usuários no catálogo, selecione
**ATIVAR TODOS OS PLANOS**.
* Para ocultar o serviço ou o iniciador de seus usuários no
catálogo do {{site.data.keyword.Bluemix_notm}}, selecione
**DESATIVAR TODOS OS PLANOS**.
* Para controlar a visibilidade de um plano individual, selecione o nome do plano e, em seguida, use o menu suspenso para selecionar **Ativar para todas as organizações**, **Desativar para todas as organizações** ou **Ativar plano para organizações específicas**.

### Administrando as organizações
{: #oc_organizations}

Você pode gerenciar suas organizações criando e excluindo organizações, incluindo gerenciadores para organizações e monitorando o uso de cota.

Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DA ORGANIZAÇÃO**. 

É possível expandir e visualizar várias seções. Também é possível revisar e gerenciar os planos de cota para suas organizações.

* Para criar uma nova organização e incluir os gerenciadores, clique em <strong>CRIAR ORGANIZAÇÃO</strong>.
Insira um nome para a organização e, em seguida, digite o nome ou
e-mail da pessoa que deseja incluir como um gerente. É possível incluir mais de um gerenciador inserindo e selecionando múltiplos nomes. Clique em <strong>CRIAR ORGANIZAÇÃO</strong> para salvar suas mudanças e criar a organização.
* Na seção Monitoramento de cota, é possível expandir a seção e visualizar as informações a
seguir:
    * Uso de memória do ambiente. Esta seção detalha o uso de memória para o ambiente do sistema integral.
	O gráfico
fornece informações que incluem a memória do sistema usado, a memória do sistema total, a cota que é usada e a cota
total alocada. A lista de termos a seguir define os tipos de uso de memória que são exibidos no gráfico.
	<dl>
	<dt><strong>Memória do sistema usado</strong></dt>
	<dd>A memória física que é usada por seu ambiente.</dd>
	<dt><strong>Memória total do sistema</strong></dt>
	<dd>A memória física total disponível para seu ambiente.</dd>
	<dt><strong>Cota implementada</strong></dt>
	<dd>A soma de memória que é alocada para todos os apps implementados, em todas as organizações. A
soma da
	cota implementada pode exceder a memória total do sistema
físico para seu ambiente. Por exemplo, se você tiver uma memória total do
sistema de 16 GB e alocar 4 GB de memória cada num total de cinco organizações diferentes,
a cota total excede a memória total do sistema que foi alocada para todas as organizações. No entanto, em muitos
casos, as organizações podem não usar a cota total que é alocada individualmente para cada organização. Além disso,
todas as organizações podem não usar sua alocação de memória de cota total ao mesmo tempo. </dd>
	<dt><strong>Cota total</strong></dt>
	<dd>A memória total que é alocada em todas as organizações.</dd>
	</dl>
	* Uso de memória da organização. Esta seção detalha o uso de memória em um nível de organização. É possível
visualizar o abono da cota total e a cota que é implementada para cada organização. O gráfico fornece informações que
são listadas pelo mais alto uso de memória por organização e a organização que usa a maior quantia de memória, por
padrão, é listada primeiro. É possível classificar por **Mais alto uso de memória** e
**Excesso de alocação de memória**.
	<dl>
	<dt><strong>Mais alto uso de memória</strong></dt>
	<dd>Use esta opção para identificar a organização que usa a maior quantidade de memória. Classifique
pelo mais alto uso
	de memória para identificar as organizações que estão usando a maior quantia de memória. A lista é classificada pela cota
implementada. </dd>
	<dt><strong>Alocação de memória em excesso</strong></dt>
	<dd>Use esta opção para identificar as organizações que possuem um plano de cota que é maior do que o necessário.
	Classifique
por uso de memória em excesso para identificar as organizações que estão usando a menor quantia de memória para a cota
que foi alocada para a organização. </dd>
	</dl>
* Para mudar o plano de cota para uma organização, clique na
barra no gráfico da organização que você deseja editar na seção Uso
de memória da organização ou selecione o nome da organização a partir da
seção Lista de organização. Na página Editar organização, é possível mudar o
plano de cota, mudar o nome da organização e incluir ou remover gerenciadores. Se selecionar um plano de cota que não seja suficiente para o uso atual para a organização, receberá uma mensagem. Para
salvar qualquer mudança feita na página Editar organização,
clique em **SALVAR**.
* Na seção Lista da organização, você pode visualizar todas as organizações no
ambiente do {{site.data.keyword.Bluemix_notm}}.
	* Para excluir a organização, clique em
![Excluir](images/icon_trash.svg) na coluna Ações.
	* Para visualizar e editar o plano de cota para uma organização, clique no nome para a organização na lista.
	* Para editar o nome da organização e incluir ou remover os gerenciadores, clique no nome para a organização na lista.

### Gerenciando usuários e permissões
{: #oc_useradmin}

Você pode incluir usuários em sua instância do
{{site.data.keyword.Bluemix_notm}} a partir do registro de
usuário de sua empresa usando LDAP. É possível incluir usuários individualmente
ou em grupos e visualizar permissões do usuário. Se você estiver designado com a permissão `admin`,
também poderá configurar e gerenciar permissões para outros usuários. Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DE USUÁRIO**. 

A página Administração de usuário exibe todos os usuários da
instância local ou dedicada.
Permissões para cada usuário são exibidas. As permissões podem ser as seguintes: Nenhuma,
`Admin`, `Catalog`, `Login`,
`Reports` e `Users`. As permissões podem ser ativadas, ou o
usuário pode receber a capacidade `view` ou  `write` para essa
permissão, conforme representado por ícones. Consulte
[Permissões](#permissions) para obter descrições de cada tipo e explicação dos ícones.

Escolha a partir das opções a seguir:
* Localizar usuários. É possível localizar usuários na tabela usando o campo de **Procura**.
* Incluir usuários. Se você tiver a permissão `admin` ou
`users` com a capacidade `write`, poderá incluir usuários. Para incluir um usuário ou um grupo de usuários, clique em **INCLUIR ÚNICO USUÁRIO** ou **INCLUIR
GRUPO DE USUÁRIOS**. No campo **Procurar**, digite um nome de usuário ou um nome de grupo para
procurar e selecione a organização na qual incluir o usuário ou o grupo de usuários na
lista **Org.**. Ao localizar o usuário ou o grupo que deseja incluir, clique no
nome do usuário e, em seguida, clique em **INCLUIR USUÁRIO** ou **INCLUIR USUÁRIOS** para incluir.
Grupos de mais de 50 usuários são incluídos por meio de uma tarefa em lote de segundo plano. Quando a operação de inclusão
é bem-sucedida, o usuário ou o grupo é incluído na tabela para você visualizar e procurar. Quando os usuários são
incluídos, eles não possuem permissões designadas.
* Editar permissões e organizações. Se você tiver a permissão `admin`, poderá editar
permissões e organizações para outros usuários. Para editar permissões, localize o usuário e clique no nome do usuário. Para ativar ou desativar permissões, selecione as opções a seguir na janela que se abre:
	* Selecione **On** na lista para ativar uma permissão.
	* Selecione **Ler** na lista para permitir que o usuário tenha
capacidade `view` (somente leitura) para aquela permissão, ou **Gravar**
para permitir a capacidade `write` (editar, ou incluir e remover) para essa permissão.
	* Selecione **Off** para desativar a permissão.
Para editar organizações, selecione as opções a seguir:
	* Inclua o usuário em uma organização usando o campo de procura para localizar uma organização, clicando para selecionar a partir das opções e clicando em **INCLUIR**.
	* Remova um usuário de uma organização clicando no ícone ![Remover, representado por um sinal de menos](images/icon_remove.svg).
Ao concluir, clique em **SALVAR**.
* Remover usuários. Se você tiver a permissão `admin` ou
`users` com a capacidade `write`, poderá remover usuários.
Para remover um usuário, localize o usuário e clique no ícone ![Excluir](images/icon_trash.svg) e, em seguida, em **Remover**.

### Permissões
{: #permissions}

Os usuários podem ser designados com as permissões a seguir:

| **Permissão do usuário** | **Descrição** |       
|-----------------|-------------------|
| Administrador | Usuários com a permissão `admin` podem
editar permissões para outros usuários. |
| Catálogo | Usuários com a permissão `catalog`
podem ter a capacidade `view` ou
`write` (modificar) de quais serviços estão
disponíveis na instância local ou dedicada. |  
| Login | Usuários com permissão `login` podem ver a página Administração. Sem essa permissão, os usuários não podem ver a opção de menu Administração. |
| Relatórios | Usuários com a permissão `reports` podem ser designados com a capacidade para
visualizar (`view`) ou modificar (`write`) relatórios de segurança. |
| Usuários | Usuários com a permissão `users` podem ser designados com a capacidade para
visualizar (`view`) a lista de usuários ou modificar (`write`) (incluir ou remover) usuários. Essa permissão não permite configurar permissões para outros usuários.|

*Tabela 2. Permissões*

As permissões podem ser ativadas, ou o usuário pode receber a capacidade `view` ou
`write` para aquela permissão, conforme representado pelos ícones a seguir:

* O ícone ![Ativado,
representado por uma marca de seleção](images/icon_enabled.svg) ao lado de uma
permissão significa que ela está ativada.
* O ícone ![Visualizar, representado por um olho](images/icon_read.svg) significa que o usuário possui a capacidade `view` (somente leitura) para aquela
permissão.
* O ícone ![Gravar, representado por um lápis](images/icon_write.svg) significa que o usuário possui a capacidade `write` (editar, incluir ou remover) para
aquela permissão.

### Gerenciando usuários com a API REST Admin
{: #usingadminapi}

É possível usar a API REST `Admin` para
incluir e remover usuários de sua instância do {{site.data.keyword.Bluemix_notm}}.
Os terminais da API REST `Admin` e respostas JSON são fornecidos numa base experimental para ativar as operações básicas a partir de uma linha de comandos. Os terminais e URLs nos exemplos nessas informações podem mudar ou podem ser descontinuados em breve.

As ferramentas a seguir são pré-requisitos para usar os exemplos abaixo. É possível optar por
            usar outras ferramentas também.
* cURL, para inserir solicitações API REST como comandos. cURL é um utilitário grátis que pode
                    ser usado para enviar solicitações de HTTP para um servidor e receber as respostas
                    do servidor por meio de uma interface de linha de comandos. É
possível fazer o download de cURL a partir do
[site de download de cURL](http://curl.haxx.se/download.html){: new_window}.
* Python, para usar a ferramenta JSON de pretty-print do Python. Essa ferramenta opcional considera o texto JSON como entrada e fornece saída fácil de ler. Você
pode fazer o download do Phython no
[site de downloads de
Python](https://www.python.org/downloads){: new_window}.

#### Efetuando login no Console administrativo

Antes que quaisquer solicitações de API `Admin` possam ser executadas, deve-se efetuar login no Console administrativo. Se você tiver a permissão `admin` ou
`users` com a capacidade `write`, poderá incluir ou remover usuários. Deve-se ter permissão `admin` para editar permissões de outros usuários.

Para efetuar login no Console administrativo, é possível usar a
autenticação de acesso básico no terminal `https://<your_host>.ibm.com/login`. O servidor retorna um cookie com a sua sessão. Use esse cookie para todas as operações com o Console administrativo.

**Nota:** A sessão se torna inválida se não usada por algumas horas.

Para efetuar login no Console administrativo, execute o comando a seguir:

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://<your_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">Aceita o ID de usuário e a senha e envia um cabeçalho de Autorização básica.</dd>


<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">Armazena o ID de usuário e a senha especificados como um cookie no arquivo especificado.</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">Envia um cabeçalho Aceitar.</dd>

</dl>

O exemplo a seguir mostra a saída a partir deste
                comando:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

#### Listando organizações
{: #listingorg}

Ao incluir um usuário, você deve especificar uma organização. É possível usar a API REST `Admin` para listar todas as organizações. Você
deve ter a permissão `users` com a
capacidade `read` para listar organizações. Para
listar todas as organizações, execute o seguinte comando:

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passa o ID de usuário e a senha que foram armazenados previamente com a opção <samp class="ph codeph">-c</samp> no arquivo para o servidor HTTP como um cookie.</dd>

</dl>

Para cada organização, os resultados incluem as informações a seguir
* `"guid"`, GUID da organização
* `"name"`, nome da organização

O exemplo a seguir mostra a saída a partir deste
                comando:
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

#### Listando usuários
{: #listingusr}

É possível determinar se um usuário já foi incluído no
ambiente do {{site.data.keyword.Bluemix_notm}} usando
a API REST `Admin` para listar usuários registrados. Deve-se ter permissão
`users` com a capacidade `read`
para listar usuários registrados. Para listar todos os usuários,
execute o seguinte comando:

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passa o ID de usuário e a senha que foram armazenados previamente com a opção <samp class="ph codeph">-c</samp> no arquivo para o servidor HTTP como um cookie.</dd>
</dl>

Para cada usuário registrado, os resultados incluem as informações a seguir
* `"first_name"` (nome) e `"last_name"` (sobrenome)
* `"user_id"`, ID de usuário e endereço de e-mail
* `"guid"`, GUID da organização.
* `"permissions"` que são designadas ao usuário para o Console administrativo.

O exemplo a seguir mostra a saída a partir deste
                comando:

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

#### Incluindo um usuário

É possível usar a API REST `Admin` para
incluir usuários na instância do {{site.data.keyword.Bluemix_notm}}. Deve-se ter permissão `users` com capacidade de `write` para incluir usuários.

Você pode incluir um usuário ou uma lista de usuários. Você
pode incluir usuários em uma única organização, ou em diversas organizações.-->Para incluir um usuário, você deve fornecer as seguintes informações:

* Primeiro nome (nome) e último nome (sobrenome) do usuário. Forneça
`"first_name"` e `"last_name"` em
[Listando usuários](index.html#listingusr).
* Endereço de e-mail e ID de usuário: forneça
`"user_id"` em
[Listando usuários](index.html#listingusr) para o
endereço de e-mail e o ID de usuário.
* `"guid"`. Forneça o GUID da organização em
[Listando organizações](index.html#listingorg).

Forneça as informações em um arquivo JSON.

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passa o ID de usuário e a senha que foram armazenados previamente com a opção <samp class="ph codeph">-c</samp> no arquivo para o servidor HTTP como um cookie.</dd>
</dl>

<ol>
<li>Crie um arquivo JSON que contenha as informações em um formato JSON apropriado.
<p>Por exemplo, crie um arquivo nomeado `user.json` que possua o conteúdo a seguir:</p>
<pre>
{
    "members": [
        {
            "emails": [
                "some_user_id@domain.com"
            ],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Poste o conteúdo do arquivo JSON para o terminal do usuário
executando o seguinte comando:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">Especifica a saída detalhada.</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Especifica uma solicitação POST, substituindo a solicitação GET padrão.</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Especifica o cabeçalho do tipo de conteúdo que, nesse caso, é JSON.</dd>


<dt class="pt dlterm">-d *data*</dt>
<dd class="pd">Especifica os dados, nesse caso, o arquivo `user.json`, a ser enviado na solicitação POST para o servidor HTTP.</dd>

</dl>



O exemplo a seguir mostra a saída a partir deste
                comando:

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

#### Removendo um usuário

É possível usar a API REST `Admin` para
remover usuários da instância do {{site.data.keyword.Bluemix_notm}}. Deve-se ter permissão `users` com capacidade de `write` para remover usuários.

Para remover um usuário, deve-se fornecer o ID de usuário do usuário. Execute o comando a seguir:

`curl -v -b ./cookies.txt -X DELETE https://<your_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Especifica uma solicitação DELETE.</dd>
</dl>

O exemplo a seguir mostra a saída a partir deste
                comando:

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

### API de serviço customizado
{: #servicebrokerapi}

Há três APIs que podem ser usadas para registrar ou criar um novo serviço, atualizar um serviço e excluir um serviço.

Todas as APIs são relativas a <code>https://opsconsole.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>Este valor é o nome da sua instância local ou dedicada. O nome de
subdomínio de sua instância do {{site.data.keyword.Bluemix}}
foi designado durante o onboarding.</dd>
</dl>

### Registrando um novo serviço

Use a API a seguir e os exemplos de código para registrar um novo serviço.

#### Rotear

```
POST /codi/v1/serviceBrokers
```
{: screen}

#### Pedido

*Tabela 3. Campos*

| **Nome** | **Descrição** |
|-----------------|-------------------|
| Nome | Nome do broker de serviço. |
| auth_username | Nome do usuário usado para conectar ao broker de serviço. |
| auth_password | Senha usada para conectar ao broker de serviço. |
| broker_url | URL usada para conectar ao broker de serviço. |
| owningOrganization | Organização inicial para incluir o serviço na lista de desbloqueio. |

##### Corpo

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### Cabeçalhos

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Resposta

##### Barra de Status

```
201 Criado
```
{: screen}

##### Corpo

```
{
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

### Atualizando um serviço

Use a API a seguir e os exemplos de código para atualizar um serviço.

#### Rotear

`PUT /codi/v1/serviceBrokers`
{: screen}

#### Pedido

*Tabela 4. Campos*

| **Nome** | **Descrição** |
|-----------------|-------------------|
| Nome | Nome do broker de serviço. O nome com que esse serviço foi criado não pode ser mudado. |
| auth_username | Nome do usuário usado para conectar ao broker de serviço. |
| auth_password | Senha usada para conectar ao broker de serviço. |
| broker_url | URL usada para conectar ao broker de serviço. |
| owningOrganization | Organização inicial para incluir o serviço na lista de desbloqueio. |

##### Corpo

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### Cabeçalhos

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Resposta

##### Barra de Status

```
201 Criado
```
{: screen}

##### Corpo

```
{
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

### Excluindo um serviço

Use a API a seguir e os exemplos de código para excluir um serviço.

*Tabela 5. Parâmetro*

| **Nome** | **Descrição** |
|-----------------|-------------------|
| Nome | Nome do broker de serviço. O nome com que esse serviço foi criado não pode ser mudado. |

#### Rotear

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

#### Pedido

##### Cabeçalhos

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Resposta

##### Barra de Status

```
204 Sem conteúdo
```
{: screen}

### Gerenciando usuários com a CLI cf
{: #usingadmincli}

É possível gerenciar usuários para o ambiente do seu
{{site.data.keyword.Bluemix_notm}} Local ou {{site.data.keyword.Bluemix_notm}} Dedicated usando
a interface da linha de comandos do Cloud Foundry com o plug-in
da CLI Admin do {{site.data.keyword.Bluemix_notm}}. Por
exemplo, é possível incluir usuários a partir de um registro LDAP.

Antes de iniciar, instale a interface de linha de comandos do cf. O plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}
requer o cf versão 6.11.2 ou posterior. [Download
da interface de linha de comandos do Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restrição:** A interface de linha de
comandos do Cloud Foundry não é suportada por
Cygwin. Use a interface de linha de comandos do Cloud Foundry
em uma janela de linha de comandos diferente da janela de linha de comandos do Cygwin.

#### Incluindo o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}

Após a interface de linha de comandos do cf ser instalada, é possível
incluir o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}.

Conclua as etapas a seguir para incluir o repositório e instalar
o plug-in:

<ol>
<li>Para incluir o repositório de plug-in de administrador do {{site.data.keyword.Bluemix_notm}}, execute o comando a seguir: <br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Subdomínio da URL da sua instância do
{{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Para instalar o plug-in CLI admin do
{{site.data.keyword.Bluemix_notm}}, execute o seguinte
comando:<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Para ver uma lista de comandos, execute o comando
a seguir:

`cf plugins`
{: codeblock}

Para obter ajuda adicional para um comando, use a opção `-help`.

Para obter mais informações sobre como trabalhar com o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}, veja  [Admin do {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html).
