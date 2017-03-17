---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Prerequisites for Delivery Insights
{: #prereqs}

To see information from your IBM UrbanCode Deploy servers in {{site.data.keyword.DRA_short}}, you must host an instance of DevOps Connect on a system that can connect to your IBM UrbanCode Deploy servers. This system can be a physical computer or a virtual machine. 
{:shortdesc}

The system that hosts DevOps Connect must have the following prerequisites:
- The system must have a Java Runtime Environment (JRE) version 8 or later.
- The system `PATH` variable must include the location of the JRE.
- The system must allow DevOps Connect to create outgoing connections to IBM Bluemix.

To install DevOps Connect for use with Delivery Insights, open the DevOps Insights service and click **Settings > Delivery Insights Setup**.