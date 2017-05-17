---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-17"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Enabling support for Wally data
{: #wallysupport}

{{site.data.keyword.iotinsurance_full}} supports integration with data from Wally sensors and services. Wally is a third-party wireless sensor provider.
{: shortdesc}

## Prerequisites
To enable {{site.data.keyword.iotinsurance_short}} to use Wally data, you must have an active Wally organization that is associated with the accounts for which data is to be retrieved. Your Wally account must be enabled to use the Partner REST API, and you must obtain a security token from the Wally settings page. For more information, see the [Wally website ![External link icon](../../icons/launch-glyph.svg)](https://my.wallyhome.com/){:new_window}.

## Configuring {{site.data.keyword.iotinsurance_short}} to use Wally as a data provider
{: #configuringwally}

Use environment variables to configure the {{site.data.keyword.iotinsurance_short}} transformer to pull events and activities for the accounts that are associated with a Wally organization.

1. From your Bluemix dashboard, open the iot4i-transformer application.
2. Select **Runtime**, then click **Environment Variables**.
3. In the **User Defined** section, click **Add**.
4. Enter the following environment variables and associated values as required, then click **Save**.

  <table>
<thead>
<tr>
<th>Name</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>WALLY_ORG</td>
<td>string</td>
<td>(Required) The name of the Wally organization to use, provided by Wally.</td>
</tr>
<tr>
<td>WALLY_SECURITY_TOKEN</td>
<td>string</td>
<td>(Required) The security token that is used to access the data, provided by Wally.</td>
</tr>
<tr>
<td>WALLY_CREATE_DEVICES</td>
<td>true or false</td>
<td>(Optional) `true` indicates that the Wally provider creates an IoT device in the associated IoT Platform instance for each Wally device. The default value is false. </td>
</tr>
<tr>
<td>WALLY_POLLING_INTERVAL</td>
<td>Integer from '2' to '60'</td>
<td>(Optional) The interval at which the IoT4I transformer polls data from the Wally cloud. The default value is '2'.</td>
</tr>
</tbody>
</table>

5. Restart the iot4i-transformer application by clicking the Restart icon that is next to the Routes button.


## Associating {{site.data.keyword.iotinsurance_short}} users with Wally data
{: #associatingusers}

Associating {{site.data.keyword.iotinsurance_short}} users with Wally data is done by creating a user, creating a device ID, and then associating the device ID with a user.

1. Create an {{site.data.keyword.iotinsurance_short}} user by using the 'addUser' API. For information about using the API to create users, see the [{{site.data.keyword.iotinsurance_short}} API documentation ![External link icon](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/#!/user/addUser){:new_window}.

2. Create a device ID for each Wally sensor by using the 'addDevice' API. The device record must contain the Wally sensor ID that is provided by the Wally REST API. For information about using the API to add devices, see the [{{site.data.keyword.iotinsurance_short}} API documentation ![External link icon](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/#!/device/addDevice){:new_window}.

3. Create a device record to associate each device ID with a user by using the 'device' API and use a payload that is similar to the following example:

   ```
{
  "iot4i_device_id": "90-7a-e2-00-41-d6-02-4d",
  "usr": "user@example.com"
}
```

To see an example of the /device API that is used to associate a device ID with a user, see the [{{site.data.keyword.iotinsurance_short}} /device API example ![External link icon](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/device.js){:new_window}.  
