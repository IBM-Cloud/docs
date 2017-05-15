---

copyright:
  years: 2015, 2016
  
lastupdated: "2016-08-12"

---



{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# 有关服务的故障诊断
{: #services}


{{site.data.keyword.Bluemix}} 服务问题可能包括删除服务实例时发生的网关超时错误。只需执行几个简单的步骤即可解决这些问题。
{:shortdesc}

## 删除服务实例时服务代理程序发生错误
{: #ts_service_broker}

当您尝试删除已从云控制器删除的服务实例时，可能会收到错误消息。
{:shortdesc}

尝试删除服务实例时，看到服务代理程序错误消息：
{: tsSymptoms}
`网关超时`

如果已从云控制器删除服务实例，那么会发生此问题。
{: tsCauses}

使用相同服务名称创建服务实例，然后将其绑定到应用程序。随后，可以删除服务实例和使用该服务的应用程序。   
{: tsResolve}
