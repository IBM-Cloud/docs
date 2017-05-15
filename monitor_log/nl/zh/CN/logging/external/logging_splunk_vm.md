---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 示例：将 Cloud Foundry 应用程序日志以流方式传送到 Splunk
{: #splunk}

在本示例中，名为 Jane 的开发者使用 IBM Virtual Servers Beta 和 Ubuntu 映像，创建了一个虚拟服务器。Jane 尝试以流方式，将 Cloud Foundry 应用程序日志从 {{site.data.keyword.Bluemix_notm}} 传送到 Splunk。
{:shortdesc}

  1. 要开始该操作，Jane 设置了 Splunk。

     a. Jane 从[下载 Splunk Light 站点 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} 下载了 Splunk Light，然后使用以下命令对其进行了安装。该软件安装在 */opt/splunk*。

	    

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane 安装并修补 RFC5424 syslog 技术附加组件，以与 {{site.data.keyword.Bluemix_notm}} 集成。有关安装附加组件的指示信息的更多信息，请参阅 [Cloud Foundry 准则 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}。

	    Jane 使用以下命令安装附加组件：

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        然后，Jane 通过将 */opt/splunk/etc/apps/rfc5424/default/transforms.conf* 替换为包含以下文本的 *transforms.conf* 文件，对附加组件进行修补：

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. 设置完 Splunk 之后，Jane 必须在 Ubuntu 机器上打开一些端口，以接受传入的 syslog 漏出（端口 5140）和 Splunk Web UI（端口 8000），因为缺省情况下，{{site.data.keyword.Bluemix_notm}} 虚拟服务器已设置防火墙。

	    **注：**这里已完成 iptable 配置，以供 Jane 进行评估，并且这只是暂时的。要在生产环境中的 Bluemix 虚拟服务器上配置防火墙设置，请参阅[网络安全组 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} 文档以获取详细信息。

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   然后，Jane 使用以下命令来运行 Splunk：

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane 配置 Splunk 设置，以从 {{site.data.keyword.Bluemix_notm}} 接受 syslog 漏出。她必须针对 syslog 漏出创建数据输入。

     a. 在 Splunk Web 界面中，Jane 单击**数据 > 数据输入**。此时将显示 Splunk 支持的输入类型列表。

     b. 她选择 **TCP**，因为 syslog 漏出使用 TCP 协议。

     c. 在 **TCP** 窗格的**端口**字段中，她输入 **5140**，将其他字段保留空白，然后单击**下一步**。

     d. 从**源类型**列表中，她选择**未分类 > rfc5424_syslog**。

     e. 对于**方法**类型，她选择 **IP**。

     f. 在**索引**字段中，Jane 单击**创建新索引**。她将新索引命名为“bluemix”，然后单击**保存**。

     g. 最后，在**复查**窗口中，Jane 确认设置正确，然后单击**提交**，以启用此数据输入。

  3. 在 {{site.data.keyword.Bluemix_notm}} 中，Jane 创建了 syslog 漏出服务，并将该服务绑定到某个应用程序。

     a. Jane 通过 cf CLI，使用以下命令，创建 syslog 漏出服务：

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **注：** *dummyhost* 不是实名。它用于隐藏实际主机名。

     b. Jane 将 syslog 漏出服务绑定到其空间内的某个应用程序，然后重新编译打包该应用程序。

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane 尝试使用该应用程序，然后在 Splunk Web 界面输入以下查询字符串：

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane 在其 Splunk Web 界面中看到日志流。虽然 Jane 安装的 Splunk 是 Splunk Light，但是她仍可以每天保留 500MB 日志。

