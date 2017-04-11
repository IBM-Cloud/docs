---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Working with a proxy
{: #working_with_proxy}



In some environments such as [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) and
[Bluemix Local](/docs/local/index.html#local) a proxy may be configured which effects the
behavior of your application during staging and runtime.

You can configure your application to work with the proxy using the following environment variables:
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

You can set these environment variables using *cf se* or via the *manifest.yml* file.  If your application requires
resources to be downloaded from the internet during staging and a proxy environment variable is set,  then depending
on how the proxy environment variables are configured your resources will be donwloaded via the configured proxy.

For example, suppose you have a nodejs application and are running in an environment with *http_proxy* set to
*yourProxyURL*.  Furthermore suppose you do want to allow npm to download node modules from the internet. To achieve this you
could set *no_proxy* to *npmjs.org*.

**Note**: It may be the case that your application takes advantage of the proxy during runtime.  This is entirely application
dependent and unaffected by the buildpack and any of these three environment variables.

## Java applications
{: #java_apps}

For [Liberty for Java](/docs/runtimes/liberty/index.html) and the [java_buildpack](/docs/runtimes/tomcat/index.html) applications the proxy settings can be passd to the runtime via the **JAVA_OPTS** environment variable.  For example you can issue the command:
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

and restage your application.  Your application will then use the specified proxy settings at runtime. See [Java Networking and Proxies](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html) for more information about the Java proxy options.

# rellinks
{: #rellinks notoc}
## general
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
