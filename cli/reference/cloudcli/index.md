{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}


# cloud-cli commands

*Last updated: 9 November 2015*

The {{site.data.keyword.IBM}} {{site.data.keyword.Bluemix}} command line interface, which is called cloud-cli, provides extra capabilities for service offerings.
{:shortdesc}

You can use cloud-cli to complete the following tasks:

* Create, update, and delete V2 service brokers.
* Register, list, and unregister templates.

*Note:* cloud-cli requires Java&trade 1.7.0.
You can download cloud-cli from {{site.data.keyword.Bluemix_notm}} to use on your local system as a complement to the {{site.data.keyword.Bluemix_notm}} user interface.

## Syntax

cloud-cli syntax differs from cf in that it has extra options to specify *targetURL*, *userID*, and *password* as command arguments instead of issuing separate target and login commands.

cloud-cli has the following syntax:
```
cloud-cli commandName [global_options] [command_options] [<args>]
```

## Parameters
<dl>
<dt>commandName</dt>
<dd>The specific cloud-cli command.</dd>
<dt>global_options</dt>
<dd>Options that are common for all commands.</dd>
<dt>command_options</dt>
<dd>Options that are specific to a particular command.</dd>
<dt>args</dt>
<dd>Arguments that are required for a command.</dd>
</dl>

## cloud-cli commands

You can specify one of the following commands for the commandName variable in the syntax:

<dl>
<dt>`login`</dt>
<dd>Log in to the Bluemix controller.</dd>
<dt>`logout`</dt>
<dd>Log out of the Bluemix controller.</dd>
<dt>`target`</dt>
<dd>Set the target URL for commands.</dd>
<dt>`create-service-broker`</dt>
<dd>Create a service broker.</dd>
<dt>`update-service-broker`</dt>
<dd>Update a service broker.</dd>
<dt>`delete-service-broker`</dt>
<dd>Delete a service broker.</dd>
<dt>`register-template`</dt>
<dd>Register a template. Overwrites any existing template registration.</dd>
<dt>`deregister-template`</dt>
<dd>Removes the template from the Bluemix registry.</dd>
<dt>`templates`</dt>
<dd>Removes the template from the Bluemix registry.</dd>
<dt>`version`</dt>
<dd>Displays the version number of cloud-cli.</dd>
<dt>`help`</dt>
<dd>Show command help.</dd>
</dl>

For help about a command, enter the following command:
```
cloud-cli help commandName
```
For example, enter the following command to get detailed information about the `update-application` command:
```
cloud-cli help update-application
```
Typically, you can use the following commands to log in to {{site.data.keyword.Bluemix_notm}} and then operates your applications:
```
cloud-cli target https://ace.stage1.ng.bluemix.net           - You need to enter this command only once
```
```
cf api https://api.stage1.ng.bluemix.net                     - You need to enter this command only once ```
```
cloud-cli login -userID <your user ID> -pw <yourPassword>      - You need to enter this command once per session 
```
```
cloud-cli commandName
```

Alternatively, you can use only one command to log in to {{site.data.keyword.Bluemix_notm}}:
```
cloud-cli commandName -userID <your user ID> -pw <yourPassword> - The login is not saved
```

## Global options

The following options can be used for any cloud-cli commands.
<dl>
<dt>*target* targetURL</dt>
<dd>The URL of the {{site.data.keyword.Bluemix_notm}} Server, usually http://ace.{{site.data.keyword.domainname}}. This is an alternative to using the target command.</dd>
<dt>*userID* yourUserID</dt>
<dd>The {{site.data.keyword.Bluemix_notm}} user ID. This is an alternative to using the login command to log in.</dd>
<dt>*pw* yourPassword</dt>
<dd>The user's password for {{site.data.keyword.Bluemix_notm}}. This is an alternative to using the login command to log in.</dd>
<dd>*Important:* If you provide your password by using the *pw* parameter, the password might be recorded in the command history and might be visible to other users of the local operating system. For security reasons, avoid providing the password by using the parameter. Instead, enter the password when the command line interface prompts you.</dd>
</dl>

## target
```
cloud-cli target BlueMixServerURL 
```
Use this command to set the URL of the {{site.data.keyword.Bluemix_notm}} server that subsequent commands target. Typically, the BlueMixServerURL is https://console.{{site.data.keyword.domainname}}. The URL that is specified for the target command is saved, so you do not have to enter the command again until you want to specify a different target.

## login
```
cloud-cli login [global_options] [command_options]
```
Use this command to log in to {{site.data.keyword.Bluemix_notm}}. The login needs to be done only one time per session. An alternative to the `login` command is to pass the `-userID` and `-pw` parameters on individual commands. You must set the URL of the {{site.data.keyword.Bluemix_notm}} server by using the `cloud-cli target` command and specify the URL of the cf API endpoint by using the `cf api` command before your login.

You can use the following options to specify your user id and password:
<dl>
<dt>*userID* yourUserID</dt>
<dd>The {{site.data.keyword.Bluemix_notm}} user ID.</dd>
<dt>*pw* yourPassword</dt>
<dd>The user's password for {{site.data.keyword.Bluemix_notm}}.</dd>
<dd>*Important:* If you provide your password by using the pw parameter, the password might be recorded in the command history and might be visible to other users of the local operating system. For security reasons, avoid providing the password by using the parameter. Instead, enter the password when the command line interface prompts you.</dd>
</dl>

## logout
```
cloud-cli logout
```
Use this command to log out of cloud controller.

## create-service-broker
```
cloud-cli create-service-broker [global_options] [command_options] serviceBrokerJsonFile
```

If you are using the V2 {{site.data.keyword.Bluemix_notm}} Service Broker, use this command to register a new service broker with {{site.data.keyword.Bluemix_notm}}, where the *serviceBrokerJsonFile* file contains the definition of the service broker.

If you do not want to provide billing information for the service broker, you can use the `-noBilling` command option.

## update-service-broker
```
cloud-cli update-service-broker [global_options] [command_options] serviceBrokerJsonFile
```
Use this command to update a V2 service broker that has been registered with {{site.data.keyword.Bluemix_notm}}.
<dl>
<dt>originalName</dt>
<dd>The original name of the service broker. This option is required only if you rename the service broker.</dd>
</dl>

## delete-service-broker
```
cloud-cli delete-service-broker [global_options] [command_options] serviceBrokerName
```
Use this command to delete a V2 service broker from {{site.data.keyword.Bluemix_notm}}.

## register-template
```
cloud-cli register-template [global_options] [command_options] templateId
```
Use this command to register template metadata with {{site.data.keyword.Bluemix_notm}}. This command overwrites existing template or creates a new one.
<dl>
<dt>*url* arg</dt>
<dd>The URL of the template metadata.</dd>
</dl>

## deregister-template
```
cloud-cli deregister-template [global_options] templateId
```
Use this command to unregister template metadata with {{site.data.keyword.Bluemix_notm}}. This command runs even if the template does not exist.

## templates
```
cloud-cli templates [global_options]
```
Use this command to get the template registry of the template IDs and metadata URLs.

## version
```
cloud-cli version [global_options]
```
Use this command to display the version of the command line.

## help
```
cloud-cli help commandName
```
Use this command to get help information that is specific to *commandName*.

