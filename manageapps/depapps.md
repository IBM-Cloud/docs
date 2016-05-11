---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Deploying apps
{: #deployingapps}

*Last updated: 9 May 2016*

You can deploy applications to {{site.data.keyword.Bluemix}} by using various methods, such as the command line interface and integrated development environments (IDEs). You can also use application manifests to deploy applications. By using an application manifest, you reduce the number of deployment details that you must specify every time that you deploy an application to {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

##Application deployment
{: #appdeploy}

Deploying an application to {{site.data.keyword.Bluemix_notm}} includes two phases, staging the application and starting the application.

###Staging an application

During the staging phase, a droplet execution agent (DEA) uses the information that you provide in the cf command line interface or the `manifest.yml` file to decide what to create for application staging. The DEA selects an appropriate buildpack to stage your application, and the result of the staging process is a droplet. For more information about deploying an application to {{site.data.keyword.Bluemix_notm}}, see [{{site.data.keyword.Bluemix_notm}} architecture, How {{site.data.keyword.Bluemix_notm}} works](../public/index.html#publicarch).

During the staging process, the DEA checks whether the buildpack matches the application. For example, a Liberty runtime for a .war file, or a Node.js runtime for .js files. The DEA then creates an isolated container that contains the buildpack and the application code. The container is managed by the Warden component. For more information, see [How Applications Are Staged](http://docs.cloudfoundry.org/concepts/how-applications-are-staged.html){:new_window}.

###Starting an application

When an application is started, the instance or instances of the warden container are created. You can use the **cf files** command to see the files that are stored on the file system of the Warden container, such as the logs. If the application fails to start, the DEA stops the application and the entire contents of your Warden container are removed. Therefore, if an application stops or if the staging process of an application fails, log files will not be available for you to use.

If the logs for your application are no longer available so that the **cf files** command can no longer be used to see the cause of the staging errors, you can use the **cf logs** command instead. The **cf logs** command uses the Cloud Foundry log aggregator to collect the details of your application logs and system logs, and you can see what was buffered within the log aggregator. For more information about the log aggregator, see [Logging in Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.

**Note:** The buffer size is limited. If an application runs for a long time and is not restarted, logs might not be displayed when you enter `cf logs appname --recent` because the log buffer might have been cleared. Therefore, to debug staging errors for a large application, you can enter `cf logs appname` in a separate command line from the cf command line interface to track the logs when you deploy the application.

If you experience problems when you stage your applications on {{site.data.keyword.Bluemix_notm}}, you can follow the steps in [Debugging staging errors](../debug/index.html#debugging-staging-errors) to resolve the problem.

##Deploying applications by using the cf command
{: #dep_apps}

When you deploy your applications to {{site.data.keyword.Bluemix_notm}} from the command line interface, a buildpack must be provided as the runtime environment according to your application language and framework. You can also use the Delivery Pipeline service to deploy applications to {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} provides built-in buildpacks that support Java and Node.js. If you are using these languages and frameworks, you don't need to specify the buildpack when you deploy your application by using the command line interface. Because {{site.data.keyword.Bluemix_notm}} is built on Cloud Foundry, the command defaults to these buildpacks.

If you use an external buildpack, you must specify the URL of the buildpack by using the **-b** option when you deploy your application to {{site.data.keyword.Bluemix_notm}} from the command prompt.

  * To deploy Liberty server packages to {{site.data.keyword.Bluemix_notm}}, use the following command from your source directory:
  
  ```
  cf push
  ```
  
  For more information about Liberty Buildpack, see [Liberty for Java](../runtimes/liberty/index.html).
  
  * To deploy Java Tomcat applications to {{site.data.keyword.Bluemix_notm}}, use the following command:
  
  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```
  
  * To deploy WAR packages to {{site.data.keyword.Bluemix_notm}}, use the following command:
  
  ```
  cf push appname -p app.war
  ```
  Or, you can specify a directory that contains your application files by using the following command:
  
  ```
  cf push appname -p "./app"
  ```
  
  * To deploy Node.js applications to {{site.data.keyword.Bluemix_notm}}, use the following command:
  
  ```
  cf push appname -p app_path
  ```
  
A `package.json` file must be in your Node.js application for the application to be recognized by the Node.js buildpack. The `app.js` file is the entry script for the application, and can be specified in the `package.json` file. The following example shows a simple `package.json` file:

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```
    
  For more information about the `package.json` file, see [package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window}.
  
  * To deploy PHP, Ruby, or Python applications to {{site.data.keyword.Bluemix_notm}}, use the following command from the directory that contains your application source:
  
  ```
  cf push appname
  ```

###Deploying an app in multiple spaces

An app is specific to the space where it is deployed. You can't move or copy an app from one space to another in {{site.data.keyword.Bluemix_notm}}. To deploy an app in multiple spaces, you must deploy your app in each space where you want to use the app by the following steps:

  1. Switch to the space where you want to deploy your app by using the **cf target** command with the **-s** option:
  
  ```
  cf target -s <space_name>
  ```
  
  2. Go to your app directory and deploy your app by using the **cf push** command, where appname must be unique within your domain.
  
  ```
  cf push appname
  ```
  
##Application manifest
{: #appmanifest}

Application manifests contain options that are applied to the **cf push** command. You can use an application manifest to reduce the number of deployment details that you must specify every time that you push an application to {{site.data.keyword.Bluemix_notm}}.

In application manifests, you can specify options such as the number of application instances to create, the amount of memory and disk quota to allocate to applications, and other environment variables for the application. You can also use application manifests to automate application deployments. The default name of a manifest file is `manifest.yml`.

###Supported options in the manifest file

The following table shows the supported options that you can use in an application manifest file. If you choose to use a different file name other than `manifest.yml`, you must use the **-f** option with the **cf push** command. In the following example, `appManifest.yml` is the file name:

```
cf push -f appManifest.yml
```

<p>  </p>


|Options	|Description	|Usage or example|
|:----------|:--------------|:---------------|
|**buildpack**	|The URL or name of the custom buildpack.	|`buildpack:` *buildpack_URL*|
|**disk_quota**	|The disk quota that is allocated for an application. The default value is 1 G.	|`disk_quota: 500M`|
|**domain**	|The domain name of the application in {{site.data.keyword.Bluemix_notm}}.	|`domain:` ng.bluemix.net|
|**host**	|The host name of the application in {{site.data.keyword.Bluemix_notm}}. This value must be unique in the {{site.data.keyword.Bluemix_notm}} environment.	|`host:` *host_name*|
|**name**	|The application name in {{site.data.keyword.Bluemix_notm}}. This value must be unique in the {{site.data.keyword.Bluemix_notm}} environment.	|`name:` *appname*|
|**path**	|The location of your application. This value can be a relative path or absolute path.	|`path:` *path_to_application*|
|**command**	|The custom start command for your application, or the command to run script files.	|`command:` *custom_command* `command:` *bash ./run.sh*|
|**memory**	|The amount of memory to allocate for the application. The default value is 1G.	|`memory: 512M`|
|**instances**	|The number of instances to be created for your application.	|`instances: 2`|
|**timeout**	|The maximum amount of time in seconds that is used to start the application. The default value is 60 seconds.	|`timeout: 80`|
|**no-route**	|A Boolean value to prevent a route from being assigned to the application if the application is just running background. The default value is **false**.	|`no-route: true`|
|**random-route**	|A Boolean value to assign a random route to the application. The default value is **false**.	|`random-route: true`|
|**services**	|The services to bind to the application.	|`services: - mysql_maptest`|
|**env**	|The custom environment variables for the application.|`env: DEV_ENV: production`|
*Table 1. Supported options in the manifest.yml file*

###A sample `manifest.yml` file

The following example shows a manifest file for a Node.js application that uses the built-in community Node.js buildpack in {{site.data.keyword.Bluemix_notm}}.

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

##Environment variables
{: #app_env}

Environment variables contain the environment information of a deployed application on {{site.data.keyword.Bluemix_notm}}. Besides environment variables set by a *Droplet Execution Agent (DEA)* and buildpacks, you can also set application-specific environment variables for applications on {{site.data.keyword.Bluemix_notm}}.

You can view the following environment variables of a running {{site.data.keyword.Bluemix_notm}} application by using the **cf env** command or from the {{site.data.keyword.Bluemix_notm}} user interface:
	
  * User-defined variables that are specific for an application. For information about how to add a user-defined variable to an app, see [Adding user-defined environment variables](#ud_env){:new_window}.
	 
  * The VCAP_SERVICES variable, which contains connection information to access a service instance. If your application is bound to multiple services, the VCAP_SERVICES variable includes the connection information for each service instance. For example:
  
  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```
        
You also have access to the environment variables that are set by the DEA and buildpacks.

The following variables are defined by the DEA:

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>The root directory of the deployed application.</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>The maximum amount of memory that each instance of your application can use. You can specify the value in an application <span class="ph filepath">manifest.yml</span> file, or on the command line when you push the application.</dd>
  <dt><strong>PORT</strong></dt>
  <dd>The port on the DEA for communication with the application. The DEA allocates a port to the application at staging time.</dd>
  <dt><strong>PWD</strong></dt>
  <dd>The current working directory where the buildpack is running.</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>The directory where temporary and staging files are stored.</dd>
  <dt><strong>USER</strong></dt>
  <dd>The user ID under which the DEA runs.</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>The IP address of the DEA host.</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>A JSON string that contains information about the deployed application. The information includes the application name, URIs, memory limits, time stamp at which the application achieved its current state, and so on. For example: 
  <pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>A JSON string that contains information of the service that is bound to the deployed application. For example:
  <pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
            "tags": [
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

Variables that are defined by buildpacks are different for each buildpack. See [Buildpacks](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window} for any other compatible buildpacks.

<ul>
    <li>The following variables are defined by the Liberty Buildpack:
	
	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>The location of Java SDK that runs the application.</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>The Java SDK options to use when running the application.</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>The Java command to start up a Liberty profile server instance in the DEA.</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>The location of shared resources and server definitions when starting up a Liberty profile server instance in the DEA.</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>The location of generated output such as log files and working directory of a running Liberty profile server instance.</dd>
	  </dl>
</li>   
<li>The following variables are defined by the Node.js Buildpack:
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>The directory of the Node.js runtime environment.</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>The directory that the Node.js runtime environment uses for caching.</dd>
	<dt><strong>PATH</strong></dt>
	<dd>The system path that is used by the Node.js runtime environment.</dd>
	</dl>
</li>
</li>
</ul>	

You can use the following sample Node.js code to get the value of the VCAP_SERVICES environment variable:

```
if (process.env.VCAP_SERVICES) {
    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

For more information about each environment variable, see [Cloud Foundry Environment Variables](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

## Customizing application deployments
{: #customize_dep}

You can customize deployment tasks for your applications. For example, you can specify the start commands for your applications, and you can configure your application startup environment.
{:shortdesc}

### Specifying start commands

To specify start commands for your application, you can use one of the following ways. The start commands that you specify will overwrite the default start commands that the buildpack provides.

**Note:** If you want the buildpack start commands to take precedence, specify **null** as the start command.

  * Use the **cf push** command and specify the -c parameter. For example, when you deploy a Node.js application, you can specify the **node app.js** start command on the -c parameter:
  
  ```
  cf push appname -p app_path -c "node app.js"
  ```
  
  * Use the command parameter in the `manifest.yml` file. For example, when you deploy a Node.js application, you can specify the **node app.js** start command in the manifest file:
  
  ```
  command: node app.js
  ```
  

### Adding user-defined environment variables
{: #ud_env}

User-defined environment variables are specific for an application. You have the following options to add a user-defined environment variable to a running app:

  * Use the {{site.data.keyword.Bluemix_notm}} user interafce. Complete the following steps:
    1. On the {{site.data.keyword.Bluemix_notm}} Dashboard, click your app tile. The App details page is displayed.
	2. On the left navigation pane, click **Environment Variables**.
	3. Click **USER-DEFINED**, then click **ADD**.
	4. Fill in the required fields, then click **SAVE**.
  * Use the cf command line interface. Add a user-defined variable by using the `cf set-env` command. For example: 
    ```
    cf set-env appname env_var_name env_var_value
    ```
	
  * Use the `manifest.yml` file. Add value pairs in the file. For example: 
    ```
	env:
      VAR1:value1
      VAR2:value2
    ```
	
After you have added a user-defined environment variable, you can use the following sample Node.js code to get the value of the variable that you defined:

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```
	
### Configuring the startup environment

To configure the startup environment for your application, you can add shell scripts into the `/.profile.d` directory. The `/.profile.d` directory is under the build directory of your application. Scripts in the `/.profile.d` directory are run by {{site.data.keyword.Bluemix_notm}} before the application is run. For example, you can set the NODE_ENV environment variable to **production** by putting a `node_env.sh` file that contains the following content under the `/.profile.d` directory:

```
export NODE_ENV=production;
```

###Preventing files and directories from being uploaded

When you use the cf command line interface to deploy an application, you can save upload time by skipping certain files and directories that {{site.data.keyword.Bluemix_notm}} can obtain elsewhere. To prevent these files and directories from being uploaded to {{site.data.keyword.Bluemix_notm}}, you can create a `.cfignore` file at the root directory of your application.

**Note:** The `.cfignore` file must be in UTF-8 format.

The `.cfignore` file contains the names of files and directories that you want to ignore, one name per line. You can use an asterisk (*) as a wildcard character. When you specify a directory, all files and subdirectories under that directory are ignored also. For example, the following content in the `.cfignore` file indicates that all the `.swp` files and all files and subdirectories under the `tmp/` directory won't be uploaded to {{site.data.keyword.Bluemix_notm}}.

```
*.swp
tmp/
```

# Related Links
{: #rellinks}

## Related Links
{: #general}

* [Deploying with Application Manifests](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator](http://cfmanigen.mybluemix.net/){:new_window}
* [Getting Started with cf v6](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Getting Started with IBM Continuous Delivery Pipeline for Bluemix](../services/DeliveryPipeline/index.html#getstartwithCD)
