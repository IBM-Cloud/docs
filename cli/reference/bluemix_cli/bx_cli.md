---



copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} (bx) commands
{: #bluemix_cli}

Version: 0.5.2

The {{site.data.keyword.Bluemix_notm}} command line interface (CLI) provides a set of commands that are grouped by namespace for users to interact with {{site.data.keyword.Bluemix_notm}}. Some {{site.data.keyword.Bluemix_notm}} commands are wrappers of existing cf commands, while others provide extended capabilities for {{site.data.keyword.Bluemix_notm}} users. The following information lists commands that are supported by {{site.data.keyword.Bluemix_notm}} CLI, and includes their names, options, usage, prerequisites, descriptions, and examples.
{:shortdesc}

**Note:** *Prerequisites* list which actions are required before using the command. Commands that have no prerequisite actions list **None**. Otherwise, prerequisites might include one or more of the following actions:

<dl>
<dt>Endpoint</dt>
<dd>An API endpoint must be set through the <code>bluemix api</code> before using the command.</dd>
<dt>Login</dt>
<dd>Login by using the <code>bluemix login</code> command is required before using this command.
If logging in with federated ID, use '--sso' option to authenticate with one time passcode, or use '--apikey' to authenticate with API key. Go to {{site.data.keyword.Bluemix_notm}} console “Manage” -> “Security” -> “Bluemix API keys” to create API keys.
</dd>
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
 <td>[bluemix help](bx_cli.html#bluemix_help)</td>
 <td>[bluemix api](bx_cli.html#bluemix_api)</td>
 <td>[bluemix login](bx_cli.html#bluemix_login)</td>
 <td>[bluemix logout](bx_cli.html#bluemix_logout)</td>
 <td>[bluemix target](bx_cli.html#bluemix_target)</td>
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

<table summary="bluemix commands that you can use to manage accounts, orgs, spaces, roles and API keys.">
<caption>Table 2. Commands for managing accounts, orgs, spaces, roles and API keys</caption>
 <thead>
 <th colspan="5">Commands for managing accounts, orgs, spaces, roles and API keys</th>
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
 <td>[bluemix iam account-users](bx_cli.html#bluemix_iam_account_users)</td>
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

<table summary="bluemix commands that you can use to manage cf apps and app related domains, routes and certificates.">
<caption>Table 3. Commands for managing cf apps and app related domains, routes and certificates</caption>
 <thead>
 <th colspan="5">Commands for managing cf apps and app related domains, routes and certificates</th>
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

<table summary="bluemix commands that you can use to manage Bluemix services.">
<caption>Table 4. Commands for managing Bluemix services</caption>
 <thead>
 <th colspan="5">Commands for managing Bluemix services</th>
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

<table summary="bluemix commands that you can use to manage Bluemix catalog, plug-ins, billing, and security settings.">
<caption>Table 5. Commands for managing Bluemix catalog, plug-ins, billing, and security settings</caption>
 <thead>
 <th colspan="5">Commands for managing Bluemix catalog, plug-ins, billing, and security settings</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix catalog templates](bx_cli.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](bx_cli.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](bx_cli.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](bx_cli.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](bx_cli.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](bx_cli.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](bx_cli.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](bx_cli.html#bluemix_plugin_list)</td>
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



## bluemix api
{: #bluemix_api}
Set or view the {{site.data.keyword.Bluemix_notm}} API endpoint.

```
bluemix api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

<strong>Prerequisites</strong>: None

<strong>Command options</strong>:
   <dl>
   <dt>API_ENDPOINT (optional)</dt>
   <dd>The API endpoint that is targeted, for example, `https://api.chinabluemix.net`. If both *API_ENDPOINT* and `--unset` options are not specified, the current API endpoint is displayed.</dd>
   <dt>--unset (optional)</dt>
   <dd>Remove the API endpoint setting.</dd>
   <dt>--skip-ssl-validation (optional)</dt>
   <dd>Bypass SSL validation of HTTP requests.</dd>
   </dl>
<strong>Examples</strong>:

Set the API endpoint to api.chinabluemix.net:

```
bluemix api api.chinabluemix.net
```

```
bluemix api https://api.chinabluemix.net --skip-ssl-validation
```

View the current API endpoint:

```
bluemix api
```

Unset the API endpoint:

```
bluemix api --unset
```


## bluemix login
{: #bluemix_login}

Log in user. 

```
bluemix login [OPTIONS...]
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:
<dl>
  <dt>-a <i>API_ENDPOINT</i> (optional)</dt>
  <dd> API endpoint (For example: api.ng.bluemix.net)</dd>
  <dt> --apikey <i>API_KEY or @API_KEY_FILE_PATH</i>
  <dd> API key content or the path of an API key file indicated by @</dd>
  <dt> --sso (optional) </dt>
  <dd> use one time passcode to login </dd>
  <dt> -u <i>USERNAME</i> (optional)</dt>
  <dd> Username</dd>
  <dt> -p <i>PASSWORD</i> (optional)</dt>
  <dd> Password</dd>
  <dt> -c <i>ACCOUNT_ID</i> (optional) </dt>
  <dd> ID of the target account</dd>
  <dt> -o <i>ORG_NAME</i> (optional) </dt>
  <dd> Name of the target organization </dd>
  <dt> -s <i>SPACE_NAME</i> (optional) </dt>
  <dd> Name of the target space</dd>
  <dt> --skip-ssl-validation (optional) </dt>
  <dd> Bypass SSL validation of HTTP requests. This option is not recommended.</dd>
</dl>

<strong>Examples</strong>:

Interactive login:

```
bluemix login
```

Login with username and password, and set target account, org and space:

```
bluemix login -u username -p password -c MyAccountID -o MyOrg -s MySpace
```

Login with one time passcode and set target account, org and space

```
bluemix login --sso -c MyAccountID -o MyOrg -s MySpace
```

Login with API key and set targets:

* API key has account associated

```
bluemix login --apikey api-key-string -o MyOrg -s MySpace
```

```
bluemix login --apikey @filename -o MyOrg -s MySpace
```

* API key has no account associated

```
bluemix login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
bluemix login --apikey @fileName -c MyAccountID -o MyOrg -s MySpace
```

<strong>Note:</strong> If the API Key has account associated, switch to another account is not allowed.


## bluemix logout
{: #bluemix_logout}

Log out user.

```
bluemix logout
```

<strong>Prerequisites</strong>:  None


## bluemix target
{: #bluemix_target}


Set or view the target account, region, organization or space.

```
bluemix target [-c ACCOUNT_ID] [-r REGION] [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
   <dl>
   <dt>-c <i>ACCOUNT_ID</i> (optional)</dt>
   <dd>The ID of the account to be targeted.</dd>
   <dt>-r <i>REGION</i> (optional)</dt>
   <dd>The region to be switched to.</dd>
   <dt>-o <i>ORG_NAME</i> (optional)</dt>
   <dd>The name of the organization to be targeted.</dd>
   <dt>-s <i>SPACE_NAME</i> (optional)</dt>
   <dd>The name of the space to be targeted.</dd>
   </dl>
If none of the options are specified, the current account, region, org and space are displayed.

<strong>Examples</strong>:

Set the current account, organization and space

```
bluemix target -c MyAccountID -o MyOrg -s MySpace
```

Switch to a new region

```
bluemix target -r eu-gb
```

View the current account, region, org and space:

```
bluemix target
```


## bluemix info
{: #bluemix_info}

View the basic {{site.data.keyword.Bluemix_notm}} information, including the current region, the cloud controller version, and some useful endpoints, such as endpoints for login and exchanging access token.

```
bluemix info
```

<strong>Prerequisites</strong>:  Endpoint


## bluemix config
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


## bluemix curl
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

## bluemix update
{: #bluemix_update}

Update CLI to the latest version

```
bluemix update
```

<strong>Prerequisites</strong>:  None

## bluemix regions
{: #bluemix_regions}

View the information for all regions on {{site.data.keyword.Bluemix_notm}}.

```
bluemix regions
```

<strong>Prerequisites</strong>:  Endpoint


## bluemix iam orgs
{: #bluemix_iam_orgs}

List all organizations

```
bluemix iam orgs [-r REGION] [--guid]
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

## bluemix iam org
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


## bluemix iam org-create
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

## bluemix iam org-replicate
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


## bluemix iam org-rename
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

## bluemix iam org-delete
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


## bluemix iam spaces
{: #bluemix_iam_spaces}

This command has the same function and options as the `cf spaces` command.


## bluemix iam space
{: #bluemix_iam_space}

This command has the same function and options as the `cf space` command.


## bluemix iam space-create
{: #bluemix_iam_space_create}

This command has the same function and options as the `cf create-space` command.


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


This command has the same function and options as the `cf rename-space` command.


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


This command has the same function and options as the `cf delete-space` command.

## bluemix iam org-users
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

## bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

Add a user into org (org manager required).

```
 bluemix iam org-user-add USER_NAME ORG
```

## bluemix iam org-user-remove
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

## bluemix iam org-roles
{: #bluemix_iam_org_roles}

Get all organization roles of the current user

```
bluemix iam org-roles
```

<strong>Prerequisites</strong>:  Endpoint, Login

## bluemix iam org-role-set
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


## bluemix iam org-role-unset
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

## bluemix iam space-users
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


## bluemix iam space-role-set
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

## bluemix iam space-role-unset
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

## bluemix iam accounts
{: #bluemix_iam_accounts}

List all accounts of the current user

```
bluemix iam accounts
```

<strong>Prerequisites</strong>:  Endpoint, Login


## bluemix iam org-account
{: #bluemix_iam_org_account}

Display the account of specified organization(org user required)

```
bluemix iam org-account ORG_NAME [--guid]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
<dl>
  <dt>--guid (optional)</dt>
  <dd>Display account ID only</dd>
</dl>


## bluemix iam account-users
{: #bluemix_iam_account_users}

Displays users associated with the account. This operation can be performed only by the account owner.

```
bluemix iam account-users
```

## bluemix iam account-user-delete
{: #bluemix_iam_account_user_delete}

Delete a user from the current account(account owner only)

```
bluemix iam account-user-delete USERNAME [-f]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
<dl>
<dt>USERNAME (required)</dt>
<dd>Username</dd>
<dt>--force, -f (optional)</dt>
<dd>Force deletion without confirmation.</dd>
</dl>

## bluemix iam account-user-invite
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

## bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

Resend invitation to a user(org manager or account owner is required)

```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```

## bluemix iam api-keys
{: #bluemix_iam api_keys}

List all Bluemix platform API keys

```
bluemix iam api-keys
```

<strong>Prerequisites</strong>:  Endpoint, Login

## bluemix iam api-key-create
{: #bluemix_iam_api_key_create}

Create a new Bluemix platform API key

```
bluemix iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
<dl>
<dt>NAME (required)</dt>
<dd>Name of the API key to be created.</dd>
<dt>-d <i>DESCRIPTION</i> (optional)</dt>
<dd>Description of the API key</dd>
<dt>-f, -- file <i>FILE</i></dt>
<dd>Save API key information to specified file. If not set, the JSON content will be displayed.</dd>
</dl>

<strong>Examples</strong>:

Create an API key and save to a file

```
bluemix iam api-key-create MyKey -d "this is my API key" -f key_file
```

## bluemix iam api-key-update
{: #bluemix_iam_api_key_update}

Update a Bluemix platform API key

```
bluemix iam api-key-update NAME [-n NAME] [-d DESCRIPTION]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
<dl>
<dt>NAME (required)</dt>
<dd>The old name of the API key to be updated.</dd>
<dt>-n <i>NAME</i> (optional)</dt>
<dd>The new name of the API key</dd>
<dt>-d <i>DESCRIPTION</i> (optional)</dt>
<dd>The new description of the API key</dd>
</dl>

<strong>Examples</strong>:

Update the description of an API key:

```
bluemix iam api-key-update MyKey -d "the new description of my key"
```

## bluemix api-key-delete
{: #bluemix_api_key_delete}

Delete a Bluemix platform API key

```
bluemix iam api-key-delete NAME [-f]
```

<strong>Prerequisites</strong>:  Endpoint, Login

<strong>Command options</strong>:
<dl>
<dt>NAME (required)</dt>
<dd>Name of the API key to be deleted.</dd>
<dt>-f  (optional)</dt>
<dd>Force deletion without confirmation.</dd>
</dl>


## bluemix app push
{: #bluemix_app_push}

This command has the same function and options as the `cf push` command.


## bluemix app list
{: #bluemix_app_list}

This command has the same function and options as the `cf apps` command.


## bluemix app show
{: #bluemix_app_show}

This command has the same function and options as the `cf app` command.


## bluemix app delete
{: #bluemix_app_delete}

This command has the same function and options as the `cf delete` command.


## bluemix app rename
{: #bluemix_app_rename}

This command has the same function and options as the `cf rename` command.


## bluemix app start
{: #bluemix_app_start}

This command has the same function and options as the `cf start` command.


## bluemix app stop
{: #bluemix_app_stop}

This command has the same function and options as the `cf stop` command.


## bluemix app restart
{: #bluemix_app_restart}

This command has the same function and options as the `cf restart` command.


## bluemix app restage
{: #bluemix_app_restage}


This command has the same function and options as the `cf restage` command.


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


This command has the same function and options as the `cf restart-app-instance` command.


## bluemix app events
{: #bluemix_app_events}

This command has the same function and options as the `cf events` command.


## bluemix app files
{: #bluemix_app_files}

This command has the same function and options as the `cf files` command.


## bluemix app logs
{: #bluemix_app_logs}

This command has the same function and options as the `cf logs` command.


## bluemix app env
{: #bluemix_app_env}

This command has the same function and options as the `cf env` command.


## bluemix app env-set
{: #bluemix_app_env_set}

This command has the same function and options as the `cf set-env` command.


## bluemix app env-unset
{: #bluemix_app_env_unset}

This command has the same function and options as the `cf unset-env` command.


## bluemix app stacks
{: #bluemix_app_stacks}

This command has the same function and options as the `cf stacks` command.


## bluemix app stack-show
{: #bluemix_app_stack_show}

This command has the same function and options as the `cf stack` command.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

This command has the same function and options as the `cf create-app-manifest` command.

## bluemix app domain-cert 
{: #bluemix_app_domain_cert}

List the certificate information of a domain.

```
bluemix app domain-cert DOMAIN_NAME
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
bluemix app domain-cert ibmcxo-eventconnect.com
```

## bluemix app domain-cert-add
{: #bluemix_app_domain_cert_add}

Add a certificate to the specified domain in the current org.

```
bluemix app domain-cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [-t TRUST_STORE_FILE]
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
   <dt>-t <i>TRUST_STORE_FILE</i> (optional)</dt>
   <dd>The trust store file.</dd>
   </dl>


<strong>Examples</strong>:

Add a certificate to the domain `ibmcxo-eventconnect.com`:

```
bluemix app domain-cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```

## bluemix app domain-cert-remove
{: #bluemix_app_domain_cert_remove}

Remove a certificate from the specified domain in current org.

```
bluemix app domain-cert-remove DOMAIN [-f]
```

<strong>Prerequisites</strong>:  Endpoint, Login, Target

<strong>Command options</strong>:

   <dl>
   <dt>DOMAIN (required)</dt>
   <dd>Domain to remove the certificate from.</dd>
   <dt>-f  (optional)</dt>
   <dd>Force deletion without confirmation.</dd>
   </dl>

## bluemix app domains
{: #bluemix_app_domains}

This command has the same function and options as the `cf domains` command.


## bluemix app domain-create
{: #bluemix_app_domain_create}

This command has the same function and options as the `cf create-domain` command.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

This command has the same function and options as the `cf delete-domain` command.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

This command has the same function and options as the `cf create-shared-domain` command.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

This command has the same function and options as the `cf delete-shared-domain` command.

## bluemix app routes
{: #bluemix_app_routes}

This command has the same function and options as the `cf routes` command.


## bluemix app route-check
{: #bluemix_app_route_check}

This command has the same function and options as the `cf check-route` command.


## bluemix app route-map
{: #bluemix_app_route_map}

Map a route to an existing cf application or container group that has the specified domain and host name.

```
bluemix app route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix app route-map my-app mychinabluemix.net
```

Map a route to 'my-container-group' with specified domain and host name:

```
bluemix app route-map my-container-group chinabluemix.net -n abc
```


## bluemix app route-unmap
{: #bluemix_app_route_unmap}

Unmap the specified route from an existing cf application or container group.

```
bluemix app route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix app route-unmap my-app mychianbluemix.net
```

Unmap `abc.chinabluexmix.net` from `my-container-group`:

```
bluemix app route-unmap my-container-group chinabluemix.net -n abc
```


## bluemix app route-create
{: #bluemix_app_route_create}

This command has the same function and options as the `cf create-route` command.


## bluemix app route-delete
{: #bluemix_app_route_delete}

This command has the same function and options as the `cf delete-route` command.


## bluemix app orphaned-routes-delete
{: #bluemix_app_orphaned_routes_delete}

This command has the same function and options as the `cf delete-orphaned-routes` command.


## bluemix app domains
{: #bluemix_app_domains}

This command has the same function and options as the `cf domains` command.


## bluemix app domain-create
{: #bluemix_app_domain_create}

This command has the same function and options as the `cf create-domain` command.


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

This command has the same function and options as the `cf delete-domain` command.


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

This command has the same function and options as the `cf create-shared-domain` command.


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

This command has the same function and options as the `cf delete-shared-domain` command.


## bluemix service offerings
{: #bluemix_service_offerings}


This command has the same function and options as the `cf marketplace` command.


## bluemix service list
{: #bluemix_service_list}

This command has the same function and options as the `cf services` command.


## bluemix service show
{: #bluemix_service_show}

This command has the same function and options as the `cf service` command.


## bluemix service create
{: #bluemix_service_create}

This command has the same function and options as the `cf create-service` command.


## bluemix service update
{: #bluemix_service_update}

This command has the same function and options as the `cf update-service` command.


## bluemix service delete
{: #bluemix_service_delete}

This command has the same function and options as the `cf delete-service` command.


## bluemix service rename
{: #bluemix_service_rename}

This command has the same function and options as the `cf rename-service` command.


## bluemix service bind
{: #bluemix_service_bind}

This command has the same function and options as the `cf bind-service` command.


## bluemix service unbind
{: #bluemix_service_unbind}

This command has the same function and options as the `cf unbind-service` command.


## bluemix service key-create
{: #bluemix_service_key_create}

This command has the same function and options as the `cf create-service-key` command.


## bluemix service key-delete
{: #bluemix_service_key_delete}

This command has the same function and options as the `cf delete-service-key` command.


## bluemix service keys
{: #bluemix_service_keys}

This command has the same function and options as the `cf service-keys` command.


## bluemix service key-show
{: #bluemix_service_key_show}

This command has the same function and options as the `cf service-key` command.


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

This command has the same function and options as the `cf create-user-provided-service` command.


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

This command has the same function and options as the `cf update-user-provided-service` command.


## bluemix catalog templates
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


## bluemix catalog template
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


## bluemix catalog template-run
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

## bluemix billing account-usage
{: #bluemix_billing_account_usage}

Show monthly usage and costs of your account.

```
bluemix billing account-usage [-d YYYY-MM] [--json]
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
bluemix billing account-usage -d 2016-06
```

## bluemix billing org-usage
{: #bluemix_billing_org_usage}

Show monthly usage details of an org. This operation can be done only by a billing manager of the org.

```
bluemix billing org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
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



## bluemix billing orgs-usage-summary
{: #bluemix_billing_orgs_usage_summary}

Show monthly usage summary for orgs in my account.

```
bluemix billing orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
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


## bluemix plugin repos
{: #bluemix_plugin_repos}

List all plugin repositories that are registered in {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repos
```

<strong>Prerequisites</strong>:  None


## bluemix plugin repo-add
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


## bluemix plugin repo-remove
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


## bluemix plugin repo-plugins
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


## bluemix plugin list
{: #bluemix_plugin_list}

List all installed plugins in {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin list
```

<strong>Prerequisites</strong>:  None


## bluemix plugin install
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

## bluemix plugin update
{: #bluemix_plugin_update}

Upgrade the plug-in from a repository

```
bluemix plugin update -r REPO_NAME [PLUGIN NAME [-v VERSION]]
```

<strong>Prerequisites</strong>:  None

<strong>Command options</strong>:
<dl>
 <dt>-r REPO_NAME (required)</dt>
 <dd>The name of the repository where the plugin binary is located.</dd>
 <dt><i>PLUGIN_NAME</i> (optional)</dt>
 <dd>If not specified, all plug-ins available for update in the given repository are listed for selection.</dd>
 <dt>-v <i>VERSION</i> (optional)</dt>
 <dd>The version of the plugin to be updated to. If not provided, update the plugin to the the latest available version.</dd>
</dl>

<strong>Examples</strong>:

check for all available upgrade in plugin repository "My-Repo":

```
bluemix plugin update -r My-Repo
```

Upgrade plugin "plugin-echo" in repository "My-Repo" to the latest:

```
bluemix plugin update -r My-Repo plugin-echo
```

Update plugin "plugin-echo" in repository "My-Repo" to version "1.0.1":

```
bluemix plugin update -r My-Repo plugin-echo -v 1.0.1
```

## bluemix plugin uninstall
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
