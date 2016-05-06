---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}
*上次更新时间：2016 年 3 月 19 日*

{{site.data.keyword.Bluemix}} 上的 Tomcat 运行时由 java_buildpack 提供技术支持。
{: shortdesc}

要在 {{site.data.keyword.Bluemix}} 上使用 Tomcat 运行时，必须使用 -b 选项指定 java_buildpack。例如：
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

有关 Tomcat 运行时的更多信息，请参阅 [java-buildpack 自述文件](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md)。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了 Tomcat 入门模板应用程序。Tomcat 入门模板应用程序是一个简单的 Tomcat 应用程序，它提供了一个可供您使用的模板。您可以体验该入门模板应用程序，对其进行更改并将更改推送到 Bluemix 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

您可以使用 JBP_CONFIG_TOMCAT 环境变量来更改应用程序要使用的 Tomcat 版本。可以使用 JBP_CONFIG_OPEN_JDK_JRE 环境变量来更改应用程序要使用的 Java 版本。这两个环境变量都可以在应用程序的清单文件中指定。例如：
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
当前缺省 Tomcat 版本为 8.0.30。当前缺省 Java 版本为 1.8.0_65。有关更多信息，请参阅 [java-buildpack 发行版](https://github.com/cloudfoundry/java-buildpack/releases)。

# 相关链接
## 常规
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
