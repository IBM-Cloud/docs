---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting started with {{site.data.keyword.Bluemix_notm}} CLI
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI provides a unified way for you to interact with your applications, virtual servers, containers, and other services by using a command line interface. {{site.data.keyword.Bluemix_notm}} CLI also integrates community tools, such as Cloud Foundry CLI, Docker CLI, and OpenStack CLI, and initializes environment settings for you to interact with different compute types.

**Restriction**: The {{site.data.keyword.Bluemix_notm}} CLI is not supported by Cygwin, so do not use the {{site.data.keyword.Bluemix_notm}} CLI in the Cygwin command line window.

**Note**: If your network contains an HTTP proxy server between the host that runs the CLI and {{site.data.keyword.Bluemix_notm}}, you must specify the host name or IP address of the proxy server in the HTTP_PROXY environment variable.

## Installing {{site.data.keyword.Bluemix_notm}} CLI
{: #install_bluemix_cli}

Before you install {{site.data.keyword.Bluemix_notm}} CLI, install the [cf CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

For Mac OS and Windows, download the [{{site.data.keyword.Bluemix_notm}} CLI package](/docs/cli/index.html#downloads), and run the installer.

For Linux, follow these steps:

  1. Download the package, and extract it. For example:

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

  2. Go to the `Bluemix_CLI` directory, and run the `./install_bluemix_cli` command with root permission. You can run the command as a root user or use the `sudo` command to get the root permission. For example:

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

You can now start using {{site.data.keyword.Bluemix_notm}} CLI or install additional plug-ins.

## Installing a plug-in
{: #install_plug-in}

Like Cloud Foundry CLI, {{site.data.keyword.Bluemix_notm}} CLI supports a plug-in extension framework to integrate other commands besides the built-in ones.

To install a plug-in from your local environment, take the following steps:

  1. Download the plug-in. For example:

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

  2. For UNIX-like systems, you must make the downloaded file executable by using the `chmod` command. For example:

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. Install the plug-in by using the `bluemix plugin install` command. For example:

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

To install from a remote server, take the following steps:

  1. Install the plug-in from a remote URL directly by using the `bluemix plugin install` command. For example:

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

You can also install a plug-in from the repository. {{site.data.keyword.Bluemix_notm}} has repositories that host {{site.data.keyword.Bluemix_notm}} CLI plug-ins and Cloud Foundry CLI plug-ins:

  * [Cloud Foundry CLI plug-ins repository](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![External link icon](../../../icons/launch-glyph.svg), which hosts plug-ins for Cloud Foundry CLI.
  * [{{site.data.keyword.Bluemix_notm}} CLI plug-ins repository](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![External link icon](../../../icons/launch-glyph.svg), which hosts plug-ins specifically for {{site.data.keyword.Bluemix_notm}} CLI.

To install from the repository, take the following steps:

  1. Find the plug-in in the repository. After you have installed {{site.data.keyword.Bluemix_notm}} CLI, the official repository `Bluemix` is added by default. You can list the plug-ins in the `Bluemix` repository by using the `bluemix plugin repo-plugins` command. For example:

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. Install the plug-in from the `Bluemix` repository by using the `bluemix plugin install` command. For example:

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## Logging in to {{site.data.keyword.Bluemix_notm}} CLI
{: #log_bmcli}

After you install {{site.data.keyword.Bluemix_notm}} CLI, you can log in to {{site.data.keyword.Bluemix_notm}} by using your IBM id and password. For example:

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

You're now ready to use {{site.data.keyword.Bluemix_notm}} built-in commands. For example, run the `bluemix catalog templates` command to list all the available {{site.data.keyword.Bluemix_notm}} boilerplate templates:

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

# {{site.data.keyword.Bluemix_notm}} (bx) commands
{: #bluemix_cli}

Version: 0.4.6

The {{site.data.keyword.Bluemix_notm}} command line interface (CLI) provides a set of commands that are grouped by namespace for users to interact with {{site.data.keyword.Bluemix_notm}}. Some {{site.data.keyword.Bluemix_notm}} commands are wrappers of existing cf commands, while others provide extended capabilities for {{site.data.keyword.Bluemix_notm}} users. The following information lists commands that are supported by {{site.data.keyword.Bluemix_notm}} CLI, and includes their names, options, usage, prerequisites, descriptions, and examples.
{:shortdesc}

**Note:** *Prerequisites* list which actions are required before using the command. Commands that have no prerequisite actions list **None**. Otherwise, prerequisites might include one or more of the following actions:

<dl>
<dt>Endpoint</dt>
<dd>An API endpoint must be set through the <code>bluemix api</code> before using the command.</dd>
<dt>Login</dt>
<dd>Login by using the <code>bluemix login</code> command is required before using this command. If logging in with federated ID, use '--sso' option to authenticate with one time passcode.</dd>
<dt>Target</dt>
<dd>The <code>bluemix target</code> command must be used to set an org and space before using this command.</dd>
<dt>Docker</dt>
<dd>The Docker CLI (docker) must be installed to run this command.</dd>
</dl>

## bluemix commands index
{: #bx_commands_index}

Use the indexes in the following tables to refer to the frequently used bluemix commands.

**Note:** You can use the short format of bluemix commands; for example, `bx api` is short for `bluemix api`.


<table summary="General bluemix commands.">
<caption>Table 1. General bluemix commands</caption>
 <thead>
 <th colspan="5">General bluemix commands</th>
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


<table summary="bluemix commands that you can use to manage orgs, spaces, and users.">
<caption>Table 2. Commands for managing orgs, spaces, and users</caption>
 <thead>
 <th colspan="5">Commands for managing orgs, spaces, and users</th>
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


<table summary="bluemix commands that you can use to manage Cloud Foundry apps.">
<caption>Table 3. Commands for managing cf apps</caption>
 <thead>
 <th colspan="5">Commands for managing cf apps</th>
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


<table summary="bluemix commands that you can use to manage Bluemix services.">
<caption>Table 4. Commands for managing Bluemix services</caption>
 <thead>
 <th colspan="5">Commands for managing Bluemix services</th>
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


<table summary="bluemix commands that you can use to manage Bluemix catalog, plug-ins, billing, and security settings.">
<caption>Table 5. Commands for managing Bluemix catalog, plug-ins, billing, and security settings</caption>
 <thead>
 <th colspan="5">Commands for managing Bluemix catalog, plug-ins, billing, and security settings</th>
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


<table summary="bluemix commands that you can use to manage network settings.">
<caption>Table 6. Commands for managing network settings</caption>
 <thead>
 <th colspan="5">Commands for managing network settings</th>
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

<table summary="bluemix commands that you can use to manage containers on Bluemix.">
<caption>Table 7. Commands for managing containers on Bluemix</caption>
 <thead>
 <th colspan="5">Commands for managing containers on Bluemix</th>
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
Display the general help for first-level built-in commands and supported namespaces of {{site.data.keyword.Bluemix_notm}} CLI, or the help for a specific built-in command or namespace.

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:

   <dl>
   <dt>COMMAND|NAMESPACE (optional)</dt>
   <dd>The command or namespace that help is displayed for. If not specified, the general help for {{site.data.keyword.Bluemix_notm}} CLI is shown.</dd>
   </dl>



<strong>Examples</strong>:

Display general help for {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix help
```

Display help for the `info` command:

```
bluemix help info
```

Display help for the `ic` plug-in:

```
bluemix help ic
```

or

```
bluemix ic help
```

Display help for the `group-create` command under the `ic` plug-in:

```
bluemix ic help group-create
```


### bluemix api
{: #bluemix_api}
Set or view the {{site.data.keyword.Bluemix_notm}} API endpoint. This command wraps the `cf api` command.

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
   <dl>
   <dt>API_ENDPOINT (optional)</dt>
   <dd>The API endpoint that is targeted, for example, `https://api.chinabluemix.net`. If both *API_ENDPOINT* and `--unset` options are not specified, the current API endpoint is displayed.</dd>
   <dt>--unset (optional)</dt>
   <dd>Remove the API endpoint setting.</dd>
    </dl>
<strong>Examples</strong>:

Set the API endpoint to api.chinabluemix.net:

```
bluemix api api.chinabluemix.net
```

View the current API endpoint:

```
bluemix api
```

Unset the API endpoint:

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

Log in user. This command wraps the `cf login` command. Command options are the same as `cf login` command options.

```
bluemix login [OPTIONS...]
```

<strong>Prerequisites</strong>:  Endpoint

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>Command options</strong>:
For information about options supported by the `login` command, see `cf login` command usage information for cf commands for managing applications.

<strong>Note</strong>:
If logging in with federated ID, use '--sso' option to authenticate with one time passcode.

### bluemix logout
{: #bluemix_logout}

Log out user. This command wraps the `cf logout` command.

```
bluemix logout
```

<strong>Prerequisites</strong>:  None


### bluemix target
{: #bluemix_target}


Set or view the target org or space. This command wraps the `cf target` command.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>-o <i>ORG_NAME</i> (optional)</dt>
   <dd>The name of the organization to be targeted.</dd>
   <dt>-s <i>SPACE_NAME</i> (optional)</dt>
   <dd>The name of the space to be targeted.</dd>
   </dl>
If neither -o *ORG_NAME* or -s *SPACE_NAME* are specified, the current org and space are displayed.
<strong>Examples</strong>:

Set the current org to `MyOrg` and space to `MySpace`:

```
bluemix target -o MyOrg -s MySpace
```

View the current org and space:

```
bluemix target
```


### bluemix info
{: #bluemix_info}

View the basic {{site.data.keyword.Bluemix_notm}} information, including the current region, the cloud controller version, and some useful endpoints, such as endpoints for login and exchanging access token.

```
bluemix info
```

<strong>Prerequisites</strong>:  Endpoint


### bluemix config
{: #bluemix_config}


Write default values to the configuration file.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>The timeout value for HTTP requests. The default value is 60 seconds.</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>Trace HTTP requests to the terminal or specified file.</dd>
   <dt>--color true|false</dt>
   <dd>Enable or disable color output. Color output is enabled by default.</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>Set a default locale. If LOCALE is <i>CLEAR</i>, previous locale is deleted.</dd>
   <dt>--check-version true|false</dt>
   <dd>Enable or disable CLI version check</dd>
   </dl>

Only one of these options can be specified at a time.

<strong>Examples</strong>:

Set HTTP request timeout to 30 seconds:

```
bluemix config --http-timeout 30
```

Enable trace output for HTTP requests:

```
bluemix config --trace true
```

Trace HTTP requests to a specified file */home/usera/my_trace*:

```
bluemix config --trace /home/usera/my_trace
```

Disable color output:

```
bluemix config --color false
```

Set the locale to zh_Hans:

```
bluemix config --locale zh_Hans
```

Clear the locale settings:

```
bluemix config --locale CLEAR
```


### bluemix curl
{: #bluemix_curl}

Execute a raw HTTP request to {{site.data.keyword.Bluemix_notm}}. *Content-Type* is set to *application/json* by default. This command sends the request to {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. For supported paths, refer to the API path definitions in the [CloudFoundry API document](http://apidocs.cloudfoundry.org/){: new_window} ![External link icon](../../../icons/launch-glyph.svg).

```
bluemix curl PATH [OPTIONS...]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt><i>PATH</i> (required)</dt>
   <dd>The URL path of the resource. For example, /v2/apps.</dd>
   <dt><i>OPTIONS</i> (optional)</dt>
   <dd>The options that are supported by the `bluemix curl` command are the same as those for the `cf curl` command.</dd>
   </dl>

<strong>Examples</strong>:

View the information for all organizations of the current account:

```
bluemix curl /v2/organizations
```


### bluemix iam orgs
{: #bluemix_iam_orgs}

List all organizations

```
bluemix iam orgs [-r REGION --guid]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>-r <i>REGION</i> (optional)</dt>
   <dd>For which region the organization information is shown. If set to 'all', all organizations in all regions are listed.</dd>
   <dt>--guid (optional)</dt>
   <dd>Display the GUID of the organizations.</dd>
   </dl>

<strong>Examples</strong>:

List all the organizations in region: `us-south` with the GUID displayed

```
bluemix iam orgs -r us-south --guid
```

### bluemix iam org
{: #bluemix_iam_org}

Show the information for the specified organization.

```
bluemix iam org ORG_NAME [--guid]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization.</dd>
   <dt>--guid (optional)</dt>
   <dd>Display the GUID of the organization.</dd>
   </dl>

<strong>Examples</strong>:

Show the information of organization `IBM` with the GUID displayed

```
bluemix iam org IBM --guid
```

### bluemix iam org-create
{: #bluemix_iam_org_create}

Create a new organization. This operation can only be performed by account owner.

```
bluemix iam org-create ORG_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization being created.</dd>
   </dl>

<strong>Examples</strong>:

Create an organization named `IBM`.

```
bluemix iam org-create IBM
```


### bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Replicate an org from the current region to another region.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the existing org that is to be replicated.</dd>
   <dt>REGION_NAME (required)</dt>
   <dd>The name of the region that hosts the replicated org.</dd>
   </dl>

<strong>Examples</strong>:

Replicate the org `myorg` to the region `eu-gb`:

```
bluemix iam org-replicate myorg eu-gb
```


### bluemix iam org-rename
{: #bluemix_iam_org_rename}

Rename an organization. This operation can be done only by an org manager.

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>OLD_ORG_NAME (required)</dt>
   <dd>The old name of the org that is to be renamed.</dd>
   <dt>NEW_ORG_NAME (required)</dt>
   <dd>The new name of the org that it is renamed to.</dd>
   </dl>

### bluemix iam org-delete
{: #bluemix_iam_org_delete}

Delete the specified organization in current region.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the existing org that is to be deleted.</dd>
   <dt>-f (optional)</dt>
   <dd>Force deletion without confirmation.</dd>
   <dt>--all (optional)</dt>
   <dd>Delete the organization from all regions.</dd>
   </dl>


### bluemix iam spaces
{: #bluemix_iam_spaces}

This command has the same function and options as the `cf spaces` command.


### bluemix iam space
{: #bluemix_iam_space}

This command has the same function and options as the `cf space` command.


### bluemix iam space-create
{: #bluemix_iam_space_create}

This command has the same function and options as the `cf create-space` command.


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


This command has the same function and options as the `cf rename-space` command.


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


This command has the same function and options as the `cf delete-space` command.


### bluemix iam account-users
{: #bluemix_iam_account_users}

Displays users associated with the account. This operation can be performed only by the account owner.

```
bluemix iam account-users
```

### bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}


Invites a user to the account with an organization and space role already set. This operation can be performed only by the account owner.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>Prerequisites</strong>:  Endpoint, Login


<strong>Command options</strong>:

   <dl>
   <dt>USER_NAME (required)</dt>
   <dd>The name of the user being invited.</dd>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization this user is invited to.</dd>
   <dt>ORG_ROLE (required)</dt>
   <dd>The name of the organization role this user is invited to. For example:
   <ul>
  <li>OrgManager: This role can invite and manage users, select and change plans, and set spending limits.</li>
  <li>BillingManager: This role can create and manage the billing account and payment information.</li>
  <li>OrgAuditor: This role has read-only access to org information and reports.</li>
  </ul> </dd>
   <dt>SPACE_NAME (required)</dt>
   <dd>The name of the space this user is invited to.</dd>
   <dt>SPACE_ROLE (required)</dt>
   <dd>The name of the space this user is invited to. The name of the space role this user is invited to. For example:
   <ul>
<li>SpaceManager: This role can invite and manage users, and enable features for a given space.</li>
<li>SpaceDeveloper: This role can create and manage apps and services, and see logs and reports.</li>
<li>SpaceAuditor: This role can view logs, reports, and settings for the space.</li>
</ul>
</dd>
</dl>

<strong>Examples</strong>:

Invite user `Mary` to the organization `IBM` as `OrgManager` role and the space `Cloud` as `SpaceAuditor` role:

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Resend invitation to a user(org manager or account owner is required)
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
{: #bluemix_iam_org_users}

Display users in the specified organization by role.

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization.</dd>
   <dt>-a (optional)</dt>
   <dd>List all the users in the specified organization, not grouped by role.</dd>
    </dl>

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Add a user into org (org manager required).
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

Remove a user from org (org manager or user him/herself only)
```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>Command options</strong>:
  <dl>
   <dt>--force, -f</dt>
   <dd>Force deletion without confirmation.</dd>
 </dl>

### bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Assign an organization role to a user. This operation can be performed only by an organization manager.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
  <dl>
   <dt>USER_NAME (required)</dt>
   <dd>The name of the user being assigned.</dd>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization this user is assigned to.</dd>
   <dt>ORG_ROLE (required)</dt>
   <dd>The name of the organization role this user is assigned to. For example:
   <ul>
   <li>OrgManager: This role can invite and manage users, select and change plans, and set spending limits.</li>
   <li>BillingManager: This role can create and manage the billing account and payment information.</li>
   <li>OrgAuditor: This role has read-only access to org information and reports.</li>
   </ul>
   </dd>
    </dl>

<strong>Examples</strong>:

Assign user `Mary` to the organization `IBM` as `OrgManager` role:

```
bluemix iam org-role-set Mary IBM OrgManager
```


### bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Remove an organization role from a user. This operation can be performed only by an organization manager.

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>USER_NAME (required)</dt>
   <dd>The name of the user being removed.</dd>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization this user is removed from.</dd>
   <dt>ORG_ROLE (required)</dt>
   <dd>The name of the organization role this user is removed from. For example:
   <ul>
   <li>OrgManager: This role can invite and manage users, select and change plans, and set spending limits.</li>
   <li>BillingManager: This role can create and manage the billing account and payment information.</li>
   <li>OrgAuditor: This role has read-only access to org information and reports.</li>
   </ul>
   </dd>
    </dl>

<strong>Examples</strong>:

Remove user `Mary` from the organization `IBM` as `OrgManager` role:

```
bluemix iam org-role-unset Mary IBM OrgManager
```


### bluemix iam space-users
{: #bluemix_iam_space_users}

Display users in the specified space by role.

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization.</dd>
   <dt>SPACE_NAME (required)</dt>
   <dd>The name of the space.</dd>
   </dl>


### bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Assign a space role to a user. This operation can be performed only by a space manager.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:

   <dl>
   <dt>USER_NAME (required)</dt>
   <dd>The name of the user being assigned.</dd>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization this user is assigned to.</dd>
   <dt>SPACE_NAME (required)</dt>
   <dd>The name of the space this user is assigned to.</dd>
   <dt>SPACE_ROLE (required)</dt>
   <dd>The name of the space role this user is assigned to. For example:
   <ul>
   <li>SpaceManager: This role can invite and manage users, and enable features for a given space.</li>
   <li>SpaceDeveloper: This role can create and manage apps and services, and see logs and reports.</li>
   <li>SpaceAuditor: This role can view logs, reports, and settings for the space.</li>
   </ul></dd>
    </dl>

<strong>Examples</strong>:

Assign user `Mary` to the organization `IBM` and space `Cloud` as `SpaceManager` role:

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

### bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Remove a space role from a user. This operation can be performed only by a space manager.

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:

   <dl>
   <dt>USER_NAME (required)</dt>
   <dd>The name of the user being removed.</dd>
   <dt>ORG_NAME (required)</dt>
   <dd>The name of the organization this user is removed from.</dd>
   <dt>SPACE_NAME (required)</dt>
   <dd>The name of the space this user is removed from.</dd>
   <dt>SPACE_ROLE (required)</dt>
   <dd>The name of the space role this user is removed from. For example:
   <ul>
   <li>SpaceManager: This role can invite and manage users, and enable features for a given space.</li>
   <li>SpaceDeveloper: This role can create and manage apps and services, and see logs and reports.</li>
   <li>SpaceAuditor: This role can view logs, reports, and settings for the space.</li>
   </ul></dd>
    </dl>


<strong>Examples</strong>:

Remove user `Mary` from the organization `IBM` and space `Cloud` as `SpaceManager` role:

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


### bluemix app push
{: #bluemix_app_push}

This command has the same function and options as the `cf push` command.


### bluemix app list
{: #bluemix_app_list}

This command has the same function and options as the `cf apps` command.


### bluemix app show
{: #bluemix_app_show}

This command has the same function and options as the `cf app` command.


### bluemix app scale
{: #bluemix_app_scale}

This command has the same function and options as the `cf scale` command.


### bluemix app delete
{: #bluemix_app_delete}

This command has the same function and options as the `cf delete` command.


### bluemix app rename
{: #bluemix_app_rename}

This command has the same function and options as the `cf rename` command.


### bluemix app start
{: #bluemix_app_start}

This command has the same function and options as the `cf start` command.


### bluemix app stop
{: #bluemix_app_stop}

This command has the same function and options as the `cf stop` command.


### bluemix app restart
{: #bluemix_app_restart}

This command has the same function and options as the `cf restart` command.


### bluemix app restage
{: #bluemix_app_restage}


This command has the same function and options as the `cf restage` command.


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


This command has the same function and options as the `cf restart-app-instance` command.


### bluemix app events
{: #bluemix_app_events}

This command has the same function and options as the `cf events` command.


### bluemix app files
{: #bluemix_app_files}

This command has the same function and options as the `cf files` command.


### bluemix app logs
{: #bluemix_app_logs}

This command has the same function and options as the `cf logs` command.


### bluemix app env
{: #bluemix_app_env}

This command has the same function and options as the `cf env` command.


### bluemix app env-set
{: #bluemix_app_env_set}

This command has the same function and options as the `cf set-env` command.


### bluemix app env-unset
{: #bluemix_app_env_unset}

This command has the same function and options as the `cf unset-env` command.


### bluemix app stacks
{: #bluemix_app_stacks}

This command has the same function and options as the `cf stacks` command.


### bluemix app stack
{: #bluemix_app_stack}

This command has the same function and options as the `cf stack` command.


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

This command has the same function and options as the `cf create-app-manifest` command.


### bluemix service offerings
{: #bluemix_service_offerings}


This command has the same function and options as the `cf marketplace` command.


### bluemix service list
{: #bluemix_service_list}

This command has the same function and options as the `cf services` command.


### bluemix service show
{: #bluemix_service_show}

This command has the same function and options as the `cf service` command.


### bluemix service create
{: #bluemix_service_create}

This command has the same function and options as the `cf create-service` command.


### bluemix service update
{: #bluemix_service_update}

This command has the same function and options as the `cf update-service` command.


### bluemix service delete
{: #bluemix_service_delete}

This command has the same function and options as the `cf delete-service` command.


### bluemix service rename
{: #bluemix_service_rename}

This command has the same function and options as the `cf rename-service` command.


### bluemix service bind
{: #bluemix_service_bind}

This command has the same function and options as the `cf bind-service` command.


### bluemix service unbind
{: #bluemix_service_unbind}

This command has the same function and options as the `cf unbind-service` command.


### bluemix service key-create
{: #bluemix_service_key_create}

This command has the same function and options as the `cf create-service-key` command.


### bluemix service key-delete
{: #bluemix_service_key_delete}

This command has the same function and options as the `cf delete-service-key` command.


### bluemix service keys
{: #bluemix_service_keys}

This command has the same function and options as the `cf service-keys` command.


### bluemix service key-show
{: #bluemix_service_key_show}

This command has the same function and options as the `cf service-key` command.


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

This command has the same function and options as the `cf create-user-provided-service` command.


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

This command has the same function and options as the `cf update-user-provided-service` command.


### bluemix catalog templates
{: #bluemix_catalog_templates}

View the boilerplate templates on Bluemix.

```
bluemix catalog templates [-d]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:

   <dl>
   <dt>-d (optional)</dt>
   <dd>If the <i>-d</i> option is specified, the description of each template is also displayed. Otherwise, only the ID and name of each template is shown.</dd>
   </dl>


### bluemix catalog template
{: #bluemix_catalog_template}

View the detailed information of a specified boilerplate template.

```
bluemix catalog template TEMPLATE_ID
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>TEMPLATE_ID (required)</dt>
   <dd>The ID of the boilerplate template. Use <i>bluemix templates</i> to view all templates' IDs.</dd>
   </dl>


<strong>Examples</strong>:

View details of the template `mobileBackendStarter`:

```
bluemix catalog template mobileBackendStarter
```


### bluemix catalog template-run
{: #bluemix_catalog_template_run}

Create a cf application that is based on the specified template with the specified URL and description. By default, the new app is started automatically.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
   <dl>
   <dt>TEMPLATE_ID (required)</dt>
   <dd>The template that the application will be based on when it is created. Use <i>bluemix templates</i> to see all templates' ID.</dd>
   <dt>CF_APP_NAME (required)</dt>
   <dd>The name of the cf application to be created.</dd>
   <dt>-u <i>URL</i> (optional)</dt>
   <dd>The route of the application. If not specified, the route is set by Bluemix automatically based on your app name and default domain.</dd>
   <dt>-d <i>DESCRIPTION</i> (optional)</dt>
   <dd>Description of the application.</dd>
   <dt>--no-start (optional)</dt>
   <dd>Do not start the application automatically after it is created. If not specified, the application is started automatically after it is created.</dd>
   </dl>


<strong>Examples</strong>:

Create a cf application `my-app` based on `javaHelloWorld` template:

```
bluemix catalog template-run javaHelloWorld my-app
```

Create an application `my-ruby-app` based on `rubyHelloWorld` template with route `myrubyapp.chinabluemix.net` and description `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Create an application `my-python-app` based on `pythonHelloWorld` template without automatic start:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


### bluemix network regions
{: #bluemix_network_regions}

View the information for all regions on {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

<strong>Prerequisites</strong>:  Endpoint


### bluemix network region-set
{: #bluemix_network_region_set}

Switch to the region that is specified. This command automatically retargets to the same org and space in the new region, if possible. Otherwise, the command prompts the user to select a new org and space if the user is already logged in. The API endpoint is changed accordingly.

```
bluemix network region-set REGION_NAME
```

<strong>Prerequisites</strong>:  Endpoint

<strong>Command options</strong>:

   <dl>
   <dt>REGION_NAME (required)</dt>
   <dd>The name of the region that you want to switch to. You can use the <i>bluemix network regions</i> command to see all region names.</dd>
    </dl>

<strong>Examples</strong>:

Set the current region to `eu-gb`:

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

This command has the same function and options as the `cf routes` command.


### bluemix network route-check
{: #bluemix_network_route_check}

This command has the same function and options as the `cf check-route` command.


### bluemix network route-map
{: #bluemix_network_route_map}

Map a route to an existing cf application or container group that has the specified domain and host name.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (required)</dt>
   <dd>The name of the cf application or container group to be mapped with a route.</dd>
   <dt>DOMAIN (required)</dt>
   <dd>The domain of the route. For example, mychinabluemix.net or chinabluemix.net. </dd>
   <dt>-n <i>HOST_NAME</i> (optional)</dt>
   <dd>The host name of the route. If not provided, the host name is set to the app name or container group name by default.</dd>
   </dl>

<strong>Examples</strong>:

Map a route to `my-app` with specified domain:

```
bluemix network route-map my-app mychinabluemix.net
```

Map a route to 'my-container-group' with specified domain and host name:

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

Unmap the specified route from an existing cf application or container group.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (required)</dt>
   <dd>The name of the cf application or container group.</dd>
   <dt>DOMAIN (required)</dt>
   <dd>The domain of the route (for example, mychinabluemix.net or chinabluemix.net).</dd>
   <dt>-n <i>HOST_NAME</i> (optional)</dt>
   <dd>The host name of the route. If not provided, the host name is set to app name or container group name by default.</dd>
   </dl>

<strong>Examples</strong>:

Unmap `my-app.mychinabluemix.net` from `my-app`:

```
bluemix network route-unmap my-app mychianbluemix.net
```

Unmap `abc.chinabluexmix.net` from `my-container-group`:

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

This command has the same function and options as the `cf create-route` command.


### bluemix network route-delete
{: #bluemix_network_route_delete}

This command has the same function and options as the `cf delete-route` command.


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

This command has the same function and options as the `cf delete-orphaned-routes` command.


### bluemix network domains
{: #bluemix_network_domains}

This command has the same function and options as the `cf domains` command.


### bluemix network domain-create
{: #bluemix_network_domain_create}

This command has the same function and options as the `cf create-domain` command.


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

This command has the same function and options as the `cf delete-domain` command.


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

This command has the same function and options as the `cf create-shared-domain` command.


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

This command has the same function and options as the `cf delete-shared-domain` command.



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

Show monthly usage and costs of your account.

```
bluemix bss account-usage [-d YYYY-MM] [--json]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:

<dl>
  <dt>-d MONTH_DATE (optional)</dt>
  <dd>Display data for month and date specifying by using the YYYY-MM format. If not specified, usage of the current month is shown.</dd>
  <dt>--json (optional)</dt>
  <dd>Display the usage result in JSON format.</dd>
</dl>

<strong>Examples</strong>:

Show my account's usage and cost report in 2016-06:

```
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

Show monthly usage details of an org. This operation can be done only by a billing manager of the org.

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:

<dl>
  <dt>ORG_NAME (required)</dt>
  <dd>Name of the org.</dd>
  <dt>-d MONTH_DATE (optional)</dt>
  <dd>Display data for month and date specified by using the YYYY-MM format. If not specified, usage of the current month is shown.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Name of the region that hosts the org. If set to 'all', org usage in all regions is shown.</dd>
  <dt>--json (optional)</dt>
  <dd>Display the usage result in JSON format.</dd>
</dl>



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

Show monthly usage summary for orgs in my account.

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:

<dl>
  <dt>-d MONTH_DATE (optional)</dt>
  <dd>Display data for month and date specified by using the YYYY-MM format. If not specified, usage of the current month is shown.</dd>
  <dt>-r REGION_NAME</dt>
  <dd>Name of the region that hosts the orgs. If set to 'all', usage summary of the orgs in all regions is shown.</dd>
  <dt>--json (optional)</dt>
  <dd>Display the usage result in JSON format.</dd>
</dl>



### bluemix security cert
{: #bluemix_security_cert}

List the certificate information of a domain.

```
bluemix security cert DOMAIN_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:

   <dl>
   <dt>DOMAIN_NAME (required)</dt>
   <dd>The domain that hosts the certificate.</dd>
   </dl>



<strong>Examples</strong>:

View the certificate information of the domain `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

Add a certificate to the specified domain in the current org.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
   <dl>
   <dt>DOMAIN (required)</dt>
   <dd>The domain that the certificate is added to.</dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i> (required)</dt>
   <dd>The private key file path.</dd>
   <dt>-c <i>CERT_FILE</i> (required)</dt>
   <dd>The certificate file path.</dd>
   <dt>-p <i>PASSWORD</i> (optional)</dt>
   <dd>The password for the certificate.</dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i> (optional)</dt>
   <dd>The intermediate certificate file path.</dd>
   <dt>--verify-client (optional)</dt>
   <dd>Whether to enable the client certificate verification.</dd>
   </dl>


<strong>Examples</strong>:

Add a certificate to the domain `ibmcxo-eventconnect.com`:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

Remove a certificate from the specified domain in current org.

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>DOMAIN (required)</dt>
   <dd>Domain to remove the certificate from.</dd>
   <dt>-f  (optional)</dt>
   <dd>Force deletion without confirmation.</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

List all plugin repositories that are registered in {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repos
```

<strong>Prerequisites</strong>:  None


### bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Add a new plugin repository to {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>REPO_NAME (required)</dt>
   <dd>The name of the repository to be added. You can define your own name for each repository.</dd>
   <dt>REPO_URL (required)</dt>
   <dd>The URL of the repository to be added. The repository URL must contain the protocol (for example, http://plugins.ng.bluemix.net instead of plugins.ng.bluemix.net). http://plugins.ng.bluemix.net is the official plugin repository of Bluemix CLI.</dd>
    </dl>


<strong>Examples</strong>:

Add the official plugin repository of Bluemix CLI as `bluemix-repo`:

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


### bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

Remove a plugin repository from {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-remove REPO_NAME
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:
   <dl>
   <dt>REPO_NAME (required)</dt>
   <dd>The name of the repository to be removed.</dd>
   </dl>

<strong>Examples</strong>:

Remove `bluemix-repo` repository from {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix plugin repo-remove bluemix-repo
```


### bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

List all available plugins in all added repositories or a specific repository.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>-r <i>REPO_NAME</i> (optional)</dt>
   <dd>List only the plugins in specified repository.</dd>
   </dl>

<strong>Examples</strong>:

List all plugins in all added repositories:

```
bluemix plugin repo-plugins
```

List all plugins in the `bluemix-repo` repository:

```
bluemix plugin repo-plugins -r bluemix-repo
```


### bluemix plugin list
{: #bluemix_plugin_list}

List all installed plugins in {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin list
```

<strong>Prerequisites</strong>:  None


### bluemix plugin install
{: #bluemix_plugin_install}

Install the specific version of plugin to {{site.data.keyword.Bluemix_notm}} CLI from the specified path or repository.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME (required)</dt>
   <dd>If -r <i>REPO_NAME</i> is not specified, plugin is installed from the specified local path or remote URL.</dd>
   <dt>-r <i>REPO_NAME</i> (optional)</dt>
   <dd>The name of the repository where the plugin binary is located.</dd>
   <dt>-v <i>VERSION</i> (optional)</dt>
   <dd>The version of the plugin to be installed. If not provided, the latest version of the plugin is installed. This option is valid only when you install the plugin from the repository.</dd>
    </dl>

<strong>Examples</strong>:

Install a plugin from the local file:

```
bluemix plugin install /downloads/new_plugin
```

Install a plugin from the remote URL:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Install the `IBM-Containers` plugin of the latest version from the `bluemix-repo` repository:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
Install the `IBM-Containers` plugin with the  version `0.5.800` from the `bluemix-repo` repository:

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```






### bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Uninstall the specified plugin from {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:

   <dl>
   <dt>PLUGIN_NAME (required)</dt>
   <dd>The name of the plugin to be uninstalled.</dd>
    </dl>

<strong>Examples</strong>:

Uninstall the `IBM-Containers` plugin that was previously installed:

```
bluemix plugin uninstall IBM-Containers
```


### bluemix ic attach
{: #bluemix_ic_attach}

Control a running container or view its output. Use `CTRL+C` to exit and stop the container. This command calls the Docker CLI. For more information, see the [attach](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>--no-stdin (optional)</dt>
   <dd>Do not include the standard input.</dd>
   <dt>--sig-proxy (optional)</dt>
   <dd>Proxy all received signals to the process. The default value is <i>true</i>.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
    </dl>

<strong>Examples</strong>:

The following example shows a request to attach to the container `my_container`:
```
bluemix ic attach my_container
```


### bluemix ic build
{: #bluemix_ic_build}

Call the IBM Containers build service to build a Docker image locally or in your private {{site.data.keyword.Bluemix_notm}} repository. This command calls the Docker CLI. For more information, see the [build](https://docs.docker.com/engine/reference/commandline/build/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (required)</dt>
   <dd>The repository name to apply to the image that is created.</dd>
   <dt>--no-cache (optional)</dt>
   <dd>Do not use the cache when the image is built. The default is <i>false</i>.</dd>
   <dt>--pull (optional)</dt>
   <dd>Attempt to pull the base image from the registry even if it is cached.</dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Suppress the verbose output that is generated by the containers. The default is <i>false</i>.</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (required)</dt>
   <dd>The path to the Dockerfile and context on the local host.</dd>
    </dl>

<strong>Examples</strong>:

The following example shows a request to build an image that is named *myimage*. The Dockerfile and other artifacts to be used in the build are in the same directory that the command is running from. Because the registry and namespace are included with the image name, the image is built in your organization's private {{site.data.keyword.Bluemix_notm}} repository.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


### bluemix ic cp
{: #bluemix_ic_cp}
Copy files or folders between a container and the local filesystem. This command calls the Docker CLI. For more information, see the [cp](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.


### bluemix ic cpi
{: #bluemix_ic_cpi}

Access a Docker Hub image or an image from your local registry and copy the image to your private {{site.data.keyword.Bluemix_notm}} repository.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i> (required)</dt>
   <dd>The source repository and image name.</dd>
   <dt><i>DESTINATION_IMAGE</i> (required)</dt>
   <dd>The private {{site.data.keyword.Bluemix_notm}} repository URL, which includes the namespace and the destination image name. A tag for the image is optional.</dd>
   </dl>

<strong>Examples</strong>:

Copy an image from the source repository to your private repository and add a tag for the image:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copy the `sinatra` image from the `training` repository to your private repository `registry.ng.bluemix.net/mynamespace` and name the image as `mysinatra`. Add a tag `v1` for the image `mysinatra`.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


### bluemix ic exec
{: #bluemix_ic_exec}

Execute a command within a container. For more information, see the [exec](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-d|--detach (optional)</dt>
   <dd>Run the specified command in the background.</dd>
   <dt>-it (optional)</dt>
   <dd>Interactive mode. Keep the standard input displaying. Type <i>exit</i> to exit.</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i> (optional)</dt>
   <dd>The user name.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>The command to execute within the container or containers specified.</dd>
   </dl>

<strong>Examples</strong>:

Execute the `bash` command within the `my_container` container in the interactive mode:

```
bluemix ic exec -it my_container bash
```

Execute the `date` command within the `my_container` container:

```
bluemix ic exec my_container date
```


### bluemix ic group-create
{: #bluemix_ic_group_create}

Create a scalable container group.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRONMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (required)</dt>
   <dd>The image to be included in each container instance in the container group. You can list commands after the image, but do not put any options after the image. Include all options before you specify an image. <br><br>If you use an image in your organization's private {{site.data.keyword.Bluemix_notm}} repository, specify the image in the format: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>If you use an image that is provided by IBM Containers, do not include your organization's namespace. Specify the image in the format: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt>--name <i>GROUP_NAME</i> (required)</dt>
   <dd>Assign a name to the group. <i>-n</i> is deprecated.<br>
   <strong>Tip:</strong> The container name must start with a letter. The name can include uppercase letters, lowercase letters, numbers, periods ., underscores _, or hyphens -.</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (optional)</dt>
   <dd>Assign a memory limit to the group in MB. When you create a container group from the CLI, the default value for each container instance is <i>64</i> MB. When you create a container group from the {{site.data.keyword.Bluemix_notm}} Dashboard, the default value for each container instance is <i>256</i> MB. Accepted values are <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> and <i>2048</i>. After a memory limit is assigned, the value can't be changed.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (optional)</dt>
   <dd>The host name, such as <i>mycontainerhost</i>. The host and the domain combine to form the full public route URL, such as <i>http://mycontainerhost.mybluemix.net</i>. When you review the details of a container group with the <i>bluemix ic group-inspect</i> command, the host and the domain are listed together as the route.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>Usually, the domain is <i>.mybluemix.net</i>. The host and the domain are combined to form the full public route URL, such as <i>http://mycontainerhost.mybluemix.net</i>. When you review the details of a container group with the <i>bluemix ic group-inspect</i> command, the host and the domain are listed together as the route.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (optional)</dt>
   <dd>Set the environment variable. List multiple keys separately. If quotation marks are included, include them around both the environment variable name and the value. For example: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  The following table shows some commonly used environment variables that you can specify:</dd>
    </dl>


|  Environment variable                              |     Description                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Bind a service to a container. Use the `CCS_BIND_APP` environment variable to bind an app to the container. The app is bound to the target service and acts as a bridge that allows {{site.data.keyword.Bluemix_notm}} to bring your bridge app’s `VCAP_SERVICES` information to the running container instance.|
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | To bind a Bluemix service directly to a container without using a bridge app, use CCS_BIND_SRV. This binding allows Bluemix to inject the VCAP_SERVICES information into the running container instance. To list multiple Bluemix services, include them as part of the same environment variable. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Add a log file to be monitored in the container. Include the `LOG_LOCATIONS` environment variable with a path to the log file. |
{: caption="Table 8. Commonly used environment variables" caption-side="top"}


 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i> (optional)</dt>
   <dd> Import environment variables from a file where ENVFILE is the path to your file on your local directory. Every line in the file represents one key=value pair. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (optional)</dt>
   <dd>Attach a volume to a container by specifying the details in the format <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: The volume ID or name.</li>
   <li><i>CONTAINER_PATH</i>: The absolute path to the volume in the container.</li>
   <li>ro: Optional. Specifying <i>ro</i> makes the volume read-only instead of the default read/write.</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (optional)</dt>
   <dd>Expose the port for the HTTP traffic. Containers in your group must listen to the HTTP port. HTTPS requests can't be made. For container groups, you can't include multiple ports. <br><br>When you specify a port, you make the app available to the {{site.data.keyword.Bluemix_notm}} Load Balancer or containers that are trying to reach the host in the same {{site.data.keyword.Bluemix_notm}} space. Then the {{site.data.keyword.Bluemix_notm}} load balancer or containers can use the port to reach the host and the app in the same {{site.data.keyword.Bluemix_notm}} space. If a port is specified in the Dockerfile for the image that you are using, include that port. <br>
   <strong>Tips</strong>: <ul>
   <li>For the IBM certified Liberty Server image or a modified version of this image, enter port 9080.</li>
   <li>For the IBM certified Node.js image or a modified version of this image, enter port 8000.</li>
   </ul>
   </dd>
   <dt>-P (optional)</dt>
   <dd>Publish all ports</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (optional)</dt>
   <dd>The minimum number of instances. The default is 1. If you set a minimum number of instances, the value can't be changed after the container group is created.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (optional)</dt>
   <dd>The maximum number of instances. The default is 2. If you set a maximum number of instances, the value can't be changed after the container group is created.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (optional)</dt>
   <dd>The number of instances that you require. The default is 2.</dd>
   <dt>--auto (optional)</dt>
   <dd>When the container group is created and the automatic recovery is enabled, IBM Containers check the health of each instance with an HTTP request to the port that is assigned.<br>
   If no response is received from a container instance in 2 subsequent 90 second intervals, the instance is removed and replaced with a new instance. No action is taken if the container is responsive. This process is repeated continuously. During a 30 minute window, if the total number of different containers that are members of the group equals or exceeds 3 times the maximum observed size of the group, the automatic recovery is disabled permanently for the container group. To enable automatic recovery again, you must re-create the container group.</dd>
  <dt>--anti (optional)</dt>
  <dd> Use anti-affinity to make your container group more highly available. The --anti option forces every container instance in your group to be placed on a separate physical compute node, which reduces the chances of all containers in a group crashing due to a hardware failure. You might not be able to use this option with larger group sizes because each Bluemix region and organization has a limited set of compute nodes available for deployment. If your deployment does not succeed, either reduce the number of container instances in the group or remove the --anti option. </dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>The command and arguments that are passed to the container group to execute. This command must be a long-running command. Do not use a short-lived command that does not run for very long, for example, <i>/bin/date</i>, because the short-lived command might cause the container to crash.  <br> <strong>Notes:</strong> <ul>
   <li>The command and its arguments must come at the end of the <i>bluemix ic run</i> command line.</li>
   <li>If the command arguments include the hyphen -, as in <i>-c</i> in the previous example command, the command must be preceded by two hyphens --.</li>
   </ul></dd>
   </dl>


<strong>Examples</strong>:

Create a container group `my_container_group` by using the `registry.ng.bluemix.net/ibmnode` image that is provided by IBM Containers, and then run the `ping localhost` long-running command on that container group:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Create a container group `my_container_group` by using the `registry.ng.bluemix.net/ibmnode` image that is provided by IBM Containers, and then run the `tail -f /dev/null` long-running command on that container group:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Create a scalable group `mygroup` with the automatic recovery enabled by using the `registry.ng.bluemix.net/ibmliberty` image. The port is `9080`, the host name is `mycontainerhost`, the domain name is `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


### bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

View detailed information, such as environment variables, ports, or memory, that is specified for a container group when it is created.

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to inspect the container group `my_group`:
```
bluemix ic group-inspect my_group
```


### bluemix ic group-instances
{: #bluemix_ic_group_instances}

List instances of a specified container group.

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

List all instances of the container group `my_group`:
```
bluemix ic group-instances my_group
```


### bluemix ic group-remove
{: #bluemix_ic_group_remove}

Remove a container group from a space.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-f|--force (optional)</dt>
   <dd>Forces the removal of a running or failed container.</dd>
   <dt><i>GROUP_NAME</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to remove a container group, where `my_group` is the name of the container group.
```
bluemix ic group-remove my_group
```


### bluemix ic group-update
{: #bluemix_ic_group_update}

Update a container group.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**Tip:** To update the host name or domain for a container group, use `bluemix ic route-map [-n HOST] [-d DOMAIN] CONTAINER_GROUP`.

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
 <dl>
   <dt>--anti (optional)</dt>
   <dd>Use anti-affinity to make your container group more highly available. The --anti option forces every container instance in your group to be placed on a separate physical compute node, which reduces the odds of all containers in a group crashing due to a hardware failure. You might not be able to use this option with larger group sizes because each Bluemix region and organization has a limited set of compute nodes available for deployment. If your deployment does not succeed, either reduce the number of container instances in the group or remove the --anti option.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (optional)</dt>
   <dd>The number of instances that you require. The default is <i>2</i>.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(optional)</dt>
   <dd>Set the environment variable. List multiple keys separately. If quotation marks are included, include them around both the environment variable name and the value. For example: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.</dd>
   <dt><i>GROUP_NAME</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to update the container group `my_group`:
```
bluemix ic group-update --desired 5 my_group
```


### bluemix ic groups
{: #bluemix_ic_groups}

List container groups in the private {{site.data.keyword.Bluemix_notm}} repository of the organization.

```
bluemix ic groups [-q]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:
	<dl>
	<dt>-q (optional)</dt>
   	<dd>Only display group IDs</dd>
	</dl>


### bluemix ic images
{: #bluemix_ic_images}

View a list of all available images in the organization's private {{site.data.keyword.Bluemix_notm}} repository. For more information, see the [images](https://docs.docker.com/engine/reference/commandline/images){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help. The list includes the image ID, the created date, and the image name.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-a|--all (optional)</dt>
   <dd>Include all of the image layers for each image in your organization's repository, not only the most recent layer.</dd>
   <dt>-f (optional)</dt>
   <dd>Filter the list of images by the condition provided.</dd>
   <dt>--no-trunc (optional)</dt>
   <dd>Do not truncate the output.</dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Display only the numeric IDs.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to receive a list of available images for the organization:
```
bluemix ic images
```


### bluemix ic info
{: #bluemix_ic_info}

View a set of information that describes the state of the container cloud service instance. The information includes the containers limit, containers usage, containers that are running, memory limit, memory usage, floating IP address limit, floating IP address usage, CCS host URL, registry host URL, and debug mode status.

```
bluemix ic info
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target


### bluemix ic init
{: #bluemix_ic_init}

Initialize the containers environment on your local machine to use the full capabilities of the IBM Containers service.

```
bluemix ic init
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

**Note:** Before initialization, ensure that the Docker CLI (docker) is installed and configured in your PATH environment variable. To switch to another region, use the `bluemix region-set` command.

<strong>Examples</strong>:

Switch to the `us-south` region:

```
bluemix region-set us-south
```


### bluemix ic inspect
{: #bluemix_ic_inspect}

View the information about a container. For more information, see the [inspect](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} command in the Docker help.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>IMAGE</i> (required)</dt>
   <dd>View detailed information about a specific image by specifying the image name or ID.</dd>
   <dt>images (required)</dt>
   <dd>View detailed information about all of the images in your repository.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>View detailed information about a specific container by specifying the container name or ID.</dd>
   </dl>

**Tip:** Only one of *IMAGE*, *images*, or *CONTAINER* can be specified at a time.

<strong>Examples</strong>:

The following example shows a request to inspect a container that is named `proxy`:
```
bluemix ic inspect proxy
```


### bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Bind an available floating IP address to a container.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (required)</dt>
   <dd>The IP address to be bound.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container ID or name to be bound.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to bind the IP address `192.123.12.12 to` the container `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


### bluemix ic ip-release
{: #bluemix_ic_ip_release}

Release a floating IP address from the container cloud service instance.

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (required)</dt>
   <dd>The IP address to release.</dd>
   </dl>


### bluemix ic ip-request
{: #ip_request}
Request a new floating IP address.

```
bluemix ic ip-request [-q]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-q (optional)</dt>
   <dd>List only the IP addresses, without the IDs for the containers that are bound to those IP addresses.</dd>
   </dl>


### bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Unbind a floating IP address from its container.

Public IP addresses are a limited resource in IBM Containers. Therefore, public IP addresses that are allocated to a space and not bound to a container are periodically reclaimed from free trial users, approximately on a weekly basis. Unbound public IP addresses are never reclaimed from pay as you go or subscription customers.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (required)</dt>
   <dd>The IP address to be unbound.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container ID or name to be unbound.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to unbind the IP address `192.123.12.12` from the container `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


### bluemix ic ips
{: #bluemix_ic_ips}

List the available floating IP addresses for the user that is logged. The list includes IP addresses and the container ID that the IP addresses are linked to. If the IP address is unused, no container ID will be shown.

```
bluemix ic ips [-q]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-q (optional)</dt>
   <dd>List only the IP addresses, without the IDs for the containers that are bound to those IP addresses.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to receive a list of all IP addresses for the organization.
```
bluemix ic ips -q
```


### bluemix ic kill
{: #bluemix_ic_kill}

Stop a running process in a container without stopping the container. For more information, see the [kill](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (optional)</dt>
   <dd>Send a command to the process that is running in the container.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container ID or name.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to kill the process in a container that is named `proxy`:
```
bluemix ic kill proxy
```


### bluemix ic logs
{: #bluemix_ic_logs}

Show the output or error logs for a running container. For more information, see the [logs](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.
```
bluemix ic logs [OPTIONS] CONTAINER
```


### bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

View the name of the private {{site.data.keyword.Bluemix_notm}} image repository for the organization that you are logged in to.

```
bluemix ic namespace-get
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target


### bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Set the name of the private {{site.data.keyword.Bluemix_notm}} image repository the organization that you are logged in to.

*Restriction*: You can't use a hyphen `-` in the name of your repository namespace.

```
bluemix ic namespace-set NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>NAME</i> (required)</dt>
   <dd>A one-time only function to set the repository namespace for your organization, if it is not already set. After you set the namespace, reinitialize IBM Containers through `bluemix ic init` command before you continue.</dd>
   </dl>


### bluemix ic pause
{: #pause}

Pause all processes within a running container. For more information, see the [pause](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help. To stop a container, see the [bluemix ic unpause](#unpause) command.

```
bluemix ic pause CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:
   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Responses</strong>:

- Paused container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to pause a container that is named `proxy`:
```
bluemix ic pause proxy
```


### bluemix ic port
{: #bluemix_ic_port}

List port mappings or a specific mapping for the container. This command wraps the `docker port` command. For more information, see the [port](https://docs.docker.com/engine/reference/commandline/port/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.


### bluemix ic ps
{: #bluemix_ic_ps}
View a list of containers that are running in the logged-in user's namespace. By default, this command shows only containers that are running. For more information, see the [ps](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-a|--all (optional)</dt>
   <dd>Show all containers, both running and stopped.</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (optional)</dt>
   <dd>Search containers that have a specific environment variable value. You can filter your containers by any environment variable key or value that is listed in the Env section of your CLI response when you inspect a container. Replace SEARCH_CRITERIA with the key or value you are looking for. Your search criteria does not need to be an exact match. </dd>
   <dt>-s|--size (optional)</dt>
   <dd>List the sizes of the containers.</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (optional)</dt>
   <dd>List the most recently created containers, where <i>NUM</i> is the number of the most recently created containers that you want to return. <br><br> For example, if you created containers <i>node1</i> through <i>node5</i> sequentially, the command <i>bluemix ic ps --limit 2</i> returns node4 and node5 because they are the last two containers that are created. </dd>
   <dt>-q|--quiet (optional)</dt>
   <dd>Display only container IDs.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to see all running and stopped containers:
```
bluemix ic ps -a
```


### bluemix ic rename
{: #bluemix_ic_rename}
Rename a container. For more information, see the [rename](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

<dl>
   <dt><i>OLD_NAME</i> (required)</dt>
   <dd>The old name of the container.</dd>
   <dt><i>NEW_NAME</i> (required)</dt>
   <dd>The new name of the container.</dd>
   </dl>


### bluemix ic reprovision
{: #bluemix_ic_reprovision}

Re-create the IBM Containers service in the Bluemix space that you are logged into. The original quota for the space is maintained.

<strong>Important</strong>: When you run this command, none of your single containers and groups in this space will be migrated to the re-provisioned space and they will be removed during the migration process.

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>Command options</strong>:

<dl>
   <dt>--force|-f (optional)</dt>
   <dd>Forces the re-creation of the IBM Containers service in the Bluemix space.</dd>
   <dt><i>AVAILABILITY_ZONE</i> (optional)</dt>
   <dd>The name of IBM Containers availability zone where your containers are deployed. If no availability zone is specified, the default availability zone that is set for the region is used.</dd>
   </dl>


### bluemix ic restart
{: #bluemix_ic_restart}

Restart a container. For more information, see the [restart](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (optional)</dt>
   <dd>The number of seconds to wait before the container is restarted.</dd>
   </dl>


<strong>Responses</strong>:

- Restarted container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to restart a container that is named `proxy`:
```
bluemix ic restart proxy
```


### bluemix ic rm
{: #bluemix_ic_rm}

Remove a container. For more information, see the [rm](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-f|--force (optional)</dt>
   <dd>Forces the removal of a running or failed container.</dd>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Responses</strong>:

- Removed container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service.

<strong>Examples</strong>:

The following example shows a request to remove a container that is named `proxy`:
```
bluemix ic rm proxy
```


### bluemix ic rmi
{: #bluemix_ic_rmi}

Remove an image from the logged-in user's namespace. For more information, see the [rmi](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i> (optional)</dt>
   <dd>Change the registry host. The default is to use the registry that you specify in the <i>bluemix ic init</i> command.</dd>
   <dt><i>IMAGE</i> (required)</dt>
   <dd>The name of the image that you want to remove. If a tag is not specified in the image name, the image tagged <i>latest</i> is deleted by default.</dd>
   </dl>

<strong>Responses</strong>:

- Removed: `{IMAGE}`

 Where `{IMAGE}` is the name of the image that was removed.

- Error! No registry host specified.

- Image remove failed - Could not connect to container cloud registry

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

<strong>Examples</strong>:

The following example shows a request to remove the image `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


### bluemix ic route-map
{: #bluemix_ic_route_map}

Establish the route for internet traffic to use to access the container group. You can use this command to establish a new route or update an existing route.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (optional)</dt>
   <dd>The host name for the route. The host name is the first part of the full public route URL, such as <i>mycontainerhost</i> in the URL <i>mycontainerhost.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>The domain name for the route, which is the second part of the full public route URL. In most cases, the domain is <i>mybluemix.net</i>. You can also use this parameter to specify a private domain.</dd>
   <dt><i>CONTAINER_GROUP</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to map the route for the group that is called `GROUP1`, where `my_host` is the host name, `mybluemix.net` is the domain.
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


### bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Establish the route for internet traffic to use to access the container group. You can use this command to establish a new route or update an existing route.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (optional)</dt>
   <dd>The host name for the route.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (optional)</dt>
   <dd>The domain name for the route.</dd>
   <dt><i>CONTAINER_GROUP</i> (required)</dt>
   <dd>The container group ID or name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to unmap the route for the group that is called `GROUP1`, where `my_host` is the host name and `organization.com` is the domain.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


### bluemix ic run
{: #bluemix_ic_run}

Start a new container in the container cloud service from an image name. For more information, see the [run](https://docs.docker.com/engine/reference/commandline/run/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Note:** Ensure that the Cloud Foundry command tool is installed and that you have a Cloud Foundry token. Successful login by using `bluemix login` and `bluemix ic init` generates the required token and certificates.


<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>  (optional)</dt>
   <dd>Expose the port for the HTTP traffic. Include any ports that are specified in the Dockerfile for the image that you are using. You can include multiple ports with multiple <i>-p</i> options. Exposing a port will automatically bind a public IP address to the container if a public IP address is available. <br><br>If you have an existing IP address in the space that you want to bind to the container, you can specify the IP address rather than bind it later. The IP address must be specified in the  format: &lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br><br>For more information about requesting IP addresses for a space, see <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a> command. <br><br>When you specify a port, you are making the app available to the {{site.data.keyword.Bluemix_notm}} Load Balancer or containers in the same {{site.data.keyword.Bluemix_notm}} space that are trying to reach the host. If a port is specified in the Dockerfile for the image that you are using, include that port. <br><br><strong>Tips:</strong><ul><li>For the IBM certified Liberty Server image or a modified version of this image, enter port 9080.</li><li>For the IBM certified Node.js image or a modified version of this image, enter port 8000.</li></ul></dd>
   <dt>-P (optional)</dt>
   <dd>Automatically expose the ports that are specified in the image's Dockerfile for the HTTP traffic.</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i> (optional)</dt>
   <dd>Assign a memory limit to the group in MB. When you create a container group from the CLI, the default value for each container instance is 64 MB.  When you create a container group from the {{site.data.keyword.Bluemix_notm}} Dashboard, the default value for each instance is 256 MB. Accepted values are 64, 256, 512, 1024 and 2048. After a memory limit is assigned, the value can't be changed.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (optional)</dt>
   <dd>Set the environment variable, where <i>ENV</i> is a key=value pair. List multiple keys separately. If you include quotation marks, include them around both the environment variable name and the value. For example: -e "key1=value1" -e "key2=value2" -e "key3=value3". The following table shows some commonly used environment variables that you can specify:</dd>
   </dl>


|      Environment variable                          |   Description                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Bind a service to a container. Use the `CCS_BIND_APP` environment variable to bind an app to the container. The app is bound to the target service and acts as a bridge that allows {{site.data.keyword.Bluemix_notm}} to bring your bridge app’s `VCAP_SERVICES` information into the running container instance. For more information about creating a bridge app, see [Binding a service to a container](/docs/containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | To bind a Bluemix service directly to a container without using a bridge app, use CCS_BIND_SRV. This binding allows Bluemix to inject the VCAP_SERVICES information into the running container instance. To list multiple Bluemix services, include them as part of the same environment variable. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Add a log file to be monitored in the container. Include the `LOG_LOCATIONS` environment variable with a path to the log file. |
{: caption="Table 9. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (optional)</dt>
   <dd>Attach a volume to a container by specifying the details in the format <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: The volume ID or name.</li>
   <li><i>CONTAINER_PATH</i>: The absolute path to the volume in the container.</li>
   <li>ro: Optional. Specifying <i>ro</i> makes the volume read-only instead of the default read/write.</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i> (required)</dt>
   <dd>Assign a name to the container. <br> <strong>Tip:</strong> The container name must start with a letter. The name can include uppercase letters, lowercase letters, numbers, periods ., underscores _, or hyphens -.</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i> (optional)</dt>
   <dd>Whenever you want a container to communicate with another container that is running, you can address it by using an alias for the host name.</dd>
   <dt>-it (optional)</dt>
   <dd>Run the container in an interactive mode. After the container is created, keep the standard input displaying. Type <i>exit</i> to exit.</dd>
   <dt><i>IMAGE</i> (required)</dt>
   <dd>The image to be included in the container. You can list commands after the image, but don't put any options after the image. Include all options before specifying an image. Include all options before you specify an image. <br><br>If you use an image in your organization's private {{site.data.keyword.Bluemix_notm}} repository, specify the image in the format: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>If you use an image that is provided by IBM Containers, specify the image in the format: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt><i>CMD</i> (optional)</dt>
   <dd>The command and arguments that are passed to the container group to execute. This command must be a long-running command. Do not use a short-lived command that does not run for very long, for example, <i>/bin/date</i>, because the short-lived command might cause the container to crash.</dd>
   </dl>


<strong>Examples</strong>:

Run the `sh -c "while true; do date; sleep 20; done"` long-running command on the `my_container` container that is built on the `registry.ng.bluemix.net/ibmnode` image.
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Create and then start a container `proxy` with a `1024` MB memory limit by using the `my_namespace/nginx` image, where `my_namespace` is the namespace associated with the logged-in users.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Create and then start a container by using the `my_namespace/blog` image, pass the credentials as environmental variables. `my_namespace` is the namespace associated with the logged-in users.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

Add a volume to a container by using the `my_namespace/blog` image, where `my_namespace` is the namespace associated with the logged-in users.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


### bluemix ic service-bind
{: #bluemix_ic_service-bind}

Add a service to a running container group. This command is available only to container groups. Single containers must bind a service as part of the bluemix ic run command.

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE
```
<strong>Command options</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (required)</dt>
   <dd>The group ID or name.</dd>
   <dt><i>SERVICE_INSTANCE</i> (required)</dt>
   <dd>The name of the service instance to be added to the container group.</dd>
   </dl>


### bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Remove a service from a running container group. This command is available only to container groups. Single containers must remove the container and create a new container without the service.

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE
```
<strong>Command options</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (required)</dt>
   <dd>The group ID or name.</dd>
   <dt><i>SERVICE_INSTANCE</i> (required)</dt>
   <dd>The name of the service instance to be added to the container group.</dd>
   </dl>


### bluemix ic start
{: #ic_start}
Start a stopped container. For more information, see the [start](https://docs.docker.com/engine/reference/commandline/start/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help. To stop a container, see the [bluemix ic stop](#ic_stop) command.

```
bluemix ic start CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>


<strong>Responses</strong>:

- Started container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to start a container that is named `proxy`.
```
bluemix ic start proxy
```


### bluemix ic stats
{: #bluemix_ic_stats}

For one or more containers, view live usage statistics. Use `CTRL+C` to exit. For more information, see the [stats](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} command in the Docker help.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   <dt>--no-stream (optional)</dt>
   <dd>Display only the latest result and do not include any information that precedes it.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request for the most recent statistics about a container:
```
bluemix ic stats --no-stream my_container
```


### bluemix ic stop
{: #ic_stop}
Stop a running container. For more information, see the [stop](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help. To start a container, see the [bluemix ic start](#ic_start) command.

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (optional)</dt>
   <dd>The number of seconds to wait before the container is killed.</dd>
   </dl>

<strong>Responses</strong>:

- Stopped container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to stop a container that is named `proxy`.
```
bluemix ic stop proxy
```


### bluemix ic top
{: #bluemix_ic_top}

Show the processes that are running in the container. For more information, see the [top](https://docs.docker.com/engine/reference/commandline/top/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to display the processes in a container that is called `my_container`.
```
bluemix ic top my_container
```


### bluemix ic unpause
{: #unpause}

Unpause all processes within a running container. For more information, see the [unpause](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help. To pause a container, see the [bluemix ic pause](#pause) command.

```
bluemix ic unpause CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Responses</strong>:

- Unpaused container successfully.

- Command failed with container cloud service

 `{message}`

 Where `{message}` is the related error.

- Command failed - Could not connect to container cloud service

<strong>Examples</strong>:

The following example shows a request to unpause a container that is named `proxy`:
```
bluemix ic unpause proxy
```


### bluemix ic unprovision
{: #bluemix_ic_unprovision}

Delete the IBM Containers service from the Bluemix space that you are logged into.

<strong>Attention</strong>: When you run this command, all your single containers and container groups are lost. Your space is still available in Bluemix. To start using the IBM Containers again, you must run `bluemix ic reprovision` to provision the IBM Containers service again.

```
bluemix ic reprovision [--force|-f]
```
<strong>Command options</strong>:

<dl>
   <dt>--force|-f (optional)</dt>
   <dd>Forces the deletion of the Bluemix from the Bluemix space.</dd>
 </dl>


### bluemix ic version
{: #bluemix_ic_version}

Show the version of Docker and the IBM Containers API.

```
bluemix ic version
```

<strong>Prerequisites</strong>:  Docker

To see the version of the IBM Containers, run `bluemix ic info`. For more information, see the [version](https://docs.docker.com/engine/reference/commandline/version/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.


### bluemix ic volume-create
{: #bluemix_ic_volume_create}

Create a volume.

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>FS_NAME</i> (optional)</dt>
   <dd>The file share name. If no file share is available or named the volume will be built on the space's default file share.</dd>
   <dt><i>VOLUME_NAME</i> (required)</dt>
   <dd>The volume name. The name can contain lowercase letters, numbers, underscores _, and hyphens -.</dd>
   </dl>


<strong>Examples</strong>:

The following example shows a request to create a volume.
```
bluemix ic volume-create volume_name fileshare_name
```


### bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

List file shares.

```
bluemix ic volume-fs
```


### bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Create a file share.

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (required)</dt>
   <dd>The file share name. The name can contain lowercase letters, numbers, underscores _, and hyphens -.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to create a file share.
```
bluemix ic volume-fs-create my_file_share
```


### bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

List all file share flavors.

```
bluemix ic volume-fs-flavors
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target


### bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspect a file share.

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i> (required)</dt>
   <dd>The file share name.</dd>
   </dl>

<strong>Examples</strong>:

The following example is a request to inspect a file share, where `my_file_share` is the name of the file share.
```
bluemix ic volume-fs-inspect my_file_share
```


### bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Remove a file share.

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (required)</dt>
   <dd>The file share name.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to remove a file share, where `my_file_share` is the name of the file share.
```
bluemix ic volume-fs-remove my_file_share
```


### bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspect a volume.

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (required)</dt>
   <dd>The volume name.</dd>
   </dl>

<strong>Examples</strong>:

The following example is a request to inspect a volume, where `volume_name` is the name of the volume.
```
bluemix ic volume-inspect volume_name
```


### bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Remove a volume.

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (required)</dt>
   <dd>The volume name.</dd>
    </dl>

<strong>Examples</strong>:

The following example shows a request to remove a volume, where `volume_name` is the name of the volume.
```
bluemix ic volume-remove volume_name
```


### bluemix ic volumes
{: #bluemix_ic_volumes}

List volumes.

```
bluemix ic volumes
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target


### bluemix ic wait
{: #bluemix_ic_wait}

Exit a container and display the exit code as confirmation. For more information, see the [wait](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} ![External link icon](../../../icons/launch-glyph.svg) command in the Docker help.

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to exit a container that is called `my_container`:
```
bluemix ic wait my_container
```


### bluemix ic wait-status
{: #bluemix_ic_wait_status}

Wait for a single container or container group to reach a non-transient state. During this waiting time your command line does not return and you cannot enter commands. As soon as the container reaches a non-transient state, an OK message is displayed. For single containers, the non-transient states include Running, Shutdown, Crashed, Paused, or Suspended. For container groups, the non-transient states include CREATE_COMPLETE, UPDATE_COMPLETE, or FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target, Docker

<strong>Command options</strong>:

   <dl>
   <dt><i>CONTAINER</i> (required)</dt>
   <dd>The container name or ID.</dd>
   </dl>

<strong>Examples</strong>:

The following example shows a request to exit a container that is called `my_container`:
```
bluemix ic wait my_container
```



# Related Links
{: #rellinks}

## Related Links
{: #general}

* [bx tool](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![External link icon](../../../icons/launch-glyph.svg)
