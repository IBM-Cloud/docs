---

copyright:
  years: 2015, 2015
  
lastupdated: "2016-08-12"


---


{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# General services problems
{: #general}


{{site.data.keyword.Bluemix}} services problems might include a gateway time out error that occurs when you delete a service instance. However, in many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}

## Service broker error occurs when you delete a service instance
{: #ts_service_broker}

You might receive an error message when you try to delete a service instance that is already deleted from the cloud controller.
{:shortdesc}


When you try to delete a service instance, you see the service broker error message, `Gateway timeout`.
{: tsSymptoms}


This problem happens if the service instance is already deleted from the cloud controller.
{: tsCauses}


To resolve this problem, create a service instance with the same service name, and then bind it to your applications. After that, you can delete the service instance and the applications that use the service.   
{: tsResolve}
