---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 웹훅 사용 
{: #tag_based_notifications}
마지막 업데이트 날짜: 2017년 3월 1일
{: .last-updated}


{{site.data.keyword.mobilepushshort}} 서비스를 사용하면 변경된 정보에 관한 경보를 수신하도록 선택할 수 있습니다. 엔터프라이즈 정보가 변경되면 이벤트가 작성되며 이를 웹훅 이벤트로 등록하여 알림을 수신할 수 있습니다. 이러한 웹훅 이벤트는 경보를 트리거합니다.  

웹훅은 이벤트에서 트리거하는 사용자 정의 콜백입니다(예: 디바이스 등록 또는 태그 구독). {{site.data.keyword.mobilepushshort}} 서비스에서 다음 웹훅 이벤트에 등록할 수 있습니다.  

- **onDeviceRegister**: 웹훅 이벤트가 푸시에 등록된 디바이스에 대해 트리거됩니다. 
- **onDeviceUpdate**: 등록된 디바이스에 대한 정보를 업데이트할 때 웹훅 이벤트가 트리거됩니다. 
- **onDeviceUnregister**: 디바이스의 등록이 해지될 때 웹훅 이벤트가 트리거됩니다.  
- **onSubscribe**: 사용자가 태그를 구독할 때 웹훅 이벤트가 트리거됩니다. 
- **onUnsubscribe**: 사용자가 태그의 구독을 해지할 때 웹훅 이벤트가 트리거됩니다. 
- **onNotificationSend**: 디스패치된 알림이 있을 때 웹훅 이벤트가 트리거됩니다. 
- **onNotificationFailure**: 알림이 실패하면 웹훅 이벤트가 트리거됩니다. 


**참고**: 일괄처리로 알림 디스패치가 실행됩니다. 메시지 디스패치에 여러 웹훅 이벤트가 있으며 실패 및 성공 이벤트가 모두 포함될 수 있습니다.
웹훅 이벤트의 메시지 ID가 디스패치된 메시지 ID와 동일할 수 있습니다.  

웹훅에 대한 자세한 정보는 [IBM Push Notifications REST API ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}을 참조하십시오. 

## 웹훅 이벤트에서 경보 받기
{: #webhook_alert_event}

구독자는 JSON 파일과 같은 웹훅 이벤트에서 경보를 받도록 선택할 수 있습니다. 이벤트 구조 및 샘플 페이로드는 다음과 같습니다. 

- 디바이스 등록
	```
		{ type: 'onDeviceRegister',
		entity:
		{ id: 1,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		applicationId: 'app1',
		eventTimeStamp: 1487523766958 }
	```
		{: codeblock}

- 디바이스 등록 취소
	```
		{ type: 'onDeviceUnregister',
		entity:
		{ id: 1,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		applicationId: 'app1',
		eventTimeStamp: 1487523841874 }
	```
		{: codeblock}

- 태그 구독
	```
		{ type: 'onSubscribe',
		entity:
		{ device:
		{ id: 18,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		tagName: 'tag1',
		deviceId: 'device1',
		subscriptionId: 'b0246677bfa655385fbc2b5532f6443f' },
		applicationId: 'app1',
		eventTimeStamp: 1487755527470 }
	```
		{: codeblock}

- 태그 구독 취소
	```
		{ type: 'onUnsubscribe',
		entity:
		{ device:
		{ id: 18,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		tagName: 'tag1',
		deviceId: 'device1',
		subscriptionId: 'b0246677bfa655385fbc2b5532f6443f' },
		applicationId: 'app1',
		eventTimeStamp: 1487755581059 }
	```
		{: codeblock}

- 알림 전송
	```
		{ type: 'onNotificationSent',
		entity:
		{ applicationId: 'app1',
		deviceIds:
		[ 'device1',
		'device2'],
		platform: 'A',
		msgStatus: 'dispatched',
		messageId: '55cb688' },
		applicationId: 'app1',
		eventTimeStamp: 1487524517353 }
	```
		{: codeblock}

- 알림 실패
	```
		{ type: 'onNotificationFailure',
		entity:
		{ applicationId: 'app1',
		deviceIds: [ 'device1' ],
		platform: 'G',
		msgStatus: 'failure',
		failureReason: 'InvalidRegistration',
		messageId: '55cb688' },
		applicationId: 'app1',
		eventTimeStamp: 1487524519453 }
	```
		{: codeblock}

