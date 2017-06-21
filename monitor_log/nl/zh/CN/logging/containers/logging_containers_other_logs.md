---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 从容器收集非缺省日志数据
{: #logging_containers_collect_data}

要从容器内的非缺省日志位置捕获数据，请在创建容器时，设置 **LOG_LOCATIONS** 环境变量。
{:shortdesc}

* 创建容器时，添加带有日志文件路径的 **LOG_LOCATIONS** 环境变量。 
* 可以添加多个日志文件，各文件之间用逗号分隔。 

## 通过 Bluemix 控制台收集非缺省日志数据
{: #logging_containers_collect_data_ui}

要通过控制台收集非缺省数据，请完成以下步骤：

1. 在目录中，选择**容器**，然后选择映像。 

    显示的映像列表包括 {{site.data.keyword.IBM}} 提供的映像以及存储在专用 {{site.data.keyword.Bluemix_notm}} 注册表中的映像。 

2. 定义容器。选择类型，输入容器名称，选择容器大小，然后定义其他属性，例如 IP 地址详细信息和端口。有关更多信息,请参阅[通过 {{site.data.keyword.Bluemix_notm}} UI 创建和部署单个容器](/docs/containers/container_single_ui.html#gui)。 

3. 展开**高级选项**部分，并选择**添加新的环境变量**。

4. 添加 **LOG_LOCATIONS** 变量，并将其值设置为要分析的日志。

    例如，添加基于最新 Liberty 映像的容器时，要分析日志文件 *dpkg.log*，请将该环境值设置为以下值：
    
    <table>
      <caption>表 1. 日志位置样本值</caption>
      <tbody>
        <tr>
          <th align="center">变量名称</th>
          <th align="center">值</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. 单击**创建**。

这将打开容器仪表板。检查容器的状态是否为*正在运行*，然后检查**监视和日志**选项卡中的日志。


## 通过 CLI 收集非缺省日志数据
{: #logging_containers_collect_data_cli}

要通过 CLI 收集非缺省日志数据，请完成以下步骤：

1. 设置终端以使用 {{site.data.keyword.containershort}} CLI。有关更多信息，请参阅[设置 IBM Bluemix Container Service CLI](/docs/containers/container_cli_cfic_install.html)。

2. 通过使用以下命令登录到 Cloud Foundry CLI：`cf login`。收到提示时，请输入 {{site.data.keyword.Bluemix_notm}} 标识、密码、组织和空间。 

    缺省情况下，您会登录到美国南部区域或上次登录的区域。 
    
    可以包含 **–a** 选项以登录到 {{site.data.keyword.Bluemix_notm}} 中的特定区域。例如，下表列出了每个区域的命令：

    <table>
      <caption>表 2. 每个区域的命令</caption>
      <tbody>
        <tr>
          <th align="center">区域</th>
          <th align="center">命令</th>
        </tr>
        <tr>
          <td align="left">美国南部</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">英国</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
	 <tr>
          <td align="left">法兰克福</td>
          <td align="left">cf login -a api.eu-de.bluemix.net</td>
        </tr>
       </tbody>
    </table>
    

3. 通过使用以下命令登录到 {{site.data.keyword.containershort}}：`cf ic login`。

4. 基于映像创建单个容器。包含 LOG_LOCATIONS 环境变量以包含非缺省日志位置。  

    要添加定制位置，以便可以在 Kibana 中查看该日志信息，请在创建容器时添加 **LOG_LOCATIONS** 环境变量。输入以下命令：
    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    其中
    
     <table>
      <caption>表 3. 命令选项</caption>
      <tbody>
        <tr>
          <th align="center">选项</th>
          <th align="center">描述</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> 如果要使应用程序可从因特网进行访问，您需要公开公共端口。包含在 Dockerfile 中为要使用的映像指定的任何端口。<br> 您可以选择 UDP 或 TCP，以指示要使用的 IP 协议。如果未指定协议，那么端口会自动公开用于 TCP 流量。<br> 公开公共端口时，将为容器创建公用网络安全组，该组只允许您在公开的端口上发送和接收公共数据。其他所有公共端口都将关闭，且无法用于从因特网访问应用程序。<br> 可以使用多个 -p 选项包含多个端口。</td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">设置环境变量。<br> 可以分别列出多个键。用引号将环境变量名称和值括起。<br> 如果添加要在容器中监视的日志文件，请包含带有日志文件路径的 LOG_LOCATIONS 环境变量。</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">定义容器的名称。</td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">公共区域中的注册表。例如，对于美国南部区域，缺省域名为 `ng.bluemix.net`；对于英国，缺省域名为 `eu-gb.bluemix.net`。</td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">要添加的映像的名称。</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">要添加的映像的标记。</td>
        </tr>
      </tbody>
    </table>
    
    例如，要基于最新的 Liberty 映像创建容器，并包含日志文件 `/var/log/dpkg.log`，请使用以下命令： 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    dpkg.log 文件是标准 Ubuntu 日志文件，通常在容器创建期间生成，但不会自动推送到 Kibana。

要检查容器的状态，请运行命令 `docker ps`。状态为*正在运行*时，请在 {{site.data.keyword.Bluemix_notm}} 控制台中、通过命令行或通过 Kibana 来检查日志。



