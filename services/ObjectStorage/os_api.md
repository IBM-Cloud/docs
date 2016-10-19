---

copyright:
  years: 2014, 2016
lastupdated: "2016-10-07"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

## Using the Swift REST API to access {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}


You can use the Swift REST API with a command–line client interface, such as cURL, or call the API from your application.
{: shortdesc}

### Constructing your {{site.data.keyword.objectstorageshort}} URL {: #access-points}

To interact with the {{site.data.keyword.objectstorageshort}} API, construct the {{site.data.keyword.objectstorageshort}} URL as follows:
  ```
  https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> URL pieces  </th>
    <th> Definition </th>
  </tr>
  <tr>
    <td> API version  </td>
    <td> Version 1: v1 </td>
  </tr>
  <tr>
    <td> Account information  </td>
    <td> This is your ProjectID and the prefix combined. It can be found in the UI. </td>
  </tr>
  <tr>
    <td> Container namespace  </td>
    <td> The name of your container. Can be found in the UI. </td>
  </tr>
  <tr>
    <td> Object namespace  </td>
    <td> The name of your file or object. Can be found in the UI. </td>
  </tr>
  <tr>
    <td> Access point</td>
    <td> London: https://lon.objectstorage.open.softlayer.com/
    <br> Dallas: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

*Table 1. {{site.data.keyword.objectstorageshort}} URL pieces explained*

For example:

![{{site.data.keyword.objectstorageshort}} URL pieces shown in an example image](images/Swift_URL.png)


### {{site.data.keyword.objectstorageshort}} API {: #openstack-reference}

See the [OpenStack Swift API complete reference](http://developer.openstack.org/api-ref-objectstorage-v1.html) for a comprehensive list of the {{site.data.keyword.objectstorageshort}} REST API options and examples.
