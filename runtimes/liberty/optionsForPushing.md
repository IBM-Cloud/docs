---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Options for pushing Liberty apps
{: #options_for_pushing}

*Last Updated: 23 March 2016*

The behavior of the Liberty server in Bluemix is controlled by the Liberty buildpack. Buildpacks can provide a complete runtime environment for a specific class of applications. They are key to providing portability across clouds and contributing to an open cloud architecture. The Liberty buildpack provides WebSphere Liberty container capable of running Java EE 7 and OSGi applications. It supports popular frameworks such as Spring and includes the IBM JRE. WebSphere Liberty enables rapid application development that is suited to the cloud. The Liberty buildpack supports multiple applications that are deployed into a single Liberty server. As part of the Liberty buildpack integration into Bluemix, the buildpack ensures that environment variables for binding services are shown as configuration variables in the Liberty server.

You can use the following methods to deploy your Liberty applications to Bluemix.

* Pushing a stand-alone application
* Pushing a server directory
* Pushing a packaged server

Important: When you deploy an application with the Liberty buildpack, specify a minimum of 512M as the memory limit for your applications. For more information, see [Memory limits and the Liberty buildpack](memoryLimits.html).

## Stand-alone apps
{: #stand_alone_apps}

Stand-alone applications such as WAR or EAR files can be deployed to Liberty in Bluemix.

To deploy a stand-alone application, run the cf push command with the -p parameter that points to your WAR or EAR file.
For example:

```
    $ cf push <yourappname> -p myapp.war
```
{: codeblock}

When a stand-alone application is deployed, a default Liberty configuration is provided for the application. The default configuration enables the following Liberty features:

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

These features correspond to the Java EE 7 Web Profile features. You can specify a different set of Liberty features by setting the JBP_CONFIG_LIBERTY environment variable. For example, to enable jsp-2.3 and websocket-1.1 features only, run the command and restage the application:

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: codeblock}

Note: For best results, set the Liberty features with the JBP_CONFIG_LIBERTY environment variable or deploy your application as a [server directory](optionsForPushing.html#server_directory) or [packaged server](optionsForPushing.html#packaged_server) with a custom server.xml file. Setting this environment variable ensures that your application uses only the feature that it needs and it is not affected by the buildpack's default Liberty feature set changes. If you need to provide extra Liberty configuration beyond the feature set, use the [server directory](optionsForPushing.html#server_directory) or the [packaged server](optionsForPushing.html#packaged_server) option to deploy your application.

If you deployed a WAR file, the web application is accessible under the context root as set in the embedded ibm-web-ext.xml file. If the ibm-web-ext.xml file does not exist, or does not specify the context root, the application is accessible under the root context. For example,

```
    http://<yourappname>.mybluemix.net/
```
{: codeblock}

If you deployed an EAR file, the embedded web application is accessible under the context root as defined in the EAR deployment descriptor. For example,

```
    http://<yourappname>.mybluemix.net/acme/
```
{: codeblock}

The entire default Liberty server.xml configuration file is as follows:
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: codeblock}

### CDI 1.2
{: #cdi12}

For performance reasons, when deploying WAR and EAR files only, the [CDI 1.2 implicit bean archives scanning](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html) is disabled by default. Implicit bean archive scanning can be enabled using the JBP_CONFIG_LIBERTY environment variable.
For example:

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: codeblock}

Important: In order for your environment variable changes to take effect you must restage your application:

```
    $ cf restage myapp
```
{: codeblock}

## Server directory
{: #server_directory}

In some cases, it might be necessary to provide a custom Liberty server configuration with your application. This custom configuration might be needed when you deploy a WAR or EAR file and the default server.xml file does not have the certain settings that your application needs.

If you installed the Liberty profile on your workstation and you already created a Liberty server with your application, you can push the contents of that directory to Bluemix.
For example, if your Liberty server is named defaultServer, run the command:

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer
```
{: codeblock}

If a Liberty profile is not installed on your workstation, you can use the following steps to create a server directory with your application:

1. Create a directory that is named defaultServer.
2. Create an apps directory in the defaultServer directory.
3. Copy your WAR or EAR file into the defaultServer/apps directory.
4. In the defaultServer directory, create a server.xml file with the example content that follows.  In addition:
  * Make sure to update the location or the type attribute of the application element to match the file name and the type of your application.
  * The server.xml file in the diagram shows a minimal feature set. You might have to adjust the feature set depending on your application's needs.

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id="defaultHttpEndpoint" host="*" httpPort="8080" />

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: codeblock}

After the server directory is ready, you can deploy it to Bluemix.

```
    $ cf push <yourappname> -p defaultServer
```
{: codeblock}

Note: The web applications that are deployed as part of the server directory are accessible under the [context root, as determined by the Liberty profile](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6). For example:

```
    http://<yourappname>.mybluemix.net/acme/
```
{: codeblock}

## Packaged server
{: #packaged_server}

You can also push a packaged server file to Bluemix. The packaged server file is created by using Liberty's server package command. In addition to the application and configuration files, the packaged server file can contain shared resources and Liberty user features needed by the application.

To package a Liberty server, use the ./bin/server package command from your Liberty installation directory. Specify your server name and include the '––include=usr' option.
For example, if your Liberty server is defaultServer, run the command:

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: codeblock}

This command generates a serverName.zip file in the server's directory. You can then push that compressed file to Bluemix with the cf push command.
For example:

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: codeblock}

Note: The web applications that are deployed as part of the packaged server are accessible under the context root, as determined by the Liberty profile.

### Modification of the server.xml file
{: #modifications_of_serverxml}

When a packaged server or a Liberty server directory is pushed, the Liberty buildpack detects the server.xml file along with your application. The Liberty buildpack makes the following modifications to the server.xml file.

* The buildpack ensures that there is exactly one httpEndpoint element in the file.
* The buildpack ensures that the httpPort attribute in the httpEndpoint element points to a system variable that is called ${port}. The buildpack also overrides the host attribute.
* The buildpack sets the logDirectory attribute in the logging element to point to a system log directory.
* The buildpack ensures that a runtime-vars.xml file is logically merged with your server.xml file. Specifically, the buildpack appends the line *&lt;include location="runtime-vars.xml" /&gt;* to your server.xml file.

### Referenceable variables
{: #referenceable_variables}

The following variables are defined in the runtime-vars.xml file, and referenced from a pushed server.xml file. All the variables are case-sensitive.

* ${port}: The HTTP port that the Liberty server is listening on.
* ${vcap_console_port}: The port where the vcap console is running (usually the same as ${port}).
* ${vcap_app_port}: The port where the app server is listening (usually the same as ${port}).
* ${vcap_console_ip}: The IP address of the vcap console (usually the IP address that the Liberty server is listening on).
* ${application_name}: The name of the application, as defined by using the options in the cf push command.
* ${application_version}: The version of this instance of the application, which takes the form of a UUID, such as b687ea75-49f0-456e-b69d-e36e8a854caa. This variable changes with each successive push of the application that contains new code or changes to the application artifacts.
* ${host}: The IP address of the DEA that is running the application (usually the same as ${vcap_console_ip}).
* ${application_uris}: A JSON-style array of the endpoints that can be used to access this application, for example: myapp.mydomain.com.
* ${start}: The time and date that the application was started, taking a form similar to 2013-08-22 10:10:18 -0400.

### Accessing information of bound services
{: #accessing_info_of_bound_services}

When you want to bind a service to your application, information about the service, such as connection credentials, is included in the [VCAP_SERVICES environment variable](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES) that Cloud Foundry sets for the application. For [automatically configured services](autoConfig.html), the Liberty buildpack generates or updates service binding entries in the server.xml file. The contents of the service binding entries can be in one of the following forms:

* cloud.services.&lt;service-name&gt;.&lt;property&gt;, which describes the information such as the name, type, and plan of the service.
* cloud.services.&lt;service-name&gt;.connection.&lt;property&gt;, which describes the connection information for the service.

The typical set of information is as follows:
* name: The name of the service. For example, mysql-e3abd.
label: The type of the created service. For example, mysql-5.5.
* plan: The service plan, as indicated by the unique identifier for that plan. For example, 100.
connection.name: A unique identifier for the connection, which takes the form of a UUID. For example, d01af3a5fabeb4d45bb321fe114d652ee.
* connection.hostname: The host name of the server that is running the service. For example, mysql-server.mydomain.com.
* connection.host: The IP address of the server that is running the service. For example, 9.37.193.2.
* connection.port: The port on which the service is listening for incoming connections. For example, 3306,3307.
* connection.user: The user name that is used to authenticate this application to the service. The user name is auto-generated by Cloud Foundry. For example: unHwANpjAG5wT.
* connection.username: An alias for connection.user.
* connection.password: The password that is used to authenticate this application to the service. The password is auto-generated by Cloud Foundry. For example: pvyCY0YzX9pu5.

For bound services that are not automatically configured by the Liberty buildpack, the application needs to manage the access of the backend resource on its own.

# rellinks
## general
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
