---

copyright:
  years: 2016
lastupdated: "2016-06-21"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Oracle JRE
{: #using_oraacle_jre}

您可以选择使用 Oracle JRE 在 Bluemix 上运行 Liberty 应用程序。为此，必须执行以下操作：
* 在 buildpack 可以下载该 JRE 的位置托管该 JRE。
* 托管一个 index.yml 文件，用于提供托管 JRE 的位置。
* 配置应用程序，以使用该 JRE。

## 托管 JRE 和 index.yml
{: #hosting_jre}

Oracle JRE 文件必须在 Web 服务器上进行托管，并且 Liberty buildpack 必须能够从该服务器下载该文件。可以使用任一可用的服务器工具在 Bluemix 本身上托管该 jar 文件，也可以在某些公共可用的位置进行托管。该服务器必须配置有一个 index.yml 文件，该文件用于指定有关 JRE 文件的详细信息。要托管 JRE 和 index.yml，请完成以下步骤：
  1. 获取 Oracle JRE。请注意，JRE 必须是能够在 UNIX 64 位操作系统上使用的版本，且必须是 tar.gz 文件。
  2. 在 Liberty buildpack 可以下载该 JRE 文件的位置中托管该文件。 
  3. 确保在托管位置提供 index.yml 文件。index.yml 文件中必须有一个条目包含以下信息：Oracle JRE 的版本标识，后跟一个冒号和该 JRE 文件所在位置的完整 URL。index.yml 的格式如下所示：
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * 例如：
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## 配置应用程序
{: #configure_app}

在 Liberty 应用程序上必须设置两个环境变量：*JBP_CONFIG_OPENJDK*（必须设置该变量来指定 index.yml 文件的位置）和 *JVM* 环境变量（必须将该变量设置为 *openjdk*，以将该 buildpack 配置为使用替代 JRE）。

对于 JBP_CONFIG_OPENJDK 变量，值为：
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

要设置此值，请发出类似下面的命令：
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

请注意，*repository_root* URL 不包含“index.yml”，而只包含其之前的位置路径。

要设置 JVM 环境变量，请发出类似下面的命令：
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**注**：设置环境变量后，必须重新编译打包应用程序。

## 确认
{: #confirmation}

要确认是否正在使用所需的 JRE，请在 staging_task.log 中查看是否有类似下面的消息：
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# 相关链接
{: #rellinks}
## 常规
{: #general}
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
