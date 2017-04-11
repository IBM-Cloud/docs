---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Node-RED 디바이스 시뮬레이터 작성 및 연결
Node-RED를 사용하여 디바이스 시뮬레이터를 작성하고 시뮬레이션된 디바이스 데이터를 {{site.data.keyword.iot_full}} 조직에 보냅니다.  
{:shortdesc}

Node-RED는 새롭고 흥미로운 방식으로 하드웨어 디바이스, API 및 온라인 서비스를 함께 연결하는 데 사용하는 도구입니다. 자세한 정보는 [Node-RED ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://nodered.org/){: new_window} 웹 사이트를 참조하십시오.   

고유 환경에서 Node-RED 인스턴스를 실행하고 {{site.data.keyword.Bluemix_notm}} 애플리케이션으로 사용할 수 있습니다. 다음 프로세스에는 {{site.data.keyword.Bluemix_notm}}의 지시사항이 포함됩니다.

Node-RED 디바이스 시뮬레이터를 작성하여 연결하려면 다음을 수행하십시오.

1. Node-RED 디바이스 시뮬레이터 작성
   디바이스 시뮬레이터를 사용하여 MQTT 디바이스 메시지를 {{site.data.keyword.iot_short_notm}}에 보냅니다. 디바이스 시뮬레이터는 운송 컨테이너의 데이터를 MQTT 브로커(예: {{site.data.keyword.iot_short_notm}})에 보내기를 시뮬레이션합니다.
    1. https://console.ng.bluemix.net에서 {{site.data.keyword.Bluemix_notm}}에 로그인합니다.
    2. **카탈로그** 탭을 선택합니다.
    3. 서비스 카탈로그의 표준 유형 섹션을 찾아 **Node-RED Starter Community BETA**를 클릭합니다. **팁:** Node-RED Starter 페이지로 바로 이동하려면 [여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/catalog/starters/node-red-starter/){: new_window}를 클릭하십시오. 
    4. Node-RED Starter 페이지에서 Node-RED를 배치할 영역을 선택하고 앱 작성 선택사항을 확인하고 **작성**을 클릭하여 Node-RED를 Bluemix 조직에 추가합니다.  
예를 들어 다음과 같습니다.  
     - 영역: dev
     - 이름: myDevice
     - 호스트: myDevice

    나머지 옵션은 기본값으로 두십시오. 애플리케이션이 배치되고 나면 Node-RED로 코딩 시작 페이지가 표시됩니다.  
    **참고:** 스테이징 프로세스는 몇 분이 걸릴 수 있습니다.

    3. 라우트 링크를 클릭하여 Node-RED를 엽니다.  
    예: `http://simulatedDevice.mybluemix.net`
    4. **Node-RED 플로우 편집기로 이동**을 클릭하여 편집기를 엽니다.
    5. 이 문서의 [Node-RED 노드 플로우 데이터](#flow_data) 섹션에 있는 Node-RED 플로우 데이터를 복사합니다.
    5. Node-RED 플로우 편집기에서 오른쪽 상단에 있는 메뉴를 클릭하고 **가져오기 > 클립보드**를 선택합니다.  
    6. 가져오기 노드 입력 필드에 클립보드를 붙여넣고 **확인**을 클릭합니다.
    디바이스 시뮬레이터 플로우를 플로우 편집기로 가져옵니다.

2. {{site.data.keyword.iot_short_notm}}  에 디바이스 등록
다음 단계를 따라 Node-RED 샘플 디바이스에 연결하십시오.
 1. {{site.data.keyword.Bluemix_notm}}에서 대시보드로 이동합니다.
 2. {{site.data.keyword.iot_short_notm}}을 배치한 영역을 선택합니다.
 3. **{{site.data.keyword.iot_short_notm}}** 타일을 클릭합니다.
 4. **대시보드 실행**을 클릭하여 {{site.data.keyword.iot_short_notm}} 대시보드를 엽니다.
 5. **디바이스**를 선택합니다.
 6. **디바이스 추가**를 클릭합니다.
 7. **디바이스 유형 작성**을 클릭합니다.
 9. 디바이스 유형의 설명적 이름과 설명(예: `sample_device`)을 입력합니다.
 10. 선택사항: 디바이스 유형 속성을 입력합니다.
 11. 선택사항: 디바이스 유형 메타데이터를 입력합니다.
 12. **작성**을 클릭하여 새 디바이스 유형을 추가합니다.
 13. **다음**을 클릭하여 디바이스를 추가합니다.
 14. 디바이스 ID(예: `Device001`)를 입력합니다.
 15. 선택사항: 디바이스 메타데이터를 입력합니다.
 16. **다음**를 클릭하여 자동 생성 인증 토큰과 디바이스 연결을 추가합니다.
 17. 요약 정보가 올바른지 확인한 다음 **추가**를 클릭하여 연결을 추가합니다.
 18. 디바이스 정보 페이지가 열리면 다음 디바이스 정보를 복사하고 저장합니다.  
  <ul>
  <li> 조직 ID
  <li> 디바이스 유형
  <li> 디바이스 ID
<li> 인증 메소드
  <li> 인증 토큰
  </ul>
  **팁:** 연결을 완료하기 위해 Node-Red 애플리케이션 구성을 완료하려면 다음 몇 단계에서 조직 ID, 인증 토큰, 디바이스 유형 및 디바이스 ID가 필요합니다.

2. {{site.data.keyword.iot_short_notm}}에 디바이스를 연결하십시오.  
 1. Node-RED 플로우 편집기를 엽니다.
 2. IoT 노드에 공개를 두 번 클릭합니다.
 3. 주제 항목이 `iot-2/evt/event_name/fmt/json`인지 확인합니다. **팁:** 주제의 /event_name 파트는 공개된 이벤트의 이벤트 이름을 설정합니다.
 4. 서버 필드 옆의 편집 아이콘을 클릭합니다.
 5. {{site.data.keyword.iot_short_notm}} 조직에 맞게 서버 이름을 업데이트합니다.  
 ```
 {organization_ID}.messaging.internetofthings.ibmcloud.com
 ```  
 여기서 {organization_ID}는 이전에 저장한 *조직 ID*입니다.
 6. 클라이언트 ID를 조직 ID, 디바이스 유형 및 디바이스 ID로 업데이트합니다.
 ```
 d:{organization_ID}:{device_type}:{device_ID}
   ```  
   여기서 {organization_ID}, {device_type} 및 {device_ID}는 이전에 저장한 값입니다.
 7. **보안** 탭을 클릭합니다.
 8. 사용자 이름 필드에 `use-token-auth` 값이 있는지 확인합니다.
 9. 이전에 저장한 *인증 토큰*으로 비밀번호 필드를 업데이트합니다.
 10. **업데이트**를 클릭한 다음 **확인**을 클릭합니다.
 12.  Node-RED 플로우 편집기의 오른쪽 상단에서 **배치**를 클릭합니다.
 13. IoT에 공개 노드 연결 상태에 *연결됨*이 표시되는지 확인합니다. **팁:** 연결이 되지 않으면 입력한 설정을 다시 확인하십시오. 사소한 잘라내어 붙여넣기 오류만 있어도 연결에 실패할 수 있습니다.

4. 디바이스 연결 유효성 검증
 1. 다른 브라우저 탭 또는 창에서 {{site.data.keyword.iot_short_notm}} 대시보드를 엽니다.
 2. **디바이스**를 선택하고 **Device001** 또는 추가한 디바이스 이름이 다른 경우 해당 이름을 클릭합니다.  
디바이스 정보 페이지가 열립니다. 이 보기를 사용하면 디바이스의 연결 상태를 볼 수 있습니다. 이 단계에서는 디바이스가 연결된 것으로 표시되어야 합니다.   
 3. Node-RED 플로우 편집기로 돌아가 삽입 노드의 단추를 클릭하여 자산 페이로드를 생성합니다.  
페이로드는 다음 데이터 점을 포함합니다.  
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

 3. 오른쪽 분할창의 디버그 탭에서 메시지가 작성되었는지 확인합니다.  
 4. {{site.data.keyword.iot_short_notm}} 디바이스 정보 페이지로 돌아오면 이제 디바이스가 연결되어야 합니다. 디바이스에서 받은 점과 동일한 데이터 점이 표시되는지 확인합니다.  
 ```
 Event	Datapoint	 Value	Time Received
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 이제 샘플 IoT 디바이스를 {{site.data.keyword.iot_short_notm}}에 연결했으므로 디바이스 데이터를 볼 수 있습니다.

## Node-RED 노드 플로우 데이터
{: #flow_data}  
클립보드에 다음 텍스트를 복사한 다음 Node-RED 플로우 편집기에 노드를 가져올 때 가져오기 클립보드에 붙여넣으십시오.   
**중요:** 선행 및 후행 대괄호를 포함하여 모든 텍스트를 복사하십시오.  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"organization_ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:organization_ID:device_type:device_ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Double click the node.\n2. Click the edit icon next to the Server field.\n3. Update the Server name to correspond to your Watson IoT Platform organization.\n `organization_ID.messaging.internetofthings.ibmcloud.com`\n\n4. Update the Client ID with your orgainzaiton ID, device type, and device ID:\n `d:organization_ID:device_type:device_ID`\n\n5. Click the Security tab.\n6. Verify that the Username field has the value use-auth-token.\n7. Update the Password field with the Authentication Token that you saved earlier.\n8. Click Update and then OK.\n9. In the upper right corner of the Node-RED flow editor, click Deploy. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"The Function node allows you to pass each message though a JavaScript function.\n\nThe Javascript function creates the message payload that is sent to your Watson IoT Platform organization.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.","x":75,"y":236,"wires":[]}]
```
{:codeblock}
