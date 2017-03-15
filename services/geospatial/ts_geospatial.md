---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-09"

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

#{{site.data.keyword.geospatialshort_Geospatial}} troubleshooting
{: #ts_geospatial}


Get the answers to several common questions about using {{site.data.keyword.geospatialshort_Geospatial}} on {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##When I stop my app, the service is still monitoring regions
{: #stop-monitoring}


Stopping your app does not automatically stop {{site.data.keyword.geospatialshort_Geospatial}}.
{:shortdesc}


You stopped your application that uses {{site.data.keyword.geospatialshort_Geospatial}}, but you see on the service administration dashboard that the service is still monitoring the regions you specified in your app.
{: tsSymptoms}


If you stop your application, your {{site.data.keyword.geospatialshort_Geospatial}} service instance will continue to run. The service continues to monitor regions until you stop the service, regardless of whether your app is running.
{: tsCauses}


Stop {{site.data.keyword.geospatialshort_Geospatial}} from the service administration dashboard. Or you can modify your app to stop the service using the REST API and then push your changes back to {{site.data.keyword.Bluemix_short}}.
{: tsResolve}

##The service is monitoring regions I didn't specify in my app
{: #unspecified-region}



If you have more than one applications bound to the same service instance, another application may have added these regions.
{:shortdesc}



When you view your {{site.data.keyword.geospatialshort_Geospatial}} instance on the service administration dashboard, you see that it is monitoring more regions than you specified in one of your apps.
{: tsSymptoms}

A single instance of {{site.data.keyword.geospatialshort_Geospatial}} monitors the regions of all apps that are bound to it. This means that when you view your service administration dashboard, you will see information for the regions specified by all of your apps.
{: tsCauses}

To stop {{site.data.keyword.geospatialshort_Geospatial}} from monitoring certain regions:

1. Stop the service.
2. Modify your app or apps to remove those regions.
3. Push your app or apps back to {{site.data.keyword.Bluemix_short}}.
{: tsResolve}


##Troubleshooting from the service administration dashboard
{: #dashboard}

As you troubleshoot your application, you'll want to go to the service administration dashboard to check the status of your service instance. If it is not processing data, you might be able to fix the problem by stopping and restarting the service.
{:shortdesc}

The status of your {{site.data.keyword.geospatialshort_Geospatial}} service instance is separate from the status of your application, and several applications can be bound to the same service instance.

The service administration dashboard provides information about the status of the {{site.data.keyword.geospatialshort_Geospatial}}, not the applications that are bound to it. The separate statuses of your service instance and your application or applications means that if you stop your application, your {{site.data.keyword.geospatialshort_Geospatial}} service instance continues to run. The service continues to monitor the regions you chose until you remove them, regardless of whether or not your app is running.
