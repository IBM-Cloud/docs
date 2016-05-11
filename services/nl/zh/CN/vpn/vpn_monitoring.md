---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 监视状态和通讯流
{: #monitor}  
*上次更新时间：2016 年 3 月 17 日*  

使用监视功能可查看内部部署或 SoftLayer 服务器 VPN 网关与 {{site.data.keyword.vpn_short}} 网关之间的连接状态和通讯流速率。
{:shortdesc}  
##在服务仪表板上监视
{: #dashboard}

选择**监视**选项卡可查看以下连接统计信息。

* **连接状态：**内部部署或 SoftLayer 服务器 VPN 网关与 IBM VPN 网关之间的 VPN 连接状态。值：1=UP 和 -1=DOWN 
* **出站流量速率，以“字节/秒”和“包/秒”为单位：**从 IBM VPN 网关到内部部署或 SoftLayer 服务器 VPN 网关的流量速率。  
* **入站流量速率，以“字节/秒”和“包/秒”为单位：**从内部部署或 SoftLayer 服务器 VPN 网关到 IBM VPN 网关的流量速率。  

监视统计信息以图形显示，其中包含过去 48 小时的数据。这些图形每 20 分钟自动更新一次。不过，只要从监视选项卡切换出来再重新返回，即可随时访存最新数据。

**注：**这些图形使用全球标准时间 (UTC) 而非本地时间。  
##在 Logmet 上监视
{: #logmet}

使用 [Logmet](https://logmet.{DomainName}) 可查看详细的连接统计信息。 

1. 使用您的 Bluemix 凭证以及创建 IBM VPN 服务实例的空间和组织名称进行登录。  
2. 选择右上方的文件夹图标 (![](images/folder.png))。
3. 从仪表板列表中选择 **VPN 服务监视**可查看图形。这些图形使用本地时间。  

**注：**您必须在 IBM VPN 服务仪表板上至少选择一次**监视**选项卡以向 Logmet 发送查询，从而在 Logmet 中创建 VPN 服务仪表板。建立 VPN 连接之后，Logmet 需要最多 10 分钟来显示连接统计信息。


