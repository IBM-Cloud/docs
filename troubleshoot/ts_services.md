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


# Troubleshooting for services
{: #services}


{{site.data.keyword.Bluemix}} services problems might include a gateway timeout error that occurs when you delete a service instance. You can recover from these problems by following a few easy steps.
{:shortdesc}

## Service broker error occurs when you delete a service instance
{: #ts_service_broker}

You might receive an error message when you try to delete a service instance that is already deleted from the cloud controller.
{:shortdesc}

When you try to delete a service instance, you see the following service broker error message:
{: tsSymptoms}
`Gateway timeout`

This problem happens if the service instance is already deleted from the cloud controller.
{: tsCauses}

Create a service instance with the same service name, then bind it to your applications. Then you can delete the service instance and the applications that use the service.   
{: tsResolve}
