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

{{site.data.keyword.Bluemix}} 上的 Tomcat 運行環境是採用 java_buildpack 技術。
{: shortdesc}

若要在 {{site.data.keyword.Bluemix}} 上使用 Tomcat 運行環境，您必須指定 java_buildpack 並搭配 -b 選項。例如：
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

如需 Tomcat 運行環境的相關資訊，請參閱
[java-buildpack ReadMe](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md)。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Tomcat 入門範本應用程式。Tomcat 入門範本應用程式是簡單的 Tomcat 應用程式，提供可以讓您使用的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 Bluemix 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](/docs/cfapps/starter_app_usage.html)。

## 運行環境版本
{: #runtime_versions}

您可以使用 JBP_CONFIG_TOMCAT 環境變數來變更應用程式要使用的 Tomcat 版本。您可以使用 JBP_CONFIG_OPEN_JDK_JRE 環境變數來變更應用程式要使用的 Java 版本。這兩者都可以在應用程式的資訊清單檔中予以指定。例如：
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
最新的 java_buildpack 版本為 3.6 版，其中包含預設的 Tomcat 8.30.0 版和預設的 Java 1.8.0_71 版。如需相關資訊，請參閱 [java-buildpack 版本](https://github.com/cloudfoundry/java-buildpack/releases)。

## HTTPS 重新導向
{: #https_redirect}

Tomcat 運行環境可以配置成信任 Bluemix 內部 Proxy，並容許將 HTTP 資料流量重新導向至 HTTPS (SSL)。
若要這樣做，請設定 RemoteIpValve Valve 元素與 internalProxies 及 protocolHeader 選項來修改 server.xml 檔案。

建置套件中所含的 Tomcat 運行環境 [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml)，預設只會設定 RemoteIpValve Valve 元素的 protocolHeader。若要在 Bluemix 中將 HTTP 資料流量重新導向至 HTTPS，請在自訂 server.xml 中配置 RemoteIpValve 元素，如下所示：

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

您可以在 [Tomcat 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://tomcat.apache.org/tomcat-8.0-doc/api/org/apache/catalina/valves/RemoteIpValve.html) 中找到 RemoteIpValve 的其他配置選項。

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
