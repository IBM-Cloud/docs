---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}

The Tomcat runtime on {{site.data.keyword.Bluemix}} is powered by the java_buildpack.
{: shortdesc}

To use the Tomcat runtime on {{site.data.keyword.Bluemix}}, you must specify the java_buildpack with the -b option. For example:
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

For more information about the Tomcat runtime, see the
[java-buildpack readme](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides a Tomcat starter application.  The Tomcat starter application is a simple Tomcat app that provides a template that you can use. You can experiment with the starter app, and make and push changes to the Bluemix environment. See [Using the starter applications](/docs/cfapps/starter_app_usage.html) for help with using the starter application.

## Runtime versions
{: #runtime_versions}

You can change the version of Tomcat to be used by your app with the JBP_CONFIG_TOMCAT environment variable.
You can change the version of Java to be used by your app with the JBP_CONFIG_OPEN_JDK_JRE environment variable.
Both of these can be specified in the application's manifest file.  For example:
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
The current java_buildpack version is v3.6 which contains default Tomcat version 8.30.0 and default Java version 1.8.0_71.
For more information please see [java-buildpack releases](https://github.com/cloudfoundry/java-buildpack/releases).

## HTTPS redirect
{: #https_redirect}

The Tomcat runtime can be configured to trust Bluemix internal proxies and allow the redirect of HTTP traffic to HTTPS (SSL).
To do so modify the server.xml file, setting the RemoteIpValve Valve element with internalProxies and protocolHeader options.

The Tomcat runtime [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml) included in the buildpack only sets the protocolHeader of the RemoteIpValve Valve element by default.  To redirect HTTP traffic to HTTPS in Bluemix configure the RemoteIpValve element in your custom server.xml as follows:

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

More configuration options for the RemoteIpValve can be found in the
[Tomcat documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://tomcat.apache.org/tomcat-8.0-doc/api/org/apache/catalina/valves/RemoteIpValve.html).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
