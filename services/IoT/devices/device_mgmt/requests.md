---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}  
{:codeblock: .codeblock}
{:pre: .pre}


# Device management requests
{: #requests}


The {{site.data.keyword.iot_full}} provides actions that can be initiated for one or more devices. These actions can be initiated by using the dashboard or the REST API. The types of available actions are **device actions** and **firmware actions**.

## Initiating device management requests by using the dashboard
{: #initiating-dm-dashboard}

Requests can be initiated through the dashboard by using the **Actions** tab of the Devices page. Click **Initiate Action** to select an action, select devices, and specify any additional parameters that the selected action supports.

## Initiating device management requests by using the REST API
{: #initiating-dm-api}

Requests can be initiated by using the following REST API sample:  

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

For more information about the body of a device management request, see the [API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/deviceMgmt.html#!/Device_Management_Requests){: new_window}.

## Device actions
{: #device-actions}

A device can specify that it supports device actions when it publishes a manage request. A device action request indicates to the {{site.data.keyword.iot_short_notm}} that the device is able to respond to device reboot and device reset actions.


## Device actions - reboot
{: #device-actions-reboot}

You can initiate the reboot device action by using the {{site.data.keyword.iot_short_notm}} dashboard or by using the REST API.

To initiate a device reboot by using the REST API, issue a POST request to:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Provide the following information:

- The action ``device/reboot``
- A list of devices to reboot, with a maximum of 5000 devices

Example device reboot request:

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

After a request is initiated, an MQTT message is published to all devices that are specified in the body of the reboot request. For each device, a response must be sent back to indicate whether the reboot action can be initiated. If this operation can be initiated immediately, set the `rc` parameter to `202`. If the reboot attempt fails, set the `rc` parameter to `500` and set the `message` parameter accordingly. If reboot is not supported, set the `rc` parameter to `501` and optionally set the `message` parameter accordingly.

The reboot action is complete when the device sends a Manage Device request after its reboot.

### Topic for device reboot request

The server publishes a reboot request to a device on the following topic:

```
iotdm-1/mgmt/initiate/device/reboot
```

### Message format for device reboot request


Request Format:

```
Incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

Response Format:

```
Outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## Device actions - factory reset
{: #device-actions-factory-reset}

You can initiate the factory reset action by using the {{site.data.keyword.iot_short_notm}} dashboard or by using the REST API.

To initiate a device factory reset by using the REST API, issue a POST request to:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

The following information is provided:

- The action ``device/factoryReset``
- A list of devices to reset, with a maximum of 5000 devices

The following sample provides an example device reset request:

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

When a device reset request is initiated, an MQTT message is published to all devices that are specified in body of the request. For each device, a response must be returned to indicate whether the factory reset action can be initiated. The response code is set to ``202`` if this action can be initiated immediately. If the factory reset attempt fails, set the ``rc`` parameter to ``500`` and set the ``message`` parameter accordingly. If the factory reset action is not supported, set the ``rc`` parameter  to ``501`` and optionally set the ``message`` parameter accordingly.

The factory reset action is complete when the device sends a Manage Device request after the factory reset.

### Topic for factory reset request

The server publishes the following request to a device:

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### Message format for factory reset request


Request format:

```
The following topic shows the incoming message from the server:

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

Response format:

```
The following topic shows an outgoing message from the device:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## Firmware actions
{: #firmware-actions}

The firmware level that is known to be on a device is stored in the ``deviceInfo.fwVersion`` attribute. The ``mgmt.firmware`` attributes are used to perform a firmware update and observe its status.

**Important:** The managed device must support observation of the ``mgmt.firmware`` attribute to support firmware actions.

The firmware update process is separated into distinct actions:
- Downloading firmware
- Updating firmware

The status of each of firmware actions is stored in a separate attribute on the device. The ``mgmt.firmware.state`` attribute describes the status of the firmware download. The following table describes the possible values that can be set for the ``mgmt.firmware.state`` attribute:

 |Value |State  | Meaning |
 |:---|:---|:---|
 |0  | Idle        | The device is not downloading firmware. |  
 |1  | Downloading | The device is downloading firmware. |
 |2  | Downloaded  | The device successfully downloaded a firmware update and is ready to install it. |


The ``mgmt.firmware.updateStatus`` attribute describes the status of the firmware update. The possible values for the ``mgmt.firmware.updateStatus`` attribute are:

|Value |State | Meaning |  
|:---|:---|:---|
|0 | Success | The firmware was successfully updated. |
|1 | In Progress | The firmware update was initiated but is not yet complete.|
|2 | Out of Memory | An out-of-memory condition was detected during the operation.|
|3 | Connection Lost     | The connection was lost during the firmware download. |
|4 | Verification Failed | The firmware did not pass verification. |
|5 | Unsupported Image   | The downloaded firmware image is not supported by the device. |
|6 | Invalid URI         | The device could not download the firmware from the provided URI. |

## Firmware actions - download
{: #firmware-actions-download}

You can initiate the download firmware action by using the {{site.data.keyword.iot_short_notm}} dashboard or by using the REST API.

To initiate a firmware download by using the REST API, issue a POST request to:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

The following information is provided:

- The action ``firmware/download``
- A list of devices to receive the image, with a maximum of 5000 devices
- The URI for the firmware image (optional)
- Verification string to validate the image (optional)
- Firmware name (optional)
- Firmware version  (optional)

The following sample shows the firmware download request on which all the following example messages are based:

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

If none of the optional parameters are specified, the first step in the following process is skipped.

The device management server in {{site.data.keyword.iot_short_notm}} uses the Device Management Protocol to send a request to the devices, which initiates the firmware download. The download process consists of the following steps:

1. A firmware details update request is sent on topic ``iotdm-1/device/update``.
The update request lets the device validate if the requested firmware differs from the currently installed firmware. If there is a difference, set the ``rc`` parameter to ``204``, which translates to the status ``Changed``.  
The following example shows which message to expect for the previously sent example firmware download request and which response is sent when a difference is detected:
```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/device/update
   Message:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields" : [{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   This response triggers the next request.
2. Observation request for firmware download status ``iotdm-1/observe`` is sent.
The observation request verifies whether the device is ready to start the firmware download. When the download can be started immediately, set the ``rc`` parameter to ``200`` (``Ok``), the ``mgmt.firmware.state`` attribute to
   ``0`` (``Idle``) and the ``mgmt.firmware.updateStatus`` attribute to ``0`` (``Idle``). The following code is an example exchange between the {{site.data.keyword.iot_short_notm}} and device:
   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/observe
   Message:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields" : [ {
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
This exchange triggers the last step.  

3. The download request is sent on topic ``iotdm-1/mgmt/initiate/firmware/download``:

   The download request tells a device to start the firmware download. If the action can be initiated immediately, set the ``rc`` parameter to ``202``. The following code provides an example of the initiation of a download request:

   ```
   Incoming request from the {{site.data.keyword.iot_short_notm}}:

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   Outgoing response from device:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

After a firmware download is initiated this way, the device needs to report the status of the download to the {{site.data.keyword.iot_short_notm}}. The device reports the status by publishing a message to the ``iotdevice-1/notify``-topic, where the ``mgmt.firmware.state`` attribute is set to either ``1`` (``Downloading``) or ``2`` (``Downloaded``).
The following samples show an example of the initiation of the firmware download:

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "123456789",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


Wait some time...


Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "1234567890",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



After the notification is published with the ``mgmt.firmware.state`` attribute set to ``2``, a request is triggered on the ``iotdm-1/cancel``-topic. This request cancels the observation of the ``mgmt.firmware`` attribute.
After a response that has the ``rc`` parameter set to ``200`` is sent, the firmware download is completed. The following code provides an example:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

The following information is useful for error handling:

- If the ``mgmt.firmware.state`` attribute is not ``0`` ("Idle"), send an error that has response code ``400`` and an optional message text.
- If the ``mgmt.firmware.uri`` attribute is not set or is not a valid URI, set the ``rc`` parameter to ``400``.
- If the firmware download attempt fails, set the ``rc`` parameter to ``500`` and optionally set the ``message`` parameter accordingly.
- If the firmware download is not supported, set the ``rc`` parameter to ``500`` and optionally set the ``message`` parameter accordingly.
- When an execute request is received by the device, change the ``mgmt.firmware.state`` attribute from ``0`` (Idle) to ``1`` (Downloading).
- When the download is completed successfully, set the ``mgmt.firmware.state`` attribute to ``2`` (Downloaded).
- If an error occurs during download, set the ``mgmt.firmware.state`` attribute to ``0`` (Idle) and set the ``mgmt.firmware.updateStatus`` attribute to one of the following error status values:
  - 2 (Out of Memory)
  - 3 (Connection Lost)
  - 6 (Invalid URI)
- If a firmware verifier was set, the device attempts to verify the firmware  image. If the image verification fails, set the ``mgmt.firmware.state`` attribute to ``0`` (Idle) and set the ``mgmt.firmware.updateStatus`` attribute to the error status value ``4`` (Verification Failed).

## Firmware Actions - Update
{: #firmware-actions-update}

The installation of the downloaded firmware is initiated by using the REST API by issuing a POST request to:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

The following information is provided:

- The action ``firmware/update``
- The list of devices to receive the image, all of the same device type.
- The URI for the firmware image (optional)
- Verification string to validate the image (optional)
- Firmware name (optional)
- Firmware version  (optional)

The following code is an example request:

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

If any of the optional parameters are specified, then the first message that is received by the device is a device update request. This device update request is similar to the first message of the firmware download request.

To monitor the status of the firmware update, the {{site.data.keyword.iot_short_notm}} first triggers an observer request on the topic ``iotdm-1/observe``. When the device is ready to start the update process, it sends a response that has the ``rc`` parameter set to ``200``, the ``mgmt.firmware.state`` attribute set to ``0``, and the ``mgmt.firmware.updateStatus`` attribute set to ``0``.

The following code provides an example:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/observe
Message:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [
         {
            "field": "mgmt.firmware"
         }
      ]
   }
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



After the firmware update is successfully downloaded, the device management server in the {{site.data.keyword.iot_short_notm}} uses the Device Management Protocol to request that the devices that are specified initiate the firmware installation by using the topic ``iotdm-1/mgmt/initiate/firmware/update``.
If this operation can be initiated immediately, set the ``rc`` parameter to ``202``.
If firmware was not previously downloaded successfully, set the ``rc`` parameter to ``400``.

The following code shows an example:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

Outgoing response from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

To finish the firmware update request, the device reports its update status to the {{site.data.keyword.iot_short_notm}} by using a status message that is published on its ``iotdevice-1/notify``-topic.
When a firmware update is finished, the ``mgmt.firmware.updateStatus`` attribute is set to ``0`` (Success), the ``mgmt.firmware.state`` attribute is set to ``0`` (Idle). The downloaded firmware image can then be deleted from the device, and the ``deviceInfo.fwVersion`` attribute is set to the value of the ``mgmt.firmware.version`` attribute.

The following code provides an example of a notify message:

```
Outgoing message from device:

Topic: iotdevice-1/notify
Message:
{
   "d" : {
      "fields": [
         {
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

When the {{site.data.keyword.iot_short_notm}} receives notification of a completed firmware update, it triggers a last request on the ``iotdm-1/cancel``-topic to cancel the observation of the ``mgmt.firmware`` attribute.


When a response that has the ``rc`` parameter set to ``200`` is sent, the firmware update request is completed, as shown in the following example:

```
Incoming request from the {{site.data.keyword.iot_short_notm}}:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Outgoing message from device:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

The following list provides some useful information for error and process handling:

- If the firmware update attempt fails, set the ``rc`` parameter to ``500`` and optionally set the ``message`` parameter to contain relevant information.
- If the firmware update is not supported, set the ``rc`` parameter to ``501`` and optionally set the ``message`` parameter to contain relevant information.
- If the ``mgmt.firmware.state`` attribute is not ``2`` (Downloaded), send an error that has the ``rc`` parameter set to ``400`` and an optional message text.
- Otherwise, set the ``mgmt.firmware.updateStatus`` attribute to ``1`` (In Progress), and the firmware installation typically is started.
- If firmware installation fails, set the ``mgmt.firmware.updateStatus`` attribute to one of the following values:
  - ``2`` (Out of Memory)
  - ``5`` (Unsupported Image)


**Important:** All parameters that are listed as part of the ``mgmt.firmware`` attribute must be set at the same time so that if there is a current observation for ``mgmt.firmware``, only a single notify message is sent.

## Recipes on Device Actions and Firmware Actions

The following recipes demonstrate the complete flow that is required to perform device and firmware actions.

- [Device Management in WIoT Platform – Roll Back & Factory Reset ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [Device Initiated Firmware Update ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [Platform Initiated Firmware Update ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Platform Initiated Firmware Update with Background Execution ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Firmware Roll Back & Factory Reset ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
