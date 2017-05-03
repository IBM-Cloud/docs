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

{{site.data.keyword.Bluemix}} 上的 Tomcat 运行时由 java_buildpack 提供技术支持。
{: shortdesc}

要在 {{site.data.keyword.Bluemix}} 上使用 Tomcat 运行时，必须使用 -b 选项指定 java_buildpack。例如：
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

有关 Tomcat 运行时的更多信息，请参阅
[java-buildpack 自述文件](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md)。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了 Tomcat 入门模板应用程序。Tomcat 入门模板应用程序是一个简单的 Tomcat 应用程序，它提供了一个可供您使用的模板。您可以体验该入门模板应用程序，对其进行更改并将更改推送到 Bluemix 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](/docs/cfapps/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

您可以使用 JBP_CONFIG_TOMCAT 环境变量来更改应用程序要使用的 Tomcat 版本。
可以使用 JBP_CONFIG_OPEN_JDK_JRE 环境变量来更改应用程序要使用的 Java 版本。
这两个环境变量都可以在应用程序的清单文件中指定。例如：
```
env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
当前的 java_buildpack 版本为 V3.6，其中包含缺省 Tomcat V8.30.0 和缺省 Java V1.8.0_71。有关更多信息，请参阅 [java-buildpack 发行版](https://github.com/cloudfoundry/java-buildpack/releases)。

## HTTPS 重定向
{: #https_redirect}

Tomcat 运行时可以配置为信任 Bluemix 内部代理，并允许将 HTTP 流量重定向为 HTTPS (SSL)。
要执行该操作，请修改 server.xml 文件，使用 internalProxies 和 protocolHeader 选项设置 RemoteIpValve Valve 元素。

该 buildpack 中包含的 Tomcat 运行时 [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml)在缺省情况下，仅设置 RemoteIpValve Valve 元素的 protocolHeader。要在 Bluemix 中将 HTTP 流量重定向为 HTTPS，请在定制 server.xml 中如下配置 RemoteIpValve 元素：

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

在 [Tomcat 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://tomcat.apache.org/tomcat-8.0-doc/api/org/apache/catalina/valves/RemoteIpValve.html) 中可以找到 RemoteIpValve 的更多配置选项。

# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
