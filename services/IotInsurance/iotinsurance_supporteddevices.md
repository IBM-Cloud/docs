---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Supported devices and vendors
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} supports integration with multiple cloud vendors and devices.
{: shortdesc}

## Supported devices by vendor
{: #supportedvendors}
The following table lists the vendors and devices that are supported by {{site.data.keyword.iotinsurance_short}} and describes the integration type. The following integration types are available:

  - **{{site.data.keyword.iot_short_notm}}** - the device or hub publishes the sensor events directly in {{site.data.keyword.iot_short_notm}}. {{site.data.keyword.iotinsurance_short}} can process the sensor events either directly or after the {{site.data.keyword.iotinsurance_short}} Transformer modifies them slightly.

  - **Cloud to Cloud** - the device or hub publishes the sensor events in a third-party cloud. The {{site.data.keyword.iotinsurance_short}} Transformer reads those events from the third-party cloud and publishes them in {{site.data.keyword.iot_short_notm}}.

<table>
<thead>
<tr>
<th>Vendor name</th>
<th>Integration type</th>
<th>Devices tested</th>
<th>Vendor information </th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
A gateway app was written to test the integration.</td>
<td>Bosch Retrofit E-Call</td>
<td>[Vendor website ![External link icon](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Button</li>
<li>Contact</li>
<li>Temperature</li>
</ul>
</td>
<td>[Vendor website ![External link icon](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Smoke Detector</li>
<li>Button</li></td>
</ul>
<td>[Vendor website ![External link icon](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>Cloud to Cloud</td>
<td>Water Leak</td>
<td>[Vendor website ![External link icon](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} and Cloud to Cloud</td>
<td>No sensors were tested.</td>
<td>[Vendor website ![External link icon](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## Integrating devices and vendor clouds
{: #integratingdevices}
You can integrate your devices and vendor clouds with {{site.data.keyword.iotinsurance_short}}. The following sections provide integration procedures and sample user records for each vendor.

For more information about integrating sensors and devices, see [Device Toolkit](iotinsurance_device_toolkit.html):


### EnOcean
#### Integration procedure
  1. Create a gateway in the {{site.data.keyword.iot_short_notm}} instance that is connected to {{site.data.keyword.iotinsurance_short}}.
  2. Connect the EnOcean hub to the {{site.data.keyword.iot_short_notm}} gateway.
  3. Add the gateway identifier to the user record in {{site.data.keyword.iotinsurance_short}}.

#### Sample user record

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "digital-concepts-gateway1"
    ],
    ...
}
```

### WiButler (iExergy)

#### Integration procedure
Integration with WiButler data is currently supported as a proof of concept or technical preview only and is not intended for production use. WiButler hardware requires a firmware update to stream data to the {{site.data.keyword.iot_short_notm}}.

#### Sample user record

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "Wibutler-Gateway-ID"
    ],
    ...
}
```

### Wink

#### Integration procedure

**Option 1**
  1. Obtain the [Wink authorization tokens ![External link icon](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window}.
  2. Add the authorization token to the corresponding user in the {{site.data.keyword.iotinsurance_short}} system by using the {{site.data.keyword.iotinsurance_short}} API.

**Option 2**  
Integrate by using the mobile app (deprecated). This method works only with version 1.0 of {{site.data.keyword.iotinsurance_short}}.

#### Sample user record

```
{
  "username": "user@example.com",
  "password": "",
  ....
  "deviceID": "528DB5CA-7F3D-4478-A4EB-994E7F118B6B",
  "assets": [
    {
      "name": "default",
      "providers": [
        {
          "name": "wink",
          "tokens": {
            "data": {
              "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
              "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
              "token_type": "bearer",
              "token_endpoint": "https://api.wink.com/oauth2/token",
              "scopes": "full_access"
            },
            "errors": [],
            "pagination": {},
            "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
            "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
            "token_type": "bearer",
            "token_endpoint": "https://api.wink.com/oauth2/token",
            "scopes": "full_access"
          }
        }
      ]
    }
  ]
}

```

### Yanzi
#### Integration procedure
**Option 1**  
  Add credentials of the Yanzi Cloud into yanzi-config.json in the provider's directory of the transformer repository.  The "yanziCloud" object is the correct location of the credentials.  

**Option 2**  
  Yanzi uses a cloud-to-cloud integration between the Yanzi cloud and {{site.data.keyword.iot_short_notm}}. Authorization for this integration occurs within the Yanzi cloud. After authorization is complete, the Yanzi cloud sends events to {{site.data.keyword.iot_short_notm}}. You must also add the credentials of the {{site.data.keyword.iot_short_notm}} instance into yanzi-config.json in the provider's directory of transformer repository by using the "iotfCredentials" object.

#### Sample user record

```
{
  "yanziCloud": {
      "cirrusHost": "wss://",
      "username": "",
      "password": "",
      "locationId": "",
      "unitDid": ""
  },
  "iotfCredentials": {
      "org": "",
      "apiKey": "",
      "apiToken": "",
      "type": "shared",
      "mqtt_host": "gbdprt.messaging.internetofthings.ibmcloud.com",
      "domain": "internetofthings.ibmcloud.com"
  }
}
```

### Weather Company data
#### Integration procedure
Integration with Weather Company data is currently supported as a proof of concept or technical preview only and is not intended for production use.

Supply an address to retrieve the current weather (outside temperature) conditions from the Weather Company for a specific location.



#### Sample user record

```
{ "username": "johndoe",
   "fullname": "John Doe",
    "firstname": "John",
    "lastname": "Doe",
    "password": "",
     "accessLevel": 13,
     "address": "Mies-van-der-Rohe-Straße 6, 80807 München, Germany",
     ...
}

```
