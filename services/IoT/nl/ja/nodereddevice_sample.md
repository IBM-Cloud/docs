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

# Node-RED デバイス・シミュレーターの作成と接続
Node-RED を使用して、デバイス・シミュレーターを作成し、シミュレートしたデバイス・データを {{site.data.keyword.iot_full}} 組織に送信します。  
{:shortdesc}

Node-RED は、ハードウェア・デバイス、API、オンライン・サービスを、新しい興味深い方法で接続するツールです。詳しくは、[Node-RED](http://nodered.org/) の Web サイトを参照してください。  

Node-RED インスタンスは、独自の環境で実行することもできますし、{{site.data.keyword.Bluemix_notm}} アプリケーションとして使用することもできます。以下の処理には、{{site.data.keyword.Bluemix_notm}} のための手順が含まれています。

Node-RED デバイス・シミュレーターを作成して接続するには、以下のようにします。

1. Node-RED デバイス・シミュレーターを作成します
   デバイス・シミュレーターを使用して、MQTT デバイス・メッセージを {{site.data.keyword.iot_short_notm}} に送信します。デバイス・シミュレーターは、貨物輸送コンテナーのデータを {{site.data.keyword.iot_short_notm}} などの MQTT ブローカーに送信する処理をシミュレートしたものです。
    1. {{site.data.keyword.Bluemix_notm}} (https://console.ng.bluemix.net) にログインします。
    2. **「カタログ」**タブを選択します。
    3. サービス・カタログの「ボイラープレート」セクションを見つけて、**「Node-RED Starter コミュニティー ベータ」**をクリックします。**ヒント:** [ここ](https://console.ng.bluemix.net/catalog/starters/node-red-starter/)をクリックすると、「Node-RED Starter」ページに直接移動できます。
    4. 「Node-RED Starter」ページで、Node-RED のデプロイ場所となるスペースを選択し、「アプリの作成」選択項目を確認し、**「作成」**をクリックして Node-RED を Bluemix 組織に追加します。
      
以下に例を示します。  
     - スペース: dev
     - 名前: myDevice
     - ホスト: myDevice

    残りのオプションはデフォルト値のままにします。アプリケーションのデプロイ後、「Start coding with Node-RED」ページが表示されます。  
    **注:** ステージング・プロセスには数分かかることがあります。

    3. 「経路」リンクをクリックして、Node-RED を開きます。
      
例: `http://simulatedDevice.mybluemix.net`
    4. **「Go to your Node-RED flow editor」**をクリックして、エディターを開きます。
    5. この文書の [Node-RED ノード・フロー・データ](#flow_data)セクションにある Node-RED フロー・データをコピーします。
    5. Node-RED フロー・エディターの右上隅のメニューをクリックし、**「Import」>「Clipboard」**を選択します。  
    6. クリップボードをインポート・ノードの入力フィールドに貼り付けて、**「Ok」**をクリックします。
    デバイス・シミュレーター・フローがフロー・エディターにインポートされます。

2. デバイスを {{site.data.keyword.iot_short_notm}}   に登録します
Node-RED サンプル・デバイスを接続するには、以下の手順を実行します。
 1. {{site.data.keyword.Bluemix_notm}} でダッシュボードに移動します。
 2. {{site.data.keyword.iot_short_notm}} をデプロイしたスペースを選択します。
 3. **{{site.data.keyword.iot_short_notm}}** タイルをクリックします。
 4. **「ダッシュボードを起動」**をクリックして、{{site.data.keyword.iot_short_notm}} ダッシュボードを開きます。
 5. **「デバイス」**を選択します。
 6. **「デバイスの追加」**をクリックします。
 7. **「デバイス・タイプの作成」**をクリックします。
 9. デバイス・タイプの記述名 (`sample_device` など) と説明を入力します。
 10. オプション: デバイス・タイプの属性を入力します。
 11. オプション: デバイス・タイプのメタデータを入力します。
 12. **「作成」**をクリックして、新しいデバイス・タイプを追加します。
 13. **「次へ」**をクリックしてデバイスを追加します。
 14. デバイス ID を入力します (`Device001` など)。
 15. オプション: デバイスのメタデータを入力します。
 16. **「次へ」**をクリックして、自動生成認証トークンを使用するデバイス接続を追加します。
 17. 要約情報が正しいことを確認してから、**「追加」**をクリックして接続を追加します。
 18. 表示されるデバイス情報のページで、デバイス情報をコピーして保存します。  
  <ul>
  <li> 組織 ID
  <li> デバイス・タイプ
  <li> デバイス ID
  <li> 認証方式
  <li> 認証トークン
  </ul>
  **ヒント:** 次のいくつかのステップで、Node-RED アプリケーションの構成を終了して接続を完了するときに、組織 ID、認証トークン、デバイス・タイプ、デバイス ID が必要になります。

2. デバイスを {{site.data.keyword.iot_short_notm}} に接続します  
 1. Node-RED フロー・エディターを開きます。
 2. 「Publish to IoT」ノードをダブルクリックします。
 3. トピック・エントリーが `iot-2/evt/event_name/fmt/json` であることを確認します。**ヒント:** トピックの /event_name の部分で、パブリッシュされるイベントのイベント名が設定されます。
 4. 「Server」フィールドの横にある編集アイコンをクリックします。
 5. サーバー名が {{site.data.keyword.iot_short_notm}} 組織に対応するように更新します。  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 {organization_ID} は前に保存した*組織 ID* です。
 6. 組織 ID、デバイス・タイプ、デバイス ID によりクライアント ID を更新します。
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   {organization_ID}、{device_type}、{device_ID} は、前に保存した値です。
 7. **「Security」**タブをクリックします。
 8. 「Username」フィールドの値が `use-token-auth` であることを確認します。
 9. 「Password」フィールドを、前に保存した*認証トークン*により更新します。
 10. **「Update」**をクリックしてから**「OK」**をクリックします。
 12. Node-RED フロー・エディターの右上隅で、**「Deploy」**をクリックします。
 13. 「Publish to IoT」ノードの接続状況の表示が*「connected」*であることを確認します。**ヒント:** 接続が確立されていない場合は、入力した設定値を再度確認してください。カット・アンド・ペーストでわずかな誤りがあっても、接続は失敗します。

4. デバイスの接続を検証します
 1. ブラウザーの別のタブまたはウィンドウで、{{site.data.keyword.iot_short_notm}} ダッシュボードを開きます。
 2. **「Devices」**を選択し、**Device001** (または追加したデバイスの名前がそれとは違う場合はその名前) をクリックします。
   
デバイス情報のページが表示されます。このビューで、デバイスの接続状況を確認できます。この段階で、デバイスは切断されているものとして表示されているはずです。   
 3. Node-RED フロー・エディターに戻り、「Inject」ノードのボタンをクリックして、アセット・ペイロードを生成します。
   
ペイロードには、以下のデータ・ポイントが含まれています。  
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

 3. 右側ペインのデバッグ・タブで、メッセージが作成されていることを確認します。  
 4. {{site.data.keyword.iot_short_notm}} デバイス情報ページに戻ります。デバイスが接続状態になっているはずです。データ・ポイントがデバイスから受信したのと同じであることを確認してください。  
 ```
 Event	Datapoint	 Value	Time Received
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 これでサンプル IoT デバイスが {{site.data.keyword.iot_short_notm}} に接続され、デバイス・データが表示されるようになりました。

## Node-RED ノード・フロー・データ
{: #flow_data}  
以下のテキストをクリップボードにコピーし、Node-RED フロー・エディターでノードをインポートする際にインポート・クリップボードにそれを貼り付けます。   
**重要:** 前後の大括弧を含め、テキストのすべてを確実にコピーしてください。  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Double click the node.\n2. Click the edit icon next to the Server field.\n3. Update the Server name to correspond to your Watson IoT Platform organization.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Update the Client ID with your orgainzaiton ID, device type, and device ID:\n `d:organization_ID:device_type:device_ID`\n\n5. Click the Security tab.\n6. Verify that the Username field has the value use-auth-token.\n7. Update the Password field with the Authentication Token that you saved earlier.\n8. Click Update and then OK.\n9. In the upper right corner of the Node-RED flow editor, click Deploy. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"The Function node allows you to pass each message though a JavaScript function.\n\nThe Javascript function creates the message payload that is sent to your Watson IoT Platform organization.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.","x":75,"y":236,"wires":[]}]
```
{:codeblock}
