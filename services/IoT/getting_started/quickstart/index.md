---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Quickstart

[Quickstart ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://quickstart.internetofthings.ibmcloud.com/#/){: new_window} is an open sandbox that you can use to quickly connect your devices to the {{site.data.keyword.iot_full}}. If your devices support the MQTT messaging protocol, they can be easily connected to Quickstart.

For examples, recipes, and tutorials that explain how you can connect different devices to the Quickstart service, go to [DeveloperWorks Recipes ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/){: new_window}, for example:

- [OpenBlocks IoT BX1G ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/openblocks-iot-bx1g-for-iot-foundation-quickstart/){: new_window}
- [Reactive Blocks ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/reactive-blocks-and-java-to-iot-foundation-part-1-quickstart/){: new_window}


**Important:** If your {{site.data.keyword.iot_short_notm}} instance uses the Quickstart service, scalable applications are not supported.

## Simulated devices

In addition to the Quickstart recipes and tutorials, a browser-based simulated device for mobile devices is available for you to use to connect any device with a web browser to the Quickstart service. To launch a browser-based simulated device that connects to {{site.data.keyword.iot_short}} from a mobile phone or tablet, open the following URL:

```
http://quickstart.internetofthings.ibmcloud.com/iotsensor
```

When you connect to the simulated device URL on a mobile device, a browser-based simulated device that is connected to the {{site.data.keyword.iot_short}} is started. Use the following UI controls to manage the sensors:

- Temperature
- Humidity
- Object temperature


![image](iotsensor.png)

## Data visualization

To see the data that is generated from your mobile device, ensure that the simulated device runs on your mobile device, and then start the Quickstart application. Enter the 12 character device ID for the device, which is displayed in the upper right corner of the UI.

![image](quickstart.png)

As you adjust the sensor values in your simulated device, you can see the data from your device visualized in real time within the Quickstart application, as outlined in the following screen capture:

![image](iotsensor_data.png)


## Mosquitto demonstration

[Mosquitto ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://mosquitto.org/){: new_window} is a cross platform open source MQTT client that you can use to experiment with the {{site.data.keyword.iot_short}} service. After you install the Mosquitto client, choose an application ID and a device ID that are unique. If the application and device IDs are not unique, your test connection might  result in a conflict with another user who is completing the same Quickstart test procedure.

The *appId*, *type_id*, *device_type*, and *device_id* values must be no more than 36 characters and can contain only the following characters:
- Alpha-numeric characters (a-z, A-Z, 0-9)
- Dashes ( - )
- Underscores ( _ )
- Dots ( . )

After you define the application ID and the device ID, create a connection that represents your application by using `mosquitto_sub`. Use the following examples of `<applicationId>` = myApplicationId and `<deviceId>` = myDeviceId:
```
    [user@host ~]$ mosquitto_sub -h quickstart.messaging.internetofthings.ibmcloud.com -p 1883 -i "a:quickstart:myApplicationId" -t iot-2/type/mosquitto/id/myDeviceId/evt/helloworld/fmt/json

```

While the previous process is running, you can create your device. In this example. connect a device of type `mosquitto` and then send two events to the service by using `mosquitto_pub`, as outlined in the following code:

```
    [user@host ~]$ mosquitto_pub -h quickstart.messaging.internetofthings.ibmcloud.com -p 1883 -i "d:quickstart:mosquitto:myDeviceId" -t iot-2/evt/helloworld/fmt/json -m "{\"helloworld\": 1}"
    [user@host ~]$ mosquitto_pub -h quickstart.messaging.internetofthings.ibmcloud.com -p 1883 -i "d:quickstart:mosquitto:myDeviceId" -t iot-2/evt/helloworld/fmt/json -m "{\"helloworld\": 2}"
```
When you look at your application terminal, the two events that you just published are displayed, as outlined in the following example output:

```
   [user@host ~]$ mosquitto_sub -h quickstart.messaging.internetofthings.ibmcloud.com -p 1883 -i "a:quickstart:myApplicationId" -t iot-2/type/mosquitto/id/myDeviceId/evt/helloworld/fmt/json
    {"helloworld": 1}
    {"helloworld": 2}
```

That’s all there is to it. By completing the Quickstart example procedure, you have:
- Successfully connected a device and an application to the {{site.data.keyword.iot_short}} over MQTT
- Sent an event from the device to the service
- Received the event in your application


## Related links

- [Quickstart ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://quickstart.internetofthings.ibmcloud.com){: new_window}
- [DeveloperWorks Recipes ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes){: new_window}
- [OpenBlocks IoT BX1G ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/openblocks-iot-bx1g-for-iot-foundation-quickstart/){: new_window}
- [Reactive Blocks ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/reactive-blocks-and-java-to-iot-foundation-part-1-quickstart/){: new_window}
- [Quickstart application ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://quickstart.internetofthings.ibmcloud.com){: new_window}
- [Mosquitto ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](http://mosquitto.org/){: new_window}
