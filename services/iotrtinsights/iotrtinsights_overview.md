---

copyright:
  years: 2015,2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# About {{site.data.keyword.iotrtinsights_short}}
{: #iotrtinsights_overview}
*Last updated: 11 February 2016*

{{site.data.keyword.iotrtinsights_short}} provides a real-time analytics engine and analytics authoring capability that enables the contextualization and monitoring of IoT device data, speeds understanding of current conditions, and improves decision-making and responses to emerging issues.
{:shortdesc}

## {{site.data.keyword.iotrtinsights_full}}
{: #iotrtinsights_concept}
{{site.data.keyword.iotrtinsights_short}} uses a simple rules-based composition model and an extensible framework to help you leverage Internet of Things data, combine it with master asset data, analyze situations in context, and automate responses to improve operations, availability, and service levels.

{{site.data.keyword.iotrtinsights_short}} connects to the {{site.data.keyword.Bluemix_notm}} Internet of Things ({{site.data.keyword.iot_short}}) service for real-time device data feeds. The incoming data is interpreted through a virtual data model that can be augmented with asset master data from an asset management system, such as IBM Maximo&reg; Asset Management.

In addition, user-defined rules are applied to the real-time streaming data to identify conditions that need attention. The action engine lets you define automated responses to the detected conditions, such as sending an email, triggering an IFTTT recipe, executing a Node-RED workflow, or using webhooks to connect to a variety of web services.  

And finally, real-time data is also displayed in a configurable dashboard for an at-a-glance view of the location, data, metrics, and alerts for your IoT devices.

![The {{site.data.keyword.iotrtinsights_short}} architecture.](images/iota.svg "{{site.data.keyword.iotrtinsights_short}} architecture")
