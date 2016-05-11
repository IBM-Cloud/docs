---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cloud Foundry (cf) commands

*Last updated: 29 January 2016*

You can use Cloud Foundry (cf) commands to manage your apps.
{:shortdesc}

The following information lists the cf commands used most commonly for managing apps. To list all of the cf commands and their help information, use `cf help`. Use `cf command_name -h` to view detailed help information for a particular command.

*Note:* If your network contains an HTTP proxy server between the host that runs the cf commands and the Cloud Foundry API endpoint, you must specify the host name or IP address of the proxy server by setting the `HTTP_PROXY` environment variable. For details, see [Using the cf CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html).

## cf api

Displays or specifies the URL of the API endpoint of {{site.data.keyword.Bluemix_notm}}.
```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>The URL of the Bluemix API endpoint that you must specify when you connect to {{site.data.keyword.Bluemix_notm}}. Typically, this URL is https://api.{DomainName}. 
If you want to display the URL of the API endpoint that you are currently using, you do not need to specify this parameter for the cf api command.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Disables the SSL validation process. Use of this parameter might cause security problems.</dd>
<dt>*--unset*</dt>
<dd>Removes connection information for all API endpoints.</dd>
</dl>

## cf apps

Lists all of the applications that you deployed in the current space. The status of each application is also displayed.

Assume that you have one instance for an app, in the instances column of the response from the cf apps command, you see 1/1 if your app is up and 0/1 if your app is down. If you see ?/1 which indicates that the app instance state is unknown, you can copy the app URL to your browser to check whether your app responds, or you can tail the log by the ``cf logs appname`` command to see if the app is generating log content.

## cf bind-service

Binds an existing service instance to your application.
```
cf bind-service appname service_instance
```

For example, if you have a service instance that is named `my_dataworks` in your current organization and space, you can use `cf bind-service my_app my_dataworks` to bind this service instance to your application.

<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
<dt>service_instance</dt>
<dd>The name of the existing service instance.</dd>
</dl>

## cf create-service

Creates a service instance.
```
cf create-service service_name service_plan service_instance
```
For example, you can use `cf create-service DataWorks free my_dataworks` to create an instance of the {{site.data.keyword.dataworks_short}} service with a free plan.

<dl>
<dt>service_name</dt>
<dd>The name of the service.</dd>
<dt>service_plan</dt>
<dd>The name of the service plan.</dd>
<dt>service_instance</dt>
<dd>The name that you want to use for the new service instance that you create.</dd>
</dl>

## cf create-space

Creates a space.
```
cf create-space space_name
```
<dl>
<dt>space_name</dt>
<dd>The name of the space.</dd>
<dt>*-o*</dt>
<dd>The name of the organization that you want to create a space within.</dd>
<dt>*-q*</dt>
<dd>The quota to assign to the newly created space. If not specified, a default quota is automatically assigned.</dd>
</dl>

## cf delete

Deletes an existing application.
```
cf delete appname
```
<dl>
<dt>appname</dt>
<dd>The name of the application.<dd>
<dt>*-f*</dt>
<dd>Forces deletion of the application without any confirmation. This parameter is optional.</dd>
<dt>*-r*</dt>
<dd>Deletes all domain names that are associated with the application. This parameter is optional.</dd>
</dl>

## cf delete-space

Deletes a space.
```
cf delete-space space_name
```
<dl>
<dt>space_name</dt>
<dd>The name of the space.</dd>
<dt>*-f*</dt>
<dd>Forces deletion of the space without any confirmation. This parameter is optional.</dd>
*Note:* Deleting a space is an irreversible operation.
</dl>

## cf events

Displays runtime events that are related to an application.
```
cf events appname
```
<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
</dl>

## cf help

Displays help information for all cf commands, or for a specific cf command if the command_name parameter is used.
```
cf help command_name
```
<dl>
<dt>command_name</dt>
<dd>The name of a command. If you want help information that is specific to a command, you can use this parameter.</dd>
<dd>If you do not specify this parameter, help information of all cf commands is displayed.</dd>
</dl>


## cf login

Logs you in to {{site.data.keyword.Bluemix_notm}}.
```
cf login
```
You can use one or more of the following parameters when you issue the cf login command:
<dl>
<dt>*-a* https://api.{DomainName}</dt>
<dd>The URL of the API endpoint of {{site.data.keyword.Bluemix_notm}}. This parameter is optional.</dd>
<dt>*-u* user_name</dt>
<dd>Your user name. This parameter is optional.</dd>
<dt>*-p* password</dt>
<dd>Your password.</dd>
<dd>*Important:* If you provide your password by using the *-p* parameter on the command line interface, the password might be recorded in the command line history. For security reasons, avoid providing the password by using the -p parameter. Instead, enter the password when the command line interface prompts you.</dd>
<dt>*-o* organization_name</dt>
<dd>The name of the organization that you want to log in to.</dd>
<dt>*-s* space_name</dt>
<dd>The name of the space that you want to log in to.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Disables the SSL validation process. Use of this parameter might cause security problems.</dd>
</dl>

*Note:* If you provide your password in the *-p* parameter of this command, your password might be recorded in the shell command history file and might be visible to other users of the local operating system.


## cf logs

Displays the STDOUT and STDERR log streams of an application.
```
cf logs appname
```
<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
<dt>*--recent*</dt>
<dd>Retrieves recent logs.</dd>
</dl>

## cf marketplace

Lists all of the services that are available in the marketplace. The services listed by this command are also shown in the {{site.data.keyword.Bluemix_notm}} Catalog.
```
cf marketplace
```

## cf push

Deploys a new application to Bluemix, or updates an existing application in Bluemix.
```
cf push appname 
```
<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
<dt>*-b* buildpack_name</dt>
<dd>The name of the buildpack. The buildpack_name can be a custom buildpack by name or a Git URL, for example, `my-buildpack` or `https://github.com/heroku/heroku-buildpack-play.git`.</dd>
<dt>*-c* start_command</dt>
<dd>The start command of your application. To use the default start command, specify a value of null for this option. For example:</dd>
<dd>```
cf push appname -c null
```</dd>
<dd>You can also use this option to run script files. For example:
```
cf push appname -c “bash ./<run.sh>"
```</dd>
<dt>*-f* manifest_path</dt>
<dd>The path to the manifest file. The default manifest file is manifest.yml under the root directory of your application.</dd>
<dt>*-i* instance_number</dt>
<dd>The number of instances.</dd>
<dt>*-k* disk_limit</dt>
<dd>The disk limit for the application, for example, *256M*, *1024M*, or *1G*.</dd>
<dt>*-m* memory_limit</dt>
<dd>The memory limit for the application, for example, *256M*, *1024M*, or *1G*.</dd>
<dt>*-n* host_name</dt>
<dd>The host name for the application, for example, *my-subdomain*.</dd>
<dt>*-p* app_path</dt>
<dd>The path to the application directory or the application archive file.</dd>
<dt>*-t* timeout</dt>
<dd>Maximum time in seconds for the application to start. Other server-side timeouts might override this value.</dd>
<dt>*-s* stackname</dt>
<dd>The stack to run the apps. A stack is per-built file system including the operation system. Use `cf stacks` to view the available stacks in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*--no-hostname*</dt>
<dd>Maps the Bluemix system domain to this application.</dd>
<dt>*--no-manifest*</dt>
<dd>Ignores the default manifest file.</dd>
<dt>*--no-route*</dt>
<dd>Does not map a route to this application.</dd>
<dt>*--no-start*</dt>
<dd>Does not start the application after the application is deployed.</dd>
<dt>*--random-route*</dt>
<dd>Creates a random route for the application.</dd>
</dl>

