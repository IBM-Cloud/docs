---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# HTTP API for applications
{: #api}

Use the {{site.data.keyword.iot_full}} API to build and customize applications that interact with your organization on {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## API capabilities
{: #capabilities}

The {{site.data.keyword.iot_short_notm}} API supports the following functions for applications:

- View organization details
- Bulk device operations (list, add, and remove)
- Device type operations (list, create, delete, view details, and update)
- Device operations (list, add, remove, view details, update, view location, and view management information)
- Device diagnostic operations (clear logs, retrieve logs, add log information, delete logs, get specific logs, clear error codes, get device error codes, and add error codes)
- Connection problem determination (list device connection log events)
- Historical event retrieval (view events for all devices, view events by device type, and view events for a specific device)
- Device management request operations (list device management requests, initiate requests, clear request status, get details of a request, list all request statuses by device, and get the request status for a specific device)
- Usage management (retrieve number of active devices over a period, retrieve total amount of storage that is used by historical event data, and retrieve total amount of data used)
- Publish events on behalf of devices (beta)
- Service status queries (retrieve service statuses by organization)

## API version information
{: #version_information}

Use the [{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) to build and customize applications for your organization.


**Important:**
While the [{{site.data.keyword.iot_short_notm}} API V1](https://docs.internetofthings.ibmcloud.com/swagger/v0001.html) is supported, some of the capabilities that are described in this section are either limited or are not available. The following list outlines some of the limitations of using version 1:
  - Many of the API paths that relate to devices are different
  - The only device type operation that is supported is the capability to list all device types
  - Operations that are related to device management, device management requests, diagnostic information, or location are not available
