---



copyright:

  years: 2016, 2017

lastupdated: "2017-05-03"


---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}


# Cloud Foundry (cf) commands
{: #cf}

The Cloud Foundry (cf) command line interface (CLI) provides a set of commands for managing your apps. The following information lists the cf commands used most commonly for managing apps and includes their names, options, usage, prerequisites, descriptions, and examples. To list all of the cf commands and associated help information, use `cf help`. Use `cf command_name -h` to view detailed help information for a particular command.
{: shortdesc}

**Note**: If your network contains an HTTP proxy server between the host that runs the cf commands and the Cloud Foundry API endpoint, you must specify the host name or IP address of the proxy server by setting the `HTTP_PROXY` environment variable. For details, see [Using the cf CLI with an HTTP Proxy Server ![External link icon](../../../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html){: new_window}.


## Cloud Foundry CLI commands index
{: #CLIname_commands_index}

Use the index in the following table to refer to the frequently used Cloud Foundry commands:

<table summary="Alphabetically ordered general Cloud Foundry commands that have links that bring you to more info for the command">
<caption>Table 1. General Cloud Foundry commands</caption>
 <thead>
 <th colspan="6">General Cloud Foundry commands</th>
 </thead>
 <tbody>
 <tr>
 <td>[api](/docs/cli/reference/cfcommands/index.html#cf_api)</td>
 <td>[help](/docs/cli/reference/cfcommands/index.html#cf_help)</td>
 <td>[login](/docs/cli/reference/cfcommands/index.html#cf_login)</td>
 <td>[stacks](/docs/cli/reference/cfcommands/index.html#cf_stacks)</td>
 <td>[target](/docs/cli/reference/cfcommands/index.html#cf_target)</td>
 <td>[-v](/docs/cli/reference/cfcommands/index.html#cf_v)</td>
 </tr>
   </tbody>
 </table>


<table summary="Alphabetically ordered commands for managing apps, spaces, and services. Each command has a link that brings you to more info for the command.">
<caption>Table 2. Commands for managing apps, spaces, and services</caption>
 <thead>
 <th colspan="5">Commands for managing apps, spaces, and services</th>
 </thead>
 <tbody>
 <tr>
 <td>[apps](/docs/cli/reference/cfcommands/index.html#cf_apps)</td>
 <td>[bind-service](/docs/cli/reference/cfcommands/index.html#cf_bind-service)</td>
 <td>[create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service)</td>
 <td>[create-space](/docs/cli/reference/cfcommands/index.html#cf_create-space)</td>
 <td>[delete](/docs/cli/reference/cfcommands/index.html#cf_delete)</td>
  </tr>
 <tr>
 <td>[delete-space](/docs/cli/reference/cfcommands/index.html#cf_delete-space)</td>
 <td>[events](/docs/cli/reference/cfcommands/index.html#cf_events)</td>
 <td>[logs](/docs/cli/reference/cfcommands/index.html#cf_logs)</td>
 <td>[marketplace](/docs/cli/reference/cfcommands/index.html#cf_marketplace)</td>
 <td>[push](/docs/cli/reference/cfcommands/index.html#cf_push)</td>
  </tr>
 <tr>
 <td>[scale](/docs/cli/reference/cfcommands/index.html#cf_scale)</td>
 <td>[services](/docs/cli/reference/cfcommands/index.html#cf_services)
 <td>[set-env](/docs/cli/reference/cfcommands/index.html#cf_set-env)</td>
 <td>[ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)</td>
 <td>[stop](/docs/cli/reference/cfcommands/index.html#cf_stop)</td>
 </tr>
 </tbody>
 </table>

## cf api
{: #cf_api}

Use this command to display or specify the URL of the API endpoint of {{site.data.keyword.Bluemix_notm}}.

```
cf api [BluemixServerURL] [--skip-ssl-validation] [--unset]
```

<strong>Prerequisites</strong>: None.

<strong>Command options</strong>:

   <dl>
   <dt>BluemixServerURL (optional)</dt>
   <dd>The URL of the Bluemix API endpoint that you must specify when you connect to {{site.data.keyword.Bluemix_notm}}. Typically, this URL is `https://api.{DomainName}`.
   If you want to display the URL of the API endpoint that you are currently using, you do not need to specify this parameter for the cf api command.</dd>
   <dt>* --skip-ssl-validation</dt>
   <dd>Disables the SSL validation process. Use of this parameter might cause security problems.</dd>
   <dt>* --unset</dt>
   <dd>Removes connection information for all API endpoints.</dd>
    </dl>

<strong>Examples</strong>:

View the current API endpoint
```
cf api
```
{: codeblock}

Remove connection to all API endpoints for api.ng.bluemix.net
```
cf api api.ng.bluemix.network --unset
```
{: codeblock}

Disable the SSL validation process for api.ng.bluemix.network
```
cf api api.ng.bluemix.network --skip-ssl-validation
```
{: codeblock}


## cf apps
{: #cf_apps}

Lists all of the applications that you deployed in the current space. The status of each application is also displayed.

Assume that you have one instance for an app, in the instances column of the response from the cf apps command, you see 1/1 if your app is up and 0/1 if your app is down. If you see ?/1, which indicates that the app instance state is unknown, you can copy the app URL to your browser to check whether your app responds, or you can tail the log by the `cf logs appname` command to see if the app is generating log content.

```
cf apps
```

<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`


## cf bind-service
{: #cf_bind-service}

Binds an existing service instance to your application.

```
cf bind-service appname service_instance
```

<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

   <dl>
   <dt>appname (required)</dt>
   <dd>The name of the application.</dd>
   <dt>service_instance (required)</dt>
   <dd>The name of the existing service instance.</dd>
    </dl>

<strong>Examples</strong>:

Bind a service instance named `my_dataworks` to your app named `my_app`.
```
cf bind-service my_app my_dataworks
```
{: codeblock}


## cf create-service
{: #cf_create-service}

Creates a service instance

```
cf create-service service_name service_plan service_instance
```

<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

   <dl>
   <dt>service_name (required)</dt>
   <dd>The name of the service.</dd>
   <dt>service_plan (required)</dt>
   <dd>The name of the service plan.</dd>
   <dt>service_instance (required)</dt>
   <dd>The name that you want to use for the new service instance that you create.</dd>
    </dl>

<strong>Examples</strong>:

Create an instance of the {{site.data.keyword.dataworks_short}} service with a `free` plan.
```
cf create-service DataWorks free my_dataworks
```
{: codeblock}


## cf create-space
{: #cf_create-space}

Creates a space.

```
cf create-space space_name [-o] [-q]
```

<strong>Prerequisites</strong>: `cf api`, `cf login`

<strong>Command options</strong>:

   <dl>
   <dt>space_name (required)</dt>
   <dd>The name of the space.</dd>
   <dt>*-o* (optional)</dt>
   <dd>The name of the organization that you want to create a space within.</dd>
   <dt>*-q* (optional)</dt>
   <dd>The quota to assign to the newly created space. If not specified, a default quota is automatically assigned.</dd>
    </dl>

<strong>Examples</strong>:

Create a space named new_space
```
cf create-space new_space
```
{: codeblock}


## cf delete
{: #cf_delete}

Deletes an existing application.

```
cf delete appname [-f] [-r]
```

<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

   <dl>
   <dt>appname (required)</dt>
   <dd>The name of the application.</dd>
   <dt>*-f* (optional)</dt>
   <dd>Forces deletion of the application without any confirmation.</dd>
   <dt>*-r* (optional)</dt>
   <dd>Deletes all domain names that are associated with the application. </dd>
    </dl>

<strong>Examples</strong>:

Deletes an application named `my_app` (will require confirmation).
```
cf delete my_app
```
{: codeblock}

Deletes an application named `my_app` without requiring confirmation.
```
cf delete my_app -f
```
{: codeblock}

Deletes an application named `my_app` and all domain names associated with `my_app`.
```
cf delete my_app -r
```
{: codeblock}

Deletes an application named `my_app` and all domain names associated with `my_app` without requiring confirmation.
```
cf delete my_app -f -r
```
{: codeblock}


## cf delete-space
{: #cf_delete-space}

Deletes a space.

```
cf delete-space space_name [-f]
```

<strong>Prerequisites</strong>: `cf api`, `cf login`

<strong>Command options</strong>:

   <dl>
   <dt>space_name (required)</dt>
   <dd>The name of the space.</dd>
   <dt>*-f* (optional)</dt>
   <dd>Forces deletion of the space without any confirmation.</dd>
   *Note:* Deleting a space is an irreversible operation.
    </dl>

<strong>Examples</strong>:

Deletes an application named `my_app` (will require confirmation).
```
cf delete my_app
```
{: codeblock}

Deletes an application named `my_app` without requiring confirmation.
```
cf delete my_app -f
```
{: codeblock}

Deletes an application named `my_app` and all domain names associated with `my_app`.
```
cf delete my_app -r
```
{: codeblock}

Deletes an application named `my_app` and all domain names associated with `my_app` without requiring confirmation.
```
cf delete my_app -f -r
```
{: codeblock}


## cf events
{: #cf_events}

Displays runtime events that are related to an application.

```
cf events [appname]
```

<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

   <dl>
   <dt>appname</dt>
   <dd>The name of the application.</dd>
   </dl>

<strong>Examples</strong>:

Displays the events for an application named `my_app`.
```
cf events my_app
```
{: codeblock}


## cf help
{: #cf_help}

Displays help information for all cf commands or for a specific cf command.

```
cf help [command_name]
```

<strong>Prerequisites</strong>: None.

<strong>Command options</strong>:

   <dl>
   <dt>command_name (optional)</dt>
   <dd>The name of a command.</dd>
    </dl>

<strong>Examples</strong>:

Display the help information for all cf commands.
```
cf help
```
{: codeblock}

Display the help information for the events command.
```
cf help events
```
{: codeblock}


## cf login
{: #cf_login}

Logs you in to {{site.data.keyword.Bluemix_notm}}.

If you are logging in with a [federated ID](/docs/admin/account.html#signup), you must use the single sign-on (SSO) parameter to log in. 

**Note**: You can also use an {{site.data.keyword.Bluemix_notm}} Platform API key to log in. Use the user name "apikey" and your api key value as password.

```
cf login [-a url] [-u user_name] [-p password] [-sso] [-o organization_name] [-s space_name] [--skip-ssl-validation]
```

<strong>Prerequisites</strong>: None.

<strong>Command options</strong>:

<dl>
<dt>*-a* https://api.{DomainName} (optional)</dt>
<dd>The URL of the API endpoint of {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*-u* user_name (optional)</dt>
<dd>Your user name.</dd>
<dt>*-p* password (optional)</dt>
<dd>Your password.</dd>
<dd>*Important:* If you provide your password by using the *-p* parameter on the command line interface, the password might be recorded in the command line history. For security reasons, avoid providing the password by using the -p parameter. Instead, enter the password when the command line interface prompts you.</dd>
<dt>*-sso*</dt>
<dd>You must use the single sign-on option (SSO) when logging in with a federated ID. This is not required when logging in with an IBMid. If you try to sign in with a federated ID, and you do not specify the SSO parameter, you will be prompted to include it. Using the SSO parameter prompts you to enter the one-time passcode upon login.</dd>
<dt>*-o* organization_name</dt>
<dd>The name of the organization that you want to log in to.</dd>
<dt>*-s* space_name</dt>
<dd>The name of the space that you want to log in to.</dd>
<dt>*--skip-ssl-validation* (optional)</dt>
<dd>Disables the SSL validation process. Use of this parameter might cause security problems.</dd>
</dl>

*Note:* If you provide your password in the *-p* parameter of this command, your password might be recorded in the shell command history file and might be visible to other users of the local operating system.

<strong>Examples</strong>:

Log in to {{site.data.keyword.Bluemix_notm}}.
```
cf login
```
{: codeblock}

Log in to {{site.data.keyword.Bluemix_notm}} with a defined endpoint of `https://api.ng.bluemix.net`.
```
cf login -a https://api.ng.bluemix.net
```
{: codeblock}

Log in to {{site.data.keyword.Bluemix_notm}} with a defined endpoint of `https://api.ng.bluemix.net`, a user name of `user_name`, and no specified password for security reasons.
```
cf login -a https://api.ng.bluemix.net -u user_name
```
{: codeblock}

Log in to {{site.data.keyword.Bluemix_notm}} with a defined endpoint of `https://api.ng.bluemix.net`, a user name of `user_name`, no specified password for security reasons, and an organization name of `org_name` and space name of `space_name`.
```
cf login -a https://api.ng.bluemix.net -u user_name -o org_name -s space_name
```
{: codeblock}


## cf logs
{: #cf_logs}

Displays the STDOUT and STDERR log streams of an application.

```
cf logs appname [--recent]
```
<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
<dt>*--recent* (optional)</dt>
<dd>Retrieves recent logs.</dd>
</dl>

<strong>Examples</strong>:

Display the log streams for an application named `my_app`.
```
cf logs my_app
```
{: codeblock}

Display the recent log streams for an application named `my_app`.
```
cf logs my_app --recent
```
{: codeblock}


## cf marketplace
{: #cf_marketplace}

Lists all of the services that are available in the marketplace. The services listed by this command are also shown in the {{site.data.keyword.Bluemix_notm}} Catalog.

```
cf marketplace
```
<strong>Prerequisites</strong>: `cf api`

<strong>Command options</strong>: None.

<strong>Examples</strong>:

List all services in the marketplace
```
cf marketplace
```
{: codeblock}


## cf push
{: #cf_push}

Deploys a new application to {{site.data.keyword.Bluemix_notm}}, or updates an existing application in {{site.data.keyword.Bluemix_notm}}.

```
cf push appname [-b buildpack_name] [-c start_command] [-f manifest_path] [-i instance_number] [-k disk_limit] [-m memory_limit] [-n host_name] [-p app_path] [-s stack_name] [-t timeout_length] [--no-hostname] [--no-manifest] [--no-route] [--no-start] [--random-route]
```

<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

<dl>
<dt>appname (required)</dt>
<dd>The name of the application.</dd>
<dt>*-b* buildpack_name (optional)</dt>
<dd>The name of the buildpack. The buildpack_name can be a custom buildpack by name (for example liberty-for-java), or a Git URL (for example https://github.com/cloudfoundry/java-buildpack.git), or a Git URL with a branch or tag (for example, https://github.com/cloudfoundry/java-buildpack.git#v3.3.0 for the v3.3.0 tag).</dd>
<dt>*-c* start_command (optional)</dt>
<dd>The start command of your application. To use the default start command, specify a value of null for this option. </dd>
<dt>*-f* manifest_path (optional)</dt>
<dd>The path to the manifest file. The default manifest file is manifest.yml under the root directory of your application.</dd>
<dt>*-i* instance_number (optional)</dt>
<dd>The number of instances.</dd>
<dt>*-k* disk_limit (optional)</dt>
<dd>The disk limit for the application. Possible values are *256M*, *1024M*, or *1G*.</dd>
<dt>*-m* memory_limit (optional)</dt>
<dd>The memory limit for the application. Possible values are *256M*, *1024M*, or *1G*.</dd>
<dt>*-n* host_name (optional)</dt>
<dd>The host name for the application, for example, *my-subdomain*.</dd>
<dt>*-p* app_path (optional)</dt>
<dd>The path to the application directory or the application archive file.</dd>
<dt>*-s* stack_name (optional)</dt>
<dd>The stack to run the apps. A stack is per-built file system including the operation system. Use `cf stacks` to view the available stacks in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*-t* timeout (optional)</dt>
<dd>Maximum time in seconds for the application to start. Other server-side timeouts might override this value.</dd>
<dt>*--no-hostname* (optional)</dt>
<dd>Maps the {{site.data.keyword.Bluemix_notm}} system domain to this application.</dd>
<dt>*--no-manifest* (optional)</dt>
<dd>Ignores the default manifest file.</dd>
<dt>*--no-route* (optional)</dt>
<dd>Does not map a route to this application.</dd>
<dt>*--no-start* (optional)</dt>
<dd>Does not start the application after the application is deployed.</dd>
<dt>*--random-route* (optional)</dt>
<dd>Creates a random route for the application.</dd>
</dl>

<strong>Examples</strong>:

Start an application named `my_app` with the default start command.
```
cf push `my_app` -c null
```
{: codeblock}

Start an application named `my_app` with the option to run a script file named `run.sh`.
```
cf push `my_app` -c "bash ./<run.sh>"
```
{: codeblock}



## cf scale
{: #cf_scale}

Displays or changes the instance number, disk space limit, and memory limit for an application.

```
cf scale appname [-i instance_number] [-k disk_limit] [-m memory_limit] [-f]
```

<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

<dl>
<dt>appname (required)</dt>
<dd>The name of the application.</dd>
<dt>*-i* instance_number (optional)</dt>
<dd>The number of instances</dd>
<dt>*-k* disk_limit (optional)</dt>
<dd>The disk limit for the application; possible values are `256M`, `1024M`, or `1G`.</dd>
<dt>*-m* memory_limit (optional)</dt>
<dd>The memory limit for the application; possible values are `256M`, `1024M`, or `1G`.</dd>
<dt>*-f* (optional)</dt>
<dd>Forces the application to restart without prompt.</dd>
</dl>

<strong>Examples</strong>:

Display the instance number, disk space limit, and memory limit for an application named `my_app`.
```
cf scale my_app
```
{: codeblock}

Modify the instance number to `1234`, disk space limit to `1G`, and memory limit to `1G` for an app named `my_app`.
```
cf scale appname -i 1234 -k 1G -m 1G
```
{: codeblock}


## cf services
{: #cf_services}

Lists all of the services that are available in the current space.

```
cf services
```
<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>: None.

<strong>Examples</strong>:

List all services in the current space.
```
cf services
```
{: codeblock}


## cf set-env
{: #cf_set-env}

Sets an environment variable for an application

```
cf set-env appname var_name var_value
```
<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

<dl>
<dt>appname (required)</dt>
<dd>The name of the application.</dd>
<dt>var_name (required)</dt>
<dd>The name of the environment variable.</dd>
<dt>var_value (required)</dt>
<dd>The value of the environment variable.</dd>
</dl>

<strong>Examples</strong>:

Set an environment variable named `variable_a` with a value of `123` for the application named `my_app`.
```
cf set-env my_app variable_a 123
```
{: codeblock}


## cf ssh
{: #cf_ssh}

Securely access the application container. The `cf ssh` command can be used to set up an interactive SSH session, run remote commands, transfer files, and set up port forwarding with a specific application container instance.

```
cf ssh
```
<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

By default, SSH access is enabled for Diego applications. You can use the `cf ssh-enabled` command to verify if SSH access is enabled or the `cf enable-ssh` command to enable the access if it was disabled. 

<strong>Command options</strong>:

<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
<dt>-c</dt>
<dd>Specifies a remote command to run.</dd>
<dt>-i</dt>
<dd>Targets a specific instance of an application. If not specified, the first instance of the application is used (an instance with index 0).</dd>
<dt>-L</dt>
<dd>Enables local port forwarding, which binds an output port on your machine to an input port on the application VM.</dd>
<dt>-N</dt>
<dd>Do not run a remote command.</dd>
<dt>-t, -tt, or -T</dt>
<dd>Enables you to run an SSH session in pseudo-tty mode rather than generate terminal line output.<dd>
</dl>

<strong>Examples</strong>:

Start an interactive SSH session with the container instance running the `my_app` application.
```
$ cf ssh my_app
```
{: codeblock}

Run a single command on the `my_app` application container instance.
```
$ cf ssh my_app -c "ls -l"
```

Transfer a single file from the `my_app` application container instance.
```
$ cf ssh my_app -c "/bin/cat logs/messages.log" > messages.log
```

Setup port forwarding of the 7777 port on the local machine to the 8888 port on the `my_app` application container instance.
```
$ cf ssh -N -T -L 7777:localhost:8888 my_app

```

## cf stacks
{: #cf_stacks}

Lists all stacks. A stack is a pre-built file system, including an operating system that can run apps.

```
cf stacks
```
<strong>Prerequisites</strong>: `cf api`, `cf login`

<strong>Command options</strong>: None.

<strong>Examples</strong>:

List all stacks.
```
cf stacks
```
{: codeblock}


## cf stop
{: #cf_stop}

Stops an application

```
cf stop appname
```
<strong>Prerequisites</strong>: `cf api`, `cf login`, `cf target`

<strong>Command options</strong>:

<dl>
<dt>appname (required)</dt>
<dd>The name of the application.</dd>
</dl>

<strong>Examples</strong>:

Stop the application named `my_app`.
```
cf stop my_app
```
{: codeblock}


## cf target
{: #cf_target}

Sets or views the targeted organization or space

```
cf target [-o org_name] [-s space_name]
```
<strong>Prerequisites</strong>: `cf api`, `cf login`

<strong>Command options</strong>:

<dl>
<dt>-o *org_name* (optional)</dt>
<dd>The name of the organization where the space is located.</dd>
<dt>-s *space_name* (optional)</dt>
<dd>The name of the space.</dd>
</dl>

<strong>Examples</strong>:

Set the target to the organization named "my_org" and the space named "my_space".
```
cf target -o my_org -s my_space
```
{: codeblock}


## cf -v
{: #cf_v}

Displays the version of the cf command line interface.

```
cf -v
```
<strong>Prerequisites</strong>: None.

<strong>Command options</strong>: None.

<strong>Examples</strong>:

Display the version of the cf command line interface.
```
cf -v
```
{: codeblock}



# Related Links
{: #rellinks}

## Related Links
{: #general}

* [Download Cloud Foundry CLI ![External link icon](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases)
{: new_window}
* [Quick Reference Card - cf commands ![External link icon](../../../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/cf_cli_refcard.html)
{: new_window}
