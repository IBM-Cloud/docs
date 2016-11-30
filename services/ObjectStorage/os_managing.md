---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Managing {{site.data.keyword.objectstorageshort}} across regions {: #multi-regions}


The {{site.data.keyword.objectstorageshort}} service supports the Dallas and London storage regions. These storage regions are independent of the {{site.data.keyword.Bluemix_notm}} region, such as US-South and United Kingdom, in which the {{site.data.keyword.objectstorageshort}} service instance is created. If you create an instance in the US-South {{site.data.keyword.Bluemix_notm}} region, you can read and write data to either the Dallas or London storage region.
{: shortdesc}

For the US-South {{site.data.keyword.Bluemix_notm}} region, the Dallas storage region is the default. For the United Kingdom {{site.data.keyword.Bluemix_notm}} region, the London storage region is the default.  The {{site.data.keyword.objectstorageshort}} user interface always launches to the default storage region of the {{site.data.keyword.Bluemix_notm}} region. To switch regions, click the {{site.data.keyword.objectstorageshort}} Region drop-down list and choose another region.

**Note:** The {{site.data.keyword.objectstorageshort}} service does NOT support cross storage region replication.

### Multi-region access

To use the {{site.data.keyword.objectstorageshort}} service, you must [authenticate to OpenStack Keystone](../ObjectStorage/os_api.html#keystone-authentication){: new_window}. After you have successfully authenticated, an `X-Subject-Token` and the {{site.data.keyword.objectstorageshort}} endpoints will be available in the response. Each storage region has a different [access point](../ObjectStorage/os_api.html#access-points).


For example, to create a container that is named `my_container` in the Dallas storage region, specify a Dallas access point in the curl command as follows:

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
You would receive the following as an output:

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

To create a container named `my_container` in the London storage region, specify a London access point in the curl command as follows:

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
You would receive the following as an output:

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**Note:** The `X-Subject-Token` acquired from Keystone, labeled as `X-Trans-ID` in the example, works across storage regions.
