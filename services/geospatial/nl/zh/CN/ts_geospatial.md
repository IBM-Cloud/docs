---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.geospatialshort_Geospatial}} 故障诊断 
{: #ts_geospatial}


获取在 {{site.data.keyword.Bluemix_short}} 上使用 {{site.data.keyword.geospatialshort_Geospatial}} 时遇到的几个常见问题的解决方法。
{:shortdesc}

##我停止应用程序时，服务仍在监视区域
{: #stop-monitoring}


停止应用程序不会自动停止 {{site.data.keyword.geospatialshort_Geospatial}}。
{:shortdesc}


您停止了使用 {{site.data.keyword.geospatialshort_Geospatial}} 的应用程序，但是您在服务管理仪表板上看到服务仍在监视您在应用程序中指定的区域。
{: tsSymptoms}


即使停止应用程序，{{site.data.keyword.geospatialshort_Geospatial}} 服务实例也将继续运行。不管应用程序是否在运行，该服务将继续监视区域，直到您停止服务为止。
{: tsCauses}


从服务管理仪表板上停止 {{site.data.keyword.geospatialshort_Geospatial}}。或者可以修改应用程序以使用 REST API 停止服务，然后将更改推送回 {{site.data.keyword.Bluemix_short}}。
{: tsResolve}

##服务正在监视我未在应用程序中指定的区域
{: #unspecified-region}



如果您有多个应用程序绑定到同一服务实例，那么另一个应用程序可能已添加这些区域。
{:shortdesc}



在服务管理仪表板上查看 {{site.data.keyword.geospatialshort_Geospatial}} 实例时，您会看到该实例监视的区域比您在其中一个应用程序中指定的多。
{: tsSymptoms}

{{site.data.keyword.geospatialshort_Geospatial}} 的单个实例会监视绑定到该实例的所有应用程序的区域。这意味着查看服务管理仪表板时，您将看到所有应用程序指定的区域的信息。
{: tsCauses}

要停止 {{site.data.keyword.geospatialshort_Geospatial}} 监视特定区域：

1. 停止服务。
2. 修改应用程序以除去那些区域。
3. 将应用程序推送回 {{site.data.keyword.Bluemix_short}}。
{: tsResolve}


##从服务管理仪表板进行故障诊断
{: #dashboard}

当您对应用程序进行故障诊断时，可能想要转至服务管理仪表板来检查服务实例的状态。如果服务未在处理数据，那么您可能能够通过停止并重新启动服务来解决该问题。
{:shortdesc}

{{site.data.keyword.geospatialshort_Geospatial}} 服务实例的状态与应用程序的状态是分开的，并且多个应用程序可以绑定到同一服务实例。 

服务管理仪表板提供有关 {{site.data.keyword.geospatialshort_Geospatial}}（而非绑定到它的应用程序）的状态的信息。服务实例和应用程序的独立状态意味着如果停止应用程序，{{site.data.keyword.geospatialshort_Geospatial}} 服务实例继续运行。服务会继续监视您选择的区域，直到您将其除去为止，不管应用程序是否在运行。
