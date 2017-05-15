---

copyright:

  years: 2015, 2017

lastupdated: "2017-02-20"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI do administrador do {{site.data.keyword.Bluemix_notm}}
{: #bluemixadmincli}


É possível gerenciar o seu ambiente do {{site.data.keyword.Bluemix_notm}} Local ou do {{site.data.keyword.Bluemix_notm}} Dedicated
usando a interface de linha de comandos do Cloud Foundry com o plug-in da CLI do Administrador do {{site.data.keyword.Bluemix_notm}}. Por
exemplo, é possível incluir usuários a partir de um registro LDAP. Se estiver procurando informações sobre como gerenciar sua conta do {{site.data.keyword.Bluemix_notm}} Public, consulte [Administrando](/docs/admin/adminpublic.html#administer).

Antes de iniciar, instale a interface de linha de comandos do cf. O plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}
requer o cf versão 6.11.2 ou posterior. [Fazer download da interface da linha de comandos do Cloud Foundry ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restrição:** A interface de linha de
comandos do Cloud Foundry não é suportada por
Cygwin. Use a interface de linha de comandos do Cloud Foundry
em uma janela de linha de comandos diferente da janela de linha de comandos do Cygwin.

**Observação**: a CLI do administrador do {{site.data.keyword.Bluemix_notm}} é usada somente para o ambiente {{site.data.keyword.Bluemix_notm}} Local e {{site.data.keyword.Bluemix_notm}} Dedicated. Ele não é suportado pelo {{site.data.keyword.Bluemix_notm}} Public.

## Incluindo o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}

Após a interface de linha de comandos do cf ser instalada, é possível
incluir o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}.

**Nota**: se você tiver instalado
anteriormente o plug-in Administrador do
{{site.data.keyword.Bluemix_notm}}, poderá ser necessário desinstalar o plug-in, excluir o repositório e reinstalar para obter as atualizações mais recentes.

Conclua as etapas a seguir para incluir o repositório e instalar
o plug-in:

<ol>
<li>Para incluir o repositório do plug-in de administrador do {{site.data.keyword.Bluemix_notm}}, execute o comando a seguir:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
</li>
<li>Para instalar o plug-in da CLI do Administrador do {{site.data.keyword.Bluemix_notm}}, execute o comando a seguir:<br/><br/>
<code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

Se você precisar desinstalar o plug-in, será possível usar os comandos a seguir; em
seguida, poderá incluir o repositório atualizado e instalar o plug-in mais recente:

* Desinstalar o plug-in: `cf uninstall-plugin BluemixAdminCLI`
* Remover o repositório de plug-in: `cf remove-plugin-repo BluemixAdmin`


## Usando o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}

É possível usar o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}} para incluir ou remover usuários, designar ou remover designação de usuários de organizações e
executar outras tarefas de gerenciamento.

Para ver uma lista de comandos, execute o comando
a seguir:

```
cf plugins
```
{: codeblock}

Para obter ajuda adicional para um comando, use a opção `-help`.

### Conectando e efetuando login no {{site.data.keyword.Bluemix_notm}}

Antes de poder usar o plug-in da CLI do Administrador, deverá conectar e efetuar login, se
ainda não fez isso.

<ol>
<li>Para conectar-se ao terminal da API do {{site.data.keyword.Bluemix_notm}}, execute o comando a seguir:<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Subdomínio da URL da sua instância do {{site.data.keyword.Bluemix_notm}}.<br />
</dd>
</dl>
<p>É possível verificar a página Recursos e informações do Console
administrativo para a URL correta. A URL é mostrada
na seção Informações da API no campo **URL da API**.</p>
</li>
<li>Efetue login no {{site.data.keyword.Bluemix_notm}} com o comando a seguir:<br/><br/>
<code>
cf login
</code>
</li>
</ol>

