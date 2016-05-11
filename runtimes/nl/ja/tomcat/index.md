---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}
*最終更新日時: 2016 年 3 月 19 日*

{{site.data.keyword.Bluemix}} の Tomcat ランタイムには java_buildpack が採用されています。
{: shortdesc}

{{site.data.keyword.Bluemix}} で Tomcat ランタイムを使用するには、-b オプションを使用して java_buildpack を指定する必要があります。例えば、次のように指定します。
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

Tomcat ランタイムについて詳しくは、[java-buildpack のreadme](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md) を参照してください。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Tomcat スターター・アプリケーションが用意されています。Tomcat スターター・アプリケーションは、使用可能なテンプレートを提供する、シンプルな Tomcat アプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../../cfapps/starter_app_usage.html)を参照してください。

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
現行のデフォルト Tomcat バージョンは 8.0.30 です。現行のデフォルト Java バージョンは 1.8.0_65 です。詳しくは、[java-buildpack のリリース](https://github.com/cloudfoundry/java-buildpack/releases) を参照してください。

# 関連リンク
## 一般
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
