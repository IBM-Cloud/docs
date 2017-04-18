---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}

{{site.data.keyword.Bluemix}} の Tomcat ランタイムには java_buildpack が採用されています。
{: shortdesc}

{{site.data.keyword.Bluemix}} で Tomcat ランタイムを使用するには、-b オプションを使用して java_buildpack を指定する必要があります。例えば、次のように指定します。
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

Tomcat ランタイムについて詳しくは、[java-buildpack のreadme](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md) を参照してください。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Tomcat スターター・アプリケーションが用意されています。Tomcat スターター・アプリケーションは、使用可能なテンプレートを提供する、シンプルな Tomcat アプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションで使用する Tomcat のバージョンは、JBP_CONFIG_TOMCAT 環境変数を使用して変更できます。
アプリケーションで使用する Java のバージョンは、JBP_CONFIG_OPEN_JDK_JRE 環境変数を使用して変更できます。
これらはいずれも、アプリケーションのマニフェスト・ファイルで指定できます。例えば、次のように指定します。
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
現在の java_buildpack バージョンは v3.6 です。これには、デフォルトの Tomcat バージョン 8.30.0 とデフォルトの Java バージョン 1.8.0_71 が含まれています。詳しくは、[java-buildpack のリリース](https://github.com/cloudfoundry/java-buildpack/releases) を参照してください。

## HTTPS リダイレクト
{: #https_redirect}

Tomcat ランタイムは、Bluemix 内部プロキシーを信頼し、HTTP トラフィックの HTTPS (SSL) へのリダイレクトを許可するように構成できます。
これを行うには、server.xml ファイルを変更して、RemoteIpValve バルブ・エレメントを internalProxies オプションおよび protocolHeader オプションを使用して設定します。

ビルドパックに含まれている Tomcat ランタイム [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml) は、デフォルトでは RemoteIpValve バルブ・エレメントの protocolHeader のみが設定されます。HTTP トラフィックを Bluemix 内の HTTPS にリダイレクトするには、カスタム server.xml で  RemoteIpValve エレメントを次のように構成します。

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

RemoteIpValve のその他の構成オプションについては、[Tomcat の資料](https://tomcat.apache.org/tomcat-8.0-doc/api/org/apache/catalina/valves/RemoteIpValve.html)を参照してください。

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