## cf scale

Displays or changes the instance number, disk space limit, and memory limit for an application.
```
cf scale appname -i instance_number -k disk_limit -m memory_limit
```
<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
<dt>*-i* instance_number</dt>
<dd>The number of instances</dd>
<dt>*-k* disk_limit</dt>
<dd>The disk limit for the application, for example, *256M*, *1024M*, or *1G*.</dd>
<dt>*-m* memory_limit</dt>
<dd>The memory limit for the application, for example, *256M*, *1024M*, or *1G*.</dd>
<dt>*-f*</dt>
<dd>Forces the application to restart without prompt.</dd>
</dl>

## cf services

Lists all of the services that are available in the current space.
```
cf services
```

## cf set-env

Sets an environment variable for an application.
```
cf set-env appname var_name var_value
```
<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
<dt>var_name</dt>
<dd>The name of the environment variable.</dd>
<dt>var_value</dt>
<dd>The value of the environment variable.</dd>
</dl>

## cf stacks

Lists all stacks. A stack is a pre-built file system, including an operating system that can run apps.
```
cf stacks
```

## cf stop

Stops an application.
```
cf stop appname
```
<dl>
<dt>appname</dt>
<dd>The name of the application.</dd>
</dl>

## cf -v

Displays the version of the cf command line interface.
```
cf -v
```

# rellinks
{: #rellinks}
## general 
{: #general}
* [Quick Reference Card - cf commands](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
