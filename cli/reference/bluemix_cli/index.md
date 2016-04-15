---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} (bx) commands
{: #bluemix_cli}

*Last updated: 15 Apr 2016*

The {{site.data.keyword.Bluemix_notm}} command line interface (CLI) provides a set of commands that are grouped by namespace for users to interact with {{site.data.keyword.Bluemix_notm}}. Some {{site.data.keyword.Bluemix_notm}} of the commands are wrappers of existing cf commands, while others provide extended capabilities for {{site.data.keyword.Bluemix_notm}} users. The information that follows lists all commands that are supported by {{site.data.keyword.Bluemix_notm}} CLI and includes their names, options, usage, prerequisites, descriptions, and examples.
{:shortdesc}
 
**Note:** *Prerequisites* list which actions are required before using the command. Commands that have no prerequisite actions list **None**. Otherwise, prerequisites might include one or more of the following actions:
<dl>
<dt>Endpoint</dt>
<dd>An API endpoint must be set through the <code>bluemix api</code> before using the command.</dd>
<dt>Login</dt>
<dd>Login by using the <code>bluemix login</code> command is required before using this command.</dd>
<dt>Target</dt>
<dd>The <code>bluemix target</code> command must be used to set an org and space before using this command.</dd>
<dt>Docker</dt>
<dd>The Docker CLI (docker) must be installed to run this command.</dd>
</dl>

You can use the following {{site.data.keyword.Bluemix_notm}} commands:

 <table role="presentation"> 
 <tbody> 
 <tr> 
 <td>[bluemix help](index.html#bluemix_help)</td> 
 <td>[bluemix api](index.html#bluemix_api)</td> 
 <td>[bluemix login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr> 
 <tr> 
 <td> 
 [bluemix info](index.html#bluemix_info) </td> 
 <td>[bluemix config](index.html#bluemix_config)</td> 
 <td>[bluemix list](index.html#bluemix_list)</td>
 <td>[bluemix scale](index.html#bluemix_scale)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs) </td> 
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td> 
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete) </td> 
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td> 
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete) </td> 
 <td>[bluemix iam account-users](index.html#bluemix_iam_account-users)</td> 
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account-user-invite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset) </td> 
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td> 
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app list](index.html#bluemix_app_list) </td> 
 <td>[bluemix app show](index.html#bluemix_app_show)</td> 
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app start](index.html#bluemix_app_start) </td> 
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td> 
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app events](index.html#bluemix_app_events) </td> 
 <td>[bluemix app files](index.html#bluemix_app_files)</td> 
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset) </td> 
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td> 
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 </tr>
 
 <tr> 
 <td>[bluemix service list](index.html#bluemix_service_list) </td> 
 <td>[bluemix service show](index.html#bluemix_service_show)</td> 
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service rename](index.html#bluemix_service_rename) </td> 
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td> 
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service keys](index.html#bluemix_service_keys) </td> 
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td> 
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix catalog template](index.html#bluemix_catalog_template) </td> 
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td> 
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td> 
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td> 
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td> 
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td> 
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td> 
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td> 
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td> 
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td> 
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td> 
 <td>[bluemix ic init](index.html#bluemix_ic_init)</td> 
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic create](index.html#bluemix_ic_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td> 
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td> 
 <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td> 
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td> 
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
 <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic info](index.html#bluemix_ic_info)</td> 
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td> 
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td> 
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td> 
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic unpause](index.html#unpause)</td> 
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td> 
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td> 
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td> 
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic stop](index.html#ic_stop)</td> 
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td> 
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td> 
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td> 
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td> 
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td> 
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td> 
 </tr>
 
 <tr>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td> 
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
 
 
 </tbody> 
 </table> 

  

## bluemix help
{: #bluemix_help}
Display the general help for first-level built-in commands and supported namespaces of {{site.data.keyword.Bluemix_notm}} CLI, or the help for a specific built-in command or namespace.

```
bluemix help [COMMAND|NAMESPACE]
```

**Prerequisites**: None

**Command options**:

*COMMAND*|*NAMESPACE* (optional): The command or namespace that help is displayed for. If not specified, the general help for {{site.data.keyword.Bluemix_notm}} CLI is shown.

**Examples**:

Display general help for {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix help
```

Display help for the `info` command:

```
bluemix help info
```

Display help for the `ic` namespace:

```
bluemix help ic
```

or 

```
bluemix ic help
```

Display help for the `group-create` command under the `ic` namespace:

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
Set or view the {{site.data.keyword.Bluemix_notm}} API endpoint. This command wraps the `cf api` command.

```
bluemix api [API_ENDPOINT] [--unset]
```

**Prerequisites**: None

**Command options**:

*API_ENDPOINT* (optional): The API endpoint that is targeted, for example, https://api.ng.bluemix.net. If both *API_ENDPOINT* and `--unset` options are not specified, the current API endpoint is displayed.

`--unset` (optional): Remove the API endpoint setting.

**Examples**:

Set the API endpoint to api.ng.bluemix.net:

```
bluemix api api.ng.bluemix.net
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

Log in user. This command wraps the `cf login` command. Command options are the same as `cf login` command options.

```
bluemix login [OPTIONS...]
```

**Prerequisites**: Endpoint

**Command options**:
For information about options supported by the `login` command, see `cf login` command usage information for cf commands for managing applications.


## bluemix logout
{: #bluemix_logout}

Log out user. This command wraps the `cf logout` command.

```
bluemix logout
```

**Prerequisites**:  None


## bluemix target
{: #bluemix_target}


Set or view the target org or space. This command wraps the `cf target` command.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**Prerequisites**:  Endpoint, Login

**Command options**:

-o *ORG_NAME* (optional):  The name of the organization to be targeted.

-s *SPACE_NAME* (optional):  The name of the space to be targeted.

If neither -o *ORG_NAME* or -s *SPACE_NAME* are specified, the current org and space are displayed.

**Examples**:

Set the current org to `MyOrg` and space to `MySpace`:

```
bluemix target -o MyOrg -s MySpace
```

View the current org and space:

```
bluemix target
```


## bluemix info
{: #bluemix_info}

View the basic {{site.data.keyword.Bluemix_notm}} information, including the current region, the cloud controller version, and some useful endpoints, such as endpoints for login and exchanging access token.

```
bluemix info
```

**Prerequisites**:  Endpoint


## bluemix config
{: #bluemix_config}


Write default values to the configuration file.

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**Prerequisites**:  None

**Command options**:

--http-timeout *TIMEOUT_IN_SECONDS*:  The timeout value for HTTP requests. The default value is 60 seconds.

--trace true|false|*path/to/file*:  Trace HTTP requests to the terminal or specified file.

--color true|false:  Enable or disable color output. Color output is enabled by default.

--locale *LOCALE*:  Set a default locale. If LOCALE is *CLEAR*, previous locale is deleted.

Only one of these options can be specified at a time.

**Examples**:

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


## bluemix list
{: #bluemix_list}

List all cf applications, containers, container groups, and VM groups in the current space.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

apps (optional):  Display only the applications information.

containers (optional):  Display only the containers information.

container-groups (optional):  Display only the container groups information.

vm-groups (optional):  Display only the VM groups information.

Only one of `apps`, `containers`, `container-groups`, or `vm-groups` can be specified at a time. If none of them is specified, all the cf apps, containers, container groups, and VM groups are listed.

**Examples**:

List all cf applications:

```
bluemix list apps
```

List all container instances:

```
bluemix list containers
```

List all apps, containers, container groups, and VM groups:

```
bluemix list
```


## bluemix scale
{: #bluemix_scale}

Scale in or scale out the cf application or container group to a specified instance count, disk quota, and memory size.

**Note:** Only an instance number can be specified for scaling a container group. If no option is specified, this command lists the current instance count for the container group, and also disk quota and memory size for the cf application.

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT] [-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (required):  The name of the cf application or container group to be scaled.

-i *INSTANCE_COUNT*  (optional):  The new instance number for the cf application or container group to be scaled. This option is the only valid option for container group to be scaled.

-k *DISK_QUOTA* (optional):  The new disk quota of the cf application. Not valid for scaling a container group.

-m *MEMORY_SIZE* (optional):  The new memory size for the cf application. Not valid for scaling a container group.

**Examples**:

Display the current instance number for `my-container-group`:

```
bluemix scale my-container-group
```

Scale `my-container-group` to 2 instances:

```
bluemix scale my-container-group -i 2
```

Scale `my-java-app` to 3 instances, 8G disk quota, and 1024M memory size:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
{: #bluemix_curl}

Execute a raw HTTP request to {{site.data.keyword.Bluemix_notm}}. *Content-Type* is set to *application/json* by default. This command sends the request to {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. For supported paths, refer to the API path definitions in the [CloudFoundry API document](http://apidocs.cloudfoundry.org/){: new_window}.

```
bluemix curl PATH [OPTIONS...]
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*PATH*  (required):  The URL path of the resource. For example, /v2/apps.

*OPTIONS*  (optional):  The options that are supported by the `bluemix curl` command are the same as those for the `cf curl` command.

**Examples**:

View the information for all organizations of the current account:

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

List all organizations

```
bluemix iam orgs [-r REGION --guid]
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*-r REGION*  (optional): For which region the organization information is shown. If set to 'all', all organizations in all regions are listed.

*--guid* (optional): Display the GUID of the organizations.

**Examples**:
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

**Prerequisites**:  Endpoint, Login

**Command options**:

*ORG_NAME* (required): The name of the organization.

*--guid* (optional): Display the GUID of the organization.


**Examples**:
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

**Prerequisites**:  Endpoint, Login

**Command options**:

*ORG_NAME* (required): The name of the organization being created.

**Examples**:
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

**Prerequisites**:  Endpoint, Login

**Command options**:

*ORG_NAME* (required):  The name of the existing org that is to be replicated.

*REGION_NAME*  (required):  The name of the region that hosts the replicated org.

**Examples**:

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

**Prerequisites**:  Endpoint, Login

**Command options**:

*OLD_ORG_NAME* (required):  The old name of the org that is to be renamed.

*NEW_ORG_NAME*  (required):  The new name of the org that it is renamed to.


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Delete the specified organization in current region.

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*ORG_NAME* (required):  The name of the existing org that is to be deleted.

*-f* (optional): Force deletion without confirmation.

*--all* (optional): Delete the organization from all regions.


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


## bluemix iam account-users
{: #bluemix_iam_account_users}

Displays users associated with the account. This operation can be performed only by the account owner.

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


Invites a user to the account with an organization and space role already set. This operation can be performed only by the account owner.

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**Prerequisites**:  Endpoint, Login


**Command options**:

*USER_NAME* (required): The name of the user being invited.

*ORG_NAME* (required): The name of the organization this user is invited to.

*ORG_ROLE* (required): The name of the organization role this user is invited to. For example:

<dl>
<dt>OrgManager</dt>
<dd>This role can invite and manage users, select and change plans, and set spending limits.</dd>
<dt>BillingManager</dt>
<dd>This role can create and manage the billing account and payment information.</dd>
<dt>OrgAuditor</dt>
<dd>This role has read-only access to org information and reports.</dd>
</dl> 

*SPACE_NAME* (required): The name of the space this user is invited to.

*SPACE_ROLE* (required): The name of the space role this user is invited to. For example:

<dl>
<dt>SpaceManager</dt>
<dd>This role can invite and manage users, and enable features for a given space.</dd>
<dt>SpaceDeveloper</dt>
<dd>This role can create and manage apps and services, and see logs and reports.</dd>
<dt>SpaceAuditor</dt>
<dd>This role can view logs, reports, and settings for the space.</dd>
</dl> 

**Examples**:

Invite user `Mary` to the organization `IBM` as `OrgManager` role and the space `Cloud` as `SpaceAuditor` role:

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

Display users in the specified organization by role.

```
bluemix iam org-users ORG_NAME [-a]
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*ORG_NAME* (required): The name of the organization.

*-a* (optional): List all the users in the specified organization, not grouped by role.


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Assign an organization role to a user. This operation can be performed only by an organization manager.

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*USER_NAME* (required): The name of the user being assigned.

*ORG_NAME* (required): The name of the organization this user is assigned to.

*ORG_ROLE* (required): The name of the organization role this user is assigned to. For example:

<dl>
<dt>OrgManager</dt>
<dd>This role can invite and manage users, select and change plans, and set spending limits.</dd>
<dt>BillingManager</dt>
<dd>This role can create and manage the billing account and payment information.</dd>
<dt>OrgAuditor</dt>
<dd>This role has read-only access to org information and reports.</dd>
</dl> 

**Examples**:

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

**Prerequisites**:  Endpoint, Login

**Command options**:

*USER_NAME* (required): The name of the user being removed.

*ORG_NAME* (required): The name of the organization this user is removed from.

*ORG_ROLE* (required): The name of the organization role this user is removed from. For example:

<dl>
<dt>OrgManager</dt>
<dd>This role can invite and manage users, select and change plans, and set spending limits.</dd>
<dt>BillingManager</dt>
<dd>This role can create and manage the billing account and payment information.</dd>
<dt>OrgAuditor</dt>
<dd>This role has read-only access to org information and reports.</dd>
</dl> 

**Examples**:

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

**Prerequisites**:  Endpoint, Login

**Command options**:

*ORG_NAME* (required): The name of the organization

*SPACE_NAME* (required): The name of the space.


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Assign a space role to a user. This operation can be performed only by a space manager.

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*USER_NAME* (required): The name of the user being assigned.

*ORG_NAME* (required): The name of the organization this user is assigned to.

*SPACE_NAME* (required): The name of the space this user is assigned to.

*SPACE_ROLE* (required): The name of the space role this user is assigned to. For example:

<dl>
<dt>SpaceManager</dt>
<dd>This role can invite and manage users, and enable features for a given space.</dd>
<dt>SpaceDeveloper</dt>
<dd>This role can create and manage apps and services, and see logs and reports.</dd>
<dt>SpaceAuditor</dt>
<dd>This role can view logs, reports, and settings for the space.</dd>
</dl> 


**Examples**:

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

**Prerequisites**:  Endpoint, Login

**Command options**:

*USER_NAME* (required): The name of the user being removed.

*ORG_NAME* (required): The name of the organization this user is removed from.

*SPACE_NAME* (required): The name of the space this user is removed from.

*SPACE_ROLE* (required): The name of the space role this user is removed from. For example:

<dl>
<dt>SpaceManager</dt>
<dd>This role can invite and manage users, and enable features for a given space.</dd>
<dt>SpaceDeveloper</dt>
<dd>This role can create and manage apps and services, and see logs and reports.</dd>
<dt>SpaceAuditor</dt>
<dd>This role can view logs, reports, and settings for the space.</dd>
</dl> 

**Examples**:

Remove user `Mary` from the organization `IBM` and space `Cloud` as `SpaceManager` role:

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

This command has the same function and options as the `cf push` command.


## bluemix app list
{: #bluemix_app_list}

This command has the same function and options as the `cf apps` command.


## bluemix app show
{: #bluemix_app_show}

This command has the same function and options as the `cf app` command.


## bluemix app scale
{: #bluemix_app_scale}

This command has the same function and options as the `cf scale` command.


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


## bluemix app stack
{: #bluemix_app_stack}

This command has the same function and options as the `cf stack` command.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

This command has the same function and options as the `cf create-app-manifest` command.


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

**Prerequisites**:  Endpoint, Login

**Command options**:

-d (optional):  If the `-d` option is specified, the description of each template is also displayed. Otherwise, only the ID and name of each template is shown.


## bluemix catalog template
{: #bluemix_catalog_template}

View the detailed information of a specified boilerplate template.

```
bluemix catalog template TEMPLATE_ID
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*TEMPLATE_ID*  (required):  The ID of the boilerplate template. Use 'bluemix templates' to view all templates' IDs.

**Examples**:

View details of the template `mobileBackendStarter`:

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

Create a cf application that is based on the specified template with the specified URL and description. By default, the new app is started automatically.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*TEMPLATE_ID* (required):  The template that the application will be based on when it is created. Use `bluemix templates` to see all templates' ID.

*CF_APP_NAME*  (required):  The name of the cf application to be created.

-u *URL*  (optional):  The route of the application. If not specified, the route is set by {{site.data.keyword.Bluemix_notm}} automatically based on your app name and default domain.

-d *DESCRIPTION*  (optional):  Description of the application.

--no-start  (optional):  Do not start the application automatically after it is created. If not specified, the application is started automatically after it is created.

**Examples**:

Create a cf application `my-app` based on `javaHelloWorld` template:

```
bluemix catalog template-run javaHelloWorld my-app
```

Create an application `my-ruby-app` based on `rubyHelloWorld` template with route `myrubyapp.ng.bluemix.net` and description `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Create an application `my-python-app` based on `pythonHelloWorld` template without automatic start:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
{: #bluemix_network_regions}

View the information for all regions on {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

**Prerequisites**:  Endpoint


## bluemix network region-set
{: #bluemix_network_region_set}

Switch to the region that is specified. This command automatically retargets to the same org and space in the new region, if possible. Otherwise, the command prompts the user to select a new org and space if the user is already logged in. The API endpoint is changed accordingly.

```
bluemix network region-set REGION_NAME
```

**Prerequisites**:  Endpoint

**Command options**:

*REGION_NAME* (required):  The name of the region that you want to switch to. You can use the `bluemix network regions` command to see all region names.

**Examples**:

Set the current region to `eu-gb`:

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

This command has the same function and options as the `cf routes` command.


## bluemix network route-check
{: #bluemix_network_route_check}

This command has the same function and options as the `cf check-route` command.


## bluemix network route-map
{: #bluemix_network_route_map}

Map a route to an existing cf application or container group that has the specified domain and host name.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (required):  The name of the cf application or container group to be mapped with a route.

*DOMAIN*  (required):  The domain of the route. For example, mybluemix.net or ng.bluemix.net. 

-n *HOST_NAME* (optional):  The host name of the route. If not provided, the host name is set to the app name or container group name by default.

**Examples**:

Map a route to `my-app` with specified domain:

```
bluemix network route-map my-app mybluemix.net
```

Map a route to 'my-container-group' with specified domain and host name:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
{: #bluemix_network_route_unmap}

Unmap the specified route from an existing cf application or container group.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (required):  The name of the cf application or container group.

*DOMAIN*  (required):  The domain of the route (for example, mybluemix.net or ng.bluemix.net). 

-n *HOST_NAME* (optional):  The host name of the route. If not provided, the host name is set to app name or container group name by default.

**Examples**:

Unmap `my-app.mybluemix.net` from `my-app`:

```
bluemix network route-unmap my-app mybluemix.net
```

Unmap `abc.ng.bluexmix.net` from `my-container-group`:

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
{: #bluemix_network_route_create}

This command has the same function and options as the `cf create-route` command.


## bluemix network route-delete
{: #bluemix_network_route_delete}

This command has the same function and options as the `cf delete-route` command.


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

This command has the same function and options as the `cf delete-orphaned-routes` command.


## bluemix network domains
{: #bluemix_network_domains}

This command has the same function and options as the `cf domains` command.


## bluemix network domain-create
{: #bluemix_network_domain_create}

This command has the same function and options as the `cf create-domain` command.


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

This command has the same function and options as the `cf delete-domain` command.


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

This command has the same function and options as the `cf create-shared-domain` command.


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

This command has the same function and options as the `cf delete-shared-domain` command.


## bluemix security cert
{: #bluemix_security_cert}

List the certificate information of a domain.

```
bluemix security cert DOMAIN_NAME
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*DOMAIN_NAME* (required):  The domain that hosts the certificate.

**Examples**:

View the certificate information of the domain `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

Add a certificate to the specified domain in the current org.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*DOMAIN* (required):  The domain that the certificate is added to.

-k *PRIVATE_KEY_FILE* (required):  The private key file path.

-c *CERT_FILE* (required):  The certificate file path.

-p *PASSWORD* (optional):  The password for the certificate.

-i *INTERMEDIATE_CERT_FILE* (optional):  The intermediate certificate file path.

--verify-client (optional):  Whether to enable the client certificate verification.

**Examples**:

Add a certificate to the domain `ibmcxo-eventconnect.com`:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
{: #bluemix_security_cert_remove}

Remove a certificate from the specified domain in current org.

```
bluemix security cert-remove DOMAIN [-f]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*DOMAIN* (required):  Domain to remove the certificate from.

-f  (optional):  Force deletion without confirmation.







## bluemix plugin repos
{: #bluemix_plugin_repos}

List all plugin repositories that are registered in {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repos
```

**Prerequisites**:  None


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

Add a new plugin repository to {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**Prerequisites**:  None

**Command options**:

*REPO_NAME* (required):  The name of the repository to be added. You can define your own name for each repository.

*REPO_URL* (required):  The URL of the repository to be added. The repository URL must contain the protocol (for example, http://plugins.ng.bluemix.net instead of plugins.ng.bluemix.net). http://plugins.ng.bluemix.net is the official plugin repository of {{site.data.keyword.Bluemix_notm}} CLI.

**Examples**:

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

**Prerequisites**:  None

**Command options**:

*REPO_NAME* (required):  The name of the repository to be removed.

**Examples**:

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

**Prerequisites**:  None

**Command options**:

-r *REPO_NAME* (optional):  List only the plugins in specified repository.

**Examples**:

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

**Prerequisites**:  None


## bluemix plugin install
{: #bluemix_plugin_install}

Install the specific version of plugin to {{site.data.keyword.Bluemix_notm}} CLI from the specified path or repository.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

**Prerequisites**:  None

**Command options**:

*PLUGIN_PATH*|*PLUGIN_NAME* (required):  If `-r *REPO_NAME*` is not specified, plugin is installed from the specified local path or remote URL.

-r *REPO_NAME*  (optional):  The name of the repository where the plugin binary is located.
-v *VERSION*  (optional):  The version of the plugin to be installed. If not provided, the latest version of the plugin is installed. This option is valid only when you install the plugin from the repository.

**Examples**:

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






## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

Uninstall the specified plugin from {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin uninstall PLUGIN_NAME
```

**Prerequisites**:  None

**Command options**:

*PLUGIN_NAME* (required):  The name of the plugin to be uninstalled.

**Examples**:

Uninstall the `IBM-Containers` plugin that was previously installed:

```
bluemix plugin uninstall IBM-Containers
```


## bluemix ic init
{: #bluemix_ic_init}

Initialize the containers environment on your local machine to use the full capabilities of the IBM Containers service.

```
bluemix ic init
```

**Prerequisites**:  Endpoint, Login, Target

**Note:** Before initialization, ensure that the Docker CLI (docker) is installed and configured in your PATH environment variable. To switch to another region, use the `bluemix region-set` command. 

**Examples**:

Switch to the `us-south` region:

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

Control a running container or view its output. Use `CTRL+C` to exit and stop the container. This command calls the Docker CLI. For more information, see the [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} command in the Docker help. 

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

--no-stdin  (optional):  Do not include the standard input.

--sig-proxy  (optional):  Proxy all received signals to the process. The default is **true**.

*CONTAINER*  (required):  The container name or ID.

**Examples**:

The following example shows a request to attach to the container `my_container`:
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

Call the IBM Containers build service to build a Docker image locally or in your private {{site.data.keyword.Bluemix_notm}} repository. This command calls the Docker CLI. For more information, see the [build](https://docs.docker.com/reference/commandline/build/){: new_window} command in the Docker help. 

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

-t *TAG*|--tag *TAG*  (required):  The repository name to apply to the image that is created.

--no-cache  (optional):  Do not use the cache when the image is built. The default is **false**.

-p|--pull  (optional):  Attempt to pull the base image from the registry even if it is cached.

-q|--quiet  (optional):  Suppress the verbose output that is generated by the containers. The default is **false**.

*DOCKERFILE_LOCATION*  (required):  The path to the Dockerfile and context on the local host.

**Examples**:

The following example shows a request to build an image that is named *myimage*. The Dockerfile and other artifacts to be used in the build are in the same directory that the command is running from. Because the registry and namespace are included with the image name, the image is built in your organization's private {{site.data.keyword.Bluemix_notm}} repository.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic create
{: #bluemix_ic_create}

Create a new container in your {{site.data.keyword.Bluemix_notm}} repository. This command wraps the `docker create` command. For more information, see the [create](https://docs.docker.com/reference/commandline/create/){: new_window} command in the Docker help.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Access a Docker Hub image or an image from your local registry and copy the image to your private {{site.data.keyword.Bluemix_notm}} repository.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*SOURCE_IMAGE*  (required):  The source repository and image name.

*DESTINATION_IMAGE*  (required):  The private {{site.data.keyword.Bluemix_notm}} repository URL, which includes the namespace and the destination image name. A tag for the image is optional.

**Examples**:

Copy an image from the source repository to your private repository and add a tag for the image:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copy the `sinatra` image from the `training` repository to your private repository `registry.ng.bluemix.net/mynamespace` and name the image as `mysinatra`. Add a tag `v1` for the image `mysinatra`. 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


Execute a command within a container. For more information, see the [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} command in the Docker help.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

-d|--detach  (optional):  Run the specified command in the background.

-it  (optional):  Interactive mode. Keep the standard input displaying. Type `exit` to exit.

-u *USER*|--user *USER*  (optional):  The user name.

*CONTAINER*  (required):  The container name or ID.

*CMD*  (optional):  The command to execute within the container or containers specified.

**Examples**:

Execute the `bash` command within the `my_container` container in the interactive mode:

```
bluemix ic exec -it my_container bash
```

Execute the `date` command within the `my_container` container:

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

List container groups in the private {{site.data.keyword.Bluemix_notm}} repository of the organization.

```
bluemix ic groups
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

View detailed information, such as environment variables, ports, or memory, that is specified for a container group when it is created.

```
bluemix ic group-inspect CONTAINER_GROUP
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CONTAINER_GROUP*  (required):  The container group ID or name.

**Examples**:

The following example shows a request to inspect the container group `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

List instances of a specified container group.

```
bluemix ic group-instances CONTAINER_GROUP
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CONTAINER_GROUP*  (required):  The container group ID or name.

**Examples**:

List all instances of the container group `my_group`:
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Create a scalable container group.

```
bluemix ic group-create [-p PORT|--publish port] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] [--min MIN] [--max MAX] [--desired DESIRED] [--auto] [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] [--name NAME] IMAGE [CMD]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

-m *MEMORY*|--memory *MEMORY*  (optional):  Assign a memory limit to the group in MB. When you create a container group from the CLI, the default value for each container instance is `64` MB. When you create a container group from the {{site.data.keyword.Bluemix_notm}} Dashboard, the default value for each container instance is `256` MB. Accepted values are `64`, `256`, `512`, `1024` and `2048`. After a memory limit is assigned, the value can't be changed.

-e *ENV*|--env *ENV*  (optional):  Set the environment variable, where **ENV** is a `key=value` pair. List multiple keys separately. If quotation marks are included, include them around both the environment variable name and the value. For example: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  The following table shows some commonly used environment variables that you can specify:

|  Environment variable                              |     Description                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Bind a service to a container. Use the `CCS_BIND_APP` environment variable to bind an app to the container. The app is bound to the target service and acts as a bridge that allows {{site.data.keyword.Bluemix_notm}} to bring your bridge app’s `VCAP_SERVICES` information to the running container instance. For more information about creating a bridge app, see [Binding a service to a container](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | Add an SSH key to a container when you create the container. You can add the SSH key by using the environment variable when you create the container from the {{site.data.keyword.Bluemix_notm}} dashboard or from the CLI. For more information about SSH keys, see [Logging in to a container](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Add a log file to be monitored in the container. Include the `LOG_LOCATIONS` environment variable with a path to the log file. |
*Table 1. Commonly used environment variables*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  (optional):  Attach a volume to a container by specifying the details in the format `VolumeId:ContainerPath[:ro]`.

- *VOLUME*: The volume ID or name.
- *CONTAINER_PATH*: The absolute path to the volume in the container.
- ro: Optional. Specifying `ro` makes the volume read-only instead of the default read/write.

-p *PORT*|--publish *PORT*  (optional):  Expose the port for the HTTP traffic. Containers in your group must listen to the HTTP port. HTTPS requests can't be made. For container groups, you can't include multiple ports.

When you specify a port, you make the app available to the {{site.data.keyword.Bluemix_notm}} Load Balancer or containers that are trying to reach the host in the same {{site.data.keyword.Bluemix_notm}} space. Then the {{site.data.keyword.Bluemix_notm}} load balancer or containers can use the port to reach the host and the app in the same {{site.data.keyword.Bluemix_notm}} space. If a port is specified in the Dockerfile for the image that you are using, include that port.

**Tip:**

- For the IBM certified Liberty Server image or a modified version of this image, enter port 9080.
- For the IBM certified Node.js image or a modified version of this image, enter port 8000.

--min *MIN*  (optional):  The minimum number of instances. The default is **1**. If you set a minimum number of instances, the value can't be changed after the container group is created.

--max *MAX*  (optional):  The maximum number of instances. The default is **2**. If you set a maximum number of instances, the value can't be changed after the container group is created.

--desired *DESIRED*  (optional):  The number of instances that you require. The default is **2**.

--auto  (optional):  When the container group is created and the automatic recovery is enabled, IBM Containers check the health of each instance with an HTTP request to the port that is assigned.

If no response is received from a container instance in 2 subsequent 90 second intervals, the instance is removed and replaced with a new instance. No action is taken if the container is responsive. This process is repeated continuously. During a 30 minute window, if the total number of different containers that are members of the group equals or exceeds 3 times the maximum observed size of the group, the automatic recovery is disabled permanently for the container group. To enable automatic recovery again, you must re-create the container group.

-n *HOST*|--hostname *HOST*  (optional):  The host name, such as `mycontainerhost`. The host and the domain combine to form the full public route URL, such as `http://mycontainerhost.mybluemix.net`. When you review the details of a container group with the `bluemix ic group-inspect` command, the host and the domain are listed together as the route.

-d *DOMAIN*|--domain *DOMAIN*  (optional):  Usually, the domain is `.mybluemix.net`. The host and the domain are combined to form the full public route URL, such as `http://mycontainerhost.mybluemix.net`. When you review the details of a container group with the `bluemix ic group-inspect` command, the host and the domain are listed together as the route.

--name *NAME*  (required):  Assign a name to the group. `-n` is deprecated.

**Tip:** The container name must start with a letter. The name can include uppercase letters, lowercase letters, numbers, periods `.`, underscores `_`, or hyphens `-`.

*IMAGE*  (required):  The image to be included in each container instance in the container group. You can list commands after the image, but do not put any options after the image. Include all options before you specify an image.

If you use an image in your organization's private {{site.data.keyword.Bluemix_notm}} repository, specify the image in the format: `registry.ng.bluemix.net/NAMESPACE/IMAGE`.

If you use an image that is provided by IBM Containers, do not include your organization's namespace. Specify the image in the format: `registry.ng.bluemix.net/IMAGE`.

*CMD*  (optional):  The command and arguments that are passed to the container group to execute. This command must be a long-running command. Do not use a short-lived command that does not run for very long, for example, **/bin/date**, because the short-lived command might cause the container to crash.

**Note:**
- The command and its arguments must come at the end of the `bluemix ic run` command line.
- If the command arguments include the hyphen `-`, as in `-c` in the previous example command, the command must be preceded by two hyphens, `--`.



**Examples**:

Create a container group `my_container_group` by using the `registry.ng.bluemix.net/ibmnode` image that is provided by IBM Containers, and then run the `ping localhost` long-running command on that container group:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Create a container group `my_container_group` by using the `registry.ng.bluemix.net/ibmnode` image that is provided by IBM Containers, and then run the `tail -f /dev/null` long-running command on that container group:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Create a scalable group `mygroup` with the automatic recovery enabled by using the `registry.ng.bluemix.net/ibmliberty` image. The port is `9080`, the host name is `mycontainerhost`, the domain name is `.mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Update a container group.


```
bluemix ic group-update [--min MIN] [--max MAX] [--desired DESIRED] [--auto] CONTAINER_GROUP
```

**Tip:** To update the host name or domain for a container group, use `bluemix ic route-map [-n HOST] [-d DOMAIN] CONTAINER_GROUP`.

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

--min *MIN*  (optional):  The minimum number of instances. The default is **1**. After a minimum number of instances is set, the value can't be changed.

--max *MAX*  (optional):  The maximum number of instances. The default is **2**. After a maximum number of instances is set, the value can't be changed .

--desired *DESIRED*  (optional):  The number of instances that you require. The default is **2**.

**Tip:** Only one of `--min MIN`, `--max MAX`, or `--desired DESIRED` option can be specified at a time.

--auto  (optional):  Automatically restart failed instances by enabling auto-recovery.

*CONTAINER_GROUP*  (required):  The container group ID or name.

**Examples**:

The following example shows a request to update the container group `my_group`:
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Remove a container group from the organization's private {{site.data.keyword.Bluemix_notm}} repository.

```
bluemix ic group-remove [-f|--force] CONTAINER_GROUP
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

-f|--force  (optional):  Forces the removal of a running or failed container.

*CONTAINER_GROUP*  (required):  The container group ID or name.

**Examples**:

The following example shows a request to remove a container group, where `my_group` is the name of the container group.
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

View a list of all available images in the organization's private {{site.data.keyword.Bluemix_notm}} repository. For more information, see the [images](https://docs.docker.com/reference/commandline/images){: new_window} command in the Docker help. The list includes the image ID, the created date, and the image name.

```
bluemix ic images [-a|--all] [--no-trunc] [-q|--quiet]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

-a|--all  (optional):  Include all of the image layers for each image in your organization's repository, not only the most recent layer.

--no-trunc  (optional):  Do not truncate the output.

-q|--quiet  (optional):  Display only the numeric IDs.

**Examples**:

The following example shows a request to receive a list of available images for the organization:
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

View the information about a container. For more information, see the [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} command in the Docker help.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*IMAGE*  (required):  View detailed information about a specific image by specifying the image name or ID.

images  (required):  View detailed information about all of the images in your repository.

*CONTAINER*  (required):  View detailed information about a specific container by specifying the container name or ID.

**Tip:** Only one of *IMAGE*, images, or *CONTAINER* can be specified at a time. 

**Examples**:

The following example shows a request to inspect a container that is named `proxy`: 
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

View a set of information that describes the state of the container cloud service instance. The information includes the containers limit, containers usage, containers that are running, memory limit, memory usage, floating IP address limit, floating IP address usage, CCS host URL, registry host URL, and debug mode status.

```
bluemix ic info
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix ic ips
{: #bluemix_ic_ips}

List the available floating IP addresses for the user that is logged. The list includes IP addresses and the container ID that the IP addresses are linked to. If the IP address is unused, no container ID will be shown.

```
bluemix ic ips [-a|--all]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

-a|--all  (optional):  List all IP addresses. By default, only available IP addresses are returned.

**Examples**:

The following example shows a request to receive a list of all IP addresses for the organization, whether they are available to use or not.
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
Request a new floating IP address.

```
bluemix ic ip-request
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Release a floating IP address from the container cloud service instance.

```
bluemix ic ip-release IP_ADDRESS
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*IP_ADDRESS*  (required):  The IP address to release.


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Bind an available floating IP address to a container.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*IP_ADDRESS*  (required):  The IP address to be bound.

*CONTAINER*  (required):  The container ID or name to be bound.

**Examples**:

The following example shows a request to bind the IP address `192.123.12.12 to` the container `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Unbind a floating IP address from its container.

Public IP addresses are a limited resource in IBM Containers. Therefore, public IP addresses that are allocated to a space and not bound to a container are periodically reclaimed from free trial users, approximately on a weekly basis. Unbound public IP addresses are never reclaimed from pay as you go or subscription customers.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*IP_ADDRESS*  (required):  The IP address to be unbound.

*CONTAINER*  (required):  The container ID or name to be unbound.

**Examples**:

The following example shows a request to unbind the IP address `192.123.12.12` from the container `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

Stop a running process in a container without stopping the container. For more information, see the [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} command in the Docker help.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

-s *CMD*|--signal *CMD*  (optional):  Send a command to the process that is running in the container.

*CONTAINER*  (required):  The container ID or name.

**Examples**:

The following example shows a request to kill the process in a container that is named `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

View the name of the private {{site.data.keyword.Bluemix_notm}} image repository for the organization that you log in to.

```
bluemix ic namespace-get
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Set the name of the private {{site.data.keyword.Bluemix_notm}} image repository the organization that you log in to.

*Restriction*: You can't use a hyphen `-` in the name of your repository namespace.

```
bluemix ic namespace-set NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*NAME*  (required):  A one-time only function to set the repository namespace for your organization, if it is not already set. After you set the namespace, reinitialize IBM Containers through `bluemix ic init` command before you continue.


## bluemix ic pause
{: #pause}

Pause all processes within a running container. For more information, see the [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} command in the Docker help. To stop a container, see the [bluemix ic unpause](#unpause) command.

```
bluemix ic pause CONTAINER
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*CONTAINER*  (required):  The container name or ID.

**Responses**:

- Paused container successfully.

- Command failed with container cloud service

 `{message}`
  
 Where `{message}` is the related error.
 
- Command failed - Could not connect to container cloud service

**Examples**:

The following example shows a request to pause a container that is named `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

Unpause all processes within a running container. For more information, see the [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} command in the Docker help. To pause a container, see the [bluemix ic pause](#pause) command.

```
bluemix ic unpause CONTAINER
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*CONTAINER*  (required):  The container name or ID.

**Responses**:

- Unpaused container successfully.

- Command failed with container cloud service 

 `{message}` 
 
 Where `{message}` is the related error.
 
- Command failed - Could not connect to container cloud service

**Examples**:

The following example shows a request to unpause a container that is named `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

List port mappings or a specific mapping for the container. This command wraps the `docker port` command. For more information, see the [port](https://docs.docker.com/reference/commandline/port/){: new_window} command in the Docker help.


## bluemix ic ps
{: #bluemix_ic_ps}
View a list of containers that are running in the logged-in user's namespace. By default, this command shows only containers that are running. For more information, see the [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} command in the Docker help.

```
bluemix ic ps [-a|--all] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

-a|--all  (optional):  Show all containers, both running and stopped.

-s|--size  (optional):  List the sizes of the containers.

-l *NUM*|--limit *NUM*  (optional):  List the most recently created containers, where *NUM* is the number of the most recently created containers that you want to return.

For example, if you created containers `node1` through `node5` sequentially, the command `bluemix ic ps --limit 2` returns node4 and node5 because they are the last two containers that are created.

-q|--quiet  (optional):  Display only container IDs.

**Examples**:

The following example shows a request to see all running and stopped containers:
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

Restart a container. For more information, see the [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} command in the Docker help.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*CONTAINER*  (required):  The container name or ID.

-t *SECS*|--time *SECS*  (optional):  The number of seconds to wait before the container is restarted.

**Responses**:

- Restarted container successfully.

- Command failed with container cloud service 

 `{message}` 
 
 Where `{message}` is the related error.
 
- Command failed - Could not connect to container cloud service

**Examples**:

The following example shows a request to restart a container that is named `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Remove a container. For more information, see the [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} command in the Docker help.

```
bluemix ic rm [-f|--force] CONTAINER
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

-f|--force  (optional):  Forces the removal of a running or failed container.

*CONTAINER*  (required):  The container name or ID.

**Responses**:

- Removed container successfully.

- Command failed with container cloud service 

 `{message}` 
 
 Where `{message}` is the related error.
 
- Command failed - Could not connect to container cloud service.

**Examples**:

The following example shows a request to remove a container that is named `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Remove an image from the logged-in user's namespace. For more information, see the [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} command in the Docker help.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

-R *REGISTRY*|--registry *REGISTRY*  (optional):  Change the registry host. The default is to use the registry that you specify in the `bluemix ic init` command.

*IMAGE*  (required):  The name of the image that you want to remove. If a tag is not specified in the image name, the image tagged `latest` is deleted by default.

**Responses**:

- Removed: `{IMAGE}`

 Where `{IMAGE}` is the name of the image that was removed.
 
- Error! No registry host specified.

- Image remove failed - Could not connect to container cloud registry

- Command failed with container cloud service 

 `{message}`
 
 Where `{message}` is the related error.

**Examples**:

The following example shows a request to remove the image `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

Start a new container in the container cloud service from an image name. For more information, see the [run](https://docs.docker.com/reference/commandline/run/){: new_window} command in the Docker help.



```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Note:** Ensure that the Cloud Foundry command tool is installed and that you have a Cloud Foundry token. Successful login by using `bluemix login` and `bluemix ic init` generates the required token and certificates. 


**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

-p *PORT*|--publish *PORT*  (optional):  Expose the port for the HTTP traffic. Include any ports that are specified in the Dockerfile for the image that you are using. You can include multiple ports with multiple `-p` options. Exposing a port will automatically bind a public IP address to the container if a public IP address is available.

If you have an existing IP address in the space that you want to bind to the container, you can specify the IP address rather than bind it later. The IP address must be specified in the  format: *&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt;*

For more information about requesting IP addresses for a space, see [bluemix ic ip-request](#ip_request) command.

When you specify a port, you are making the app available to the {{site.data.keyword.Bluemix_notm}} Load Balancer or containers in the same {{site.data.keyword.Bluemix_notm}} space that are trying to reach the host. If a port is specified in the Dockerfile for the image that you are using, include that port.

**Tip:**

- For the IBM certified Liberty Server image or a modified version of this image, enter port 9080.
- For the IBM certified Node.js image or a modified version of this image, enter port 8000.

-P  (optional):  Automatically expose the ports that are specified in the image's Dockerfile for the HTTP traffic.

-m *MEMORY*|--memory *MEMORY*  (optional):  Assign a memory limit to the group in MB. When you create a container group from the CLI, the default value for each container instance is `64` MB.  When you create a container group from the {{site.data.keyword.Bluemix_notm}} Dashboard, the default value for each instance is `256` MB. Accepted values are `64`, `256`, `512`, `1024` and `2048`. After a memory limit is assigned, the value can't be changed.

-e *ENV*|--env *ENV*  (optional):  Set the environment variable, where **ENV** is a `key=value` pair. List multiple keys separately. If you include quotation marks, include them around both the environment variable name and the value. For example: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`. The following table shows some commonly used environment variables that you can specify:

|      Environment variable                          |   Description                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Bind a service to a container. Use the `CCS_BIND_APP` environment variable to bind an app to the container. The app is bound to the target service and acts as a bridge that allows {{site.data.keyword.Bluemix_notm}} to bring your bridge app’s `VCAP_SERVICES` information into the running container instance. For more information about creating a bridge app, see [Binding a service to a container](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | Add an SSH key to a container when you create the container. You can add the SSH key by using the environment variable when you create a container from the {{site.data.keyword.Bluemix_notm}} dashboard or from the CLI. For more information about SSH keys, see [Logging in to a container](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Add a log file to be monitored in the container. Include the `LOG_LOCATIONS` environment variable with a path to the log file. |
*Table 2. Commonly used environment variables*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  (optional):  Attach a volume to a container by specifying the details in the following format `VolumeId:ContainerPath[:ro]`.

- *VOLUME*: The volume ID or name.
- *CONTAINER_PATH*: The absolute path to the volume in the container.
- ro: Optional. Specifying `ro` makes the volume read-only instead of the default read/write.

-n *NAME*|--name *NAME*  (required):  Assign a name to the container.

*Tip:* The container name must start with a letter. The name can include uppercase letters, lowercase letters, numbers, periods `.`, underscores `_`, or hyphens `-`.

--link *NAME*:*ALIAS*  (optional):  Whenever you want a container to communicate with another container that is running, you can address it by using an alias for the host name.

-it  (optional):  Run the container in an interactive mode. After the container is created, keep the standard input displaying. Type `exit` to exit.

*IMAGE*  (required):  The image to be included in the container. You can list commands after the image, but don't put any options after the image. Include all options before specifying an image.

If you are using an image in your organization's private {{site.data.keyword.Bluemix_notm}} repository, specify the image in the format: *registry.ng.bluemix.net/NAMESPACE/IMAGE*.

If you are using an image that is provided by IBM Containers, specify the image in the format: *registry.ng.bluemix.net/IMAGE*.

*CMD*  (optional):  The command and arguments that are passed the container to execute. This command must be a long-running command. Do not use a short-lived command that does not run for very long, such as `/bin/date`, because the short-lived command might cause the container to crash.



**Examples**:

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


## bluemix ic route-map
{: #bluemix_ic_route_map}

Establish the route for internet traffic to use to access the container group. You can use this command to establish a new route or update an existing route.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

-n *HOST*|--hostname *HOST*  (optional):  The host name for the route. The host name is the first part of the full public route URL, such as `mycontainerhost` in the URL `mycontainerhost.mybluemix.net`.

-d *DOMAIN*|--domain *DOMAIN*  (optional):  The domain name for the route, which is the second part of the full public route URL. In most cases, the domain is `mybluemix.net`. You can also use this parameter to specify a private domain.

*CONTAINER_GROUP*  (required):  The container group ID or name.

**Examples**:

The following example shows a request to map the route for the group that is called `GROUP1`, where `my_host` is the host name, `organization.com` is the domain.
```
bluemix ic route-map -n my_host -d organization.com GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Establish the route for internet traffic to use to access the container group. You can use this command to establish a new route or update an existing route.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

-n *HOST*|--hostname *HOST*  (optional):  The host name for the route.

-d *DOMAIN*|--domain *DOMAIN*  (optional):  The domain name for the route.

*CONTAINER_GROUP*  (required):  The container group ID or name.

**Examples**:

The following example shows a request to unmap the route for the group that is called `GROUP1`, where `my_host` is the host name and `organization.com` is the domain.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic start
{: #ic_start}
Start a stopped container. For more information, see the [start](https://docs.docker.com/reference/commandline/start/){: new_window} command in the Docker help. To stop a container, see the [bluemix ic stop](#ic_stop) command.

```
bluemix ic start CONTAINER
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*CONTAINER*  (required):  The container name or ID.

**Responses**:

- Started container successfully.

- Command failed with container cloud service

 `{message}`
  
 Where `{message}` is the related error.
 
- Command failed - Could not connect to container cloud service

**Examples**:

The following example shows a request to start a container that is named `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
Stop a running container. For more information, see the [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} command in the Docker help. To start a container, see the [bluemix ic start](#ic_start) command.

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*CONTAINER*  (required):  The container name or ID.

-t *SECS*|--time *SECS*  (optional):  The number of seconds to wait before the container is killed.

**Responses**:

- Stopped container successfully.

- Command failed with container cloud service

 `{message}`
  
 Where `{message}` is the related error.
 
- Command failed - Could not connect to container cloud service

**Examples**:

The following example shows a request to stop a container that is named `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

For one or more containers, view live usage statistics. Use `CTRL+C` to exit. For more information, see the [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} command in the Docker help.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*CONTAINER*  (required):  The container name or ID.

--no-stream  (optional):  Display only the latest result and do not include any information that precedes it.

**Examples**:

The following example shows a request for the most recent statistics about a container:
```
bluemix ic stats --no-stream my_container
```


## bluemix ic top
{: #bluemix_ic_top}

Show the processes that are running in the container. For more information, see the [top](https://docs.docker.com/reference/commandline/top/){: new_window} command in the Docker help.

```
bluemix ic top CONTAINER [CONTAINER]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*CONTAINER*  (required):  The container name or ID.

**Examples**:

The following example shows a request to display the processes in a container that is called `my_container`.
```
bluemix ic top my_container
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

List volumes.

```
bluemix ic volumes
```

**Prerequisites**:  Endpoint, Login, Target


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspect a volume.

```
bluemix ic volume-inspect VOLUME_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*VOLUME_NAME*  (required):  The volume name.

**Examples**:

The following example is a request to inspect a volume, where `volume_name` is the name of the volume.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Create a volume.

```
bluemix ic volume-create VOLUME_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*VOLUME_NAME*  (required):  The volume name. The name can contain lowercase letters, numbers, underscores `_`, and hyphens `-`.

**Examples**:

The following example shows a request to create a volume.
```
bluemix ic volume-create volume_name 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Remove a volume.

```
bluemix ic volume-remove VOLUME_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*VOLUME_NAME*  (required):  The volume name.

**Examples**:

The following example shows a request to remove a volume, where `volume_name` is the name of the volume.
```
bluemix ic volume-remove volume_name
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

List file systems.

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Create a new file system.

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*FILE_SYSTEM_NAME*  (required):  The file system name. The name can contain lowercase letters, numbers, underscores `_`, and hyphens `-`.

**Examples**:

The following example shows a request to create a file system.
```
bluemix ic volume-fs-create my_file_system 
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Remove a file system.

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*FILE_SYSTEM_NAME*  (required):  The file system name.

**Examples**:

The following example shows a request to remove a file system, where `my_file_system` is the name of the file system.
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspect a file system.

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*FILE_SYSTEM_NAME*  (required):  The file system name.

**Examples**:

The following example is a request to inspect a file system, where `my_file_system` is the name of the volume.
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

List all file system flavors.

```
bluemix ic volume-fs-flavors
```

**Prerequisites**:  Endpoint, Login, Target

## bluemix ic wait
{: #bluemix_ic_wait}

Exit a container and display the exit code as confirmation. For more information, see the [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} command in the Docker help.

```
bluemix ic wait CONTAINER [CONTAINER]
```

**Prerequisites**:  Endpoint, Login, Target, Docker

**Command options**:

*CONTAINER*  (required):  The container name or ID.

**Examples**:

The following example shows a request to exit a container that is called `my_container`:
```
bluemix ic wait my_container
```


## bluemix ic version
{: #bluemix_ic_version}

Show the version of Docker. 

```
bluemix ic version
```

**Prerequisites**:  Docker

To see the version of the IBM Containers, run `bluemix ic info`. For more information, see the [version](https://docs.docker.com/reference/commandline/version/){: new_window} command in the Docker help.
