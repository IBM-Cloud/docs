---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# About Delivery Insights
{: #about_delivery}

Delivery Insights, a part of {{site.data.keyword.DRA_short}}, shows deployment statistics, metrics, and other information about your IBM UrbanCode Deploy installation. For example, it can show charts of deployment duration, successes, and failures, all sorted by logically grouped environments.
{:shortdesc}

Delivery Insights requires an installation of DevOps Connect. For setup information, see [Showing data from IBM UrbanCode Deploy servers](uc_insights_connect_ucd.html).

![Two charts from UrbanCode Insights demo data](images/uc_insights_demo_data.gif)

Some of the information that you can see on Delivery Insights includes:

- Statistics about deployment, including deployment duration and deployment volume over time.
- Statistics about deployment failure rate by application and environment.
- Statistics about component deployment, including failure rate, deployment time, and duration.

## Systems overview
{: #systems_overview}

The topology for Delivery Insights includes one or more on-premise installations of IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> and the DevOps Connect utility.

The following diagram shows a typical installation of these systems.

![Overview topology for UrbanCode Insights, including customer on-premise systems and IBM Cloud Services](images/uc_insights_overview_topology_multi_ucd.png)

- An installation of **IBM UrbanCode Deploy** provides the information about successful and failed deployments for the metrics. IBM UrbanCode Deploy requires a patch to communicate with IBM Bluemix DevOps Connect.

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect**, formerly the IBM UrbanCode Sync Utility, coordinates communication between on-premise installations of IBM UrbanCode Deploy <!-- and IBM UrbanCode Release --> and IBM-hosted services such as UrbanCode Insights. DevOps Connect uses secure HTTPS communication to the on-premise servers and token authentication to provide data to UrbanCode Insights.

  DevOps Connect requires plug-ins to connect to the other systems in the topology.

- **Delivery Insights**, part of {{site.data.keyword.DRA_short}}, provides metrics about deployment activity on IBM UrbanCode Deploy, including deployment times and failure rates according to groups of environments. Authorization is controlled by {{site.data.keyword.Bluemix}} accounts.