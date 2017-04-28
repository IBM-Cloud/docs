---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 启用 Webhook 
{: #tag_based_notifications}
上次更新时间：2017 年 3 月 1 日
{: .last-updated}


使用 {{site.data.keyword.mobilepushshort}} 服务，您可以选择接收已更改信息的警报。企业信息的更改会创建事件，通过将它们注册为 Webhook 事件，您可以接收相关通知。这些 Webhook 事件可触发警报。 

Webhook 是用户定义的回调，可由事件触发，如注册设备或预订标记。在 {{site.data.keyword.mobilepushshort}} 服务上，您可以针对以下 Webhook 事件进行注册： 

- **onDeviceRegister**：针对已为推送注册的设备触发 Webhook 事件。
- **onDeviceUpdate**：当更新已注册设备的相关信息时触发 Webhook 事件。
- **onDeviceUnregister**：当取消注册设备时触发 Webhook 事件。 
- **onSubscribe**：用户预订标记时触发 Webhook 事件。
- **onUnsubscribe**：用户取消预订标记时触发 Webhook 事件。
- **onNotificationSend**：针对已分派的通知触发 Webhook 事件。
- **onNotificationFailure**：针对通知失败触发 Webhook 事件。


**注**：通知分派以批量处理。消息分派可以具有多个 Webhook 事件，其中可能包括失败和成功。
Webhook 事件可以与已分派的消息具有相同的消息标识。 

有关 Webhook 的更多信息，请参阅 [IBM Push Notifications REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}。

## 接收关于 Webhook 事件的警报
{: #webhook_alert_event}

订户可以选择将关于 Webhook 事件的警报作为 JSON 文件接收。事件结构和样本有效内容如下所示：

- 注册设备
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

- 注销设备
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

- 预订标记
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

- 取消预订标记
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

- 发送通知
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

- 通知失败
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

