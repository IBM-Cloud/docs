---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI do administrador do {{site.data.keyword.Bluemix_notm}}
{: #bluemixadmincli}

*Última atualização: 3 de março de 2016*

É possível gerenciar usuários para o ambiente do seu
{{site.data.keyword.Bluemix_notm}} Local ou {{site.data.keyword.Bluemix_notm}} Dedicated usando
a interface da linha de comandos do Cloud Foundry com o plug-in
da CLI Admin do {{site.data.keyword.Bluemix_notm}}. Por
exemplo, é possível incluir usuários a partir de um registro LDAP. Se estiver procurando informações sobre como gerenciar sua conta do {{site.data.keyword.Bluemix_notm}} Public, consulte [Administrando](../../../admin/adminpublic.html#administer).

Antes de iniciar, instale a interface de linha de comandos do cf. O plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}
requer o cf versão 6.11.2 ou posterior. [Download
da interface de linha de comandos do Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restrição:** A interface de linha de
comandos do Cloud Foundry não é suportada por
Cygwin. Use a interface de linha de comandos do Cloud Foundry
em uma janela de linha de comandos diferente da janela de linha de comandos do Cygwin.

## Incluindo o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}

Após a interface de linha de comandos do cf ser instalada, é possível
incluir o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}.

**Nota**: se você tiver instalado
anteriormente o plug-in Administrador do
{{site.data.keyword.Bluemix_notm}}, poderá ser necessário desinstalar o plug-in, excluir o repositório e reinstalar para obter as atualizações mais recentes.

Conclua as etapas a seguir para incluir o repositório e instalar
o plug-in:

<ol>
<li>Para incluir o repositório do plug-in Administrador do {{site.data.keyword.Bluemix_notm}}, execute o comando a seguir:<br/><br/> <code> cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli </code><br/><br/>
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

## Usando o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}

É possível usar o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}} para incluir ou remover usuários, designar ou remover designação de usuários de organizações e
executar outras tarefas de gerenciamento. Para ver uma lista de comandos, execute o comando
a seguir:

```
cf plugins
```
{: codeblock}

Para obter ajuda adicional para um comando, use a opção `-help`.

### Conectando e efetuando login no {{site.data.keyword.Bluemix_notm}}

Antes de poder usar o plug-in da CLI Admin para gerenciar usuários,
deve-se conectar e efetuar login, se ainda não o fez.

<ol>
<li>Para se conectar ao terminal da API do {{site.data.keyword.Bluemix_notm}}, execute o comando a seguir:<br/><br/> <code> cf ba api https://console.&lt;subdomain&gt;.bluemix.net </code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Subdomínio da URL da sua instância do
{{site.data.keyword.Bluemix_notm}}.<br />
</dd>
</dl>
<p>É possível verificar a página Recursos e informações do Console
administrativo para a URL correta. A URL é mostrada
na seção Informações da API no campo **URL da API**.</p>
</li>
<li>Efetue login no {{site.data.keyword.Bluemix_notm}} com o
seguinte comando:<br/><br/>
<code> cf login
</code>
</li>
</ol>

### Incluindo um usuário

É possível incluir um usuário em seu ambiente do
{{site.data.keyword.Bluemix_notm}} a partir de um
registro LDAP. Insira o comando a seguir:

```
cf ba add-user <user_name> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no registro LDAP.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou GUID da organização do {{site.data.keyword.Bluemix_notm}} na qual incluir o usuário.</dd>
</dl>

**Dica:** também é possível usar **ba au** como um alias para o nome do comando mais longo **ba add-user**.

<!-- staging-only commands start. Live for interconnect -->

### Procurar um Usuário

É possível procurar um usuário. Insira o comando a seguir:

```
cf ba search-users <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Dica:** também é possível usar **ba su** como um alias para o nome do comando mais longo **ba search-users**.

### Configurar permissões para um usuário

É possível configurar permissões para um usuário especificado. Insira o comando a seguir:

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**Nota**: é possível configurar uma permissão por vez.

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">Configure as permissões para o usuário: Administrador, Login, Catálogo (acesso de leitura ou gravação), Relatórios (acesso de leitura ou gravação) ou Usuários (acesso de leitura ou gravação).</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">Para permissões de Catálogo, Relatórios ou Usuários, deve-se também configurar o nível de acesso como <code>read</code> ou <code>write</code>.</dd>
</dl>

**Dica:** também é possível usar **ba sp** como um alias para o nome do comando mais longo **ba set-permissions**.

<!-- staging-only commands end -->

### Removendo um usuário

É possível remover um usuário do ambiente do
{{site.data.keyword.Bluemix_notm}} inserindo o
seguinte comando:

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">O nome do usuário no {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Dica:** também é possível usar **ba ru** como um alias para o nome do comando mais longo **ba remove-user**.

### Incluindo e excluindo uma organização

É possível incluir e excluir uma organização.

* Para incluir uma organização, insira o comando a seguir:

```
cf ba create-organization <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} a ser incluída.</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">O nome do usuário do gerenciador para a organização.</dd>
</dl>

**Dica:** também é possível usar **ba co** como um alias para o nome do comando mais longo **ba create-organization**.

* Para excluir uma organização, insira um comando a seguir:

```
cf ba delete-organization <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} a ser excluída.</dd>
</dl>

**Dica:** também é possível usar **ba do** como um alias para o nome do comando mais longo **ba delete-organization**.

### Designando um usuário a uma organização

