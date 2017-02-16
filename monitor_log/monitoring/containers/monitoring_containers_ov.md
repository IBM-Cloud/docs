---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Containers overview
{: #monitoring_bmx_ov}

Container metrics are collected from outside of the container, without having to install and maintain agents inside of the container. In-container agents can have significant overheads and setup times for short-lived, lightweight cloud instances and auto-scaling groups, where containers can be rapidly created and destroyed. This out-of-band data collection approach eliminates these challenges and removes the burden of monitoring from the users.
{:shortdesc}

{{site.data.keyword.Bluemix}}
{{site.data.keyword.Bluemix_notm}}


Metrics that are collected by default

    A process that is running in the host performs agentless monitoring for metrics. This process, which is also called the crawler, constantly collects the following information from all of the containers.

        CPU
        Memory
        Network information

    This metric data is collected in Graphite and is displayed in both the Bluemix® user interface and the Advanced monitoring view. Docker conventions and groups accounting information are used as the basic mechanism for the collection of monitoring data.

    You can see a list of plug-ins that are installed to collect the data in /etc/collectd/collectd.conf. To learn more about what those plug-ins do, see the collectd documentation.
Metrics retention

    Up to one data point per minute is collected. Container metrics that have not been written to in 7 days are deleted.
Metrics sorting

    The data is displayed and ordered by container ID. From the command line, you can run the cf ic ps command to view a list of the container IDs for the containers in your private Bluemix images registry.

