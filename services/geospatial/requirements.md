---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-09"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Service requirements
{: #requirements}


##MQTT device message requirements

* The MQTT message broker must provide device messages in JSON format on one or more MQTT topics.
* The device messages can contain any number of attributes, but the following three attributes are always required:
	* An attribute that uniquely identifies the device.
	* An attribute that specifies the latitude of the current location of the device.
	* An attribute that specifies the longitude of the current location of the device.
* Two message modes are supported:
	* An MQTT message can contain a JSON object with information about a single device.
	* An MQTT message can contain a JSON array of objects with information about a set of devices.

##MQTT events and configuring the service

Your application subscribes to MQTT messages and controls {{site.data.keyword.geospatialshort_Geospatial}} through its [REST API](https://console.ng.bluemix.net/apidocs/246). The following actions are available through REST API calls:

* Configure and start the service.
* Add and remove geographic regions to monitor.
* Retrieve information about the service status and the set of regions currently defined.
* Stop the service.
* Restart an already configured service.