## Administrando Usuários
{: #admin_users}

### Incluindo um usuário
{: #admin_add_user}

Para incluir um usuário em seu ambiente do {{site.data.keyword.Bluemix_notm}} a partir do
registro do usuário de seu ambiente, use o comando a seguir:

```
cf ba add-user <user_name> <organization> <first_name> <last_name>
```
{: codeblock}

**Observação**: para incluir um usuário em uma organização específica, deve-se ser um **Administrador** com a permissão **users.write** (ou **Super usuário**). Se você for um gerenciador de organização, também poderá receber a capacidade de incluir usuários em sua organização por um Super usuário que executa o comando **enable-managers-add-users**.  Consulte [Ativando gerenciadores para incluir usuários](index.html#clius_emau) para obter mais informações.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no registro LDAP.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou GUID da organização do {{site.data.keyword.Bluemix_notm}} na qual incluir o usuário.</dd>
<dt class="pt dlterm">&lt;first_name&gt;</dt>
<dd class="pd">O nome do usuário a ser incluído na organização.</dd>
<dt class="pt dlterm">&lt;last_name&gt;</dt>
<dd class="pd">O sobrenome do usuário a ser incluído na organização.</dd>
</dl>

**Dica:** também é possível usar **ba au** como um alias para o nome do comando mais longo **ba add-user**.

<!-- staging-only commands start. Live for interconnect -->

### Procurando um usuário
{: #admin_search_user}

Para procurar um usuário, use o comando a seguir em conjunção com os parâmetros de filtro de procura opcionais
(nome, permissão, organização e função):

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name_value&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}. </dd>
<dt class="pt dlterm">&lt;permission_value&gt;</dt>
<dd class="pd">A permissão designada ao usuário. Por exemplo, superusuário, básico, catálogo, usuário e relatórios. Para obter mais informações sobre permissões de usuário designadas, veja [Permissões](/docs/admin/index.html#permissions). Não é possível usar esse parâmetro com o parâmetro de organização na mesma consulta. </dd>
<dt class="pt dlterm">&lt;organization_value&gt;</dt>
<dd class="pd">O nome da organização à qual o usuário pertence. Não é possível usar esse parâmetro com o parâmetro de permissão na mesma consulta.</dd>
<dt class="pt dlterm">&lt;role_value&gt;</dt>
<dd class="pd">A função de organização designada ao usuário. Por exemplo, gerente, gerente de faturamento ou auditor para a organização. Deve-se especificar a organização com esse parâmetro. Para obter mais informações sobre funções, veja [Funções de usuário](/docs/admin/users_roles.html#userrolesinfo).</dd>

</dl>

**Dica:** também é possível usar **ba su** como um alias para o nome do comando mais longo **ba search-users**.

### Configurando permissões para um usuário
{: #admin_setperm_user}

Para configurar permissões para um usuário especificado, use o comando a seguir:

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**Nota**: é possível configurar uma permissão por vez.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">Configure as permissões para o usuário: Administrador (a alternativa
disponível é Super usuário), Login (a alternativa disponível é Básico), Catálogo (acesso
de leitura ou gravação), Relatórios (acesso de leitura ou gravação) ou Usuários
(acesso de leitura ou gravação).</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">Para permissões de Catálogo, Relatórios ou Usuários, deve-se também configurar o nível de acesso como <code>read</code> ou <code>write</code>.</dd>
</dl>

**Dica:** também é possível usar **ba sp** como um alias para o nome do comando mais longo **ba set-permissions**.

<!-- staging-only commands end -->

### Removendo um usuário
{: #admin_remov_user}

Para remover um usuário de seu ambiente do {{site.data.keyword.Bluemix_notm}}, use o comando a seguir:

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Dica:** também é possível usar **ba ru** como um alias para o nome do comando mais longo **ba remove-user**.

### Ativando gerenciadores para incluir usuários
{: #clius_emau}

Se você tiver a permissão **Super usuário** em seu ambiente {{site.data.keyword.Bluemix_notm}}, poderá ativar os gerenciadores de organização para incluir usuários na organização que eles gerenciam. Para
permitir que os gerenciadores incluam usuários, use o comando a seguir:

```
cf ba enable-managers-add-users
```
{: codeblock}

**Dica:** também é possível usar **ba emau** como um alias para o nome mais longo do comando **ba enable-managers-add-users**.

### Desativando gerenciadores de incluir usuários
{: #clius_dmau}

Se os gerenciadores de organização foram ativados para incluir usuários em organizações que eles gerenciam em seu ambiente do {{site.data.keyword.Bluemix_notm}} com o comando **enable-managers-add-users** e se você tiver a permissão **Super usuário**,
será possível remover essa configuração.  Para desativar os usuários de incluírem usuários, use o comando a seguir:

```
cf ba disable-managers-add-users
```
{: codeblock}

**Dica:** também é possível usar **ba dmau** como um alias para o nome mais longo
do comando **ba disable-managers-add-users**.

## Administrando as organizações
{: #admin_orgs}

### Incluindo uma Organização
{: #admin_add_org}

Para incluir uma organização, use o comando a seguir:

```
cf ba create-org <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} a ser incluída.</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">O nome do usuário do gerenciador para a organização.</dd>
</dl>

**Dica:** também é possível usar **ba co** como um alias para o nome
do comando mais longo **ba create-org**.

### Excluindo uma Organização
{: #admin_delete_org}

Para excluir uma organização, use o comando a seguir:

```
cf ba delete-org <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} a ser excluída.</dd>
</dl>

**Dica:** também é possível usar **ba do** como um alias para o nome
do comando mais longo **ba delete-org**.

### Designando um usuário a uma organização
{: #admin_ass_user_org}

Para designar um usuário em seu ambiente do {{site.data.keyword.Bluemix_notm}} para uma
determinada organização, use o comando a seguir:

```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou GUID da organização do {{site.data.keyword.Bluemix_notm}} para a qual designar o usuário.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">Consulte [Funções](/docs/admin/users_roles.html) para obter
funções e descrições do usuário do {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

**Dica:** também é possível usar **ba so** como um alias para o nome do comando mais longo **ba set-org**.

### Removendo a designação de um usuário de uma organização
{: #admin_unass_user_org}

Para remover a designação de um usuário em seu ambiente do {{site.data.keyword.Bluemix_notm}} de
uma determinada organização, use o comando a seguir:

```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou GUID da organização do {{site.data.keyword.Bluemix_notm}} para a qual designar o usuário.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">Consulte [Atribuindo funções](/docs/admin/users_roles.html) para
obter funções de usuário e descrições do {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

**Dica:** também é possível usar **ba uo** como um alias para o nome do comando mais longo **ba unset-org**.

#### Designando funções

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Gerenciador de organização. Um gerenciador de organização possui autoridade para executar as ações a seguir:
<ul>
<li>Criam ou excluem espaços dentro da organização.</li>
<li>Convidar usuários para a organização e gerenciar usuários.</li>
<li>Gerenciam domínios da organização.</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">Gerenciador de faturamento. Um gerenciador de faturamento pode visualizar informações de tempo de execução e de uso do serviço para a
organização.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Auditor da organização. Um auditor da organização pode visualizar conteúdo do aplicativo e do serviço no
espaço.</dd>
</dl>

### Configurando uma cota para uma organização
{: #admin_set_org_quota}

Para configurar a cota de uso para uma determinada organização, use o comando a seguir:

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} para a qual configurar a cota.</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">O plano da cota para uma organização.</dd>
</dl>

**Dica:** também é possível usar **ba sq** como um alias para o nome do comando mais longo **ba set-quota**.


### Localizando cotas de contêiner para uma organização
{: #admin_find_containquotas}

Para localizar a cota para contêineres para uma organização, use o comando a seguir:

```
cf bluemix-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou ID da organização no Bluemix. Esse parâmetro
é obrigatório.</dd>
</dl>

**Dica:** também é possível usar **ba cq** como um alias para o nome mais longo
do comando **bluemix-admin containers-quota**.

### Configurando cotas de contêiner para uma organização
{: #admin_set_containquotas}

Para configurar a cota para contêineres em uma organização, use o comando a seguir com pelo menos uma das opções incluídas:

```
cf bluemix-admin set-containers-quota <organization> <options>
```
{: codeblock}

**Nota**: é possível incluir múltiplas opções, mas deve-se incluir pelo menos uma.

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou ID da organização no Bluemix. Esse parâmetro
é obrigatório.</dd>
<dt class="pt dlterm">&lt;options&gt;</dt>
<dd class="pd">Inclua uma ou mais das opções a seguir em que o valor deve ser um número inteiro:
<ul>
<li>floating-ips-max &lt;value&gt;</li>
<li>floating-ips-space-default &lt;value&gt;</li>
<li>memory-max &lt;value&gt;</li>
<li>memory-space-default &lt;value&gt;</li>
<li>image-limit &lt;value&gt;</li>
</ul>
</dd>
</dl>

**Dica:** também é possível usar os nomes abreviados a seguir como um alias para os nomes
mais longos de opções:
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;value&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;value&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;value&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

Opcionalmente, é possível fornecer um arquivo contendo parâmetros de configuração específicos em um objeto JSON válido. Se você usar a opção **-file**, ela terá precedência e as outras opções serão ignoradas. Para
fornecer um arquivo em vez de configurar as opções, use o comando a seguir:

```
cf bluemix-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

O arquivo JSON deve ter o formato mostrado no exemplo a seguir:

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**Dica:** também é possível usar **ba scq** como um alias para o nome mais longo
do comando **bluemix-admin set-containers-quota**.

## Administrando Espaços
{: #admin_spaces}

### Incluindo um espaço na organização

Para incluir um espaço na organização, use o comando a seguir:

```
cf bluemix-admin create-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou GUID da organização na qual o espaço deve ser incluído.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">O nome do espaço que deve ser criado na organização.</dd>
</dl>

**Dica:** também é possível usar **ba cs** como um alias para o nome
do comando mais longo **ba create-space**.

### Excluindo um espaço da organização

Para remover um espaço da organização, use o comando a seguir:

```
cf bluemix-admin delete-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou GUID da organização da qual o espaço deve ser removido.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">O nome do espaço que deve ser removido da organização.</dd>
</dl>

**Dica:** também é possível usar **ba cs** como um alias para o nome
do comando mais longo **ba delete-space**.

### Incluindo um usuário em um espaço com uma função

Para criar um usuário em um espaço com uma função especificada, use o comando a seguir:

```
cf bluemix-admin set-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou GUID da organização na qual o usuário deve ser incluído.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">O nome do espaço no qual o usuário deve ser incluído.</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">O nome do usuário que deve ser incluído.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">A função do usuário que deve ser designada. O valor pode ser Gerenciador, Desenvolvedor ou Auditor. Veja [Designando funções](/docs/admin/users_roles.html) para
funções de usuário e descrições
do {{site.data.keyword.Bluemix_notm}} em um espaço.</dd>
</dl>

**Dica:** também é possível usar **ba ss** como um alias para o nome
do comando mais longo **ba set-space**.


### Removendo a função de um usuário em um espaço 

Para remover a função de um usuário em um espaço, use o comando a seguir:

```
cf bluemix-admin unset-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou GUID da organização na qual o usuário deve ser incluído.</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">O nome do espaço no qual o usuário deve ser incluído.</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">O nome do usuário que deve ser incluído.</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">A função do usuário que deve ser designada. O valor pode ser Gerenciador, Desenvolvedor ou Auditor. Veja [Designando funções](/docs/admin/users_roles.html) para
funções de usuário e descrições
do {{site.data.keyword.Bluemix_notm}} em um espaço.</dd>
</dl>

**Dica:** também é possível usar **ba us** como um alias para o nome
do comando mais longo **ba unset-space**.

## Administrando o catálogo
{: #admin_catalog}

### Ativando serviços para todas as organizações
{: #admin_ena_service_org}

Para ativar um serviço para ser exibido no Catálogo do
{{site.data.keyword.Bluemix_notm}} para todas as
organizações, use o comando a seguir:

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do plano de serviço que você deseja ativar. Se você
inserir um nome de plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico", será
solicitado que escolha a partir dos planos de serviços. Para identificar um nome do plano de serviço, selecione a categoria de serviço a partir da página inicial, em seguida, selecione
**Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de serviços
que estão disponíveis para esse serviço. </dd>
</dl>

**Dica:** também é possível usar **ba esp** como um alias para o nome do comando mais longo **ba enable-service-plan**.

### Desativando serviços para todas as organizações
{: #admin_dis_service_org}

Para desativar um serviço de ficar visível no Catálogo do {{site.data.keyword.Bluemix_notm}} para todas
as organizações, use o comando a seguir:

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do plano de serviço que você deseja ativar. Se você
inserir um nome de plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico", será
solicitado que escolha a partir dos planos de serviços. Para identificar um nome do plano de serviço, selecione a categoria de serviço a partir da página inicial, em seguida, selecione
**Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de
serviços que estão disponíveis para esse serviço.</dd>
</dl>

**Dica:** também é possível usar **ba dsp** como um alias para o nome do comando mais longo **ba disable-service-plan**.

### Incluindo a visibilidade de serviço para organizações
{: #admin_addvis_service_org}

É possível incluir uma organização da lista de organizações que podem ver um serviço específico no Catálogo do {{site.data.keyword.Bluemix_notm}}. Para permitir que uma organização visualize um serviço específico no
Catálogo do {{site.data.keyword.Bluemix_notm}}, use o comando a seguir:

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do plano de serviço que você deseja ativar. Se você
inserir um nome de plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico", será
solicitado que escolha a partir dos planos de serviços. Para identificar um nome do plano de serviço, selecione a categoria de serviço a partir da página inicial, em seguida, selecione
**Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de
serviços que estão disponíveis para esse serviço.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} a ser incluída na lista de visibilidade do serviço.</dd>
</dl>

**Dica:** também é possível usar **ba aspv** como um alias para o nome do comando mais longo **ba add-service-plan-visibility**.

### Removendo a visibilidade de serviço para organizações
{: #admin_remvis_service_org}

É possível remover uma organização da lista de organizações que podem ver um
serviço específico no Catálogo do {{site.data.keyword.Bluemix_notm}}. Para remover a visibilidade de um serviço no
Catálogo do {{site.data.keyword.Bluemix_notm}} para uma organização, use o comando a seguir:

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do plano de serviço que você deseja ativar. Se você
inserir um nome de plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico", será
solicitado que escolha a partir dos planos de serviços. Para identificar um nome do plano de serviço, selecione a categoria de serviço a partir da página inicial, em seguida, selecione
**Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de
serviços que estão disponíveis para esse serviço.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} a ser removida da
lista de visibilidade do serviço.</dd>
</dl>

**Dica:** também é possível usar **ba rspv** como um alias para o nome do comando mais longo **ba remove-service-plan-visibility**.

### Editando a visibilidade de serviço para organizações
{: #admin_editvis_service_org}

É possível editar e substituir a lista de serviços que as organizações
específicas podem ver no Catálogo do {{site.data.keyword.Bluemix_notm}}. Para substituir todos os serviços visíveis existentes para uma organização ou múltiplas organizações, use o comando a seguir:

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**Nota:** Esse comando substitui os serviços
visíveis existentes para as organizações especificadas pelo serviço
que você especifica no comando.

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do plano de serviço que você deseja ativar. Se você
inserir um nome de plano de serviço não exclusivo, por exemplo, "Padrão" ou "Básico", será
solicitado que escolha a partir dos planos de serviços. Para identificar um nome do plano de serviço, selecione a categoria de serviço a partir da página inicial, em seguida, selecione
**Incluir** para visualizar os serviços para essa categoria. Clique no nome do serviço para abrir a visualização de detalhes e, então, será possível visualizar os nomes dos planos de
serviços que estão disponíveis para esse serviço.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} para a qual incluir a visibilidade. É
possível ativar a visibilidade do serviço para mais de uma organização, inserindo GUIDs ou nomes adicionais da
organização no comando.</dd>
</dl>

**Dica:** também é possível usar **ba espv** como um alias para o nome do comando mais longo **ba edit-service-plan-visibility**.

## Administrando relatórios
{: #admin_add_report}

### Incluindo Relatórios
{: #admin_add_report}

Para incluir um relatório de segurança, use o comando a seguir:

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**Nota**: Se você tiver acesso de gravação para a permissão de relatórios, poderá criar uma nova categoria e incluir um relatório em qualquer um dos formatos aceitos para seus usuários. Insira
o novo nome da categoria para o parâmetro `category` ou inclua o seu novo relatório em uma categoria existente.

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">A categoria para o relatório. Se houver um espaço no nome, use as aspas em torno do nome.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">A data do relatório no formato <samp class="ph codeph">YYYYMMDD</samp>.</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">O caminho para o PDF do relatório, arquivo de texto ou arquivo de log para upload.</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">Uma opção para incluir uma versão do Rich Text Format (RTF) do PDF. Essa opção se aplica somente se você incluiu
um caminho no PDF do relatório. A versão RTF é usada para indexação e procura.</dd>
</dl>

**Dica:** também é possível usar **ba ar** como um alias para o nome do comando mais longo **ba add-report**.

### Excluindo relatórios
{: #admin_del_report}

Para excluir um relatório de segurança, use o comando a seguir:

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">A categoria para o relatório. Se houver um espaço no nome, use as aspas em torno do nome.</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd">A data do relatório no formato <samp class="ph codeph">YYYYMMDD</samp>.</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">O nome do relatório.</dd>
</dl>

**Dica:** também é possível usar **ba dr** como um alias para o nome do comando mais longo **ba delete-report**.

### Recuperando relatórios
{: #admin_retr_report}

Para recuperar um relatório de segurança, use o comando a seguir:

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">O nome do arquivo do relatório. Se houver um espaço no nome, use as aspas em torno do nome.</dd>
</dl>

**Dica:** também é possível usar **ba rr** como um alias para o nome do comando mais longo **ba retrieve-report**.

## Visualizando informações de métrica de recurso
{: #cliresourceusage}

É possível visualizar informações de métrica de recurso, incluindo memória, disco e uso de CPU. É possível ver um resumo dos recursos físicos e reservados disponíveis, bem como o uso de recursos físicos e reservados. Também é possível ver dados de uso de Droplet Execution Agents (DEAs) e células e uso histórico de memória e disco. Os dados históricos para uso de memória e disco são exibidos semanalmente e em ordem decrescente, por padrão. Para visualizar as informações de métrica de recurso, use o comando a seguir:

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;monthly&gt;</dt>
<dd class="pd">Visualize os dados históricos de espaço em memória e em disco um mês de cada vez.</dd>
<dt class="pt dlterm">&lt;weekly&gt;</dt>
<dd class="pd">Visualize os dados históricos de espaço em memória e em disco uma semana de cada vez. Este é o valor
padrão.</dd>
</dl>

**Dica:** também é possível usar **ba rsm** como um alias para o nome mais longo
do comando **ba resource-metrics**.


## Administrando brokers de serviço
{: #admin_servbro}

### Listando brokers de serviço
{: #clilistservbro}

Para listar todos os brokers de serviço, use o comando a seguir:

```
cf ba service-brokers <broker_name>
```
{: codeblock}

**Nota**: para listar todos os brokers de serviço, insira o comando sem o parâmetro `broker_name`.

<dl class="parml">
<dt class="pt dlterm">&lt;nome_do_servidor_intermediário&gt;</dt>
<dd class="pd">Opcional: o nome do broker de serviço customizado. Use esse parâmetro se desejar obter informações de um broker de serviço específico.</dd>
</dl>

**Dica:** também é possível usar **ba sb** como um alias para o nome do comando mais longo **ba service-brokers**.

### Incluindo um broker de serviço
{: #cliaddservbro}

Para incluir um broker de serviço, de maneira que você possa incluir um serviço customizado em seu
Catálogo do {{site.data.keyword.Bluemix_notm}}, use o comando a seguir:

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_do_servidor_intermediário&gt;</dt>
<dd class="pd">O nome do broker de serviço customizado.</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário para a conta que tem acesso ao broker de serviço.</dd>
<dt class="pt dlterm">&lt;senha&gt;</dt>
<dd class="pd">A senha para a conta que tem acesso ao broker de serviço.</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">A URL para o broker de serviço.</dd>
</dl>

**Dica:** também é possível usar **ba asb** como um alias para o nome do comando mais longo **ba add-service-broker**.

### Excluindo um broker de serviço
{: #clidelservbro}

Para excluir um broker de serviço, para remover o serviço customizado de seu
Catálogo do {{site.data.keyword.Bluemix_notm}}, use o comando a seguir:

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">O nome ou o guid do broker de serviço customizado.</dd>
</dl>

**Dica:** também é possível usar **ba dsb** como um alias para o nome do comando mais longo **ba delete-service-broker**.

### Atualizando um broker de serviço
{: #cliupdservbro}

Para atualizar um broker de serviço, use o comando a seguir:

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_do_servidor_intermediário&gt;</dt>
<dd class="pd">O nome do broker de serviço customizado.</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário para a conta que tem acesso ao broker de serviço.</dd>
<dt class="pt dlterm">&lt;senha&gt;</dt>
<dd class="pd">A senha para a conta que tem acesso ao broker de serviço.</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">A URL para o broker de serviço.</dd>
</dl>

**Dica:** também é possível usar **ba usb** como um alias para o nome do comando mais longo **ba update-service-broker**.


## Administrando grupos de segurança do aplicativo
{: #admin_secgro}

Para trabalhar com grupos de segurança do aplicativo (ASGs), você deve ser um
administrador com acesso total para o ambiente local ou dedicado. Todos os usuários do
ambiente podem listar os ASGs disponíveis para a organização que está sendo alvo com o
comando. No entanto, para criar, atualizar ou ligar ASGs, você deve ser um
administrador do ambiente {{site.data.keyword.Bluemix_notm}}.

Os ASGs funcionam como firewalls virtuais que controlam o tráfego de saída dos
aplicativos no ambiente do {{site.data.keyword.Bluemix_notm}}. Cada ASG consiste
em uma lista de regras que permitem tráfego e comunicação específicos de/para a
rede externa. É possível ligar um ou mais ASGs a um conjunto de grupos de segurança
específicos, por exemplo, um conjunto de grupos usado para aplicar acesso global ou
você pode ligar aos espaços dentro de uma organização em seu ambiente do
{{site.data.keyword.Bluemix_notm}}.

O {{site.data.keyword.Bluemix_notm}} é configurado inicialmente com todos
os acessos à rede externa restrita. Dois grupos de segurança criados pela IBM,
`public_networks` e `dns`, permitem acesso global à
rede externa quando você liga esses grupos aos conjuntos de grupos de segurança padrão do
Cloud Foundry. Os dois conjuntos de grupos de segurança no Cloud Foundry que são usados
para aplicar acesso global são **Preparação padrão** e
**Execução padrão**. Esses conjuntos de grupos aplicam as regras para
permitir o tráfego para todos os apps em execução ou todos os apps de preparação. Se você
não desejar ligar a esses dois conjuntos grupos de segurança, poderá desvincular dos
conjuntos de grupos do Cloud Foundry e depois ligar o grupo de segurança a um espaço
específico. Para obter mais informações, veja [Ligando grupos de segurança do aplicativo ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

**Nota**: Os comandos a seguir que permitem trabalhar com
grupos de segurança são baseadas na versão do Cloud Foundry 1.6. Para obter mais informações, incluindo campos necessários e opcionais, veja as informações do Cloud Foundry sobre [Criando grupos de segurança do aplicativo ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

### Listando grupos de segurança
{: #clilissecgro}

* Para listar todos os grupos de segurança, use o comando a seguir:

```
cf ba security-groups
```
{: codeblock}

**Dica:** também é possível usar **ba sgs**
como alias para o nome de comando mais longo **ba security-groups**.

* Para exibir detalhes para um grupo de segurança específico, use o comando a seguir:

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

**Dica:** é possível também usar **ba sg**
como alias para o nome de comando mais longo **ba security-groups**
com o parâmetro `security-group`.


### Criando um Grupo de Segurança
{: #clicreasecgro}

Para obter mais informações sobre a criação de grupos de segurança e as regras que definem o tráfego de saída, veja [Criando grupos de segurança do aplicativo ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window}.

Para criar um grupo de segurança, use o comando a seguir:

```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

Cada grupo
de segurança que você cria tem o prefixo `adminconsole_` incluído no
nome para distingui-lo dos grupos de segurança criados pela IBM.

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
<dt class="pt dlterm">&lt;Caminho para arquivo de regras&gt;</dt>
<dd class="pd">Caminho absoluto ou relativo para um arquivo de regras</dd>
</dl>

**Dica:** também é possível usar **ba csg**
como alias para o nome de comando mais longo **ba
create-security-group**.

### Atualizando um grupo de segurança
{: #cliupdsecgro}

Para atualizar um grupo de segurança, use o comando a seguir:

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
<dt class="pt dlterm">&lt;Caminho para arquivo de regras&gt;</dt>
<dd class="pd">Caminho absoluto ou relativo para um arquivo de regras</dd>
</dl>

**Dica:** também é possível usar **ba usg**
como alias para o nome de comando mais longo **ba update-security-group**.

### Excluindo um Grupo de Segurança
{: #clidelsecgro}

Para excluir um grupo de segurança, use o comando a seguir:

```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

**Dica:** também é possível usar **ba dsg**
como alias para o nome de comando maior
**ba delete-security-group**.


### Ligando grupos de segurança
{: #clibindsecgro}

Para obter mais informações sobre a ligação de grupos de segurança, veja [Ligando grupos de segurança do aplicativo ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window}.

* Para ligar ao conjunto de grupos de segurança de Preparação padrão, use o comando a seguir:

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

**Dica:** também é possível usar **ba bssg**
como alias para o nome de comando mais longo
**ba bind-staging-security-group**.

* Para ligar ao conjunto de grupos de segurança de Execução padrão, use o comando a seguir:

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

**Dica:** também é possível usar **ba brsg**
como alias para o nome de comando mais longo **ba
bind-running-security-group**.

* Para ligar um grupo de segurança a um espaço, use o comando a seguir:

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
<dt class="pt dlterm">&lt;Organização&gt;</dt>
<dd class="pd">Nome da organização à qual ligar o grupo de segurança</dd>
<dt class="pt dlterm">&lt;Espaço&gt;</dt>
<dd class="pd">Nome do espaço dentro da organização à qual ligar o grupo de segurança</dd>
</dl>

**Dica:** também é possível usar **ba bsg**
como alias para o nome de comando mais longo **ba bind-security-group**.

### Desvinculando grupos de segurança
{: #cliunbindsecgro}

Para obter mais informações sobre a desvinculação de grupos de segurança, veja [Desvinculando grupos de segurança do aplicativo ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window}.

* Para desvincular de um conjunto de grupos de segurança de Preparação padrão, use o comando a seguir:

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

**Dica:** também é possível usar **ba ussg**
como alias para o nome de comando mais longo **ba
unbind-staging-security-group**.

* Para desvincular de um conjunto de grupos de segurança de Execução padrão, use o comando a seguir:

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
</dl>

**Dica:** também é possível usar **ba brsg**
como alias para o nome de comando mais longo **ba
bind-running-security-group**.

* Para desvincular um grupo de segurança de um espaço, use o comando a seguir:

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Grupo de segurança&gt;</dt>
<dd class="pd">Nome do grupo de segurança</dd>
<dt class="pt dlterm">&lt;Organização&gt;</dt>
<dd class="pd">Nome da organização à qual ligar o grupo de segurança</dd>
<dt class="pt dlterm">&lt;Espaço&gt;</dt>
<dd class="pd">Nome do espaço dentro da organização à qual ligar o grupo de segurança</dd>
</dl>

**Dica:** também é possível usar **ba usg**
como alias para o nome de comando mais longo **ba
unbind-staging-security-group**.

## Administrando buildpacks
{: #admin_buildpack}

### Listando buildpacks
{: #clilistbuildpack}

Se você tiver as permissões de gravação do catálogo de apps, será possível listar os buildpacks. Para listar todos os buildpacks ou visualizar um buildpack
específico, use o comando a seguir:

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">Um parâmetro opcional para especificar um buildpack específico para visualizar.</dd>
</dl>

**Dica:** também é possível usar **ba lb** como um alias para o nome mais longo do
comando **ba buildpacks**.

### Criando e fazendo upload de um buildpack
{: #clicreupbuildpack}

Se você tiver as permissões de gravação do catálogo de apps, será possível criar e fazer upload de um buildpack. É possível fazer upload de qualquer arquivo compactado que tenha um tipo de arquivo .zip. Para
fazer upload de um buildpack, use o comando a seguir:

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">O nome do buildpack a ser transferido por upload.</dd>
<dt class="pt dlterm">&lt;file_path&gt;</dt>
<dd class="pd">O caminho para o arquivo compactado buildpack.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">A ordem na qual os buildpacks são verificados durante a detecção automática de buildpack.</dd>
</dl>

**Dica:** também é possível usar **ba cb** como um alias para o nome mais longo do
comando **ba create-buildpack**.

### Atualizando um buildpack
{: #cliupdabuildpack}

Se você tiver as permissões de gravação do catálogo de apps, será possível atualizar um buildpack existente.  Para atualizar um buildpack, use o comando a
seguir:

```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">O nome do buildpack a ser atualizado.</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">A ordem na qual os buildpacks são verificados durante a detecção automática de buildpack.</dd>
<dt class="pt dlterm">&lt;ativado&gt;</dt>
<dd class="pd">Indica se o buildpack é usado para preparação.</dd>
<dt class="pt dlterm">&lt;locked&gt;</dt>
<dd class="pd">Indica se o buildpack está bloqueado para evitar atualizações.</dd>
</dl>

**Dica:** também é possível usar **ba ub** como um alias para o nome mais longo do
comando **ba update-buildpack**.

### Excluindo um buildpack
{: #clidelbuildpack}

Se você tiver as permissões de gravação do catálogo de apps, será possível excluir um buildpack existente.  Para excluir um buildpack, use o comando a seguir:

```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">O nome do buildpack a ser excluído.</dd>
</dl>

**Dica:** também é possível usar **ba db** como um alias para o nome mais longo do
comando **ba delete-buildpack**.
