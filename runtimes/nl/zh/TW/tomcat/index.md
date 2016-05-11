---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}
*前次更新：2016 年 3 月 19 日*

{{site.data.keyword.Bluemix}} 上的 Tomcat 執行時期是採用 java_buildpack 技術。
{: shortdesc}

若要在 {{site.data.keyword.Bluemix}} 上使用 Tomcat 執行時期，您必須指定 java_buildpack 並搭配 -b 選項。例如：
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

如需 Tomcat 執行時期的相關資訊，請參閱
[java-buildpack ReadMe](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md)。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Tomcat 入門範本應用程式。Tomcat 入門範本應用程式是簡單的 Tomcat 應用程式，提供可以讓您使用的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 Bluemix 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

您可以使用 JBP_CONFIG_TOMCAT 環境變數來變更應用程式要使用的 Tomcat 版本。
您可以使用 JBP_CONFIG_OPEN_JDK_JRE 環境變數來變更應用程式要使用的 Java 版本。
這兩者都可以在應用程式的資訊清單檔中予以指定。例如：
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
現行預設 Tomcat 版本是 8.0.30。現行預設 Java 版本是 1.8.0_65。
如需相關資訊，請參閱 [java-buildpack 版本](https://github.com/cloudfoundry/java-buildpack/releases)。

# 相關鏈結
## 一般
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
