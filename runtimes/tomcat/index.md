---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}
*Last updated: 19 March 2016*

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

{{site.data.keyword.Bluemix}} provides a Tomcat starter application.  The Tomcat starter application is a simple Tomcat app that provides a template that you can use. You can experiment with the starter app, and make and push changes to the Bluemix environment. See [Using the starter applications](../../cfapps/starter_app_usage.html) for help with using the starter application.

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
The current default Tomcat version is 8.0.30.  The current default Java version is 1.8.0_65.
For more information please see [java-buildpack releases](https://github.com/cloudfoundry/java-buildpack/releases).

# rellinks
## general
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
