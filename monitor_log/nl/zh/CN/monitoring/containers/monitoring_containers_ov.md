---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 监视 IBM Bluemix Container Service
{: #monitoring_bmx_containers_ov}

在 {{site.data.keyword.Bluemix}} 中，会从容器外部自动收集容器度量值，而不必在容器内部安装和维护代理程序。
{:shortdesc}

对于生命周期较短的轻量级云实例和自动扩展组（在其中可快速创建和销毁容器），容器内代理程序可能会产生大量的开销并耗用较长的设置时间。此频带外数据收集方法可避免这些问题，并免除了用户的监视负担。

有一个在主机中运行的进程会对度量值进行无代理监视。缺省情况下，此进程（也称为搜寻器）会持续从所有容器中收集以下度量值：

* CPU
* 内存
* 网络信息

度量值数据在 Graphite 中收集，并同时在 {{site.data.keyword.Bluemix_notm}} UI 和 Grafana 中显示。 

可以通过 {{site.data.keyword.Bluemix_notm}} UI 或直接通过浏览器启动 Grafana。有关更多信息，请参阅[在 Grafana 中分析度量值](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana)。

Docker 约定和组记帐信息用作监视数据收集的基本机制。

**度量值保留时间**

每分钟最多可收集一个数据点。将删除 7 天内未写入的容器度量值。
    
**度量值排序**

将显示数据并按容器标识排序。 

在命令行中，可以运行 `cf ic ps` 命令来查看专用 {{site.data.keyword.Bluemix_notm}} 映像注册表中容器的容器标识列表。