É possível designar um usuário no ambiente do
{{site.data.keyword.Bluemix_notm}} para uma organização
específica. Insira o comando a seguir:

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
<dd class="pd">Consulte [Funções](../../../admin/adminpublic.html#orgsandspaces) para obter descrições e funções de usuário do
{{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

**Dica:** também é possível usar **ba so** como um alias para o nome do comando mais longo **ba set-org**.

### Removendo a designação de um usuário de uma organização

É possível designar um usuário no ambiente do
{{site.data.keyword.Bluemix_notm}} de uma organização
específica. Insira o comando a seguir:

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
<dd class="pd">Consulte [Funções](../../../admin/adminpublic.html#orgsandspaces) para obter descrições e funções de usuário do
{{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

**Dica:** também é possível usar **ba uo** como um alias para o nome do comando mais longo **ba unset-org**.

### Funções

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Gerenciador de organização. Um gerenciador de organização possui authoridade para executar as ações a seguir:
<ul>
<li>Criar ou excluir espaços dentro da organização.</li>
<li>Convidar usuários para a organização e gerenciar usuários.</li>
<li>Gerenciar domínios da organização.</li>
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

É possível configurar a cota de uso para uma determinada organização.

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

### Incluindo, excluindo e recuperando os relatórios

É possível incluir, excluir e recuperar os relatórios de segurança.
* Para incluir um relatório, insira o comando a seguir:

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

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

* Para excluir um relatório, insira o comando a seguir:

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

* Para recuperar um relatório, insira o comando a seguir:

```
cf ba retrieve-report <category> <date> <name>
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

**Dica:** também é possível usar **ba rr** como um alias para o nome do comando mais longo **ba retrieve-report**.

### Ativando e desativando serviços para todas as organizações

É possível ativar ou desativar um serviço de ser exibido no Catálogo {{site.data.keyword.Bluemix_notm}} para todas as organizações.

* Para ativar um serviço para que fique visível no Catálogo {{site.data.keyword.Bluemix_notm}} para todas as organizações, insira o comando a seguir:

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do serviço que você deseja ativar. Se você inserir um nome do serviço não
exclusivo, serão solicitados os planos de serviço dos quais escolher.</dd>
</dl>

**Dica:** também é possível usar **ba esp** como um alias para o nome do comando mais longo **ba enable-service-plan**.

* Para desativar um serviço de ficar visível no Catálogo {{site.data.keyword.Bluemix_notm}} para todas as
organizações, insira o comando a seguir:

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do serviço que você deseja desativar. Se você inserir um nome do serviço não
exclusivo, serão solicitados os planos de serviço dos quais escolher.</dd>
</dl>

**Dica:** também é possível usar **ba dsp** como um alias para o nome do comando mais longo **ba disable-service-plan**.

### Incluindo, removendo e editando a visibilidade de serviço para organizações

É possível incluir ou remover uma organização da lista de organizações que podem ver um serviço específico
no Catálogo {{site.data.keyword.Bluemix_notm}}. Também é possível editar e substituir a lista de serviços que as
organizações específicas podem ver no Catálogo {{site.data.keyword.Bluemix_notm}}.

* Para permitir que uma organização visualize um serviço específico no Catálogo {{site.data.keyword.Bluemix_notm}}, insira o comando a seguir:

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do serviço para o qual você deseja incluir visibilidade. Se você inserir um nome do serviço não
exclusivo, serão solicitados os planos de serviço dos quais escolher.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} a ser incluída na lista de visibilidade do serviço.</dd>
</dl>

**Dica:** também é possível usar **ba aspv** como um alias para o nome do comando mais longo **ba add-service-plan-visibility**.

* Para remover a visibilidade de um serviço no Catálogo {{site.data.keyword.Bluemix_notm}} para uma organização,
insira o comando a seguir:

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do serviço para o qual você deseja remover a visibilidade. Se você inserir um nome do serviço não
exclusivo, serão solicitados os planos de serviço dos quais escolher.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} a ser removida da
lista de visibilidade do serviço.</dd>
</dl>

**Dica:** também é possível usar **ba rspv** como um alias para o nome do comando mais longo **ba remove-service-plan-visibility**.

* Para substituir todos os serviços visíveis existentes para uma organização ou múltiplas organizações, use o comando a seguir:

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**Nota:** Esse comando substitui os serviços
visíveis existentes para as organizações especificadas pelo serviço
que você especifica no comando.

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">O nome ou o GUID do serviço que você deseja tornar visível. Se você inserir um nome do serviço não
exclusivo, serão solicitados os planos de serviço dos quais escolher.</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">O nome ou o GUID da organização {{site.data.keyword.Bluemix_notm}} para a qual incluir a visibilidade. É
possível ativar a visibilidade do serviço para mais de uma organização, inserindo GUIDs ou nomes adicionais da
organização no comando.</dd>
</dl>

**Dica:** também é possível usar **ba espv** como um alias para o nome do comando mais longo **ba edit-service-plan-visibility**.

### Trabalhando com brokers de serviços

Use os comandos a seguir para listar todos os brokers de serviço, incluir ou excluir um broker de serviço ou atualizar um broker de serviço.

* É possível listar um broker de serviço
inserindo o comando a seguir:

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

* É possível incluir um broker de serviço, para que você possa incluir um serviço customizado em seu Catálogo do {{site.data.keyword.Bluemix_notm}} inserindo o comando a seguir:

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

* É possível excluir um broker de serviço para remover o serviço customizado de seu Catálogo do {{site.data.keyword.Bluemix_notm}} inserindo o comando a seguir:

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">O nome ou o guid do broker de serviço customizado.</dd>
</dl>

**Dica:** também é possível usar **ba dsb** como um alias para o nome do comando mais longo **ba delete-service-broker**.

* É possível atualizar um broker de serviço inserindo o comando a seguir:

`cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>`
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
