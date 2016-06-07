---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creating and connecting a Node-RED device simulator
Use Node-RED to create a device simulator and send simulated device data to your {{site.data.keyword.iot_full}} organization.  
{:shortdesc}

Node-RED is a tool for wiring together hardware devices, APIs and online services in new and interesting ways. For more information, see the [Node-RED](http://nodered.org/) web site.  

You can run your Node-RED instance in your own environment or use it as a {{site.data.keyword.Bluemix_notm}} application. The following process includes the instructions for {{site.data.keyword.Bluemix_notm}}.

To create and connect the Node-RED device simulator:

1. Create the Node-RED device simulator
   Use the device simulator to send MQTT device messages to {{site.data.keyword.iot_short_notm}}. The device simulator simulated sending data for a freight container to an MQTT broker such as {{site.data.keyword.iot_short_notm}}.
    1. Log in to {{site.data.keyword.Bluemix_notm}} at: https://console.ng.bluemix.net
    2. Select the **Catalog** tab.
    3. Locate the Boilerplates section of the service catalog and click  **Node-RED Starter Community BETA**. **Tip:** Click  [here](https://console.ng.bluemix.net/catalog/starters/node-red-starter/) to go directly to the Node-RED Starter page.
    4. On the Node-RED Starter page, select the space where you want to deploy Node-RED, verify the Create an app selections, and click **Create** to add Node-RED to your Bluemix organization.  
    For example:  
     - Space: dev
     - Name: myDevice
     - Host: myDevice

    Leave the rest of the options at their default values. After the application is deployed, you are brought to the Start coding with Node-RED page.  
    **Note:** The staging process might take a few minutes.

    3. Click the app link at the top of the page to open Node-RED.  
    Example: `http://simulatedDevice.mybluemix.net`
    4. Click **Go to your Node-RED flow editor** to open the editor.
    5. Copy the Node-RED flow data that you find in the [Node-RED node flow data](#flow_data) section of this document.
    5. In the Node-RED flow editor, click the menu in the upper right corner and select **Import > Clipboard**.  
    6. Paste the clipboard into the import nodes input field and and click **Ok**.
    The device simulator flow is imported to the flow editor.

2. Register your device with {{site.data.keyword.iot_short_notm}}  
Follow these steps to connect the the Node-RED sample device:
 1. In {{site.data.keyword.Bluemix_notm}}, go to Dashboard
 2. Select the space in which you deployed {{site.data.keyword.iot_short_notm}}.
 3. Click the **{{site.data.keyword.iot_short_notm}}** tile.
 4. Click **Launch dashboard** to open the {{site.data.keyword.iot_short_notm}} dashboard.
 5. Select **Devices**
 6. Click **Add Device**
 7. Click **Create device type**.
 9. Enter a descriptive name and description for the device type, such as `sample_device`.
 10. Optional: Enter device type attributes.
 11. Optional: Enter device type meta data.
 12. Click **Create** to add the new device type.
 13. Click **Next** to add your device.
 14. Enter a device ID such as `Device001`.
 15. Optional: Enter device meta data.
 16. Click **Next** to add a device connection with an auto-generated authentication token.
 17. Verify that the summary information is correct, and then click **Add** to add the connection.
 18. In the device information page that opens, copy and save the device information:  
  <ul>
  <li> Organization ID
  <li> Device Type
  <li> Device ID
  <li> Authentication Method
  <li> Authentication Token
  </ul>
  **Tip:** You will need Organization ID, Authentication Token, Device Type, and Device ID in the next few steps to finalize the configuration of the Node-RED application to complete the connection.

2. Connect your device to {{site.data.keyword.iot_short_notm}}  
 1. Open the Node-RED flow editor.
 2. Double-click the Publish to IoT node.
 3. Verify that the topic entry is: `iot-2/evt/event_name/fmt/json` **Tip:** The /event_name part of the topic sets the event name for the published events.
 4. Click the edit icon next to the Server field.
 5. Update the Server name to correspond to your {{site.data.keyword.iot_short_notm}} organization.  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 Where {organization_ID} is the *Organization ID* that you saved earlier.
 6. Update the  Client ID with your organization ID, device type, and device ID:
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   Where {organization_ID}, {device_type}, and {device_ID} where the values that you saved earlier.
 7. Click the **Security** tab.
 8. Verify that the Username field has the value `use-token-auth`.
 9. Update the Password field with the *Authentication Token* that you saved earlier.
 10. Click **Update** and then **OK**.
 12. In the upper right corner of the Node-RED flow editor, click **Deploy**.
 13. Verify that the Publish to IoT node connection status displays *connected*.  **Tip:** If the connection is not made, double check the settings that you entered. Even a small cut and paste error will cause the connection to fail.

4. Validate the device connection
 1. In another browser tab or window, open the {{site.data.keyword.iot_short_notm}} dashboard.
 2. Select **Devices** and click **Device001** or the name of the device that you added, if different.  
 The device information page opens. This view lets you see the connection status for your device. The device should show as disconnected at this stage.   
 3. Back in your Node-RED flow editor, click the button on the Inject node to generate an asset payload.  
 The payload contains the following data points:  
 ```
 {"d":
  { "name":"My Device",
    "location":
    {
      "longitude":-87.90,
      "latitude":43.03
    },
    "velocity":13,
    "type":"GPS"
  }
 }
 ```
  {:codeblock}  

 3. In the debug tab of the right pane, verify that messages are created.  
 4. Back in the {{site.data.keyword.iot_short_notm}} device information page, the device should now be connected. Verify that you see the same data points received from the device.  
 ```
 Event	Datapoint	 Value	Time Received
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 You have now connected your sample IoT device to {{site.data.keyword.iot_short_notm}} and can see device data.

## Node-RED node flow data
{: #flow_data}  
Copy the text below to your clipboard and then paste it into the import clipboard when importing nodes in the Node-RED flow editor.   
**Important:** Make sure that you copy all the text including the leading and trailing square brackets.  

```[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Double click the node.\n2. Click the edit icon next to the Server field.\n3. Update the Server name to correspond to your Watson IoT Platform organization.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Update the Client ID with your orgainzaiton ID, device type, and device ID:\n `d:organization_ID:device_type:device_ID`\n\n5. Click the Security tab.\n6. Verify that the Username field has the value use-auth-token.\n7. Update the Password field with the Authentication Token that you saved earlier.\n8. Click Update and then OK.\n9. In the upper right corner of the Node-RED flow editor, click Deploy. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"The Function node allows you to pass each message though a JavaScript function.\n\nThe Javascript function creates the message payload that is sent to your Watson IoT Platform organization.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.","x":75,"y":236,"wires":[]}]```
{:codeblock}
