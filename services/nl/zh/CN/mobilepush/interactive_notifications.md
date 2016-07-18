---

copyright:
 years: 2015, 2016

---

# 交互式通知
{: #interactive-notifications}

交互式通知允许用户在通知到达时进行操作，而无需打开应用程序。当交互式通知到达时，设备会显示通知消息及相应的操作按钮。V8 和更高版本的 iOS 设备上支持交互式通知。如果向版本低于 8 的 iOS 设备发送交互式通知，那么不会显示通知操作。

##发送交互式推送通知


使用“推送”仪表板或使用 REST API（请参阅 REST API 文档）可发送交互式通知。

从推送控制台发送： 

在“推送”仪表板中的“通知”选项卡下，单击“发送通知”。选择通知收件人，并单击“下一步”。在编写通知页面上，可以通过将“类型”设置为“缺省值”或“混合”并在“高级选项”选项卡下指定“类别”值来发送交互式推送。要在客户机上配置类别值，请查看“在本机 iOS 应用程序中处理交互式推送通知”部分。

## 在 iOS 应用程序中处理交互式推送通知

必须遵循以下步骤来接收交互式通知：

1. 为应用程序启用在后台执行接收远程通知任务的功能。如果某些操作在后台启用，那么需要执行此步骤。
1. 在 `AppDelegate (application: didRegisterForRemoteNotificationsWithDeviceTokenapplication:)` 中，先设置类别，再针对 `WLPush 对象`设置 `deviceToken`。

```
	if([application respondsToSelector:@selector(registerUserNotificationSettings:)]){
	 UIUserNotificationType userNotificationTypes = UIUserNotificationTypeNone | UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge;
	      
	 UIMutableUserNotificationAction *acceptAction = [[UIMutableUserNotificationAction alloc] init];
	 acceptAction.identifier = @"OK";
	 acceptAction.title = @"OK";
	      
	 UIMutableUserNotificationAction *rejetAction = [[UIMutableUserNotificationAction alloc] init];
	 rejetAction.identifier = @"NOK";
	 rejetAction.title = @"NOK";
	      
	 UIMutableUserNotificationCategory *cateogory = [[UIMutableUserNotificationCategory alloc] init];
	 cateogory.identifier = @"poll";
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextDefault];
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextMinimal];
	      
	 NSSet *catgories = [NSSet setWithObject:cateogory];
	 [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:userNotificationTypes categories:catgories]];
}
```

1. 在 AppDelegate 上实施新回调方法：

```
	-(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
``` 

5. 用户单击操作按钮时，将调用此新回调方法。实施此方法必须执行与指定标识关联的步骤，并执行 `completionHandler` 参数中的块。
