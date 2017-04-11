---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Managing Liberty and Node.js apps
{: #app_management}


App Management is a set of development and debugging utilities that can be enabled for your Liberty and Node.js applications on {{site.data.keyword.Bluemix}}.
{:shortdesc}

## App Management utilities
{: #Utilities}

### These utilities support both Liberty and Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

The *proxy* provides minimal application management between your application and {{site.data.keyword.Bluemix_notm}}.

When enabled, the buildpack starts a proxy agent that is located between your application's runtime and container. The *proxy* utility handles all requests that the application receives. Based on the type of request, it either performs an App Management action or forwards the request to your application. The *proxy* allows enablement of most other App Management utilities. By enabling *proxy*, your application container continues to live even if the application crashes. The proxy agent also allows for incremental file updates, which enables the "Live Edit" mode for Node.js applications.

#### noproxy
{: #noproxy}

The *noproxy* utility disables the *proxy* utility when it would have been automatically started by one of the other utilities. With Diego, the proxy is not necessary because Diego provides the capability to *ssh* directly to your application and set up port forwarding.

The *noproxy* utility is only applicable to applications running in a Diego cell.



#### devconsole
{: #devconsole}

The (*devconsole*) development console utility lets users restart, stop, or suspend their applications. Users can also enable or access the shell and inspector utilities.  It is accessible at the following URL:
```
  https://<yourappname>.mybluemix.net/bluemix-debug/manage
```

For Node version 6.3.0 or greater the development console provides a restart button for your application and access to the shell utility.  See the *inspector* discussion for more information.

The *devconsole* utility also starts *proxy*.

#### hc
{: #hc}

The (*hc*) Health Center agent enables your application to be monitored by the Health Center client.

The Health Center supports analyzing the performance of your Liberty and Node.js applications by using the IBM Monitoring and Diagnostic Tools. For more information see [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}} ![External link icon](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){: new_window}.</p></li>

The *hc* utility also starts *proxy*.

The *hc* utility can be used in conjunction with *noproxy*. To use Health Center with *noproxy*, first establish port forwarding using the `cf ssh` command. For example:

```
$ cf ssh -N -T -L 1883:127.0.0.1:1883 <appName>
```

Next, to connect with the Health Center client, use [MQTT connection ![External link icon](../icons/launch-glyph.svg)](http://www.ibm.com/support/knowledgecenter/SS3KLZ/com.ibm.java.diagnostics.healthcenter.doc/topics/connectingtojvm.html){: new_window} and specify the host as `127.0.0.1` and port as `1883`.

#### shell
{: #shell}

The *shell* utility enables a web-based shell.  It is accessible from the *devconsole* utility or by accessing the following URL:

```
  https://<yourappname>.mybluemix.net/bluemix-debug/shell
```

A terminal window is displayed with shell access into your application after you access the *shell* utility. You can do everything that is supported in a regular shell, such as editing files, checking memory usage or running diagnostic commands.

The *shell* utility also starts *proxy*.

Diego provides an interactive shell through the `cf ssh` command, so the *shell* utility is only useful to applications running on a DEA.

### These utilities support Liberty only
{: #liberty_utilities}

#### debug
{: #debug}

The *debug* utility puts the Liberty application into debug mode and enables clients such as the IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} to establish a [remote debugging](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug) session with the application.

The *debug* utility also starts *proxy*.

The *debug* utility can be used in conjunction with *noproxy*. To use debugger with *noproxy*, first establish port forwarding using the `cf ssh` command. For example:

```
$ cf ssh -N -T -L 7777:127.0.0.1:7777 <appName>
```

Next, to connect in Eclipse, use "Remote Java Configuration" and specify the host as `127.0.0.1` and port as `7777`.

#### jmx
{: #jmx}

The *jmx* utility enables the JMX REST Connector to allow a remote JMX client to manage the application by using {{site.data.keyword.Bluemix_notm}} user credentials.

For more information on configuring a JMX connector, see [Configuring secure JMX connection to the Liberty profile ![External link icon](../icons/launch-glyph.svg)](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.

The *jmx* utility does not start proxy.

#### localjmx
{: #localjmx}

The *localjmx* utility enables the [localConnector-1.0 ![External link icon](../icons/launch-glyph.svg)](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feature_localConnector-1.0.html){:new_window} Liberty feature. Combined with local port forwarding, this enables an alternate way of allowing a remote JMX client to manage the application.

The *localjmx* utility is only applicable to applications running on a Diego cell. To use *localjmx*, first establish port forwarding using the `cf ssh` command. For example:

```
$ cf ssh -N -T -L 5000:127.0.0.1:5000 <appName>
```

Next, to connect with JConsole, choose "Remote Process", specify `127.0.0.1:5000`, and use an insecure connection.


### These utilities support Node.js only
{: #node_utilities}

#### inspector
{: #inspector}

For Node.js versions prior to 6.3.0, *inspector* enables the node inspector debugger interface. The *inspector* process runs in your application container. Use this utility to create CPU usage profiles, add breakpoints, and debug code, all while your application is running on {{site.data.keyword.Bluemix_notm}}. For more information about the node inspector module, see [node-inspector on GitHub ![External link icon](../icons/launch-glyph.svg)](https://github.com/node-inspector/node-inspector){:new_window}.

For Node.js versions 6.3.0 and greater, the *inspector* utilizes the [V8 Inspector Integration for Node.js ![External link icon](../icons/launch-glyph.svg)](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}.

The inspector utility starts *proxy* by default, but how you remotely debug will depend on the Node.js version and usage of *proxy* or *noproxy*.  The table that follows shows how to access remote debugging in the various scenarios.

| | proxy | noproxy |
|---|---|---|
| < &nbsp; 6.3.0 | devconsole utility *at*<br/> https://myApp.mybluemix.net/bluemix-debug/inspector | http://127.0.0.1:8790
| >= 6.3.0 | chrome-devtools URL | chrome-devtools URL

For *noproxy* and Node.js version prior to 6.3.0 enable access to the URL via local port forwarding. For example:

```
$ cf ssh -N -T -L <localPort>:127.0.0.1:8790 <appName>
```

Then browse to http://127.0.0.1:8790 in your Chrome web browser.  Change the port by setting the BLUEMIX_APP_MGMT_INSPECTOR environment variable:

```
$ cf set-env <appName> BLUEMIX_APP_MGMT_INSPECTOR='{port: 9790}'
```

For Node.js version 6.3.0 or greater you will find a log message with a URL that can be used to attach your Chrome DevTools to your app. The log messages will be similar to the following:

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

Enable access to the URL via local port forwarding. For example:

```
$ cf ssh -N -T -L 9229:127.0.0.1:9229 <appName>
```

You will need an up-to-date version of the Chrome web browser to browse to this URL. The proxy will not route traffic to the inspector in this scenario.

#### trace
{: #trace}

The *trace* utility allows you to dynamically sets trace levels if your application is using *log4js*, *ibmbluemix*, or *bunyan* logging modules.

**Note:** Supported dependency versions:
* log4js:(0.6.0 - 0.6.24)
* bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)

Go to the Instance Details page in the {{site.data.keyword.Bluemix_notm}} web console and select **Actions** to see the UI.

The *trace* utility is not available when the application was started using the "-b buildpack" option.

The *trace* utility does not start *proxy*.

##  How to configure App Management
{: #configure}

To enable App Management utilities, set the *BLUEMIX_APP_MGMT_ENABLE* environment variable and restage your application. Multiple utilities can be enabled by separating them with a "+".

For example, to enable *devconsole* and *shell* utilities, run the following command:

```
$ cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Restage your application after you set the environment variable:

```
$ cf restage myApp
```

If you do not want the App Management utilities to be installed with your application, set the *BLUEMIX_APP_MGMT_INSTALL* environment variable to 'false' and restage your application.

For example:

```
$ cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
$ cf restage myApp
```

## Restrictions
{: #restrictions}

* App Management supports only single-instance applications when the application is running on a DEA node.
* Changes that you make to your application using App Management are transient, and are lost after exiting this mode. This mode is only for temporary development use, and is not intended to be used as a production environment due to performance.
* Most App Management utilities do not work if you set your start command in the `manifest.yml` file (command) or CF CLI (-c). Those methods are buildpack overrides, and are anti-patterns for starting Node.js applications. For best results, set the start command in the `package.json` file or `Procfile`.

## Development Mode for Eclipse Tools
{: #devmode}

Development mode is a feature of the [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) that gives developers the ability to work with their applications while they are running in the cloud.

While working with their applications on {{site.data.keyword.Bluemix_notm}}, developers might feel that they cannot perform normal development activities as they might on a local environment. To tackle this issue, development mode through Eclipse Tools provides a way for you to work in the cloud while in a temporary, secure workspace.

Development mode is supported for both Liberty and Node.js applications. With development mode enabled for your Liberty or Node.js application, you can update application files incrementally without having to push your application. You can also establish a debugging session with your application. Development mode for Liberty applications is equivalent to enabling the debug and jmx App Management utilities. For Node.js applications, it is equivalent to enabling the *devconsole*, *inspector*, and *shell* utilities.
