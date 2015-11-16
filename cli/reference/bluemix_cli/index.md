{:shortdesc: .shortdesc}

# bx commands for interacting with {{site.data.keyword.Bluemix_notm}}
{: #bluemix_cli}

*Last updated:* 19 October 2015

The {{site.data.keyword.Bluemix}} command line interface (CLI) provides a set of commands that are grouped by namespace for users to interact with {{site.data.keyword.Bluemix_notm}}. Some {{site.data.keyword.Bluemix_notm}} CLI commands, which are called bx commands, are wrappers of existing cf commands, and others are unique for {{site.data.keyword.Bluemix_notm}}. The information that follows lists all commands that are supported by {{site.data.keyword.Bluemix_notm}} CLI and includes their names, options, usage, prerequisites, descriptions, and examples.
{:shortdesc}
 
**Note:** *Prerequisites* list which actions are required before using the command. Commands that have no prerequisite actions list **None**. Otherwise, prerequisites might include one or more of the following actions:
<dl>
<dt>**Endpoint**</dt>
<dd>An API endpoint must be set through the `bluemix api` before using the command.</dd>
<dt>**Login**</dt>
<dd>Login by using the `bluemix login` command is required before using this command.</dd>
<dt>**Target**</dt>
<dd>The `bluemix target` command must be used to set an org and space before using this command.</dd>
</dl>

## bluemix help
Display the general help for first-level built-in commands and supported namespaces of {{site.data.keyword.Bluemix_notm}} CLI, or the help for a specific built-in command or namespace.

```
bluemix help [COMMAND|NAMESPACE]
```

**Prerequisites**:  None

**Command options**:

*COMMAND*|*NAMESPACE*  (optional):  The command or namespace that help is displayed for. If not specified, the general help for {{site.data.keyword.Bluemix_notm}} CLI is shown.

**Examples**:

Display general help for {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix help
```

Display help for the `catalog` namespace:

```
bluemix help catalog
```

```
bluemix catalog help
```

Display help for the `info` command:

```
bluemix help info
```

Display help for the `templates` command under the `catalog` namespace:

```
bluemix catalog help templates
```


## bluemix api
Set or view the {{site.data.keyword.Bluemix_notm}} API endpoint. This command wraps the `cf api` command.

```
bluemix api [API_ENDPOINT] [--unset]
```

**Prerequisites**:  None

**Command options**:

*API_ENDPOINT*  (optional):  The API endpoint that is targeted, for example, https://api.ng.bluemix.net. If both *API_ENDPOINT* and `--unset` options are not specified, the current API endpoint is displayed.

`--unset`  (optional):  Remove the API endpoint setting.

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
Log in user. This command wraps the `cf login` command. Command options are the same as `cf login` command options.

```
bluemix login [OPTIONS...]
```

**Prerequisites**:  Endpoint

**Command options**:
For information about options supported by the `login` command, see `cf login` command usage information for cf commands for managing applications.


## bluemix logout
Log out user. This command wraps the `cf logout` command.

```
bluemix logout
```

**Prerequisites**:  None


## bluemix target
Set or view the target org or space. This command wraps the `cf target` command.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**Prerequisites**:  Endpoint, Login

**Command options**:

-o *ORG_NAME*  (optional):  The name of the organization to be targeted.

-s *SPACE_NAME*  (optional):  The name of the space to be targeted. 

If neither -o *ORG_NAME* or -s *SPACE_NAME* are specified, the current org and space are displayed.

**Examples**:

Set the current org to 'MyOrg' and space to 'MySpace':

```
bluemix target -o MyOrg -s MySpace
```

View the current org and space:

```
bluemix target
```


## bluemix info
View the basic {{site.data.keyword.Bluemix_notm}} information, including the current region, the cloud controller version, and some useful endpoints, such as endpoints for login and exchanging access token.

```
bluemix info
```

**Prerequisites**:  Endpoint


## bluemix list
List all cf applications, containers, container groups, and VM groups in the current space.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

apps  (optional):  Display only the applications information.

containers  (optional):  Display only the containers information.

container-groups  (optional):  Display only the container groups information.

vm-groups  (optional):  Display only the VM groups information.

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
Scale in or scale out the cf application or container group to a specified instance count, disk quota, and memory size. 

**Note:** Only an instance number can be specified for scaling a container group. If no option is specified, this command lists the current instance count for the container group, and also disk quota and memory size for the cf application.

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT] [-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (required):  The name of the cf application or container group to be scaled.

-i *INSTANCE_COUNT*  (optional):  The new instance number for the cf application or container group to be scaled. This option is the only valid option for container group to be scaled.

-k *DISK_QUOTA*  (optional):  The new disk quota of the cf application. Not valid for scaling a container group.

-m *MEMORY_SIZE*  (optional):  The new memory size for the cf application. Not valid for scaling a container group.

**Examples**:

Display the current instance number for 'my-container-group':

```
bluemix scale my-container-group
```

Scale 'my-container-group' to 2 instances:

```
bluemix scale my-container-group -i 2
```

Scale 'my-java-app' to 3 instances, 8G disk quota, and 1024M memory size:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Execute a raw HTTP request to {{site.data.keyword.Bluemix_notm}}. "Content-Type" is set to "application/json" by default. This command sends a request to the {{site.data.keyword.Bluemix_notm}} console server (for example, https://console.ng.bluemix.net) instead of the cf API endpoint (for example, https://api.ng.bluemix.net).

```
bluemix curl PATH [OPTIONS...]
```

**Prerequisites**:  Endpoint, Login

**Command options**:

*PATH*  (required):  The URL path of the resource. For example, /rest/v2/apps.

*OPTIONS*  (optional):  The options that are supported by the `bluemix curl` command are the same as those for the `cf curl` command.

**Examples**:

Retrieve the information for all boilerplate templates:

```
bluemix curl /rest/templates
```


## bluemix iam orgs
This command has the same function and options as the `cf orgs` command.


## bluemix iam org
This command has the same function and options as the `cf org` command.


## bluemix iam org-create
This command has the same function and options as the `cf create-org` command.


## bluemix iam org-rename
This command has the same function and options as the `cf rename-org` command.


## bluemix iam org-delete
This command has the same function and options as the `cf delete-org` command.


## bluemix iam spaces
This command has the same function and options as the `cf spaces` command.


## bluemix iam space
This command has the same function and options as the `cf space` command.


## bluemix iam space-create
This command has the same function and options as the `cf create-space` command.


## bluemix iam space-rename
This command has the same function and options as the `cf rename-space` command.


## bluemix iam space-delete
This command has the same function and options as the `cf delete-space` command.


## bluemix iam user-create
This command has the same function and options as the `cf create-user` command.


## bluemix iam user-delete
This command has the same function and options as the `cf delete-user` command.


## bluemix iam org-users
This command has the same function and options as the `cf org-users` command.


## bluemix iam org-role-set
This command has the same function and options as the `cf set-org-role` command.


## bluemix iam org-role-unset
This command has the same function and options as the `cf unset-org-role` command.


## bluemix iam space-users
This command has the same function and options as the `cf space-users` command.


## bluemix iam space-role-set
This command has the same function and options as the `cf set-space-role` command.


## bluemix iam space-role-unset
This command has the same function and options as the `cf unset-space-role` command.


## bluemix catalog templates
View the boilerplate templates on Bluemix.

```
bluemix catalog templates [-d]
```

**Prerequisites**:  Endpoint, Login

**Command options**:

-d  (optional):  If the '-d' option is specified, the description of each template is also displayed. Otherwise, only the ID and name of each template is shown.


## bluemix catalog template-run
Create a cf application that is based on the specified template with the specified URL and description. By default, the new app is started automatically.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*TEMPLATE_ID*  (required):  The template that the application will be based on when it is created. Use 'bluemix templates' to see all templates' ID.

*CF_APP_NAME*  (required):  The name of the cf application to be created.

-u *URL*  (optional):  The route of the application. If not specified, the route is set by {{site.data.keyword.Bluemix_notm}} automatically based on your app name and default domain.

-d *DESCRIPTION*  (optional):  Description of the application.

--no-start  (optional):  Do not start the application automatically after it is created. If not specified, the application is started automatically after it is created.

**Examples**:

Create a cf application 'my-app' based on 'javaHelloWorld' template:

```
bluemix catalog template-run javaHelloWorld my-app
```

Create an application 'my-ruby-app' based on 'rubyHelloWorld' template with route 'myrubyapp.ng.bluemix.net' and description 'My first ruby app on {{site.data.keyword.Bluemix_notm}}.':

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

Create an application 'my-python-app' based on 'pythonHelloWorld' template without automatic start:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
View the information for all regions on {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

**Prerequisites**:  Endpoint


## bluemix network region-set
Switch to the region that is specified. This command automatically retargets to the same org and space in the new region, if possible, or prompts the user to select a new org and space if the user is already logged in. The API endpoint is changed accordingly.

```
bluemix network region-set REGION_NAME
```

**Prerequisites**:  Endpoint

**Command options**:

*REGION_NAME*  (required):  The name of the region you want to switch to. You can use the `bluemix regions` command to see all region names.

**Examples**:

Set the current region to 'eu-gb':

```
bluemix network region-set eu-gb
```


## bluemix network routes
This command has the same function and options as the `cf routes` command.


## bluemix network route-check
This command has the same function and options as the `cf check-route` command.


## bluemix network route-map
Map a route to an existing cf application or container group that has the specified domain and host name.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (required):  The name of the cf application or container group to be mapped with a route.

*DOMAIN*  (required):  The domain of the route. For example, mybluemix.net or ng.bluemix.net. 

-n *HOST_NAME*  (optional):  The host name of the route. If not provided, the host name is set to the app name or container group name by default.

**Examples**:

Map a route to 'my-app' with specified domain:

```
bluemix network route-map my-app mybluemix.net
```

Map a route to 'my-container-group' with specified domain and host name:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Unmap the specified route from an existing cf application or container group.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Prerequisites**:  Endpoint, Login, Target

**Command options**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (required):  The name of the cf application or container group.

*DOMAIN*  (required):  The domain of the route (for example, mybluemix.net or ng.bluemix.net). 

-n *HOST_NAME*  (optional):  The host name of the route. If not provided, the host name is set to app name or container group name by default.

**Examples**:

Unmap 'my-app.mybluemix.net' from 'my-app':

```
bluemix network route-unmap my-app mybluemix.net
```

Unmap 'abc.ng.bluexmix.net' from 'my-container-group':

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
This command has the same function and options as the `cf create-route` command.


## bluemix network route-delete
This command has the same function and options as the `cf delete-route` command.


## bluemix network orphaned-routes-delete
This command has the same function and options as the `cf delete-orphaned-routes` command.


## bluemix network domains
This command has the same function and options as the `cf domains` command.


## bluemix network domain-create
This command has the same function and options as the `cf create-domain` command.


## bluemix network domain-delete
This command has the same function and options as the `cf delete-domain` command.


## bluemix network shared-domain-create
This command has the same function and options as the `cf create-shared-domain` command.


## bluemix network shared-domain-delete
This command has the same function and options as the `cf delete-shared-domain` command.


## bluemix plugin repos
List all plugin repositories that are registered in {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repos
```

**Prerequisites**:  None


## bluemix plugin repo-add
Add a new plugin repository to {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**Prerequisites**:  None

**Command options**:

*REPO_NAME*  (required):  The name of the repository to be added. You can define your own name for each repository.

*REPO_URL*  (required):  The URL of the repository to be added. The repository URL must contain the protocol (for example, http://plugins.ng.bluemix.net instead of plugins.ng.bluemix.net). http://plugins.ng.bluemix.net is the official plugin repository of {{site.data.keyword.Bluemix_notm}} CLI.

**Examples**:

Add the official plugin repository of Bluemix CLI as 'bluemix-repo':

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Remove a plugin repository from {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin repo-remove REPO_NAME
```

**Prerequisites**:  None

**Command options**:

*REPO_NAME*  (required):  The name of the repository to be removed.

**Examples**:

Remove 'bluemix-repo' repository from {{site.data.keyword.Bluemix_notm}} CLI:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
List all available plugins in all added repositories or a specific repository.

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**Prerequisites**:  None

**Command options**:

-r *REPO_NAME*  (optional):  List only the plugins in specified repository.

**Examples**:

List all plugins in all added repositories:

```
bluemix plugin repo-plugin-list
```

List all plugins in the 'bluemix-repo' repository:

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
List all installed plugins in {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin list
```

**Prerequisites**:  None


## bluemix plugin install
Install the plugin to {{site.data.keyword.Bluemix_notm}} CLI from the specified path or repository.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**Prerequisites**:  None

**Command options**:

*PLUGIN_PATH*|*PLUGIN_NAME*  (required):  If '-r *REPO_NAME*' is not specified, plugin is installed from the specified local path or remote URL.

-r *REPO_NAME*  (optional):  The name of the repository where the plugin binary is located.

**Examples**:

Install a plugin from the local file:

```
bluemix plugin install /downloads/new_plugin
```

Install a plugin from the remote URL:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Install the 'IBM-Containers' plugin from 'bluemix-repo' repository:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Uninstall the specified plugin from {{site.data.keyword.Bluemix_notm}} CLI.

```
bluemix plugin uninstall PLUGIN_NAME
```

**Prerequisites**:  None

**Command options**:

*PLUGIN_NAME*  (required):  The name of the plugin to be uninstalled.

**Examples**:

Uninstall the 'IBM-Containers' plugin that was previously installed:

```
bluemix plugin uninstall IBM-Containers
```
