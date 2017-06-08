---



copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Comandos do {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

Versão: 0.5.2

A interface de linha de comandos (CLI) do {{site.data.keyword.Bluemix_notm}} fornece um conjunto de comandos que são agrupados por namespace para que os usuários interajam com o {{site.data.keyword.Bluemix_notm}}. Alguns
comandos do {{site.data.keyword.Bluemix_notm}} são wrappers de comandos cf existentes, enquanto outros fornecem recursos estendidos para usuários do {{site.data.keyword.Bluemix_notm}}. As
informações a seguir listam comandos que são suportados pela CLI do {{site.data.keyword.Bluemix_notm}} e incluem os seus nomes, opções, uso, pré-requisitos, descrições e exemplos.
{:shortdesc}

**Nota:** *Pré-requisitos* listam quais ações são necessárias antes de usar o comando. Os comandos que não têm ações de pré-requisito listam **Nenhum**. Caso contrário, os pré-requisitos podem incluir uma ou mais das ações a seguir:

<dl>
<dt>Nó de Extremidade</dt>
<dd>Um terminal de API deve ser configurado por meio de <code>bluemix api</code> antes de usar o comando.</dd>
<dt>Login</dt>
<dd>É necessário efetuar login usando o comando <code>bluemix login</code> antes de usar esse comando.
Se estiver efetuando login com o ID federado, use a opção '--sso' para se autenticar com uma senha única ou use '--apikey' para se autenticar com a chave API. Acesse o console do {{site.data.keyword.Bluemix_notm}}: **Gerenciar** &gt; **Segurança** &gt; **Chaves API do Bluemix** para criar chaves API.
</dd>
<dt>Destino</dt>
<dd>O comando <code>bluemix target</code> deve ser usado para configurar uma organização e um espaço antes de usar esse comando.</dd>
<dt>Docker</dt>
<dd>A CLI do Docker (docker) deve estar instalada para executar esse comando.</dd>
</dl>

## Índice de comandos do Bluemix
{: #bx_commands_index}

Use os índices nas tabelas a seguir para referir-se aos comandos do Bluemix usados frequentemente.

**Nota:** é possível usar o formato curto de comandos bluemix; por exemplo, `bx api` é a abreviação de `bluemix api`.



<table summary="Comandos gerais do Bluemix.">
<caption>Tabela 1. Comandos gerais do Bluemix</caption>
 <thead>
 <th colspan="5">Comandos gerais do Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix help
](bx_cli.html#bluemix_help)</td>
 <td>[bluemix api
](bx_cli.html#bluemix_api)</td>
 <td>[bluemix login](bx_cli.html#bluemix_login)</td>
 <td>[bluemix logout
](bx_cli.html#bluemix_logout)</td>
 <td>[bluemix target
](bx_cli.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](bx_cli.html#bluemix_info) </td>
 <td>[bluemix regions](bx_cli.html#bluemix_regions) </td>
 <td>[bluemix config](bx_cli.html#bluemix_config)</td>
 <td>[bluemix curl](bx_cli.html#bluemix_curl)</td>
 <td>[bluemix update](bx_cli.html#bluemix_update)</td>
 </tr>
 </tbody>
 </table>

<table summary="Comandos do Bluemix que podem ser usados para gerenciar contas, organizações, espaços, funções e chaves API.">
<caption>Tabela 2. Comandos para gerenciar contas, organizações, espaços, funções e chaves API</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar contas, organizações, espaços, funções e chaves API</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](bx_cli.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](bx_cli.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](bx_cli.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](bx_cli.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](bx_cli.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](bx_cli.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](bx_cli.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](bx_cli.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](bx_cli.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](bx_cli.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](bx_cli.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam org-users](bx_cli.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-user-add](bx_cli.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](bx_cli.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-roles](bx_cli.html#bluemix_iam_org_roles)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-role-set](bx_cli.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](bx_cli.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](bx_cli.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-roles](bx_cli.html#bluemix_iam_space_roles)</td>
 <td>[bluemix iam space-role-set](bx_cli.html#bluemix_iam_space_role_set)</td>
</tr>
 <tr>
 <td>[bluemix iam space-role-unset](bx_cli.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix iam accounts](bx_cli.html#bluemix_iam_accounts)</td>
 <td>[bluemix iam org-account](bx_cli.html#bluemix_iam_org_account)</td>
 <td>[bluemix iam account-users
](bx_cli.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](bx_cli.html#bluemix_iam_account_users_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam account-user-invite](bx_cli.html#bluemix_iam_account_user_invite)</td>
  <td>[bluemix iam account-user-reinvite](bx_cli.html#bluemix_iam_account_user_reinvite)</td>
  <td>[bluemix iam api-keys](bx_cli.html#bluemix_iam_api_keys)</td>
  <td>[bluemix iam api-key-create](bx_cli.html#bluemix_iam_api_key_create)</td>
  <td>[bluemix iam api-key-delete](bx_cli.html#bluemix_iam_api_key_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam api-key-update](bx_cli.html#bluemix_iam_api_key_update)</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
 </tr>
 </tbody>
 </table>

<table summary="Comandos do Bluemix que podem ser usados para gerenciar apps cf e domínios, rotas e certificados relacionados aos apps.">
<caption>Tabela 3. Comandos para gerenciar apps cf e domínios, rotas e certificados relacionados aos apps</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar apps cf e domínios, rotas e certificados relacionados aos apps</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](bx_cli.html#bluemix_app_push)</td>
 <td>[bluemix app list](bx_cli.html#bluemix_app_list)</td>
 <td>[bluemix app show](bx_cli.html#bluemix_app_show)</td>
 <td>[bluemix app delete](bx_cli.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](bx_cli.html#bluemix_app_rename)</td>
 </tr>
 <tr>
 <td>[bluemix app start](bx_cli.html#bluemix_app_start)</td>
 <td>[bluemix app stop](bx_cli.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](bx_cli.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](bx_cli.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](bx_cli.html#bluemix_app_instance_restart)</td>
 </tr>
 <tr>
 <td>[bluemix app events](bx_cli.html#bluemix_app_events)</td>
 <td>[bluemix app files](bx_cli.html#bluemix_app_files)</td>
 <td>[bluemix app logs](bx_cli.html#bluemix_app_logs)</td>
 <td>[bluemix app env](bx_cli.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](bx_cli.html#bluemix_app_env_set)</td>
 </tr>
 <tr>
 <td>[bluemix app env-unset](bx_cli.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](bx_cli.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack-show](bx_cli.html#bluemix_app_stack_show)</td>
 <td>[bluemix app manifest-create](bx_cli.html#bluemix_app_manifest_create)</td>
 <td>[bluemix app domain-cert](bx_cli.html#bluemix_app_domain_cert)</td>
 </tr>
 <tr>
  <td>[bluemix app domain-cert-add](bx_cli.html#bluemix_app_domain_cert_add)</td>
  <td>[bluemix app domain-cert-remove](bx_cli.html#bluemix_app_domain_cert_remove)</td>
  <td>[bluemix app domains](bx_cli.html#bluemix_app_domains)</td>
  <td>[bluemix app domain-create](bx_cli.html#bluemix_app_domain_create)</td>
  <td>[bluemix app domain-delete](bx_cli.html#bluemix_app_domain_delete)</td>
 </tr>
 <tr>
  <td>[bluemix app shared-domain-create](bx_cli.html#bluemix_app_shared_domain_create)</td>
  <td>[bluemix app shared-domain-delete](bx_cli.html#bluemix_app_shared_domain_delete)</td>
  <td>[bluemix app routes](bx_cli.html#bluemix_app_routes)</td>
  <td>[bluemix app route-check](bx_cli.html#bluemix_app_route_check)</td>
  <td>[bluemix app route-map](bx_cli.html#bluemix_app_route_map)</td>
 </tr>
 <tr>
  <td>[bluemix app route-unmap](bx_cli.html#bluemix_app_route_unmap)</td>
  <td>[bluemix app route-create](bx_cli.html#bluemix_app_route_create)</td>
  <td>[bluemix app route-delete](bx_cli.html#bluemix_app_route_delete)</td>
  <td>[bluemix app orphaned-routes-delete](bx_cli.html#bluemix_app_orphaned_routes_delete)</td>
  <td></td>
 </tr>
  </tbody>
 </table>

<table summary="comandos do Bluemix que podem ser usados para gerenciar serviços do Bluemix.">
<caption>Tabela 4. Comandos para gerenciar serviços do Bluemix</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar serviços do Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix service offerings](bx_cli.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](bx_cli.html#bluemix_service_list)</td>
 <td>[bluemix service show](bx_cli.html#bluemix_service_show)</td>
 <td>[bluemix service create](bx_cli.html#bluemix_service_create)</td>
 <td>[bluemix service update](bx_cli.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](bx_cli.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](bx_cli.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](bx_cli.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](bx_cli.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](bx_cli.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](bx_cli.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](bx_cli.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](bx_cli.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](bx_cli.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](bx_cli.html#bluemix_service_user_provided_update)</td>
 </tr>
  </tbody>
 </table>

<table summary="comandos do Bluemix que podem ser usados para gerenciar catálogo, plug-ins, faturamento e configurações de segurança do Bluemix.">
<caption>Tabela 5. Comandos para gerenciar catálogo, plug-ins, faturamento e configurações de segurança do Bluemix</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar catálogo, plug-ins, faturamento e configurações de segurança do Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix catalog templates](bx_cli.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](bx_cli.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](bx_cli.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos
](bx_cli.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](bx_cli.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](bx_cli.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](bx_cli.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list
](bx_cli.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](bx_cli.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](bx_cli.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix plugin update](bx_cli.html#bluemix_plugin_update)</td>
 <td>[bluemix billing account-usage](bx_cli.html#bluemix_billing_account_usage)</td>
 <td>[bluemix billing org-usage](bx_cli.html#bluemix_billing_org_usage)</td>
 <td>[bluemix billing orgs-usage-summary](bx_cli.html#bluemix_billing_orgs_usage_summary)</td>
 <td></td>
 </tr>
 </tbody>
 </table>
 
## bluemix help
{: #bluemix_help}
Exiba a ajuda geral para comandos integrados de primeiro nível e namespaces suportados da CLI {{site.data.keyword.Bluemix_notm}} ou a ajuda para um comando ou namespace integrado específico.

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:

   <dl>
   <dt>COMMAND|NAMESPACE (opcional)</dt>
   <dd>O comando ou namespace para o qual a ajuda é exibida. Se não especificado, a ajuda geral para a CLI do {{site.data.keyword.Bluemix_notm}} será mostrada.</dd>
   </dl>



<strong>Exemplos</strong>:

Exiba a ajuda geral para a CLI do {{site.data.keyword.Bluemix_notm}}:

```
bluemix help
```

Exiba a ajuda para o comando `info`:

```
bluemix help info
```



## bluemix api
{: #bluemix_api}
Configure ou visualize o terminal da API do {{site.data.keyword.Bluemix_notm}}.

```
bluemix api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:
   <dl>
   <dt>API_ENDPOINT (opcional)</dt>
   <dd>O terminal da API que é o destino, por exemplo, `https://api.chinabluemix.net`. Se as opções *API_ENDPOINT* e `--unset` não forem ambas especificadas, o terminal de API atual será exibido.</dd>
   <dt>--unset (opcional)</dt>
   <dd>Remova a configuração do terminal de API.</dd>
   <dt>--skip-ssl-validation (opcional)</dt>
   <dd>Validação SSL de bypass de solicitações de HTTP.</dd>
   </dl>
<strong>Exemplos</strong>:

Configure o terminal da API para api.chinabluemix.net:

```
bluemix api api.chinabluemix.net
```

```
bluemix api https://api.chinabluemix.net --skip-ssl-validation
```

Visualize o terminal de API atual:

```
bluemix api
```

Desconfigure o terminal de API:

```
bluemix api --unset
```


## bluemix login
{: #bluemix_login}

Efetue login do usuário. 

```
bluemix login [OPTIONS...]
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:
<dl>
  <dt>-a <i>API_ENDPOINT</i> (opcional)</dt>
  <dd> Terminal de API (Por exemplo: api.ng.bluemix.net)</dd>
  <dt> --apikey <i>API_KEY ou @API_KEY_FILE_PATH</i>
  <dd> Conteúdo da chave API ou o caminho de um arquivo de chave API indicado por @</dd>
  <dt> --sso (opcional) </dt>
  <dd> Use uma senha descartável para efetuar login </dd>
  <dt> -u <i>USERNAME</i> (opcional)</dt>
  <dd> Username</dd>
  <dt> -p <i>PASSWORD</i> (opcional)</dt>
  <dd> Senha</dd>
  <dt> -c <i>ACCOUNT_ID</i> (opcional) </dt>
  <dd> ID da conta de destino</dd>
  <dt> -o <i>ORG_NAME</i> (opcional) </dt>
  <dd> Nome da organização de destino </dd>
  <dt> -s <i>SPACE_NAME</i> (opcional) </dt>
  <dd> Nome do espaço de destino</dd>
  <dt> --skip-ssl-validation (opcional) </dt>
  <dd> Validação SSL de bypass de solicitações de HTTP. Essa opção não é recomendada.</dd>
</dl>

<strong>Exemplos</strong>:

Login interativo:

```
bluemix login
```

Efetue login com o nome do usuário e senha e configure a conta de destino, organização e espaço:

```
bluemix login -u username -p password -c MyAccountID -o MyOrg -s MySpace
```

Efetue login com uma senha descartável e configure a conta de destino, organização e espaço

```
bluemix login --sso -c MyAccountID -o MyOrg -s MySpace
```

Efetue login com a chave API e configure os destinos:

* A chave API tem conta associada

```
bluemix login --apikey api-key-string -o MyOrg -s MySpace
```

```
bluemix login --apikey @filename -o MyOrg -s MySpace
```

* A chave API não tem conta associada

```
bluemix login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
bluemix login --apikey @fileName -c MyAccountID -o MyOrg -s MySpace
```

<strong>Nota:</strong> se a chave API tiver conta associada, não será possível alternar para outra conta.


## bluemix logout
{: #bluemix_logout}

Efetue logout do usuário.

```
bluemix logout
```

<strong>Pré-requisitos</strong>: Nenhum


## bluemix target
{: #bluemix_target}


Configure ou visualize a conta de destino, região, organização ou espaço.

```
bluemix target [-c ACCOUNT_ID] [-r REGION] [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>-c <i>ACCOUNT_ID</i> (opcional)</dt>
   <dd>O ID da conta que será o destino.</dd>
   <dt>-r <i>REGION</i> (opcional)</dt>
   <dd>A região para a qual será alternada.</dd>
   <dt>-o <i>ORG_NAME</i> (opcional)</dt>
   <dd>O nome da organização que será o destino.</dd>
   <dt>-s <i>SPACE_NAME</i> (opcional)</dt>
   <dd>O nome do espaço que será o destino.</dd>
   </dl>
Se nenhuma das opções for especificada, a conta, a região, a organização e o espaço atuais serão exibidos.

<strong>Exemplos</strong>:

Configure a conta, a organização e o espaço atuais

```
bluemix target -c MyAccountID -o MyOrg -s MySpace
```

Alterne para uma nova região

```
bluemix target -r eu-gb
```

Visualize a conta, a região, a organização e o espaço atuais:

```
bluemix target
```


## bluemix info
{: #bluemix_info}

Visualize as informações básicas do {{site.data.keyword.Bluemix_notm}}, incluindo a região atual, a versão do controlador de nuvem e alguns terminais úteis, como terminais para login e a troca de token de acesso.

```
bluemix info
```

<strong>Pré-requisitos</strong>: Terminal


## bluemix config
{: #bluemix_config}


Grave os valores padrão no arquivo de configuração.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>O valor de tempo limite para solicitações de HTTP. O valor padrão é 60 segundos.</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>Rastreie solicitações de HTTP para o terminal ou arquivo especificado.</dd>
   <dt>--color true|false</dt>
   <dd>Ative ou desative a saída de cor. A saída de cor é ativada por padrão.</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>Configure um código padrão de idioma. Se LOCALE for <i>CLEAR</i>, o código de idioma anterior será excluído.</dd>
   <dt>--check-version true|false</dt>
   <dd>Ative ou desative a verificação de versão da CLI</dd>
   </dl>

Somente uma dessas opções pode ser especificada por vez.

<strong>Exemplos</strong>:

Configure o tempo limite de solicitação de HTTP como 30 segundos:

```
bluemix config --http-timeout 30
```

Ative a saída de rastreio para solicitações de HTTP:

```
bluemix config --trace true
```

Rastreie solicitações de HTTP para um arquivo especificado */home/usera/my_trace*:

```
bluemix config --trace /home/usera/my_trace
```

Desative a saída de cor:

```
bluemix config --color false
```

Configure o código de idioma como zh_Hans:

```
bluemix config --locale zh_Hans
```

Limpe as configurações do código de idioma:

```
bluemix config --locale CLEAR
```


## bluemix curl
{: #bluemix_curl}

Executar um solicitação de HTTP bruto para {{site.data.keyword.Bluemix_notm}}. *Content-Type* é configurado como *application/json* por padrão. Esse comando envia a solicitação para o {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. Para caminhos suportados, consulte as definições de caminho da API no [documento da API do CloudFoundry ](http://apidocs.cloudfoundry.org/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg).

```
bluemix curl PATH [OPTIONS...]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt><i>PATH</i> (necessário)</dt>
   <dd>O caminho da URL do recurso. Por exemplo, /v2/apps.</dd>
   <dt><i>OPTIONS</i> (opcional)</dt>
   <dd>As opções que são suportadas pelo comando `bluemix curl` são as mesmas que aquelas para o comando `cf curl`.</dd>
   </dl>

<strong>Exemplos</strong>:

Visualize as informações para todas as organizações da conta atual:

```
bluemix curl /v2/organizations
```

## bluemix update
{: #bluemix_update}

Atualizar a CLI para a versão mais recente

```
bluemix update
```

<strong>Pré-requisitos</strong>: Nenhum

## bluemix regions
{: #bluemix_regions}

Visualize as informações para todas as regiões no {{site.data.keyword.Bluemix_notm}}.

```
bluemix regions
```

<strong>Pré-requisitos</strong>: Terminal


## bluemix iam orgs
{: #bluemix_iam_orgs}

Liste todas as organizações

```
bluemix iam orgs [-r REGION] [--guid]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>-r <i>REGION</i> (opcional)</dt>
   <dd>Para qual região as informações da organização são mostradas. Se configurado como 'all', todas as organizações em todas as regiões serão listadas.</dd>
   <dt>--guid (opcional)</dt>
   <dd>Exiba o GUID das organizações.</dd>
   </dl>

<strong>Exemplos</strong>:

Liste todas as organizações na região: `us-south` com o GUID exibido

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

Mostre as informações para a organização especificada.

```
bluemix iam org ORG_NAME [--guid]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização.</dd>
   <dt>--guid (opcional)</dt>
   <dd>Exiba o GUID da organização.</dd>
   </dl>

<strong>Exemplos</strong>:

Mostre as informações da organização `IBM` com o GUID exibido

```
bluemix iam org IBM --guid
```


## bluemix iam org-create
{: #bluemix_iam_org_create}

Criar uma nova organização. Essa operação pode ser executada somente pelo proprietário da conta.

```
bluemix iam org-create ORG_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização que está sendo criada.</dd>
   </dl>

<strong>Exemplos</strong>:

Crie uma organização denominada `IBM`.

```
bluemix iam org-create IBM
```

## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Replique uma organização a partir da região atual para outra região.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização existente que deve ser replicada.</dd>
   <dt>REGION_NAME (necessário)</dt>
   <dd>O nome da região que hospeda a organização replicada.</dd>
   </dl>

<strong>Exemplos</strong>:

Replique a organização `myorg` para a região `eu-gb`:

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

Renomeie uma organização. Essa operação pode ser executada somente por um gerenciador de organização.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>OLD_ORG_NAME (necessário)</dt>
   <dd>O nome antigo da organização que deve ser renomeada.</dd>
   <dt>NEW_ORG_NAME (necessário)</dt>
   <dd>O novo nome da organização para o qual ela é renomeada.</dd>
   </dl>

## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Exclua a organização especificada na região atual.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização existente que deve ser excluída.</dd>
   <dt>-f (opcional)</dt>
   <dd>Force a exclusão sem confirmação.</dd>
   <dt>--all (opcional)</dt>
   <dd>Exclua a organização de todas as regiões.</dd>
   </dl>


## bluemix iam spaces
{: #bluemix_iam_spaces}

Esse comando tem a mesma função e opções que o comando `cf spaces`.


## bluemix iam space
{: #bluemix_iam_space}

Esse comando tem a mesma função e opções que o comando `cf space`.


## bluemix iam space-create
{: #bluemix_iam_space_create}

Esse comando tem a mesma função e opções que o comando `cf create-space`.


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


Esse comando tem a mesma função e opções que o comando `cf rename-space`.


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


Esse comando tem a mesma função e opções que o comando `cf delete-space`.

## bluemix iam org-users
{: #bluemix_iam_org_users}

Exiba usuários na organização especificada por função.

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>ORG_NAME (necessário)</dt>
<dd>O nome da organização.</dd>
<dt>-a (opcional)</dt>
<dd>Liste todos os usuários na organização especificada, não agrupados por função.</dd>
</dl>

## bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Inclua um usuário na organização (gerenciador de organização requerido).

```
 bluemix iam org-user-add USER_NAME ORG
```

## bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

Remova um usuário da organização (gerente da organização ou o próprio usuário somente)

```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>Opções de comando</strong>:
<dl>
<dt>--force, -f</dt>
<dd>Force a exclusão sem confirmação.</dd>
</dl>

## bluemix iam org-roles
{: #bluemix_iam_org_roles}

Obtenha todas as funções de organização do usuário atual

```
bluemix iam org-roles
```

<strong>Pré-requisitos</strong>: Terminal, Login

## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Designe uma função de organização a um usuário. Essa operação pode ser executada somente por um gerenciador de organização.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
  <dl>
   <dt>USER_NAME ((necessário))</dt>
   <dd>O nome do usuário que está sendo designado.</dd>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização para a qual esse usuário é designado.</dd>
   <dt>ORG_ROLE (necessário)</dt>
   <dd>O nome da função de organização para a qual esse usuário é designado. Por
exemplo:
   <ul>
   <li>OrgManager: essa função pode convidar e gerenciar usuários, selecionar e mudar planos e configurar limites de gastos.</li>
   <li>BillingManager: essa função pode criar e gerenciar a conta de cobrança e informações de pagamento.</li>
   <li>OrgAuditor: essa função possui acesso somente leitura para informações e relatórios da organização.</li>
   </ul>
   </dd>
  </dl>

<strong>Exemplos</strong>:

Designe o usuário `Mary` à organização do `IBM` como função `OrgManager`:

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Remover uma função de organização de um usuário. Essa operação pode ser executada somente por um gerenciador de organização.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>USER_NAME ((necessário))</dt>
   <dd>O nome do usuário que está sendo removido.</dd>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização da qual esse usuário é removido.</dd>
   <dt>ORG_ROLE (necessário)</dt>
   <dd>O nome da função de organização da qual esse usuário é removido. Por
exemplo:
   <ul>
   <li>OrgManager: essa função pode convidar e gerenciar usuários, selecionar e mudar planos e configurar limites de gastos.</li>
   <li>BillingManager: essa função pode criar e gerenciar a conta de cobrança e informações de pagamento.</li>
   <li>OrgAuditor: essa função possui acesso somente leitura para informações e relatórios da organização.</li>
   </ul>
   </dd>
    </dl>

<strong>Exemplos</strong>:

Remova o usuário `Mary` da organização `IBM` como função `OrgManager`:

```
bluemix iam org-role-unset Mary IBM OrgManager
```

## bluemix iam space-users
{: #bluemix_iam_space_users}

Exiba usuários no espaço especificado por função.

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização.</dd>
   <dt>SPACE_NAME (necessário)</dt>
   <dd>O nome do espaço.</dd>
   </dl>


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Designe uma função de espaço a um usuário. Essa operação pode ser executada somente por um gerenciador de espaço.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:

   <dl>
   <dt>USER_NAME ((necessário))</dt>
   <dd>O nome do usuário que está sendo designado.</dd>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização para a qual esse usuário é designado.</dd>
   <dt>SPACE_NAME (necessário)</dt>
   <dd>O nome do espaço para o qual esse usuário é designado.</dd>
   <dt>SPACE_ROLE (necessário)</dt>
   <dd>O nome da função de espaço para a qual esse usuário é designado. Por
exemplo:
   <ul>
   <li>SpaceManager: essa função pode convidar e gerenciar usuários e ativar recursos para um determinado espaço.</li>
   <li>SpaceDeveloper: essa função pode criar e gerenciar aplicativos e serviços, bem como ver logs e relatórios.</li>
   <li>SpaceAuditor: essa função pode visualizar logs, relatórios e configurações para o espaço.</li>
   </ul></dd>
    </dl>

<strong>Exemplos</strong>:

Designe o usuário `Mary` à organização `IBM` e espaço `Cloud` como função `SpaceManager`:

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Remova uma função de espaço de um usuário. Essa operação pode ser executada somente por um gerenciador de espaço.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:

   <dl>
   <dt>USER_NAME ((necessário))</dt>
   <dd>O nome do usuário que está sendo removido.</dd>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização da qual esse usuário é removido.</dd>
   <dt>SPACE_NAME (necessário)</dt>
   <dd>O nome do espaço do qual esse usuário é removido.</dd>
   <dt>SPACE_ROLE (necessário)</dt>
   <dd>O nome da função de espaço da qual esse usuário é removido. Por
exemplo:
   <ul>
   <li>SpaceManager: essa função pode convidar e gerenciar usuários e ativar recursos para um determinado espaço.</li>
   <li>SpaceDeveloper: essa função pode criar e gerenciar aplicativos e serviços, bem como ver logs e relatórios.</li>
   <li>SpaceAuditor: essa função pode visualizar logs, relatórios e configurações para o espaço.</li>
   </ul></dd>
    </dl>


<strong>Exemplos</strong>:

Remova o usuário `Mary` da organização `IBM` e espaço `Cloud` como função `SpaceManager`:

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```

## bluemix iam accounts
{: #bluemix_iam_accounts}

Liste todas as contas do usuário atual

```
bluemix iam accounts
```

<strong>Pré-requisitos</strong>: Terminal, Login


## bluemix iam org-account
{: #bluemix_iam_org_account}

Exibir a conta da organização especificada (usuário da organização necessário)

```
bluemix iam org-account ORG_NAME [--guid]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
  <dt>--guid (opcional)</dt>
  <dd>Exibir somente o ID da conta</dd>
</dl>


## bluemix iam account-users
{: #bluemix_iam_account_users}

Exibe os usuários associados à conta. Essa operação pode ser executada somente pelo proprietário da conta.

```
bluemix iam account-users
```

## bluemix iam account-user-delete
{: #bluemix_iam_account_user_delete}

Exclua um usuário da conta atual (somente o proprietário da conta)

```
bluemix iam account-user-delete USERNAME [-f]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>USERNAME (necessário)</dt>
<dd>Username</dd>
<dt>--force, -f (opcional)</dt>
<dd>Force a exclusão sem confirmação.</dd>
</dl>

## bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}

Convida um usuário para a conta com uma função de organização e espaço já configurada. Essa operação pode ser executada somente pelo proprietário da conta.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
   <dt>USER_NAME ((necessário))</dt>
   <dd>O nome do usuário que está sendo convidado.</dd>
   <dt>ORG_NAME (necessário)</dt>
   <dd>O nome da organização para a qual esse usuário é convidado.</dd>
   <dt>ORG_ROLE (necessário)</dt>
   <dd>O nome da função de organização para a qual esse usuário é convidado. Por
exemplo:
   <ul>
  <li>OrgManager: essa função pode convidar e gerenciar usuários, selecionar e mudar planos e configurar limites de gastos.</li>
  <li>BillingManager: essa função pode criar e gerenciar a conta de cobrança e informações de pagamento.</li>
  <li>OrgAuditor: essa função possui acesso somente leitura para informações e relatórios da organização.</li>
  </ul> </dd>
   <dt>SPACE_NAME (necessário)</dt>
   <dd>O nome do espaço para o qual esse usuário é convidado.</dd>
   <dt>SPACE_ROLE (necessário)</dt>
   <dd>O nome do espaço para o qual esse usuário é convidado. O nome da função do espaço para o qual esse usuário é convidado. Por
exemplo:
   <ul>
<li>SpaceManager: essa função pode convidar e gerenciar usuários e ativar recursos para um determinado espaço.</li>
<li>SpaceDeveloper: essa função pode criar e gerenciar aplicativos e serviços, bem como ver logs e relatórios.</li>
<li>SpaceAuditor: essa função pode visualizar logs, relatórios e configurações para o espaço.</li>
</ul>
</dd>
</dl>

<strong>Exemplos</strong>:

Convide o usuário `Mary` para a organização `IBM` como função `OrgManager` e o espaço `Cloud` como função `SpaceAuditor`:

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Reenviar o convite a um usuário (é necessário ser o gerente da organização ou o proprietário da conta)

```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```

## bluemix iam api-keys
{: #bluemix_iam api_keys}

Listar todas as chaves API da plataforma do Bluemix

```
bluemix iam api-keys
```

<strong>Pré-requisitos</strong>: Terminal, Login

## bluemix iam api-key-create
{: #bluemix_iam_api_key_create}

Criar uma nova chave API da Plataforma do Bluemix

```
bluemix iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>NAME (necessário)</dt>
<dd>Nome da chave API a ser criada.</dd>
<dt>-d <i>DESCRIPTION</i> (opcional)</dt>
<dd>Descrição da chave de API</dd>
<dt>-f, -- file <i>FILE</i></dt>
<dd>Salve as informações da chave API para o arquivo especificado. Se não configuradas, o conteúdo JSON será exibido.</dd>
</dl>

<strong>Exemplos</strong>:

Crie uma chave API e salve em um arquivo

```
bluemix iam api-key-create MyKey -d "this is my API key" -f key_file
```

## bluemix iam api-key-update
{: #bluemix_iam_api_key_update}

Atualizar uma chave API da plataforma do Bluemix

```
bluemix iam api-key-update NAME [-n NAME] [-d DESCRIPTION]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>NAME (necessário)</dt>
<dd>O nome antigo da chave API a ser atualizada.</dd>
<dt>-n <i>NAME</i> (opcional)</dt>
<dd>O nome novo da chave API</dd>
<dt>-d <i>DESCRIPTION</i> (opcional)</dt>
<dd>A nova descrição da chave API</dd>
</dl>

<strong>Exemplos</strong>:

Atualize a descrição de uma chave API:

```
bluemix iam api-key-update MyKey -d "the new description of my key"
```

## bluemix api-key-delete
{: #bluemix_api_key_delete}

Excluir uma chave API da plataforma do Bluemix

```
bluemix iam api-key-delete NAME [-f]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>NAME (necessário)</dt>
<dd>Nome da chave API a ser excluída.</dd>
<dt>-f (opcional)</dt>
<dd>Force a exclusão sem confirmação.</dd>
</dl>


## bluemix app push
{: #bluemix_app_push}

Esse comando tem a mesma função e opções que o comando `cf push`.


## bluemix app list
{: #bluemix_app_list}

Esse comando tem a mesma função e opções que o comando `cf apps`.


## bluemix app show
{: #bluemix_app_show}

Esse comando tem a mesma função e opções que o comando `cf app`.


## bluemix app delete
{: #bluemix_app_delete}

Esse comando tem a mesma função e opções que o comando `cf delete`.


## bluemix app rename
{: #bluemix_app_rename}

Esse comando tem a mesma função e opções que o comando `cf rename`.


## bluemix app start
{: #bluemix_app_start}

Esse comando tem a mesma função e opções que o comando `cf start`.


## bluemix app stop
{: #bluemix_app_stop}

Esse comando tem a mesma função e opções que o comando `cf stop`.


## bluemix app restart
{: #bluemix_app_restart}

Esse comando tem a mesma função e opções que o comando `cf restart`.


## bluemix app restage
{: #bluemix_app_restage}


Esse comando tem a mesma função e opções que o comando `cf restage`.


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


Esse comando tem a mesma função e opções que o comando `cf restart-app-instance`.


## bluemix app events
{: #bluemix_app_events}

Esse comando tem a mesma função e opções que o comando `cf events`.


## bluemix app files
{: #bluemix_app_files}

Esse comando tem a mesma função e opções que o comando `cf files`.


## bluemix app logs
{: #bluemix_app_logs}

Esse comando tem a mesma função e opções que o comando `cf logs`.


## bluemix app env
{: #bluemix_app_env}

Esse comando tem a mesma função e opções que o comando `cf env`.


## bluemix app env-set
{: #bluemix_app_env_set}

Esse comando tem a mesma função e opções que o comando `cf set-env`.


## bluemix app env-unset
{: #bluemix_app_env_unset}

Esse comando tem a mesma função e opções que o comando `cf unset-env`.


## bluemix app stacks
{: #bluemix_app_stacks}

Esse comando tem a mesma função e opções que o comando `cf stacks`.


## bluemix app stack-show
{: #bluemix_app_stack_show}

Esse comando tem a mesma função e opções que o comando `cf stack`.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

Esse comando tem a mesma função e opções que o comando `cf create-app-manifest`.

## bluemix app domain-cert 
{: #bluemix_app_domain_cert}

Liste as informações de certificado de um domínio.

```
bluemix app domain-cert DOMAIN_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
<dl>
<dt>DOMAIN_NAME (necessário)</dt>
<dd>O domínio que hospeda o certificado.</dd>
</dl>


<strong>Exemplos</strong>:

Visualize as informações de certificado do domínio `ibmcxo-eventconnect.com`:

```
bluemix app domain-cert ibmcxo-eventconnect.com
```

## bluemix app domain-cert-add
{: #bluemix_app_domain_cert_add}

Inclua um certificado no domínio especificado na organização atual.

```
bluemix app domain-cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [-t TRUST_STORE_FILE]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
   <dl>
   <dt>DOMAIN (necessário)</dt>
   <dd>O domínio no qual o certificado é incluído.</dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i> (necessário)</dt>
   <dd>O caminho de arquivo de chave privado.</dd>
   <dt>-c <i>CERT_FILE</i> (necessário)</dt>
   <dd>O caminho de arquivo de certificado.</dd>
   <dt>-p <i>PASSWORD</i> (opcional)</dt>
   <dd>A senha para o certificado.</dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i> (opcional)</dt>
   <dd>O caminho de arquivo de certificado intermediário.</dd>
   <dt>-t <i>TRUST_STORE_FILE</i> (opcional)</dt>
   <dd>O arquivo de armazenamento confiável.</dd>
   </dl>


<strong>Exemplos</strong>:

Inclua um certificado no domínio `ibmcxo-eventconnect.com`:

```
bluemix app domain-cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```

## bluemix app domain-cert-remove
{: #bluemix_app_domain_cert_remove}

Remova um certificado do domínio especificado na organização atual.

```
bluemix app domain-cert-remove DOMAIN [-f]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>DOMAIN (necessário)</dt>
   <dd>Domínio do qual remover o certificado.</dd>
   <dt>-f (opcional)</dt>
   <dd>Force a exclusão sem confirmação.</dd>
   </dl>

## bluemix app domains
{: #bluemix_app_domains}

Esse comando tem a mesma função e opções que o comando `cf domains`.


## bluemix app domain-create
{: #bluemix_app_domain_create}

Esse comando tem a mesma função e opções que o comando `cf create-domain`.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-domain`.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

Esse comando tem a mesma função e opções que o comando `cf create-shared-domain`.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-shared-domain`.

## bluemix app routes
{: #bluemix_app_routes}

Esse comando tem a mesma função e opções que o comando `cf routes`.


## bluemix app route-check
{: #bluemix_app_route_check}

Esse comando tem a mesma função e opções que o comando `cf check-route`.


## bluemix app route-map
{: #bluemix_app_route_map}

Mapeie uma rota para um aplicativo cf ou grupo de contêiner existente que tenha o domínio e o nome do host especificados.

```
bluemix app route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (necessário)</dt>
   <dd>O nome do aplicativo cf ou grupo de contêiner a ser mapeado com uma rota.</dd>
   <dt>DOMAIN (necessário)</dt>
   <dd>O domínio da rota. Por exemplo, mychinabluemix.net ou chinabluemix.net. </dd>
   <dt>-n <i>HOST_NAME</i> (opcional)</dt>
   <dd>O nome do host da rota. Se não fornecido, o nome do host será configurado para o nome do app ou grupo de contêiner por padrão.</dd>
   </dl>

<strong>Exemplos</strong>:

Mapeie uma rota para `my-app` com o domínio especificado:

```
bluemix app route-map my-app mychinabluemix.net
```

Mapeie uma rota para 'my-container-group' com o domínio e nome do host especificados:

```
bluemix app route-map my-container-group chinabluemix.net -n abc
```


## bluemix app route-unmap
{: #bluemix_app_route_unmap}

Remova o mapeamento da rota especificada de um aplicativo cf ou grupo de contêiner existente.

```
bluemix app route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (necessário)</dt>
   <dd>O nome do aplicativo cf ou grupo de contêiner.</dd>
   <dt>DOMAIN (necessário)</dt>
   <dd>O domínio da rota (por exemplo, mychinabluemix.net ou chinabluemix.net).</dd>
   <dt>-n <i>HOST_NAME</i> (opcional)</dt>
   <dd>O nome do host da rota. Se não fornecido, o nome do host será configurado para o nome do app ou grupo de contêiner por padrão.</dd>
   </dl>

<strong>Exemplos</strong>:

Remover o mapeamento `my-app.mychinabluemix.net` de `my-app`:

```
bluemix app route-unmap my-app mychianbluemix.net
```

Remover o mapeamento `abc.chinabluexmix.net` de `my-container-group`:

```
bluemix app route-unmap my-container-group chinabluemix.net -n abc
```


## bluemix app route-create
{: #bluemix_app_route_create}

Esse comando tem a mesma função e opções que o comando `cf create-route`.


## bluemix app route-delete
{: #bluemix_app_route_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-route`.


## bluemix app orphaned-routes-delete
{: #bluemix_app_orphaned_routes_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-orphaned-routes`.


## bluemix app domains
{: #bluemix_app_domains}

Esse comando tem a mesma função e opções que o comando `cf domains`.


## bluemix app domain-create
{: #bluemix_app_domain_create}

Esse comando tem a mesma função e opções que o comando `cf create-domain`.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-domain`.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

Esse comando tem a mesma função e opções que o comando `cf create-shared-domain`.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-shared-domain`.


## bluemix service offerings
{: #bluemix_service_offerings}


Esse comando tem a mesma função e opções que o comando `cf marketplace`.


## bluemix service list
{: #bluemix_service_list}

Esse comando tem a mesma função e opções que o comando `cf services`.


## bluemix service show
{: #bluemix_service_show}

Esse comando tem a mesma função e opções que o comando `cf service`.


## bluemix service create
{: #bluemix_service_create}

Esse comando tem a mesma função e opções que o comando `cf create-service`.


## bluemix service update
{: #bluemix_service_update}

Esse comando tem a mesma função e opções que o comando `cf update-service`.


## bluemix service delete
{: #bluemix_service_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-service`.


## bluemix service rename
{: #bluemix_service_rename}

Esse comando tem a mesma função e opções que o comando `cf rename-service`.


## bluemix service bind
{: #bluemix_service_bind}

Esse comando tem a mesma função e opções que o comando `cf bind-service`.


## bluemix service unbind
{: #bluemix_service_unbind}

Esse comando tem a mesma função e opções que o comando `cf unbind-service`.


## bluemix service key-create
{: #bluemix_service_key_create}

Esse comando tem a mesma função e opções que o comando `cf create-service-key`.


## bluemix service key-delete
{: #bluemix_service_key_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-service-key`.


## bluemix service keys
{: #bluemix_service_keys}

Esse comando tem a mesma função e opções que o comando `cf service-keys`.


## bluemix service key-show
{: #bluemix_service_key_show}

Esse comando tem a mesma função e opções que o comando `cf service-key`.


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Esse comando tem a mesma função e opções que o comando `cf create-user-provided-service`.


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Esse comando tem a mesma função e opções que o comando `cf update-user-provided-service`.


## bluemix catalog templates
{: #bluemix_catalog_templates}

Visualize os modelos de modelo no Bluemix.

```
bluemix catalog templates [-d]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:

   <dl>
   <dt>-d (opcional)</dt>
   <dd>Se a opção <i>-d</i> for especificada, a descrição de cada modelo também será exibida. Caso contrário, somente o ID e o nome de cada modelo serão mostrados.</dd>
   </dl>


## bluemix catalog template
{: #bluemix_catalog_template}

Visualize as informações detalhadas de um modelo de modelo especificado.

```
bluemix catalog template TEMPLATE_ID
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>TEMPLATE_ID (necessário)</dt>
   <dd>O ID do modelo de modelo. Use <i>modelos bluemix</i> para visualizar todos os IDs dos modelos.</dd>
   </dl>


<strong>Exemplos</strong>:

Visualize detalhes do modelo `mobileBackendStarter`:

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

Crie um aplicativo cf que seja baseado no modelo especificado com a URL e descrição especificadas. Por padrão, o novo app é iniciado automaticamente.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
   <dl>
   <dt>TEMPLATE_ID (necessário)</dt>
   <dd>O modelo no qual o aplicativo será baseado quando for criado. Use <i>bluemix templates</i> para ver todos os IDs dos modelos.</dd>
   <dt>CF_APP_NAME (necessário)</dt>
   <dd>O nome do aplicativo cf a ser criado.</dd>
   <dt>-u <i>URL</i> (opcional)</dt>
   <dd>A rota do aplicativo. Se não especificada, a rota será configurada pelo Bluemix automaticamente com base em seu nome de app e domínio padrão.</dd>
   <dt>-d <i>DESCRIPTION</i> (opcional)</dt>
   <dd>Descrição do aplicativo.</dd>
   <dt>--no-start (opcional)</dt>
   <dd>Não inicie o aplicativo automaticamente após ele ser criado. Se não especificado, o aplicativo será iniciado automaticamente após ser criado.</dd>
   </dl>


<strong>Exemplos</strong>:

Crie um aplicativo cf `my-app` baseado no modelo `javaHelloWorld`:

```
bluemix catalog template-run javaHelloWorld my-app
```

Crie um aplicativo `my-ruby-app` baseado no modelo `rubyHelloWorld`
com a rota `myrubyapp.chinabluemix.net` e a descrição `My first ruby app on
{{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Crie um aplicativo `my-python-app` baseado no modelo `pythonHelloWorld` sem início automático:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```

## bluemix billing account-usage
{: #bluemix_billing_account_usage}

Mostrar o uso mensal e os custos de sua conta.

```
bluemix billing account-usage [-d YYYY-MM] [--json]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:

<dl>
  <dt>-d MONTH_DATE (opcional)</dt>
  <dd>Exibir dados para mês e especificando data usando o formato AAAA-MM. Se não especificado, o uso do mês atual será mostrado.</dd>
  <dt>--json (opcional)</dt>
  <dd>Exibir o resultado de uso em formato JSON.</dd>
</dl>

<strong>Exemplos</strong>:

Mostrar o uso da minha conta e relatório de custo em 06/2016:

```
bluemix billing account-usage -d 2016-06
```

## bluemix billing org-usage
{: #bluemix_billing_org_usage}

Mostrar detalhes de uso mensal de uma organização. Essa operação pode ser executada somente por um gerente de faturamento da organização.

```
bluemix billing org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:

<dl>
  <dt>ORG_NAME (necessário)</dt>
  <dd>Nome da organização.</dd>
  <dt>-d MONTH_DATE (opcional)</dt>
  <dd>Exibir dados para mês e data especificada usando o formato AAAA-MM. Se não especificado, o uso do mês atual será mostrado.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Nome da região que hospeda a organização. Se configurado como 'all', o uso da organização em todas as regiões será mostrado.</dd>
  <dt>--json (opcional)</dt>
  <dd>Exibir o resultado de uso em formato JSON.</dd>
</dl>



## bluemix billing orgs-usage-summary
{: #bluemix_billing_orgs_usage_summary}

Mostrar o resumo de uso mensal para organizações na minha conta.

```
bluemix billing orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:

<dl>
  <dt>-d MONTH_DATE (opcional)</dt>
  <dd>Exibir dados para mês e data especificada usando o formato AAAA-MM. Se não especificado, o uso do mês atual será mostrado.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Nome da região que hospeda as organizações. Se configurado como 'all', o resumo de uso das organizações em todas as regiões será mostrado.</dd>
  <dt>--json (opcional)</dt>
  <dd>Exibir o resultado de uso em formato JSON.</dd>
</dl>


## bluemix plugin repos
{: #bluemix_plugin_repos}

Liste todos os repositórios de plug-in que estão registrados na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

<strong>Pré-requisitos</strong>: Nenhum


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Inclua um novo repositório de plug-in na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:

   <dl>
   <dt>REPO_NAME (necessário)</dt>
   <dd>O nome do repositório a ser incluído. É possível definir seu próprio nome para cada repositório.</dd>
   <dt>REPO_URL (necessário)</dt>
   <dd>A URL do repositório a ser incluído. A URL do repositório deve conter o protocolo (por exemplo, http://plugins.ng.bluemix.net em vez de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net é o repositório de plug-in oficial da CLI do Bluemix.</dd>
    </dl>


<strong>Exemplos</strong>:

Inclua o repositório de plug-in oficial da CLI do Bluemix CLI como `bluemix-repo`:

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Remova um repositório de plug-in da CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove REPO_NAME
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:
   <dl>
   <dt>REPO_NAME (necessário)</dt>
   <dd>O nome do repositório a ser removido.</dd>
   </dl>

<strong>Exemplos</strong>:

Remova o repositório `bluemix-repo` da CLI do {{site.data.keyword.Bluemix_notm}}:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Liste todos os plug-ins disponíveis em todos os repositórios incluídos ou um repositório específico.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:

   <dl>
   <dt>-r <i>REPO_NAME</i> (opcional)</dt>
   <dd>Liste somente os plug-ins no repositório especificado.</dd>
   </dl>

<strong>Exemplos</strong>:

Liste todos os plug-ins em todos os repositórios incluídos:

```
bluemix plugin repo-plugins
```

Liste todos os plug-ins no repositório `bluemix-repo`:

```
bluemix plugin repo-plugins -r bluemix-repo
```


## bluemix plugin list
{: #bluemix_plugin_list}

Liste todos os plug-ins instalados na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

<strong>Pré-requisitos</strong>: Nenhum


## bluemix plugin install
{: #bluemix_plugin_install}

Instale a versão específica de plug-in na CLI do {{site.data.keyword.Bluemix_notm}} a partir do caminho ou repositório especificado.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME (necessário)</dt>
   <dd>Se -r <i>REPO_NAME</i> não for especificado, o plug-in será instalado a partir do caminho local especificado ou da URL remota.</dd>
   <dt>-r <i>REPO_NAME</i> (opcional)</dt>
   <dd>O nome do repositório no qual o binário do plug-in está localizado.</dd>
   <dt>-v <i>VERSION</i> (opcional)</dt>
   <dd>A versão do plug-in a ser instalado. Se ela não for fornecida, a versão mais recente do plug-in será instalada. Essa opção é válida somente quando você instala o plug-in a partir do repositório.</dd>
    </dl>

<strong>Exemplos</strong>:

Instale um plug-in a partir do arquivo local:

```
bluemix plugin install /downloads/new_plugin
```

Instale um plug-in a partir da URL remota:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Instale o plug-in `IBM-Containers` da versão mais recente do repositório `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
Instale o plug-in `IBM-Containers` com a versão `0.5.800` do repositório `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```

## bluemix plugin update
{: #bluemix_plugin_update}

Faça upgrade do plug-in de um repositório

```
bluemix plugin update -r REPO_NAME [PLUGIN NAME [-v VERSION]]
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:
<dl>
 <dt>-r REPO_NAME (necessário)</dt>
 <dd>O nome do repositório no qual o binário do plug-in está localizado.</dd>
 <dt><i>PLUGIN_NAME</i> (opcional)</dt>
 <dd>Se não especificado, todos os plug-ins disponíveis para atualização no repositório especificado serão listados para seleção.</dd>
 <dt>-v <i>VERSION</i> (opcional)</dt>
 <dd>A versão do plug-in para a qual ele será atualizado. Se não fornecida, atualize o plug-in para a versão mais recente disponível.</dd>
</dl>

<strong>Exemplos</strong>:

Procure todos os upgrades disponíveis no repositório de plug-in "My-Repo":

```
bluemix plugin update -r My-Repo
```

Faça upgrade do plug-in "plugin-echo" no repositório "My-Repo" para o mais recente:

```
bluemix plugin update -r My-Repo plugin-echo
```

Atualize o plug-in "plugin-echo" no repositório "My-Repo" para a versão "1.0.1":

```
bluemix plugin update -r My-Repo plugin-echo -v 1.0.1
```

## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Desinstale o plug-in especificado a partir da CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:

   <dl>
   <dt>PLUGIN_NAME (necessário)</dt>
   <dd>O nome do plug-in a ser desinstalado.</dd>
    </dl>

<strong>Exemplos</strong>:

Desinstale o plug-in `IBM-Containers` que foi instalado anteriormente:

```
bluemix plugin uninstall IBM-Containers
```
