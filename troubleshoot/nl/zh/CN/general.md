---

copyright:
  years: 2015, 2016

---


{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# 一般服务问题
{: #general}

*上次更新时间：2015 年 12 月 9 日*

{{site.data.keyword.Bluemix}} 服务问题可能包括：删除服务实例时发生网关超时错误。然而，在许多情况下，只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}

## 删除服务实例时显示网关超时错误消息
{: #ts_service_broker}

当您尝试删除已从云控制器删除的服务实例时，可能会收到错误消息。
{:shortdesc}


尝试删除服务实例时，看到服务代理程序错误消息：`网关超时`。
{: tsSymptoms}


如果已从云控制器删除服务实例，那么会发生此问题。
{: tsCauses}


要解决此问题，请使用相同服务名称创建服务实例，然后将其绑定到您的应用程序。此后，您可以删除服务实例和使用该服务的应用程序。   
{: tsResolve}


