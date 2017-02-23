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

# 建立及連接 Node-RED 裝置模擬器
使用 Node-RED 來建立裝置模擬器，並將模擬的裝置資料傳送至 {{site.data.keyword.iot_full}} 組織。  
{:shortdesc}

Node-RED 是一種工具，以全新且有趣的方式，將硬體裝置、API 和線上服務連接在一起。如需相關資訊，請參閱 [Node-RED](http://nodered.org/) 網站。  

您可以在自己的環境中執行 Node-RED 實例，或是將其用來作為 {{site.data.keyword.Bluemix_notm}} 應用程式。下列程序包含 {{site.data.keyword.Bluemix_notm}} 的指示。

若要建立及連接 Node-RED 裝置模擬器，請執行下列動作：

1. 建立 Node-RED 裝置模擬器
   使用裝置模擬器，將 MQTT 裝置訊息傳送至 {{site.data.keyword.iot_short_notm}}。裝置模擬器模擬將貨櫃資料傳送至 MQTT 分配管理系統，例如 {{site.data.keyword.iot_short_notm}}。
    1. 在 https://console.ng.bluemix.net 登入 {{site.data.keyword.Bluemix_notm}}：
    2. 選取**型錄**標籤。
    3. 找到服務型錄的「樣板」區段，然後按一下 **Node-RED 入門範本社群測試版**。**提示：**按一下[這裡](https://console.ng.bluemix.net/catalog/starters/node-red-starter/)，直接移至「Node-RED 入門範本」頁面。
    4. 在「Node-RED 入門範本」頁面上，選取要部署 Node-RED 的空間，驗證「建立應用程式」選項，然後按一下**建立**，將 Node-RED 新增至您的 Bluemix 組織。  
例如：  
     - 空間：dev
     - 名稱：myDevice
     - 主機：myDevice

    將其餘選項保留為其預設值。部署應用程式之後，您會被帶到「開始使用 Node-RED 撰寫程式碼」頁面。  
    **附註：**暫置程序可能需要一些時間。

    3. 按一下「路徑」鏈結，以開啟 Node-RED。  
範例：`http://simulatedDevice.mybluemix.net`
    4. 按一下 **Go to your Node-RED flow editor**，以開啟編輯器。
    5. 複製您在本文件的 [Node-RED 節點流程資料](#flow_data)區段中找到的 Node-RED 流程資料。
    5. 在 Node-RED 流程編輯器中，按一下右上角的功能表，然後選取**匯入 > 剪貼簿**。  
    6. 在匯入節點輸入欄位中貼上剪貼簿，然後按一下**確定**。裝置模擬器流程即會匯入至流程編輯器。

2. 向 {{site.data.keyword.iot_short_notm}} 登錄裝置  
遵循下列步驟來連接 Node-RED 範例裝置：
 1. 在 {{site.data.keyword.Bluemix_notm}} 中，移至「儀表板」。
 2. 選取已在其中部署 {{site.data.keyword.iot_short_notm}} 的空間。
 3. 按一下 **{{site.data.keyword.iot_short_notm}}** 磚。
 4. 按一下**啟動儀表板**，以開啟 {{site.data.keyword.iot_short_notm}} 儀表板。
 5. 選取**裝置**。
 6. 按一下**新增裝置**。
 7. 按一下**建立裝置類型**。
 9. 輸入裝置類型的敘述性名稱和說明，例如 `sample_device`。
 10. 選用項目：輸入裝置類型屬性。
 11. 選用項目：輸入裝置類型 meta 資料。
 12. 按一下**建立**，以新增裝置類型。
 13. 按**下一步**，以新增裝置。
 14. 輸入裝置 ID，例如 `Device001`。
 15. 選用項目：輸入裝置 meta 資料。
 16. 按**下一步**，使用自動產生的鑑別記號來新增裝置連線。
 17. 驗證摘要資訊正確無誤，然後按一下**新增**，以新增連線。
 18. 在開啟的裝置資訊頁面中，複製並儲存裝置資訊：  
  <ul>
  <li> 組織 ID
  <li> 裝置類型
  <li> 裝置 ID
  <li> 鑑別方法
  <li> 鑑別記號
  </ul>
  **提示：**在接下來幾個步驟中，您需要有「組織 ID」、「鑑別記號」、「裝置類型」和「裝置 ID」才能完成 Node-RED 應用程式的配置，以完成連線。

2. 將您的裝置連接至 {{site.data.keyword.iot_short_notm}}  
 1. 開啟 Node-RED 流程編輯器。
 2. 按兩下「發佈至 IoT 節點」。
 3. 驗證主題項目為：`iot-2/evt/event_name/fmt/json` **提示：**主題的 /event_name 部分會設定所發佈事件的事件名稱。
 4. 按一下「伺服器」欄位旁的「編輯」圖示。
 5. 更新「伺服器」名稱，以對應至您的 {{site.data.keyword.iot_short_notm}} 組織。  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 其中 {organization_ID} 是您先前儲存的*組織 ID*。
 6. 使用您的組織 ID、裝置類型和裝置 ID 來更新「用戶端 ID」：
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   其中 {organization_ID}、{device_type} 和 {device_ID} 是您先前儲存的值。
 7. 按一下**安全**標籤。
 8. 驗證「使用者名稱」欄位中有 `use-token-auth` 值。
 9. 使用您先前儲存的*鑑別記號*來更新「密碼」欄位。
 10. 按一下**更新**，然後按一下**確定**。
 12. 按一下 Node-RED 流程編輯器右上角的**部署**。
 13. 驗證「發佈至 IoT 節點連線狀態」顯示為*已連接*。**提示：**如果未建立連線，請重複確認您所輸入的設定。即使是小小的剪下及貼上錯誤，都會導致連線失敗。

4. 驗證裝置連線
 1. 在另一個瀏覽器分頁或視窗中，開啟 {{site.data.keyword.iot_short_notm}} 儀表板。
 2. 選取**裝置**，然後按一下 **Device001**，或是您新增的裝置名稱（如果不同）。  
即會開啟裝置資訊頁面。此視圖可讓您查看裝置的連線狀態。在這個階段，裝置應該會顯示為斷線。   
 3. 回到 Node-RED 流程編輯器，按一下「注入」節點上的按鈕，以產生資產有效負載。  
有效負載包含下列資料點：  
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

 3. 在右窗格的除錯標籤中，驗證已建立訊息。  
 4. 回到 {{site.data.keyword.iot_short_notm}} 裝置資訊頁面，裝置現在應該已連接。驗證您看到從裝置所收到的相同資料點。  
 ```
 Event	Datapoint	 Value	Time Received
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 您現在已將 IoT 裝置範例連接至 {{site.data.keyword.iot_short_notm}}，並且可以看到裝置資料。

## Node-RED 節點流程資料
{: #flow_data}  
將下列文字複製到剪貼簿，然後在 Node-RED 流程編輯器中匯入節點時，再將它貼到匯入剪貼簿中。   
**重要事項：**請確定您複製所有文字，包括前後的方括弧。  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Double click the node.\n2. Click the edit icon next to the Server field.\n3. Update the Server name to correspond to your Watson IoT Platform organization.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Update the Client ID with your orgainzaiton ID, device type, and device ID:\n `d:organization_ID:device_type:device_ID`\n\n5. Click the Security tab.\n6. Verify that the Username field has the value use-auth-token.\n7. Update the Password field with the Authentication Token that you saved earlier.\n8. Click Update and then OK.\n9. In the upper right corner of the Node-RED flow editor, click Deploy. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"The Function node allows you to pass each message though a JavaScript function.\n\nThe Javascript function creates the message payload that is sent to your Watson IoT Platform organization.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.","x":75,"y":236,"wires":[]}]
```
{:codeblock}
