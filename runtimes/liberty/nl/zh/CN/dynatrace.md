---

copyright:
  years: 2016
lastupdated: "2016-06-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Dynatrace
{: #using_dynatrace}

Dynatrace 是第三方服务，它提供对应用程序的监视。

有关 Dynatrace 服务提供内容的更多信息，请参阅 [Dynatrace Application Monitoring](http://www.dynatrace.com/en/products/application-monitoring.html)。

将 Liberty 应用程序配置为使用 Dynatrace 时，缺省行为是 Liberty 运行时将从 Dynatrace 站点获取 Dynatrace 代理程序 jar 文件，并随您的应用程序运行该 Dynatrace 代理程序。在缺省行为下，使用 Dynatrace 所需的最低配置为创建指向 Dynatrace 收集器的用户提供服务。

## 创建指向 Dynatrace 收集器的用户提供服务

首先，您需要设置 Dynatrace 收集器。然后，还必须创建用户提供的服务来传递 Dynatrace 代理程序的信息，以便与 Dynatrace 收集器进行连接。要更好地了解 Dynatrace 组件之间的关系，请参阅 [DynatraceArchitecture](https://community.dynatrace.com/community/display/DOCDT63/Architecture)。

<ol>
<li>设置 Dynatrace 收集器。<ul>
  <li>有关下载和设置 Dynatrace 收集器的指示信息，请参阅 [Dynatrace 社区 Web 站点](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace)。</li>
  <li>确保从设置收集器的位置可以访问随 Bluemix 中应用程序运行的 Dynatrace 代理程序。</li>
  </ul>
</li>
<li>创建指向运行中 Dynatrace 收集器的用户提供服务。<b>注：</b>用户提供的服务的名称必须包含 <b>dynatrace</b>。例如，使用以下命令：<pre>
$ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'  </pre>
  {: codeblock}

在此示例中，my-dynatrace-collector 是为服务指定的名称，DynatraceCollectorIPaddress 是已配置的 Dynatrace 收集器的 IP 地址，profile 是与此受监视应用程序关联的可选 Dynatrace 概要文件名称。缺省概要文件值为 Monitoring。可以指定可选参数，如以下示例中所示。


  <pre>
  $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                        "options" : {"dynatrace-parameter-1": "value",
                                                     "dynatrace-parameter-2": "value"}}'
  </pre>
  {: codeblock}

有关可用选项的更多信息，请参阅 Dynatrace 社区 Web 站点上 [Agent Configuration 的 Agent Setting 部分](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration)。例如，使用 exclude 选项，可以排除某些类使之不受 Dynatrace 监视。有关配置用户提供的服务的更多详细信息，请参阅 [DynaTrace Agent Framework](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md)。

</li>
<li>将应用程序推送到 Bluemix 后，请将创建的用户提供服务绑定到该应用程序。例如，使用以下命令：<pre>
  $ cf bs myApp my-dynatrace-collector
  </pre>  
  {: codeblock}

**注**：绑定服务后，必须对应用程序重新编译打包。

</li>
</ol>

## 可选配置
{: #optional_configuration}

您可以选择自行获取并托管 Dynatrace 代理程序 jar 文件。在此情况下，需要执行以下额外的配置步骤。
1. 获取并托管 Dynatrace 代理程序 jar 文件，以便 Liberty buildpack 可以下载该文件。
2. 配置 Liberty 应用程序，以便其可以下载 Dynatrace 代理程序。

### 托管 Dynatrace 代理程序
{: #hosting_dynatrace_agent}
Dynatrace 代理程序必须在 Web 服务器上进行托管，并且 Liberty buildpack 必须能够从该服务器下载代理程序 jar。该服务器必须配置有一个 index.yml 文件，该文件用于指定有关代理程序 jar 的详细信息。完成下面的步骤以设置 Dynatrace 代理程序：
  1. 下载 Dynatrace 代理程序 jar。有关下载 Dynatrace 代理程序 jar 的指示信息，请参阅 Dynatrace 社区 Web 站点上的 [Dynatrace Server Platform Installers](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace)。用于在 Bluemix 上运行的相应代理程序 jar 文件为 **dynatrace-agent-unix.jar** V**6.+**。
  2. 在 Liberty buildpack 可以下载代理程序 jar 文件的位置托管该 jar 文件。可以使用任一可用的服务器工具在 Bluemix 本身上托管该 jar 文件，也可以在某些公共可用的位置进行托管。
     * 确保在托管位置提供 index.yml 文件。index.yml 文件必须包含由以下各项组成的一个条目：代理程序 jar 的版本标识，后跟一个冒号和该代理程序 jar 位置的完整 URL。例如：
```
---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```  
{: codeblock}
     * **dynatrace-agent-6.3.0-unix.jar** 文件必须在 index.yml 文件中指定的位置提供。jar 文件和 index.yml 文件的位置可以是同一目录。

### 配置 Liberty 应用程序
{: #configuring_liberty_app}

必须将要监视的 Liberty 应用程序配置为可找到先前设置的托管代理程序 jar 的服务器。可以使用 **JBP_CONFIG_DYNATRACEAPPMONAGENT** 环境变量来配置应用程序。**JBP_CONFIG_DYNATRACEAPPMONAGENT** 环境变量会通知 buildpack 从什么位置下载 Dynatrace 代理程序。要设置该环境变量，请完成以下步骤：
<ol>
   <li> 设置变量 **JBP_CONFIG_DYNATRACEAPPMONAGENT**，使其具有值 *"repository_root: URL_of_server_hosting_index.yml"*。例如，推送应用程序后，发出以下命令：
  
  <pre>   
$ cf se myApp JBP_CONFIG_DYNATRACEAPPMONAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'  </pre>
  {: codeblock}

  在此示例中，*my-dynatrace-agent-host.mybluemix.net* 是先前配置的服务器托管的 index.yml 文件的 URL。
  </li>
  <li> 设置该环境变量后，对应用程序重新编译打包。Liberty 应用程序的 staging_task.log 会发出一条消息，指示从托管服务器的代理程序成功下载了 Dynatrace 代理程序。例如：

  <pre>
从 https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s) 下载 dynatrace-agent-6.3.0-unix.jar 6.3.0  </pre>
  {: codeblock}

</li>
<li>要查看 staging_task.log，请发出以下命令：
<pre>
$ cf files myAppName logs/staging_task.log  </pre>  
  {: codeblock}

</li>
</ol>

# 相关链接
{: #rellinks}
## 常规
{: #general}
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
