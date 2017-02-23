---

copyright:
  years: 2016, 2017
lastupdated: "2016-08-26"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 创建并连接 Node-RED 设备模拟器
使用 Node-RED 创建设备模拟器并将模拟设备数据发送到 {{site.data.keyword.iot_full}} 组织。  
{:shortdesc}

Node-RED 是一款以全新且有趣的方法，将硬件设备、API 和在线服务连接在一起的工具。有关更多信息，请参阅 [Node-RED](http://nodered.org/) Web 站点。  

可以在您自己的环境中运行 Node-RED 实例或将其用作 {{site.data.keyword.Bluemix_notm}} 应用程序。以下过程包含 {{site.data.keyword.Bluemix_notm}} 的指示信息。

要创建并连接 Node-RED 设备模拟器，请执行以下操作：

1. 创建 Node-RED 设备模拟器
   使用设备模拟器将 MQTT 设备消息发送到 {{site.data.keyword.iot_short_notm}}。设备模拟器已模拟将货物集装箱的数据发送到 MQTT 代理程序（例如，{{site.data.keyword.iot_short_notm}}）。
    1. 登录到 {{site.data.keyword.Bluemix_notm}}，网址为：https://console.ng.bluemix.net
    2. 选择**目录**选项卡。
    3. 找到服务目录的“样板”部分并单击 **Node-RED 入门模板社区 BETA**。**提示：**单击[此处](https://console.ng.bluemix.net/catalog/starters/node-red-starter/)可直接转至 Node-RED 入门模板页面。
    4. 在 Node-RED 入门模板页面上，选择您要部署 Node-RED 的空间，验证“创建应用程序”的选项，并单击**创建**以将 Node-RED 添加到 Bluemix 组织。  
例如：  
     - 空间：dev
     - 名称：myDevice
     - 主机：myDevice

    将其他选项保留为缺省值。部署应用程序后，将转至“使用 Node-RED 开始编码”页面。  
    **注：**编译打包过程可能会花费几分钟。

    3. 单击“路由”链接以打开 Node-RED。
      
示例：`http://simulatedDevice.mybluemix.net`
    4. 单击**转至 Node-RED 流程编辑器**，以打开编辑器。
    5. 复制您在本文档的 [Node-RED 节点流数据](#flow_data)部分中找到的 Node-RED 流数据。
    5. 在 Node-RED 流程编辑器中，单击右上角的菜单，并选择**导入 > 剪贴板**。  
    6. 将剪贴板粘贴到导入节点输入字段并单击**确定**。
    设备模拟器流程已导入流程编辑器。

2. 向 {{site.data.keyword.iot_short_notm}}   注册您的设备
执行以下步骤以连接 Node-RED 样本设备：
 1. 在 {{site.data.keyword.Bluemix_notm}} 中，转至“仪表板”
 2. 选择在其中部署了 {{site.data.keyword.iot_short_notm}} 的空间。
 3. 单击 **{{site.data.keyword.iot_short_notm}}** 磁贴。
 4. 单击**启动仪表板**以打开 {{site.data.keyword.iot_short_notm}} 仪表板。
 5. 选择**设备**
 6. 单击**添加设备**
 7. 单击**创建设备类型**。
 9. 输入设备类型的描述性名称和描述，如 `sample_device`。
 10. 可选：输入设备类型属性。
 11. 可选：输入设备类型元数据。
 12. 单击**创建**以添加新设备类型。
 13. 单击**下一步**以添加设备。
 14. 输入设备标识，如 `Device001`。
 15. 可选：输入设备元数据。
 16. 单击**下一步**以添加通过自动生成的认证令牌实现的设备连接。
 17. 验证摘要信息是否正确，然后单击**添加**以添加连接。
 18. 在打开的设备信息页面中，复制并保存设备信息：  
  <ul>
  <li> 组织标识<li> 设备类型<li> 设备标识<li> 认证方法<li> 认证令牌</ul>
  **提示：**在接下来的几步中，您将需要“组织标识”、“认证令牌”、“设备类型”和“设备标识”来最终化 Node-RED 应用程序的配置，以完成连接。
2. 将设备连接到 {{site.data.keyword.iot_short_notm}}  
 1. 打开 Node-RED 流程编辑器。
 2. 双击“发布到 IoT”节点。
 3. 验证主题条目是否为 `iot-2/evt/event_name/fmt/json`
**提示：**主题的 /event_name 部分用于设置已发布事件的事件名称。
 4. 单击“服务器”字段旁的“编辑”图标。
 5. 更新服务器名称以使其对应于您的 {{site.data.keyword.iot_short_notm}} 组织。  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 其中 {organization_ID} 是之前保存的*组织标识*。
 6. 使用组织标识、设备类型和设备标识更新“客户机标识”：
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   其中 {organization_ID}、{device_type} 和 {device_ID} 是之前保存的值。
 7. 单击**安全性**选项卡。
 8. 验证“用户名”字段的值是否为 `use-token-auth`。
 9. 使用之前保存的*认证令牌*更新“密码”字段。
 10. 单击**更新**，然后单击**确定**。
 12. 在 Node-RED 流程编辑器的右上角，单击**部署**。
 13. 验证“发布到 IoT”节点的连接状态是否显示为*已连接*。**提示：**如果未建立连接，请仔细检查您输入的设置。即使是较小的剪切和粘贴错误也会导致连接失败。

4. 验证设备连接
 1. 在另一个浏览器选项卡或窗口中，打开 {{site.data.keyword.iot_short_notm}} 仪表板。
 2. 选择**设备**并单击 **Device001** 或您添加的设备的名称（如果不同）。
   
此时将打开设备信息页面。通过此视图，您可以查看设备的连接状态。在此阶段，设备应该会显示为已断开连接。   
 3. 回到 Node-RED 流程编辑器，单击“插入”节点上的按钮，以生成资产有效内容。
   
有效内容包含以下数据点：  
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

 3. 在右窗格的调试选项卡中，验证已创建消息。  
 4. 返回到 {{site.data.keyword.iot_short_notm}} 设备信息页面，设备现在应该已连接。验证是否会看到从设备收到的相同数据点。  
 ```
 Event	Datapoint	 Value	Time Received
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 现在，您已将样本 IoT 设备连接到 {{site.data.keyword.iot_short_notm}}，并且可看到设备数据。

## Node-RED 节点流数据
{: #flow_data}  
将以下文本复制到剪贴板，然后在 Node-RED 流程编辑器中导入节点时将其粘贴到导入剪贴板。   
**重要信息：**确保复制了包括左方括号和右方括号在内的所有文本。  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Double click the node.\n2. Click the edit icon next to the Server field.\n3. Update the Server name to correspond to your Watson IoT Platform organization.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Update the Client ID with your orgainzaiton ID, device type, and device ID:\n `d:organization_ID:device_type:device_ID`\n\n5. Click the Security tab.\n6. Verify that the Username field has the value use-auth-token.\n7. Update the Password field with the Authentication Token that you saved earlier.\n8. Click Update and then OK.\n9. In the upper right corner of the Node-RED flow editor, click Deploy. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"The Function node allows you to pass each message though a JavaScript function.\n\nThe Javascript function creates the message payload that is sent to your Watson IoT Platform organization.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.","x":75,"y":236,"wires":[]}]
```
{:codeblock}
