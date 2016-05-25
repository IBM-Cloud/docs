---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Beta 功能
{: #using_beta_features}

*上次更新时间：2016 年 3 月 23 日*

Liberty Beta 功能让您可以提早使用未来 Liberty 发行版中可能会包含的新功能和编程模型。大部分 Beta 功能还可以在部署到 Bluemix 的应用程序中使用。

**重要信息**：Beta 功能仅用于开发和测试，而不可用于生产。有关完整的使用条款，请参阅 [Beta 许可协议](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)。

Bluemix 中可用的 Liberty Beta 功能
<table>
<tr>
<th align="left">功能</th>
<th align="left">功能</th>
<th align="left">功能</th>
<th align="left">功能</th>
</tr>

<tr>
<td>cloudant-1.0</td>
<td>httpWhiteboard-1.0</td>
<td>osgiBundle-1.0</td>
<td>passwordUtilities-1.0</td>
</tr>
</table>

要在 Bluemix 中使用 Liberty Beta 功能，您将需要执行以下任一操作：

1. [部署服务器目录或打包服务器](optionsForPushing.html)，并在 server.xml 文件中启用一个或多个 Beta 功能，如以下示例中所示：```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>passwordUtilities-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  将 IBM_LIBERTY_BETA 环境变量设置为 **true**。此变量会引导 Liberty buildpack 为您的应用程序安装并启用 Beta 功能。请参阅以下示例：
  * 使用 cf 命令行工具：```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true```
{: #codeblock}

  * 或者，使用 manifest.yml 文件：```
      env:
          IBM_LIBERTY_BETA: "true"```
{: #codeblock}

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
