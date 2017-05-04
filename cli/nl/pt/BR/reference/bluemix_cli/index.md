---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução ao {{site.data.keyword.Bluemix_notm}} CLI
{: #getting-started}

O {{site.data.keyword.Bluemix_notm}} CLI fornece uma maneira unificada para você interagir com seus aplicativos, servidores virtuais, contêineres e outros serviços usando uma interface da linha de comandos. O {{site.data.keyword.Bluemix_notm}} CLI também integra ferramentas da comunidade, como o Cloud Foundry CLI, a CLI do Docker e a CLI do OpenStack, além de inicializar as configurações de ambiente para você interagir com diferentes tipos de cálculo.

**Restrição**: o {{site.data.keyword.Bluemix_notm}} CLI não é suportado por Cygwin, portanto, não use o {{site.data.keyword.Bluemix_notm}} CLI na janela de linha de comandos do Cygwin.

**Nota**: caso sua rede contenha um servidor proxy HTTP entre o host que executa a CLI e o {{site.data.keyword.Bluemix_notm}}, deve-se especificar o nome do host ou o endereço IP do servidor proxy na variável de ambiente HTTP_PROXY.

## Instalando o {{site.data.keyword.Bluemix_notm}} CLI
{: #install_bluemix_cli}

Antes de instalar o {{site.data.keyword.Bluemix_notm}} CLI, instale o [cf CLI ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

Para Mac OS e Windows, faça download do
[pacote de CLI do {{site.data.keyword.Bluemix_notm}}](/docs/cli/index.html#downloads) e execute o instalador.

Para o Linux, siga estas etapas:

  1. Faça download do pacote e extraia-o. Por
exemplo:

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. Acesse o diretório `Bluemix_CLI` e execute o comando `./install_bluemix_cli` com permissão raiz. É possível executar o comando como um usuário raiz ou usar o comando `sudo` para obter a permissão raiz. Por
exemplo:

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

Agora é possível começar a usar o {{site.data.keyword.Bluemix_notm}} CLI ou instalar plug-ins adicionais.

## Instalando um plug-in
{: #install_plug-in}

Como o Cloud Foundry CLI, o {{site.data.keyword.Bluemix_notm}} CLI suporta uma estrutura de extensão de plug-in para integrar outros comandos além daqueles integrados.

Para instalar um plug-in por meio de seu ambiente local, execute as etapas a seguir:

  1. Faça download do plug-in. Por
exemplo:

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. Para sistemas equivalentes ao UNIX, deve-se tornar o arquivo transferido por download executável usando o comando `chmod`. Por
exemplo:

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. Instale o plug-in usando o comando `bluemix plugin install`. Por
exemplo:

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Para instalar por meio de um servidor remoto, execute as etapas a seguir:

  1. Instale o plug-in por meio de uma URL remota diretamente usando o comando `bluemix plugin install`. Por
exemplo:

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

Também é possível instalar um plug-in por meio do repositório. O {{site.data.keyword.Bluemix_notm}} possui repositórios que hospedam os plug-ins do {{site.data.keyword.Bluemix_notm}} CLI e os plug-ins do Cloud Foundry CLI:

  * [Repositório
de plug-ins da CLI do Cloud Foundry](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg), que hospeda plug-ins para a CLI do Cloud Foundry.
  * [{{site.data.keyword.Bluemix_notm}} Repositório de plug-ins da CLI](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg), que hospeda plug-ins especificamente para a CLI do {{site.data.keyword.Bluemix_notm}}.

Para instalar por meio do repositório, execute as etapas a seguir:

  1. Localize o plug-in no repositório. Depois de ter instalado o {{site.data.keyword.Bluemix_notm}} CLI, o repositório oficial `Bluemix` é incluído por padrão. É possível listar os plug-ins no repositório do `Bluemix` usando o comando `bluemix plugin repo-plugins`. Por
exemplo:

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. Instale o plug-in do repositório `Bluemix` usando o comando `bluemix plugin install`. Por
exemplo:

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## Efetuando login no {{site.data.keyword.Bluemix_notm}} CLI
{: #log_bmcli}

Depois de instalar a CLI do {{site.data.keyword.Bluemix_notm}}, é possível efetuar login no {{site.data.keyword.Bluemix_notm}} usando o IBMid e a senha. Por
exemplo:

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

Agora você está pronto para usar os comandos integrados do {{site.data.keyword.Bluemix_notm}}. Por exemplo, execute o comando `bluemix catalog templates` para listar todos os modelos disponíveis do {{site.data.keyword.Bluemix_notm}}:

```
~$ bluemix catalog templates
Listing Bluemix boilerplate templates...

ID                      Name
pi-wdc-java-starter     Personality Insights Java Web Starter
xpages-starter          XPages Web Starter
mobileBackendStarter    Mobile Cloud
pi-wdc-nodejs-starter   Personality Insights Node.js Web Starter
mobileFirstPlatform     MobileFirst Services Starter
xspHelloWorld           IBM XPages
javacloudantbp          Java Cloudant Web Starter
```

# Comandos do {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

Versão: 0.4.6

A interface de linha de comandos (CLI) do {{site.data.keyword.Bluemix_notm}} fornece um conjunto de comandos que são agrupados por namespace para que os usuários interajam com o {{site.data.keyword.Bluemix_notm}}. Alguns
comandos do {{site.data.keyword.Bluemix_notm}} são wrappers de comandos cf existentes, enquanto outros fornecem recursos estendidos para usuários do {{site.data.keyword.Bluemix_notm}}. As
informações a seguir listam comandos que são suportados pela CLI do {{site.data.keyword.Bluemix_notm}} e incluem os seus nomes, opções, uso, pré-requisitos, descrições e exemplos.
{:shortdesc}

**Nota:** *Pré-requisitos* listam quais ações são necessárias antes de usar o comando. Os comandos que não têm ações de pré-requisito listam **Nenhum**. Caso contrário, os pré-requisitos podem incluir uma ou mais das ações a seguir:

<dl>
<dt>Nó de Extremidade</dt>
<dd>Um terminal de API deve ser configurado por meio de <code>bluemix api</code> antes de usar o comando.</dd>
<dt>Login</dt>
<dd>É necessário efetuar login usando o comando <code>bluemix login</code> antes de usar esse comando. Se
estiver efetuando login com o ID federado, use a opção '--sso' para
autenticar com a senha descartável.</dd>
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
 <td>[bluemix help](index.html#bluemix_help)</td>
 <td>[bluemix api](index.html#bluemix_api)</td>
 <td>[bluemix_login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](index.html#bluemix_info) </td>
 <td>[bluemix config](index.html#bluemix_config)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
  </tbody>
 </table>


<table summary="comandos do Bluemix que podem ser usados para gerenciar organizações, espaços e usuários.">
<caption>Tabela 2. Comandos para gerenciar organizações, espaços e usuários</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar organizações, espaços e usuários</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam account-users](index.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](index.html#bluemix_iam_account_users_delete)</td>
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account_user_invite)</td>
 <td>[bluemix iam account-user-reinvite](index.html#bluemix_iam_account_user_reinvite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-user-add](index.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](index.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 </tr>
 </tbody>
 </table>


<table summary="comandos do Bluemix que podem ser usados para gerenciar aplicativos Cloud Foundry.">
<caption>Tabela 3. Comandos para gerenciar apps cf</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar aplicativos cf</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 <td>[bluemix app list](index.html#bluemix_app_list)</td>
 <td>[bluemix app show](index.html#bluemix_app_show)</td>
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 </tr>
 <tr>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 <td>[bluemix app start](index.html#bluemix_app_start)</td>
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 </tr>
 <tr>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 <td>[bluemix app events](index.html#bluemix_app_events)</td>
 <td>[bluemix app files](index.html#bluemix_app_files)</td>
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 </tr>
 <tr>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
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
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](index.html#bluemix_service_list)</td>
 <td>[bluemix service show](index.html#bluemix_service_show)</td>
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](index.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](index.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
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
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](index.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix bss account-usage](index.html#bluemix_bss_account_usage)</td>
 <td>[bluemix bss org-usage](index.html#bluemix_bss_org_usage)</td>
 <td>[bluemix bss orgs-usage-summary](index.html#bluemix_orgs_usage_summary)</td>
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td>
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 </tr>
 <tr>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td></td>
 <td></td>
 </tr>
  </tbody>
 </table>


<table summary="comandos do Bluemix que podem ser usados para gerenciar configurações de rede.">
<caption>Tabela 6. Comandos para gerenciar configurações de rede</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar configurações de rede</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td>
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td>
 </tr>
 <tr>
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td>
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td>
 </tr>
 <tr>
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td>
 <td></td>
 </tr>
  </tbody>
 </table>



### bluemix help
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



### bluemix api
{: #bluemix_api}
Configure ou visualize o terminal da API do {{site.data.keyword.Bluemix_notm}}. Esse comando agrupa o comando `cf api`.

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>Pré-requisitos</strong>: Nenhum

<strong>Opções de comando</strong>:
   <dl>
   <dt>API_ENDPOINT (opcional)</dt>
   <dd>O terminal da API que é o destino, por exemplo, `https://api.chinabluemix.net`. Se as opções *API_ENDPOINT* e `--unset` não forem ambas especificadas, o terminal de API atual será exibido.</dd>
   <dt>--unset (opcional)</dt>
   <dd>Remova a configuração do terminal de API.</dd>
    </dl>
<strong>Exemplos</strong>:

Configure o terminal da API para api.chinabluemix.net:

```
bluemix api api.chinabluemix.net
```

Visualize o terminal de API atual:

```
bluemix api
```

Desconfigure o terminal de API:

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

Efetue login do usuário. Esse comando agrupa o comando `cf login`. As opções de comando são as mesmas que as opções de comando de `cf login`.

```
bluemix login [OPTIONS...]
```

<strong>Pré-requisitos</strong>: Terminal

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>Opções de comando</strong>:
Para obter informações sobre as opções suportadas pelo comando `login`, veja as informações de uso do comando `cf login` para comandos cf para gerenciar aplicativos.

<strong>Nota</strong>:
se estiver efetuando login com o ID federado, use a opção '--sso'
para autenticar com a senha descartável.

### bluemix logout
{: #bluemix_logout}

Efetue logout do usuário. Esse comando agrupa o comando `cf logout`.

```
bluemix logout
```

<strong>Pré-requisitos</strong>: Nenhum


### bluemix target
{: #bluemix_target}


Configure ou visualize a organização ou o espaço de destino. Esse comando agrupa o comando `cf target`.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Pré-requisitos</strong>: Terminal, Login

<strong>Opções de comando</strong>:
   <dl>
   <dt>-o <i>ORG_NAME</i> (opcional)</dt>
   <dd>O nome da organização que será o destino.</dd>
   <dt>-s <i>SPACE_NAME</i> (opcional)</dt>
   <dd>O nome do espaço que será o destino.</dd>
   </dl>
Se -o *ORG_NAME* ou -s *SPACE_NAME* não forem especificados, a organização e o espaço atuais serão exibidos.
<strong>Exemplos</strong>:

Configure a organização atual como `MyOrg` e o espaço como `MySpace`:

```
bluemix target -o MyOrg -s MySpace
```

Visualize a organização e o espaço atuais:

```
bluemix target
```


### bluemix info
{: #bluemix_info}

Visualize as informações básicas do {{site.data.keyword.Bluemix_notm}}, incluindo a região atual, a versão do controlador de nuvem e alguns terminais úteis, como terminais para login e a troca de token de acesso.

```
bluemix info
```

<strong>Pré-requisitos</strong>: Terminal


### bluemix config
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


### bluemix curl
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


### bluemix iam orgs
{: #bluemix_iam_orgs}

Liste todas as organizações

```
bluemix iam orgs [-r REGION --guid]
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

### bluemix iam org
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

### bluemix iam org-create
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


### bluemix iam org-replicate
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


### bluemix iam org-rename
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

### bluemix iam org-delete
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


### bluemix iam spaces
{: #bluemix_iam_spaces}

Esse comando tem a mesma função e opções que o comando `cf spaces`.


### bluemix iam space
{: #bluemix_iam_space}

Esse comando tem a mesma função e opções que o comando `cf space`.


### bluemix iam space-create
{: #bluemix_iam_space_create}

Esse comando tem a mesma função e opções que o comando `cf create-space`.


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


Esse comando tem a mesma função e opções que o comando `cf rename-space`.


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


Esse comando tem a mesma função e opções que o comando `cf delete-space`.


### bluemix iam account-users
{: #bluemix_iam_account_users}

Exibe os usuários associados à conta. Essa operação pode ser executada somente pelo proprietário da conta.

```
bluemix iam account-users
```

### bluemix iam account-user-invite
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
   <dd>O nome da função de organização para a qual esse usuário é convidado. Por exemplo:
   <ul>
  <li>OrgManager: essa função pode convidar e gerenciar usuários, selecionar e mudar planos e configurar limites de gastos.</li>
  <li>BillingManager: essa função pode criar e gerenciar a conta de cobrança e informações de pagamento.</li>
  <li>OrgAuditor: essa função possui acesso somente leitura para informações e relatórios da organização.</li>
  </ul> </dd>
   <dt>SPACE_NAME (necessário)</dt>
   <dd>O nome do espaço para o qual esse usuário é convidado.</dd>
   <dt>SPACE_ROLE (necessário)</dt>
   <dd>O nome do espaço para o qual esse usuário é convidado. O nome da função do espaço para o qual esse usuário é convidado. Por exemplo:
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


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Reenviar o convite a um usuário (é necessário ser o gerente da organização ou o proprietário da conta)
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
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

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Inclua um usuário na organização (gerenciador de organização requerido).
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
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

### bluemix iam org-role-set
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
   <dd>O nome da função de organização para a qual esse usuário é designado. Por exemplo:
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


### bluemix iam org-role-unset
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
   <dd>O nome da função de organização da qual esse usuário é removido. Por exemplo:
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


### bluemix iam space-users
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


### bluemix iam space-role-set
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
   <dd>O nome da função de espaço para a qual esse usuário é designado. Por exemplo:
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

### bluemix iam space-role-unset
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
   <dd>O nome da função de espaço da qual esse usuário é removido. Por exemplo:
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


### bluemix app push
{: #bluemix_app_push}

Esse comando tem a mesma função e opções que o comando `cf push`.


### bluemix app list
{: #bluemix_app_list}

Esse comando tem a mesma função e opções que o comando `cf apps`.


### bluemix app show
{: #bluemix_app_show}

Esse comando tem a mesma função e opções que o comando `cf app`.


### bluemix app scale
{: #bluemix_app_scale}

Esse comando tem a mesma função e opções que o comando `cf scale`.


### bluemix app delete
{: #bluemix_app_delete}

Esse comando tem a mesma função e opções que o comando `cf delete`.


### bluemix app rename
{: #bluemix_app_rename}

Esse comando tem a mesma função e opções que o comando `cf rename`.


### bluemix app start
{: #bluemix_app_start}

Esse comando tem a mesma função e opções que o comando `cf start`.


### bluemix app stop
{: #bluemix_app_stop}

Esse comando tem a mesma função e opções que o comando `cf stop`.


### bluemix app restart
{: #bluemix_app_restart}

Esse comando tem a mesma função e opções que o comando `cf restart`.


### bluemix app restage
{: #bluemix_app_restage}


Esse comando tem a mesma função e opções que o comando `cf restage`.


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


Esse comando tem a mesma função e opções que o comando `cf restart-app-instance`.


### bluemix app events
{: #bluemix_app_events}

Esse comando tem a mesma função e opções que o comando `cf events`.


### bluemix app files
{: #bluemix_app_files}

Esse comando tem a mesma função e opções que o comando `cf files`.


### bluemix app logs
{: #bluemix_app_logs}

Esse comando tem a mesma função e opções que o comando `cf logs`.


### bluemix app env
{: #bluemix_app_env}

Esse comando tem a mesma função e opções que o comando `cf env`.


### bluemix app env-set
{: #bluemix_app_env_set}

Esse comando tem a mesma função e opções que o comando `cf set-env`.


### bluemix app env-unset
{: #bluemix_app_env_unset}

Esse comando tem a mesma função e opções que o comando `cf unset-env`.


### bluemix app stacks
{: #bluemix_app_stacks}

Esse comando tem a mesma função e opções que o comando `cf stacks`.


### bluemix app stack
{: #bluemix_app_stack}

Esse comando tem a mesma função e opções que o comando `cf stack`.


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

Esse comando tem a mesma função e opções que o comando `cf create-app-manifest`.


### bluemix service offerings
{: #bluemix_service_offerings}


Esse comando tem a mesma função e opções que o comando `cf marketplace`.


### bluemix service list
{: #bluemix_service_list}

Esse comando tem a mesma função e opções que o comando `cf services`.


### bluemix service show
{: #bluemix_service_show}

Esse comando tem a mesma função e opções que o comando `cf service`.


### bluemix service create
{: #bluemix_service_create}

Esse comando tem a mesma função e opções que o comando `cf create-service`.


### bluemix service update
{: #bluemix_service_update}

Esse comando tem a mesma função e opções que o comando `cf update-service`.


### bluemix service delete
{: #bluemix_service_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-service`.


### bluemix service rename
{: #bluemix_service_rename}

Esse comando tem a mesma função e opções que o comando `cf rename-service`.


### bluemix service bind
{: #bluemix_service_bind}

Esse comando tem a mesma função e opções que o comando `cf bind-service`.


### bluemix service unbind
{: #bluemix_service_unbind}

Esse comando tem a mesma função e opções que o comando `cf unbind-service`.


### bluemix service key-create
{: #bluemix_service_key_create}

Esse comando tem a mesma função e opções que o comando `cf create-service-key`.


### bluemix service key-delete
{: #bluemix_service_key_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-service-key`.


### bluemix service keys
{: #bluemix_service_keys}

Esse comando tem a mesma função e opções que o comando `cf service-keys`.


### bluemix service key-show
{: #bluemix_service_key_show}

Esse comando tem a mesma função e opções que o comando `cf service-key`.


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Esse comando tem a mesma função e opções que o comando `cf create-user-provided-service`.


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Esse comando tem a mesma função e opções que o comando `cf update-user-provided-service`.


### bluemix catalog templates
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


### bluemix catalog template
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


### bluemix catalog template-run
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


### bluemix network regions
{: #bluemix_network_regions}

Visualize as informações para todas as regiões no {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

<strong>Pré-requisitos</strong>: Terminal


### bluemix network region-set
{: #bluemix_network_region_set}

Alterne para a região especificada. Esse comando redestina automaticamente para a mesma organização e o mesmo espaço na nova região, se possível. Caso contrário, o comando solicita que o usuário selecione uma nova organização e um novo espaço se o usuário já tiver efetuado login. O terminal de API é mudado apropriadamente.

```
bluemix network region-set REGION_NAME
```

<strong>Pré-requisitos</strong>: Terminal

<strong>Opções de comando</strong>:

   <dl>
   <dt>REGION_NAME (necessário)</dt>
   <dd>O nome da região para a qual você deseja alternar. É possível usar o comando <i>bluemix network regions</i> para ver todos os nomes de regiões.</dd>
    </dl>

<strong>Exemplos</strong>:

Configure a região atual como `eu-gb`:

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

Esse comando tem a mesma função e opções que o comando `cf routes`.


### bluemix network route-check
{: #bluemix_network_route_check}

Esse comando tem a mesma função e opções que o comando `cf check-route`.


### bluemix network route-map
{: #bluemix_network_route_map}

Mapeie uma rota para um aplicativo cf ou grupo de contêiner existente que tenha o domínio e o nome do host especificados.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix network route-map my-app mychinabluemix.net
```

Mapeie uma rota para 'my-container-group' com o domínio e nome do host especificados:

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

Remova o mapeamento da rota especificada de um aplicativo cf ou grupo de contêiner existente.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix network route-unmap my-app mychianbluemix.net
```

Remover o mapeamento `abc.chinabluexmix.net` de `my-container-group`:

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

Esse comando tem a mesma função e opções que o comando `cf create-route`.


### bluemix network route-delete
{: #bluemix_network_route_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-route`.


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-orphaned-routes`.


### bluemix network domains
{: #bluemix_network_domains}

Esse comando tem a mesma função e opções que o comando `cf domains`.


### bluemix network domain-create
{: #bluemix_network_domain_create}

Esse comando tem a mesma função e opções que o comando `cf create-domain`.


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-domain`.


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Esse comando tem a mesma função e opções que o comando `cf create-shared-domain`.


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-shared-domain`.



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

Mostrar o uso mensal e os custos de sua conta.

```
bluemix bss account-usage [-d YYYY-MM] [--json]
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
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

Mostrar detalhes de uso mensal de uma organização. Essa operação pode ser executada somente por um gerente de faturamento da organização.

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
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



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

Mostrar o resumo de uso mensal para organizações na minha conta.

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
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



### bluemix security cert
{: #bluemix_security_cert}

Liste as informações de certificado de um domínio.

```
bluemix security cert DOMAIN_NAME
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
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

Inclua um certificado no domínio especificado na organização atual.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
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
   <dt>--verify-client (opcional)</dt>
   <dd>Se ativar a verificação do certificado de cliente.</dd>
   </dl>


<strong>Exemplos</strong>:

Inclua um certificado no domínio `ibmcxo-eventconnect.com`:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

Remova um certificado do domínio especificado na organização atual.

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>DOMAIN (necessário)</dt>
   <dd>Domínio do qual remover o certificado.</dd>
   <dt>-f (opcional)</dt>
   <dd>Force a exclusão sem confirmação.</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

Liste todos os repositórios de plug-in que estão registrados na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

<strong>Pré-requisitos</strong>: Nenhum


### bluemix plugin repo-add
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


### bluemix plugin repo-remove
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


### bluemix plugin repo-plugins
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


### bluemix plugin list
{: #bluemix_plugin_list}

Liste todos os plug-ins instalados na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

<strong>Pré-requisitos</strong>: Nenhum


### bluemix plugin install
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

Instale o plug-in `container-service` da versão mais recente no repositório
`bluemix-repo`:

```
bluemix plugin install container-service -r bluemix-repo
```
Instale o plug-in `container-service` com a versão `0.5.800` no repositório
`bluemix-repo`:
```
bluemix plugin install container-service -r bluemix-repo -v 0.1.217
```






### bluemix plugin uninstall
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

Desinstale o plug-in `container-service` que foi instalado anteriormente:

```
bluemix plugin uninstall container-service
```



# Links Relacionados
{: #rellinks}

## Links Relacionados
{: #general}

* [bx tool](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg)
