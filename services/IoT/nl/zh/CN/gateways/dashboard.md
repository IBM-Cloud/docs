---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 连接网关
{: #IoT_connectGateway}

您必须将网关连接到 {{site.data.keyword.iot_full}}，然后才能开始从连接到网关的设备接收数据。将网关连接到 {{site.data.keyword.iot_short_notm}} 涉及创建网关设备类型和向 {{site.data.keyword.iot_short_notm}} 注册网关。然后，可以使用注册信息将网关连接到 {{site.data.keyword.iot_short_notm}}。
{:shortdesc}

网关是 {{site.data.keyword.iot_short_notm}} 中的一种专用类别的设备。网关用作其他设备对 {{site.data.keyword.iot_short_notm}} 的访问点。


## 开始之前
{: #Prerequisites}

网关设备具有的许可权多于常规设备，可以执行以下功能：
- 向 {{site.data.keyword.iot_short_notm}} 注册新设备
- 像直接连接的设备一样，发送和接收自己的传感器数据
- 代表与其连接的设备发送和接收数据
- 运行设备管理代理程序，以便可以对其进行管理，还可管理与其连接的设备。
  
有关网关开发者的信息，请参阅[网关的 MQTT 连接](mqtt.html)。

您还可以使用网关对网关设备发送的数据执行边缘分析。有关更多信息，请参阅[边缘分析](../edge_analytics.html)和[安装 Edge Analytics Agent](#edge)。

## 步骤 1：向 {{site.data.keyword.iot_short_notm}} 注册网关  
{: #register_gateway}

注册网关涉及将设备分类为网关类型，为网关命名，以及提供网关信息。然后，提供连接令牌，或接受 {{site.data.keyword.iot_short_notm}} 生成的令牌。

**提示：**可以在 {{site.data.keyword.iot_short_notm}} 仪表板中一次添加一个网关，也可以使用 [{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/post_bulk_devices_add) 一次添加一个或多个网关。

要在 {{site.data.keyword.iot_short_notm}} 仪表板中添加网关，请执行以下操作：

1. 在 {{site.data.keyword.iot_short_notm}} 仪表板中，选择**设备**。
2. 单击**添加设备**。
3. 为要添加的设备选择或创建设备类型。
  
连接到 {{site.data.keyword.iot_short_notm}} 的每个设备都必须与一种设备类型相关联。设备类型是共享公共特征的设备组。  
 1. 单击**创建设备类型**，然后单击**创建网关类型**。
 2. 输入设备类型名称（例如，`my_gateway_type`）和网关类型描述。
   
 **重要信息**：设备类型名称不得超过 36 个字符，仅可包含以下字符：
 <ul>
  <li>字母数字字符（a-z、A-Z 和 0-9）</li>
  <li>连字符（-）</li>
  <li>下划线 (&lowbar;)</li>
  <li>句点 (.)</li>
  </ul>3. 可选：输入网关类型属性和元数据。    
 **提示：**您可以稍后添加和编辑属性及元数据。
 4. 单击**创建**以添加新的网关类型。
10. 单击**下一步**以开始添加具有所选网关类型的网关设备的过程。
11. 输入设备标识，例如 `my_gateway_device`。
  
设备标识用于在 {{site.data.keyword.iot_short_notm}} 仪表板中标识网关设备；设备标识也是用于将网关设备连接到 {{site.data.keyword.iot_short_notm}} 的必需参数。
  
**重要信息**：设备标识不得超过 36 个字符，仅可包含以下字符：
 <ul>
 <li>字母数字字符（a-z、A-Z 和 0-9）</li>
 <li>连字符 (-)</li>
 <li>下划线 (&lowbar;)</li>
 <li>句点 (.)</li>  
 </ul>
 **提示：**对于连接网络的设备，设备标识可以是（例如）不带任何分隔冒号的设备 MAC 地址。  
12. 可选：单击**其他字段**以添加网关设备信息，例如序列号、制造商、型号等。
   
 **提示：**您可以稍后添加和编辑此信息。
12. 可选：输入设备 JSON 元数据。  
 **提示：**您可以稍后添加和编辑设备元数据。
13. 单击**下一步**以完成添加网关设备的操作。
14. 验证摘要信息是否正确，然后单击**添加**以添加网关设备。
  
**提示：**您可以选择接受自动生成的认证令牌，或自己提供认证令牌。如果选择创建自己的令牌，请确保令牌的长度介于 8 到 36 个字符之间，包含大小写字母、数字、连字符、下划线或句点的混合。此令牌不得包含重复的字符序列、字典单词、用户名或其他预定义序列。
15. 在设备信息页面中，复制并保存以下设备信息：  
 - 组织标识，例如 `tubo8x`
 - 设备类型，例如 `my_gateway_type`
 - 设备标识。**提示：**例如，对于网络连接的设备，这可能是不带任何分隔冒号的 MAC 地址。
 - 认证方法，例如 `token`
 - 认证令牌，例如 `PtBVriRqIg4uh)_-Kl`  
  **提示：**您将需要“组织标识”、“认证令牌”、“设备类型”和“设备标识”来配置设备以连接到 {{site.data.keyword.iot_short_notm}}。  

恭喜，您已注册网关设备。现在，可以配置网关设备以连接到 {{site.data.keyword.iot_short_notm}}

请参阅 [How to Register Gateways in IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/how-to-register-gateways-in-ibm-watson-iot-platform/) 诀窍，以获取演示注册网关所需流程的逐步指示信息。

## 步骤 2：将网关连接到 {{site.data.keyword.iot_short_notm}}
{: #connect_gateway}

向 {{site.data.keyword.iot_short_notm}} 注册网关后，请使用注册信息将网关连接到 {{site.data.keyword.iot_short_notm}}，然后开始从连接到该网关的设备接收数据。

有关将网关连接到 {{site.data.keyword.iot_short_notm}} 的信息，请参阅[网关的 MQTT 连接](mqtt.html)。

**提示：**有一系列的诀窍可用于将设备连接到 {{site.data.keyword.iot_short_notm}}。有关诀窍的列表，请参阅 IBM.com 上提供的[设备连接诀窍](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/)。


## 步骤 3：通过网关连接设备
{: #gateway_devices}

网关从连接到网关的设备发布消息时，该设备会自动添加到 {{site.data.keyword.iot_short_notm}}。网关针对尚不存在的设备类型和设备标识组合发布消息时，会自动创建设备类型和设备本身。

有关设备自动注册以及发布和接收所连接设备的数据的信息，请参阅[网关的 MQTT 连接](mqtt.html)。


设备成功连接到网关时，会在 {{site.data.keyword.iot_short_notm}} 组织的仪表板上显示该设备。

请参阅 [Connecting Raspberry Pi as a Gateway to Watson IoT](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-as-a-gateway-to-watson-iot-using-node-red/) 诀窍，以获取详细的流程和描述。 

**注：**在 {{site.data.keyword.iot_short_notm}} 仪表板中，直接连接到 {{site.data.keyword.iot_short_notm}} 的设备和网关会显示“状态”图标以指示其已连接。仪表板将通过网关间接连接的设备显示为“已断开连接”，因为仪表板并不知道该网关的设备连接。


## 安装 Edge Analytics Agent
{: #edge}

Edge Analytics Agent (EAA) 是基于 [Apache Quarks](http://quarks.incubator.apache.org/) 构建的软件组件，可通过在 {{site.data.keyword.iot_short_notm}} 仪表板中上传和管理边缘分析规则，对网关执行边缘分析操作。有关边缘分析的更多信息，请参阅[边缘分析](../edge_analytics.html)。

### 安装 EAA
{: #eaa_install}

要在网关上安装 EAA，请执行以下操作：
1. 在 {{site.data.keyword.iot_short}} 仪表板中，转至**规则**。
2. 单击**下载 Edge Analytics Agent** 以转至 [IBM Edge Analytics Agent 社区](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true)。
3. 浏览至 **Files** 部分，然后下载压缩的 *ibm-watson-iot-edge-analytics-dslink-java-0.0.1* 文件。
4. 有关如何在网关上安装和配置 EAA 软件组件的信息，请参阅以下诀窍：
 - [Getting started with Edge Analytics in Watson IoT Platform](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=19472)

### EAA 配置设置
{: #eaa_configuration}

可以使用 EAA config.properties 文件来设置基本软件配置参数。

要更新 EAA 配置，请执行以下操作：
1. 在运行 EAA 的网关系统上，找到 EAA config.properties 文件。  
例如：`../dglux-server/dslinks/ibm-watson-iot-edge-analytics-dslink-java-0.0.1/config.properties`
2. 开始编辑设置之前，请先制作该文件的备份副本。
3. 打开 config.properties 文件进行编辑。
4. 编辑环境的配置参数：
 <dl>
 <dt>DataDirectSendEnable</dt>
 <dd>布尔值 (true|false)</br>
 TRUE（缺省值）- 将所有数据发送到 {{site.data.keyword.iot_short_notm}}。</br>
 FALSE - 仅当引擎上设置了规则时，才将数据发送到 {{site.data.keyword.iot_short_notm}}。</dd>
 <dt>MonitorInterval</dt>
 <dd>整数（毫秒）</br>
 将新的监视消息发送到 {{site.data.keyword.iot_short_notm}} 之前间隔的时间（以毫秒为单位）。</br>
 设置较小的值会更频繁地报告监视度量值。设置较大的值可获取有关 {{site.data.keyword.iot_short_notm}} 的更详细监视信息。</br>
 缺省值：60000</br>
 建议的范围：[1000, 360000]</dd>
 <dt>MonitorLogDesample</dt>
 <dd>整数</br>
 发送到 {{site.data.keyword.iot_short_notm}} 的监视消息数与进入本地日志中的消息数的比值，即解样率。例如，如果 `MonitorLogDesample` 设置为 10，那么每发送到 {{site.data.keyword.iot_short_notm}} 10 条消息，才会写入一个本地日志条目。</br>设置为较大数字可使本地日志保持较小。设置为较小的值可提供更详细的本地日志。</br>
 缺省值：10</br>
 建议的范围：[1, 100]</dd>
 <dt>MemoryAlertThreshold</dt>
 <dd>整数（兆字节）</br>
 可用 JVM 堆内存阈值，达到此阈值后会将内存警告日志消息发送到 {{site.data.keyword.iot_short_notm}} 诊断日志。此警报通过监视驱动。</br>设置为较小的值可减少发送到 {{site.data.keyword.iot_short_notm}} 的警报消息数。设置为较大的值可在 EAA 服务器遇到内存问题时，向您及早提供警告。</br>**提示：**您可以使用[云分析](../cloud_analytics.html)规则来配置警报操作，例如通过电子邮件发送通知来向您发出内存问题警报。有关可用于构建规则的可用属性的信息，请参阅 [Edge Analytics Agent 诊断度量值](../edge_analytics.html#eaa_metrics)。</br>
 缺省值：10</br>
 建议的范围：[10 或总内存的 5%, 200]</dd>
 </dl>
5. 保存编辑过的文件，然后重新启动 EAA。

样本 EAA config.properties 文件
```
#######################################################################
# Engine Parameters
#######################################################################
# DataDirectSendEnable
#                    - BOOLEAN(true|false) Set to true to forward all
#                      the data; Set to false to disable data direct
#                      send to IOTP when there is no rule set in the
#                      engine.
#                      DEFAULT: true
#######################################################################
DataDirectSendEnable=true

#######################################################################
# Monitoring Parameters
#######################################################################
# MonitorInterval    - INTEGER Time interval in milliseconds before a  
#                      new monitoring message is generated. Set it to a
#                      small value to report the monitor metrics more
#                      frequently. Set it to a big value to have more
#                      detailed monitoring information on IoTP.
#                      DEFAULT: 60000    RECOMMEND: [1000, 360000]
# MonitorLogDesample - INTEGER The de-sampling ratio of the number of
#                      monitoring messages sent to IOTP vs. local log,
#                      i.e. number of monitoring messages N where
#                      EAA would output only one to the Info log for
#                      every N messages. Set it big to keep the size
#                      of the log small. Set it small to have detailed
#                      monitoring information in local log.
#                      DEFAULT: 10       RECOMMEND: [1, 100]
# MemoryAlertThreshold
#                    - INTEGER the free JVM heap memory in megabyte under
#                      which a log message would be generated and send to
#                      IOTP diagnosis log. The alert is driven by the
#                      monitoring. Set it small to eliminate unnecessary
#                      alert message on IoTP. Set it big to receive early
#                      alert when the system is likely to crash. Set to
#                      Min(Max(10MB, 5% of the total memory), 200MB) is
#                      recommended.
#                      DEFAULT: 10       RECOMMEND: [10, 200]
#######################################################################

MonitorInterval=60000
MonitorLogDesample=10
MemoryAlertThreshold=10
```
