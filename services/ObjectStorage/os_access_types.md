---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Types of access

{{site.data.keyword.objectstorageshort}} users can be either administrative or non-administrative. Access control lists are enabled by administrative users at the container level.
{: shortdesc}

<table>
<caption> Table 1. User roles defined </caption>
  <tr>
    <th> Administrative users (admin) </th>
    <th> Non-administrative users (member) </th>
  </tr>
  <tr>
    <td> Manage access control </td>
    <td> By default, have no access to the service or its containers </td>
  </tr>
  <tr>
    <td> Can create and delete containers </td>
    <td> Can perform actions based on the containers read/write ACLs </td>
  </tr>
  <tr>
    <td> Can read and write to containers </td>
    <td> Can perform actions as determined by the admin </td>
  </tr>
</table>


You can manage {{site.data.keyword.objectstorageshort}} users through the {{site.data.keyword.Bluemix_notm}} user interface, the Cloud Foundry API, or the Cloud Foundry CLI.
