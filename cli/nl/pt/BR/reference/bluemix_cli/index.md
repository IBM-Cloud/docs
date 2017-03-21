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

<table summary="comandos do Bluemix que podem ser usados para gerenciar contêineres no Bluemix.">
<caption>Tabela 7. Comandos para gerenciar contêineres no Bluemix</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar contêineres no Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](index.html#bluemix_ic_service-bind)</td>
 <td>[bluemix ic service-unbind](index.html#bluemix_ic_service-unbind)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](index.html#unpause)</td>
 <td>[bluemix ic unprovision](index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
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

Exiba a ajuda para o plug-in `ic`:

```
bluemix help ic
```

ou

```
bluemix ic help
```

Exiba ajuda para o comando `group-create` sob o plug-in `ic`:

```
bluemix ic help group-create
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

Mapeie uma rota para um aplicativo cf ou grupo de contêineres existente que tenha o domínio e o nome do host especificados.

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
   <dd>O nome do host da rota. Se não fornecido, o nome do host será configurado para o nome do app ou grupo de contêineres por padrão.</dd>
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

Remova o mapeamento da rota especificada de um aplicativo cf ou grupo de contêineres existente.

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
   <dd>O nome do host da rota. Se não fornecido, o nome do host será configurado para o nome do app ou grupo de contêineres por padrão.</dd>
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

Instale o plug-in `IBM-Containers` da versão mais recente do repositório `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
Instale o plug-in `IBM-Containers` com a versão `0.5.800` do repositório `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
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

Desinstale o plug-in `IBM-Containers` que foi instalado anteriormente:

```
bluemix plugin uninstall IBM-Containers
```


### bluemix ic attach
{: #bluemix_ic_attach}

Controlar um contêiner em execução ou visualizar sua saída. Use `CTRL+C` para sair e parar o contêiner. Esse comando chama a CLI do Docker. Para obter mais informações, veja o comando [attach](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>--no-stdin (opcional)</dt>
   <dd>Não inclua a entrada padrão.</dd>
   <dt>--sig-proxy (opcional)</dt>
   <dd>Efetue proxy de todos os sinais recebidos para o processo. O valor padrão é
<i>true</i>.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
    </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para conectar-se ao contêiner `my_container`:
```
bluemix ic attach my_container
```


### bluemix ic build
{: #bluemix_ic_build}

Chame o serviço de construção IBM Containers para construir uma imagem do Docker localmente ou em seu repositório privado do {{site.data.keyword.Bluemix_notm}}. Esse comando chama a CLI do Docker. Para obter mais informações, veja o comando [build](https://docs.docker.com/engine/reference/commandline/build/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (necessário)</dt>
   <dd>O nome de repositório a ser aplicado na imagem que é criada.</dd>
   <dt>--no-cache (opcional)</dt>
   <dd>Não use o cache quando a imagem é construída. O padrão é <i>false</i>.</dd>
   <dt>--pull (opcional)</dt>
   <dd>Tentativa de realizar pull da imagem base a partir do registro mesmo se for armazenada em cache.</dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Suprima a saída detalhada que é gerada pelos contêineres. O padrão é <i>false</i>.</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (obrigatório)</dt>
   <dd>O caminho para o Dockerfile e o contexto no host local.</dd>
    </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para construir uma imagem denominada *myimage*. O Dockerfile e outros artefatos a serem usados na construção estão no mesmo diretório a partir do qual o comando está em execução. Como o registro e o namespace são incluídos com o nome da imagem, a imagem será construída no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


### bluemix ic cp
{: #bluemix_ic_cp}
Copie arquivos ou pastas entre um contêiner e o sistema de arquivos local. Esse comando chama a CLI do Docker. Para obter mais informações, veja o comando [cp](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.


### bluemix ic cpi
{: #bluemix_ic_cpi}

Acesse uma imagem do Docker Hub ou uma imagem de seu registro local e copie a imagem para seu repositório privado do {{site.data.keyword.Bluemix_notm}}.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i> (obrigatório)</dt>
   <dd>O repositório de origem e o nome da imagem.</dd>
   <dt><i>DESTINATION_IMAGE</i> (obrigatório)</dt>
   <dd>A URL de repositório privado do {{site.data.keyword.Bluemix_notm}}, que inclui o namespace e o nome da imagem de destino. Uma marcação para a imagem é opcional.</dd>
   </dl>

<strong>Exemplos</strong>:

Copie uma imagem do repositório de origem para seu repositório privado e inclua uma tag para a imagem:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copie a imagem `sinatra` do repositório `training` para seu repositório privado `registry.ng.bluemix.net/mynamespace` e o nome da imagem como `mysinatra`. Inclua uma tag `v1` para a imagem `mysinatra`.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


### bluemix ic exec
{: #bluemix_ic_exec}

Executar um comando em um contêiner. Para obter mais informações, veja o comando [exec](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-d|--detach (opcional)</dt>
   <dd>Execute o comando especificado no segundo plano.</dd>
   <dt>-it (opcional)</dt>
   <dd>Modo interativo. Manter a exibição da entrada padrão. Digite <i>exit</i> para sair.</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i> (opcional)</dt>
   <dd>O nome do usuário.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>O comando a ser executado no contêiner ou nos contêineres especificados.</dd>
   </dl>

<strong>Exemplos</strong>:

Execute o comando `bash` no contêiner `my_container` no modo interativo:

```
bluemix ic exec -it my_container bash
```

Execute o comando `date` no contêiner `my_container`:

```
bluemix ic exec my_container date
```


### bluemix ic group-create
{: #bluemix_ic_group_create}

Crie um grupo de contêiner escalável.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRONMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (obrigatório)</dt>
   <dd>A imagem a ser incluída em cada instância de contêiner no grupo de contêiner. É possível listar comandos após a imagem, mas não coloque nenhuma opção após a imagem. Inclua todas as opções antes de especificar uma imagem. <br><br>Se você usar uma imagem no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização, especifique a imagem no formato: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>Se você usar uma imagem fornecida pelo IBM Containers, não inclua o namespace de sua organização. Especifique a imagem no formato: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt>--name <i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>Designe um nome ao grupo. <i>-n</i> está descontinuado.<br>
   <strong>Dica:</strong> o nome do contêiner deve iniciar com uma letra. O nome pode incluir letras maiúsculas, letras minúsculas, números, pontos., sublinhados _ ou hifens -.</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (opcional)</dt>
   <dd>Designe um limite de memória ao grupo em MB. Ao criar um grupo de contêiner a partir da CLI, o valor padrão para cada instância de contêiner é <i>64</i> MB. Ao criar um grupo de contêiner a partir do Painel do {{site.data.keyword.Bluemix_notm}}, o valor padrão para cada instância de contêiner é <i>256</i> MB. Os valores aceitos são <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> e <i>2048</i>. Após um limite de memória ser designado, o valor não poderá ser mudado.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (opcional)</dt>
   <dd>O nome do host, como <i>mycontainerhost</i>. O host e o domínio são combinados para formar a URL da rota pública completa, como <i>http://mycontainerhost.mybluemix.net</i>. Ao revisar os detalhes de um grupo de contêineres com o comando <i>bluemix ic group-inspect</i>, o host e o domínio são listados juntos como a rota.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>Geralmente, o domínio é <i>.mybluemix.net</i>. O host e o domínio são combinados para formar a URL da rota pública completa, como <i>http://mycontainerhost.mybluemix.net</i>. Ao revisar os detalhes de um grupo de contêineres com o comando <i>bluemix ic group-inspect</i>, o host e o domínio são listados juntos como a rota.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (opcional)</dt>
   <dd>Configure a variável de ambiente. Liste diversas chaves separadamente. Se aspas forem incluídas, inclua-as em torno do nome da variável de ambiente e do valor. Por
exemplo: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  A tabela a seguir mostra algumas variáveis de ambiente comumente usadas que podem ser especificadas:</dd>
    </dl>


|  Variável do ambiente                              |     Descrição                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Faça a ligação de um serviço a um contêiner. Use a variável de ambiente `CCS_BIND_APP` para ligar um aplicativo ao contêiner. O app é ligado ao serviço de destino e age como uma ponte que permite que o {{site.data.keyword.Bluemix_notm}} traga as informações de `VCAP_SERVICES` de seu app de ponte para a instância do contêiner em execução.|
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | Para ligar um serviço Bluemix diretamente a um contêiner, sem usar um app de ponte, use CCS_BIND_SRV. Essa ligação permite que o Bluemix injete as informações de VCAP_SERVICES na instância do contêiner em execução. Para listar vários serviços do Bluemix, inclua-os como parte da mesma variável de ambiente. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Inclua um arquivo de log a ser monitorado no contêiner. Inclua a variável de ambiente `LOG_LOCATIONS` com um caminho para o arquivo de log. |
{: caption="Table 8. Commonly used environment variables" caption-side="top"}


 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i> (opcional)</dt>
   <dd> Importe variáveis de ambiente de um arquivo em que ENVFILE é o caminho para seu
arquivo no diretório local. Cada linha do arquivo representa um par key=value. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (opcional)</dt>
   <dd>Anexe um volume a um contêiner especificando os detalhes no formato <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: O ID ou o nome do volume.</li>
   <li><i>CONTAINER_PATH</i>: O caminho absoluto para o volume no contêiner.</li>
   <li>ro: opcional. Especificar <i>ro</i> torna o volume somente leitura em vez de leitura/gravação padrão.</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (opcional)</dt>
   <dd>Exponha a porta para o tráfego HTTP. Contêineres em seu grupo devem atender na porta HTTP. As solicitações HTTPS não podem ser feitas. Para os grupos de contêineres, não é possível incluir várias portas. <br><br>Ao especificar uma porta, você disponibiliza o app para o Balanceador de carga do {{site.data.keyword.Bluemix_notm}} ou para contêineres que estão tentando atingir o host no mesmo espaço do {{site.data.keyword.Bluemix_notm}}. Em seguida, o balanceador de carga ou contêineres do {{site.data.keyword.Bluemix_notm}} podem usar a porta para atingir o host e o app no mesmo espaço do {{site.data.keyword.Bluemix_notm}}. Se uma porta for especificada no Dockerfile para a imagem que você está usando, inclua essa porta. <br>
   <strong>Dicas</strong>: <ul>
   <li>Para a imagem do servidor Liberty certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 9080.</li>
   <li>Para a imagem do Node.js certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 8000.</li>
   </ul>
   </dd>
   <dt>-P (opcional)</dt>
   <dd>Publicar todas as portas</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>O número mínimo de instâncias. O padrão é 1. Se você configurar um número mínimo de instâncias, o valor não poderá ser mudado após a criação do grupo de contêiner.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>O número máximo de instâncias. O padrão é 2. Se você configurar um número máximo de instâncias, o valor não poderá ser mudado após a criação do grupo de contêiner.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>O número de instância que você precisa. O padrão é 2.</dd>
   <dt>--auto (opcional)</dt>
   <dd>Quando o grupo de contêiner é criado e a recuperação automática é ativada, o IBM Containers verifica o funcionamento de cada instância com uma solicitação de HTTP para a porta designada.<br>
   Se nenhuma resposta for recebida de uma instância do contêiner em dois intervalos subsequentes de 90 segundos, a instância será removida e substituída por uma nova instância. Nenhuma ação será executada se o contêiner for responsivo. Esse processo é repetido continuamente. Durante uma janela de 30 minutos, se o número total de contêineres diferentes que são membros do grupo for igual ou exceder três vezes o tamanho máximo observado do grupo, a recuperação automática será desativada permanentemente para o grupo de contêiner. Para ativar a recuperação automática novamente, deve-se recriar o grupo de contêineres.</dd>
  <dt>--anti (opcional)</dt>
  <dd> Use antiafinidade para tornar seu grupo de contêiner mais altamente
disponível. A opção --anti força cada instância de contêiner em seu grupo a ser
colocada em um nó de cálculo físico separado, o que reduz as chances de impacto de todos os
contêineres em um grupo devido a uma falha no hardware. Você pode não ser capaz de usar
essa opção com tamanhos de grupo maiores porque cada região e organização do Bluemix tem
um conjunto limitado de nós de cálculo disponíveis para implementação. Se sua
implementação não for bem-sucedida, reduza o número de instâncias de contêiner no grupo
ou remova a opção --anti. </dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>O comando e os argumentos são passados para o grupo de contêiner executar. Esse comando deve ser um comando de longa execução. Não use um comando de curta duração que não é executado por muito tempo, por exemplo, <i>/bin/date</i>, pois o comando de curta duração pode fazer o contêiner travar.  <br> <strong>Notas:</strong> <ul>
   <li>O comando e seus argumentos devem vir no final da linha de comandos <i>bluemix ic run</i>.</li>
   <li>Se os argumentos de comando incluírem o hífen -, como em <i>-c</i> no comando de exemplo anterior, o comando deverá ser precedido por dois hifens --.</li>
   </ul></dd>
   </dl>


<strong>Exemplos</strong>:

Crie um grupo de contêiner `my_container_group` usando a imagem `registry.ng.bluemix.net/ibmnode` fornecida pelo IBM Containers e, em seguida, execute o comando de longa execução `ping localhost` nesse grupo de contêiner:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Crie um grupo de contêiner `my_container_group` usando a imagem `registry.ng.bluemix.net/ibmnode` fornecida pelo IBM Containers e, em seguida, execute o comando de longa execução `tail -f /dev/null` nesse grupo de contêiner:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Crie um grupo escalável `mygroup` com a recuperação automática ativada usando a imagem `registry.ng.bluemix.net/ibmliberty`. A porta é `9080`, o nome do host é `mycontainerhost` e o nome do domínio é `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


### bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Visualize informações detalhadas, como variáveis de ambiente, portas ou memória, especificadas para um grupo de contêiner quando criado.

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para inspecionar o grupo de contêiner `my_group`:
```
bluemix ic group-inspect my_group
```


### bluemix ic group-instances
{: #bluemix_ic_group_instances}

Liste instâncias de um grupo de contêiner especificado.

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

Liste todas as instâncias do grupo de contêiner `my_group`:
```
bluemix ic group-instances my_group
```


### bluemix ic group-remove
{: #bluemix_ic_group_remove}

Remova um grupo de contêiner de um espaço.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-f|--force (opcional)</dt>
   <dd>Força a remoção de um contêiner em execução ou com falha.</dd>
   <dt><i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover um grupo de contêiner, em que `my_group` é o nome do grupo de contêiner.
```
bluemix ic group-remove my_group
```


### bluemix ic group-update
{: #bluemix_ic_group_update}

Atualize um grupo de contêiner.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**Dica:** para atualizar o nome do host ou o domínio para um grupo de contêiner, use `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`.

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
 <dl>
   <dt>--anti (opcional)</dt>
   <dd>Use antiafinidade para tornar seu grupo de contêiner mais altamente
disponível. A opção --anti força cada instância de contêiner em seu grupo a ser colocada em um nó de cálculo físico separado, reduzindo as chances de todos os contêineres em um grupo sofrerem um impacto devido a uma falha no hardware. Você pode não ser capaz de usar
essa opção com tamanhos de grupo maiores porque cada região e organização do Bluemix tem
um conjunto limitado de nós de cálculo disponíveis para implementação. Se sua
implementação não for bem-sucedida, reduza o número de instâncias de contêiner no grupo
ou remova a opção --anti.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>O número de instância que você precisa. O padrão é <i>2</i>.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(opcional)</dt>
   <dd>Configure a variável de ambiente. Liste diversas chaves separadamente. Se aspas forem incluídas, inclua-as em torno do nome da variável de ambiente e do valor. Por
exemplo: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.</dd>
   <dt><i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para atualizar o grupo de contêiner `my_group`:
```
bluemix ic group-update --desired 5 my_group
```


### bluemix ic groups
{: #bluemix_ic_groups}

Liste grupos de contêineres no repositório privado do {{site.data.keyword.Bluemix_notm}} da organização.

```
bluemix ic groups [-q]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
	<dl>
	<dt>-q (opcional)</dt>
   	<dd>Exibir somente IDs de grupos</dd>
	</dl>


### bluemix ic images
{: #bluemix_ic_images}

Visualize uma lista de todas as imagens disponíveis no repositório privado do {{site.data.keyword.Bluemix_notm}} da organização. Para obter mais informações, veja o comando [images](https://docs.docker.com/engine/reference/commandline/images){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker. A lista inclui o ID da imagem, a data de criação e o nome da imagem.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-a|--all (opcional)</dt>
   <dd>Inclua todas as camadas de imagem para cada imagem no repositório de sua organização, não apenas a camada mais recente.</dd>
   <dt>-f (opcional)</dt>
   <dd>Filtre a lista de imagens pela condição fornecida.</dd>
   <dt>--no-trunc (opcional)</dt>
   <dd>Não trunque a saída.</dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Exiba somente os IDs numéricos.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para receber uma lista de imagens disponíveis para a organização:
```
bluemix ic images
```


### bluemix ic info
{: #bluemix_ic_info}

Visualize um conjunto de informações que descreva o estado da instância de serviço de nuvem do contêiner. As informações incluem o limite de contêineres, o uso de contêineres, contêineres que estão em execução, o limite de memória, o uso de memória, o limite de endereço IP flutuante, o uso de endereço IP flutuante, a URL do host CCS, a URL do host de registro e o status do modo de depuração.

```
bluemix ic info
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino


### bluemix ic init
{: #bluemix_ic_init}

Inicialize o ambiente de contêineres em sua máquina local para usar os recursos integrais do serviço IBM Containers.

```
bluemix ic init
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

**Nota:** antes da inicialização, assegure que a CLI do Docker (docker) esteja instalada e configurada em sua variável de ambiente PATH. Para alternar para outra região, use o comando `bluemix region-set`.

<strong>Exemplos</strong>:

Alterne para a região `us-south`:

```
bluemix region-set us-south
```


### bluemix ic inspect
{: #bluemix_ic_inspect}

Visualize as informações sobre um contêiner. Para obter mais informações, consulte o comando [inspect](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} na ajuda do Docker.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>IMAGE</i> (obrigatório)</dt>
   <dd>Visualize informações detalhadas sobre uma imagem específica especificando o nome ou o ID da imagem.</dd>
   <dt>images (necessário)</dt>
   <dd>Visualize informações detalhadas sobre todas as imagens em seu repositório.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>Visualize informações detalhadas sobre um contêiner específico especificando o nome ou o ID do contêiner.</dd>
   </dl>

**Dica:** apenas um de *IMAGEM*, *imagens* ou *CONTÊINER* pode ser especificado por vez.

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para inspecionar um contêiner denominado `proxy`:
```
bluemix ic inspect proxy
```


### bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Ligar um endereço IP flutuante disponível a um contêiner.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obrigatório)</dt>
   <dd>O endereço IP a ser ligado.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O ID ou o nome do contêiner a ser ligado.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para ligar o IP endereço `192.123.12.12` ao contêiner `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


### bluemix ic ip-release
{: #bluemix_ic_ip_release}

Liberar um endereço IP flutuante da instância do serviço de nuvem do contêiner.

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obrigatório)</dt>
   <dd>O endereço IP para liberação.</dd>
   </dl>


### bluemix ic ip-request
{: #ip_request}
Solicite um novo endereço IP flutuante.

```
bluemix ic ip-request [-q]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-q (opcional)</dt>
   <dd>Liste somente os endereços IP, sem os IDs dos contêineres que estão ligados a esses endereços IP.</dd>
   </dl>


### bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Desvincular um endereço IP flutuante de seu contêiner.

Endereços IP públicos são um recurso limitado no IBM Containers. Portanto, endereços IP públicos que são alocados para um espaço e não ligados a um contêiner são periodicamente recuperados de usuários de avaliação grátis, aproximadamente semanalmente. Endereços IP públicos desvinculados nunca são recuperados de clientes de pagamento por uso ou de clientes de assinatura.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obrigatório)</dt>
   <dd>O endereço IP a ser desvinculado.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O ID ou o nome do contêiner a ser desvinculado.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para desvincular o IP endereço `192.123.12.12` do contêiner `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


### bluemix ic ips
{: #bluemix_ic_ips}

Listar os endereços IP flutuantes disponíveis para o usuário com login efetuado. A lista inclui endereços IP e o ID do contêiner ao qual os endereços IP são vinculadas. Se o endereço IP não for usado, nenhum ID de contêiner será mostrado.

```
bluemix ic ips [-q]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-q (opcional)</dt>
   <dd>Liste somente os endereços IP, sem os IDs dos contêineres que estão ligados a esses endereços IP.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para receber uma lista de todos os endereços IP da organização.
```
bluemix ic ips -q
```


### bluemix ic kill
{: #bluemix_ic_kill}

Pare um processo em execução em um contêiner sem parar o contêiner. Para obter mais informações, veja o comando [kill](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (opcional)</dt>
   <dd>Envie um comando para o processo que estiver em execução no contêiner.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O ID ou o nome do contêiner.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para encerrar o processo em um contêiner denominado `proxy`:
```
bluemix ic kill proxy
```


### bluemix ic logs
{: #bluemix_ic_logs}

Mostre os logs de saída ou de erro para um contêiner em execução. Para obter mais informações, veja o comando [logs](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.
```
bluemix ic logs [OPTIONS] CONTAINER
```


### bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Visualize o nome do repositório de imagem privada do {{site.data.keyword.Bluemix_notm}} da organização na qual você está com login efetuado.

```
bluemix ic namespace-get
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino


### bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Configure o nome do repositório de imagem privada do {{site.data.keyword.Bluemix_notm}} da organização na qual você está com login efetuado.

*Restrição*: não é possível usar um hyphen `-` no nome de seu namespace de repositório.

```
bluemix ic namespace-set NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>NAME</i> (obrigatório)</dt>
   <dd>Uma função de vez única para configurar o namespace do repositório para a sua organização, se ele ainda não estiver configurado. Após configurar o namespace, reinicialize o IBM Containers por meio do comando `bluemix ic init` antes de continuar.</dd>
   </dl>


### bluemix ic pause
{: #pause}

Pausar todos os processos em um contêiner em execução. Para obter mais informações, veja o comando [pause](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker. Para parar um contêiner, consulte o comando [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:
   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Respostas</strong>:

- Contêiner pausado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para pausar um contêiner denominado `proxy`:
```
bluemix ic pause proxy
```


### bluemix ic port
{: #bluemix_ic_port}

Liste mapeamentos de porta ou um mapeamento específico para o contêiner. Esse comando agrupa o comando `docker port`. Para obter mais informações, veja o comando [port ](https://docs.docker.com/engine/reference/commandline/port/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.


### bluemix ic ps
{: #bluemix_ic_ps}
Visualize uma lista de contêineres que estão em execução no namespace do usuário com login efetuado. Por padrão, esse comando mostra somente os contêineres que estão em execução. Para obter mais informações, veja o comando [ps](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-a|--all (opcional)</dt>
   <dd>Mostre todos os contêineres, em execução e interrompidos.</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (opcional)</dt>
   <dd>Procure contêineres que possuem um valor específico da variável de ambiente. É possível filtrar seus contêineres por qualquer chave ou valor de variável de ambiente listados na seção Env da resposta da CLI ao inspecionar um contêiner. Substitua SEARCH_CRITERIA pela chave ou valor que você está procurando. Seus
critérios de procura não precisam ser uma correspondência exata. </dd>
   <dt>-s|--size (opcional)</dt>
   <dd>Liste os tamanhos dos contêineres.</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (opcional)</dt>
   <dd>Liste os contêineres criados mais recentemente, em que <i>NUM</i> é o número dos contêineres criados mais recentemente que você deseja retornar. <br><br> Por exemplo, se você criou contêineres
<i>node1</i> até <i>node5</i> sequencialmente, o comando <i>bluemix ic ps --limit 2</i> retornará node4 e node5 porque eles são os últimos dois contêineres criados. </dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Exiba somente os IDs de contêineres.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para ver todos os contêineres em execução e interrompidos:
```
bluemix ic ps -a
```


### bluemix ic rename
{: #bluemix_ic_rename}
Renomear um contêiner. Para obter mais informações, veja o comando [rename](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

<dl>
   <dt><i>OLD_NAME</i> (obrigatório)</dt>
   <dd>O nome antigo do contêiner.</dd>
   <dt><i>NEW_NAME</i> (obrigatório)</dt>
   <dd>O novo nome do contêiner.</dd>
   </dl>


### bluemix ic reprovision
{: #bluemix_ic_reprovision}

Recrie o serviço IBM Containers no espaço do Bluemix em que você efetuou login. A
cota original para o espaço é mantida.

<strong>Importante</strong>: quando você executa esse comando, nenhum dos seus contêineres únicos e grupos nesse espaço será migrado para o espaço reprovisionado e eles serão removidos durante o processo de migração.

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>Opções de comando</strong>:

<dl>
   <dt>--force|-f (opcional)</dt>
   <dd>Força a recriação do serviço IBM Containers no espaço do Bluemix.</dd>
   <dt><i>AVAILABILITY_ZONE</i> (opcional)</dt>
   <dd>O nome da zona de disponibilidade do IBM Containers em que seus contêineres são implementados. Se nenhuma zona de disponibilidade estiver especificada, a zona de disponibilidade padrão que está configurada para a região será usada.</dd>
   </dl>


### bluemix ic restart
{: #bluemix_ic_restart}

Reiniciar um contêiner. Para obter mais informações, veja o comando [restart](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (opcional)</dt>
   <dd>O número de segundos a aguardar antes que o contêiner seja reiniciado.</dd>
   </dl>


<strong>Respostas</strong>:

- Contêiner reiniciado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para reiniciar um contêiner denominado `proxy`:
```
bluemix ic restart proxy
```


### bluemix ic rm
{: #bluemix_ic_rm}

Remover um contêiner. Para obter mais informações, veja o comando [rm](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-f|--force (opcional)</dt>
   <dd>Força a remoção de um contêiner em execução ou com falha.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Respostas</strong>:

- Contêiner removido com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner.

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover um contêiner denominado `proxy`:
```
bluemix ic rm proxy
```


### bluemix ic rmi
{: #bluemix_ic_rmi}

Remover uma imagem do namespace do usuário com login efetuado. Para obter mais informações, veja o comando [rmi](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i> (opcional)</dt>
   <dd>Alterar o host de registro. O padrão é usar o registro que você especifica no comando <i>bluemix ic init</i>.</dd>
   <dt><i>IMAGE</i> (obrigatório)</dt>
   <dd>O nome da imagem que você deseja remover. Se uma tag não for especificada no nome da imagem, a imagem identificada por último (<i>latest</i>) será excluída, por padrão.</dd>
   </dl>

<strong>Respostas</strong>:

- Removido: `{IMAGE}`

 Em que `{IMAGE}` é o nome da imagem que foi removida.

- Erro! Nenhum host de registro especificado.

- Remoção de imagem com falha - Não foi possível se conectar ao registro de nuvem do contêiner

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover a imagem `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


### bluemix ic route-map
{: #bluemix_ic_route_map}

Estabelecer a rota para o tráfego de Internet a ser usada para acessar o grupo de contêiner. Você pode usar esse comando para estabelecer uma nova rota ou atualizar uma rota existente.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (opcional)</dt>
   <dd>O nome do host para a rota. O nome do host é a primeira parte da URL da rota pública completa, como <i>mycontainerhost</i> na URL <i>mycontainerhost.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>O nome do domínio para a rota, que é a segunda parte da URL da rota pública completa. Na maioria dos casos, o domínio é <i>mybluemix.net</i>. Também é possível usar esse parâmetro para especificar um domínio privado.</dd>
   <dt><i>CONTAINER_GROUP</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para mapear a rota para o grupo que é chamado `GROUP1`, em que `my_host` é o nome do host e `mybluemix.net` é o domínio.
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


### bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Estabelecer a rota para o tráfego de Internet a ser usada para acessar o grupo de contêiner. Você pode usar esse comando para estabelecer uma nova rota ou atualizar uma rota existente.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (opcional)</dt>
   <dd>O nome do host para a rota.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>O nome de domínio para a rota.</dd>
   <dt><i>CONTAINER_GROUP</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover mapeamento da rota para o grupo chamado `GROUP1`, em que `my_host` é o nome do host e
`organization.com` é o domínio.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


### bluemix ic run
{: #bluemix_ic_run}

Iniciar um novo contêiner no serviço de nuvem de contêiner a partir de um nome de imagem. Para
obter mais informações, veja o comando [run](https://docs.docker.com/engine/reference/commandline/run/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg)
na ajuda do Docker.


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Nota:** assegure-se de que a ferramenta de comando do Cloud Foundry esteja instalada e de que você tenha um token do Cloud Foundry. O login bem-sucedido usando `bluemix
login` e `bluemix ic init` gera o token e os certificados necessários.


<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (opcional)</dt>
   <dd>Exponha a porta para o tráfego HTTP. Inclua quaisquer portas especificadas no Dockerfile para a imagem que você está usando. É possível incluir várias portas com várias
opções <i>-p</i>. Expor uma porta irá automaticamente ligar um endereço IP público ao contêiner se um endereço IP público estiver disponível. <br><br>Se você tiver um endereço IP existente no espaço que deseja ligar ao contêiner, será possível especificar o endereço IP em vez de ligá-lo posteriormente. O endereço IP deve ser especificado no formato: &lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br><br>Para obter mais informações sobre como solicitar endereços IP para um espaço, consulte o comando <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a>. <br><br>Ao especificar uma porta, você está tornando o app disponível para o {{site.data.keyword.Bluemix_notm}} Load Balancer ou para os contêineres no mesmo espaço do {{site.data.keyword.Bluemix_notm}} que estão tentando atingir o host. Se uma porta for especificada no Dockerfile para a imagem que você está usando, inclua essa porta. <br><br><strong>Dicas:</strong><ul><li>Para a imagem do servidor Liberty certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 9080.</li><li>Para a imagem do Node.js certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 8000.</li></ul></dd>
   <dt>-P (opcional)</dt>
   <dd>Exponha automaticamente as portas que estão especificadas no Dockerfile da imagem para o tráfego HTTP.</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i> (opcional)</dt>
   <dd>Designe um limite de memória ao grupo em MB. Ao criar um grupo de contêiner a partir da CLI, o valor padrão para cada instância de contêiner é 64 MB.  Ao criar um grupo de contêiner a partir do Painel
do {{site.data.keyword.Bluemix_notm}}, o valor padrão para cada instância é 256 MB. Os valores aceitos são 64, 256, 512, 1024 e 2048. Após um limite de memória ser designado, o valor não poderá ser mudado.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (opcional)</dt>
   <dd>Configure a variável de ambiente, em que <i>ENV</i> é um par de key=value. Liste diversas chaves separadamente. Se aspas forem incluídas, inclua-as em torno do nome da variável de ambiente e do valor. Por
exemplo: -e "key1=value1" -e "key2=value2" -e "key3=value3". A tabela a seguir mostra algumas variáveis de ambiente comumente usadas que podem ser especificadas:</dd>
   </dl>


|      Variável do ambiente                          |   Descrição                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Faça a ligação de um serviço a um contêiner. Use a variável de ambiente `CCS_BIND_APP` para ligar um aplicativo ao contêiner. O app é ligado ao serviço de destino e age como uma ponte que permite que o {{site.data.keyword.Bluemix_notm}} traga as informações de `VCAP_SERVICES` de seu app de ponte para a instância do contêiner em execução. Para obter mais informações sobre como criar um app de ponte, consulte [Ligando um serviço a um contêiner](/docs/containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | Para ligar um serviço Bluemix diretamente a um contêiner, sem usar um app de ponte, use CCS_BIND_SRV. Essa ligação permite que o Bluemix injete as informações de VCAP_SERVICES na instância do contêiner em execução. Para listar vários serviços do Bluemix, inclua-os como parte da mesma variável de ambiente. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Inclua um arquivo de log a ser monitorado no contêiner. Inclua a variável de ambiente `LOG_LOCATIONS` com um caminho para o arquivo de log. |
{: caption="Table 9. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (opcional)</dt>
   <dd>Anexe um volume a um contêiner especificando os detalhes no formato <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: O ID ou o nome do volume.</li>
   <li><i>CONTAINER_PATH</i>: O caminho absoluto para o volume no contêiner.</li>
   <li>ro: opcional. Especificar <i>ro</i> torna o volume somente leitura em vez de leitura/gravação padrão.</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i> (necessário)</dt>
   <dd>Designe um nome ao contêiner. <br> <strong>Dica:</strong> o nome do contêiner deve iniciar com uma letra. O nome pode incluir letras maiúsculas, letras minúsculas, números, pontos., sublinhados _ ou hifens -.</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i> (opcional)</dt>
   <dd>Sempre que você quiser que um contêiner se comunique com outro contêiner que estiver em execução, é possível endereçá-lo usando um alias para o nome do host.</dd>
   <dt>-it (opcional)</dt>
   <dd>Execute o contêiner em um modo interativo. Após a criação do contêiner, manter a exibição da entrada padrão. Digite <i>exit</i> para sair.</dd>
   <dt><i>IMAGE</i> (obrigatório)</dt>
   <dd>A imagem a ser incluída no contêiner. É possível listar comandos após a imagem, mas não coloque nenhuma opção após a imagem. Inclua todas as opções antes de especificar uma imagem. Inclua todas as opções antes de especificar uma imagem. <br><br>Se você usar uma imagem no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização, especifique a imagem no formato: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>Se você usar uma imagem que é fornecida pelo IBM Containers, especifique a imagem no formato: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>O comando e os argumentos são passados para o grupo de contêiner executar. Esse comando deve ser um comando de longa execução. Não use um comando de curta duração que não é executado por muito tempo, por exemplo, <i>/bin/date</i>, pois o comando de curta duração pode fazer o contêiner travar.</dd>
   </dl>


<strong>Exemplos</strong>:

Execute o comando de longa execução `sh -c "while true; do date; sleep 20; done"` no contêiner `my_container` construído na imagem `registry.ng.bluemix.net/ibmnode`.
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Crie e, em seguida, inicie um contêiner `proxy` com um limite de memória de `1024` MB usando a imagem `my_namespace/nginx`, em que `my_namespace` é o namespace associado aos usuários que efetuaram login.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Crie e, em seguida, inicie um contêiner usando a imagem `my_namespace/blog`, passe as credenciais como variáveis ambientais. `my_namespace` é o namespace associado aos usuários que efetuaram login.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

Inclua um volume em um contêiner usando a imagem `my_namespace/blog`, em que `my_namespace` é o namespace associado aos usuários que efetuaram login.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


### bluemix ic service-bind
{: #bluemix_ic_service-bind}

Inclua um serviço em um grupo de contêiner em execução. Esse comando está
disponível apenas para grupos de contêineres. Contêineres únicos devem ligar um serviço
como parte do comando bluemix ic run.

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opções de comando</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>O ID ou nome do grupo.</dd>
   <dt><i>SERVICE_INSTANCE</i> (obrigatório)</dt>
   <dd>O nome da instância de serviço a ser incluída no grupo de contêiner.</dd>
   </dl>


### bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Remova um serviço de um grupo de contêiner em execução. Esse comando está
disponível apenas para grupos de contêineres. Contêineres únicos devem remover o contêiner e criar um
novo sem o serviço.

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opções de comando</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>O ID ou nome do grupo.</dd>
   <dt><i>SERVICE_INSTANCE</i> (obrigatório)</dt>
   <dd>O nome da instância de serviço a ser incluída no grupo de contêiner.</dd>
   </dl>


### bluemix ic start
{: #ic_start}
Iniciar um contêiner interrompido. Para obter mais informações, veja o comando [start](https://docs.docker.com/engine/reference/commandline/start/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker. Para parar um contêiner, consulte o comando [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>


<strong>Respostas</strong>:

- Contêiner iniciado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para iniciar um contêiner denominado `proxy`.
```
bluemix ic start proxy
```


### bluemix ic stats
{: #bluemix_ic_stats}

Para um ou mais contêineres, visualizar estatísticas de uso em tempo real. Use `CTRL+C` para sair. Para obter mais informações, consulte o comando [stats](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} na ajuda do Docker.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   <dt>--no-stream (opcional)</dt>
   <dd>Exiba somente o resultado mais recente e não inclua nenhuma informação que o preceda.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para as estatísticas mais recentes sobre um contêiner:
```
bluemix ic stats --no-stream my_container
```


### bluemix ic stop
{: #ic_stop}
Parar um contêiner em execução. Para obter mais informações, veja o comando [stop](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker. Para iniciar um contêiner, consulte o comando [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (opcional)</dt>
   <dd>O número de segundos a esperar antes que o contêiner seja eliminado.</dd>
   </dl>

<strong>Respostas</strong>:

- Contêiner interrompido com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para parar um contêiner denominado `proxy`.
```
bluemix ic stop proxy
```


### bluemix ic top
{: #bluemix_ic_top}

Mostrar os processos que estão em execução no contêiner. Para obter mais informações, veja o comando [top](https://docs.docker.com/engine/reference/commandline/top/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para exibir os processos em um contêiner chamado `my_container`.
```
bluemix ic top my_container
```


### bluemix ic unpause
{: #unpause}

Remover pausa de todos os processos em um contêiner em execução. Para obter mais informações, veja o comando [unpause](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker. Para pausar um contêiner, consulte o comando [bluemix ic pause](#pause).

```
bluemix ic unpause CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Respostas</strong>:

- Contêiner removido da pausa com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover da pausa um contêiner denominado `proxy`:
```
bluemix ic unpause proxy
```


### bluemix ic unprovision
{: #bluemix_ic_unprovision}

Exclua o serviço IBM Containers do espaço do Bluemix em que você efetuou login.

<strong>Atenção</strong>: Quando você executar esse comando, todos os contêineres
únicos e grupos de contêineres serão perdidos. Seu espaço ainda estará disponível no
Bluemix. Para começar a usar o IBM Containers novamente, deve-se executar `bluemix ic reprovision` para provisionar o serviço IBM Containers novamente.

```
bluemix ic reprovision [--force|-f]
```
<strong>Opções de comando</strong>:

<dl>
   <dt>--force|-f (opcional)</dt>
   <dd>Força a exclusão do Bluemix do espaço do Bluemix.</dd>
 </dl>


### bluemix ic version
{: #bluemix_ic_version}

Mostre a versão do Docker e a API do IBM Containers.

```
bluemix ic version
```

<strong>Pré-requisitos</strong>: Docker

Para ver a versão do IBM Containers, execute `bluemix ic info`. Para obter mais informações, veja o comando [version](https://docs.docker.com/engine/reference/commandline/version/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.


### bluemix ic volume-create
{: #bluemix_ic_volume_create}

Crie um volume.

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>FS_NAME</i> (opcional)</dt>
   <dd>O nome do compartilhamento de arquivo. Se nenhum compartilhamento de arquivo estiver disponível ou nomeado, o volume será construído
no compartilhamento de arquivo padrão do espaço.</dd>
   <dt><i>VOLUME_NAME</i> (obrigatório)</dt>
   <dd>O nome do volume. O nome pode conter letras minúsculas, números, sublinhados _ e hifens -.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para criar um volume.
```
bluemix ic volume-create volume_name fileshare_name
```


### bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Liste os compartilhamentos de arquivos.

```
bluemix ic volume-fs
```


### bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Criar um compartilhamento de arquivo.

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (obrigatório)</dt>
   <dd>O nome do compartilhamento de arquivo. O nome pode conter letras minúsculas, números, sublinhados _ e hifens -.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para criar um compartilhamento de arquivo.
```
bluemix ic volume-fs-create my_file_share
```


### bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Liste todos os tipos de compartilhamento de arquivo.

```
bluemix ic volume-fs-flavors
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino


### bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspecione um compartilhamento de arquivo.

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i> (obrigatório)</dt>
   <dd>O nome do compartilhamento de arquivo.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir é uma solicitação para inspecionar um compartilhamento de arquivo, em que `my_file_share` é o nome do compartilhamento de arquivo.
```
bluemix ic volume-fs-inspect my_file_share
```


### bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Remover um compartilhamento de arquivo.

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (obrigatório)</dt>
   <dd>O nome do compartilhamento de arquivo.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover um compartilhamento de arquivo, em que `my_file_share` é o nome do compartilhamento de arquivo.
```
bluemix ic volume-fs-remove my_file_share
```


### bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspecione um volume.

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (obrigatório)</dt>
   <dd>O nome do volume.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir é uma solicitação para inspecionar um volume, em que `volume_name` é o nome do volume.
```
bluemix ic volume-inspect volume_name
```


### bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Remova um volume.

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (obrigatório)</dt>
   <dd>O nome do volume.</dd>
    </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover um volume, em que `volume_name` é o nome do volume.
```
bluemix ic volume-remove volume_name
```


### bluemix ic volumes
{: #bluemix_ic_volumes}

Liste os volumes.

```
bluemix ic volumes
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino


### bluemix ic wait
{: #bluemix_ic_wait}

Sair de um contêiner e exibir o código de saída como confirmação. Para obter mais informações, veja o comando [wait](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg) na ajuda do Docker.

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para sair de um contêiner denominado `my_container`:
```
bluemix ic wait my_container
```


### bluemix ic wait-status
{: #bluemix_ic_wait_status}

Aguarde até que um único contêiner ou um grupo de contêiner atinja um estado não
temporário. Durante esse tempo de espera, a linha de comandos
não é retornada e você não pode inserir os comandos. Assim que o contêiner atinge um
estado não temporário, uma mensagem de OK é exibida. Para contêineres únicos, os estados
não temporários incluem Executando, Encerramento, Travado, Pausado ou Suspenso. Para
grupos de contêineres, os estados não temporários incluem CREATE_COMPLETE,
UPDATE_COMPLETE ou FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para sair de um contêiner denominado `my_container`:
```
bluemix ic wait my_container
```



# Links Relacionados
{: #rellinks}

## Links Relacionados
{: #general}

* [bx tool](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![Ícone de link externo](../../../icons/launch-glyph.svg)
