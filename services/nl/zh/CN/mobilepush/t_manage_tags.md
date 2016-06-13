---

copyright:
 years: 2015, 2016

---

# 管理标记
{: #manage_tags}

使用“推送”仪表板，可以创建和删除应用程序的标记，然后初始化基于标记的通知。预订了标记的设备会收到基于该标记的通知。


## 创建标记
{: #create_tags}

基于标记的通知是针对预订了特定标记的所有设备的通知消息。每个设备都可以预订任意数量的标记。删除标记时，与该标记关联的所有信息（包括其订户和设备）都会一并删除。无需对此标记自动取消预订，因为此标记不再存在，因此也不需要从客户机端执行进一步的操作。

1. 在“推送”仪表板上，选择**标记**选项卡。
1. 单击 + **创建标记**按钮。   

   a. 在**名称**字段中，输入标记的名称。例如，“coupons”。
   
   b. 在**描述**字段中，输入标记描述。
         
   
   c. 单击**保存**。
   
1. 在**代码片段**区域中，选择移动应用程序的平台。
1. 修改代码片段以处理错误，然后将每个标记的代码片段复制到移动应用程序中。

## 删除标记
{: #delete_tags}

1. 在**标记**选项卡中，选择要删除的标记，然后单击“删除”图标。
1. 单击**确定**。

## 编辑标记描述
{: #edit_tags}

1. 在**标记**选项卡中，选择要编辑的标记。
1. 单击“编辑” 图标。
1. 编辑标记描述，然后单击**保存**按钮。

# 获取标记
{: #get_tags}

标记不同于发送给所有应用程序的一般性广播，通过标记，可以根据用户的兴趣发送有针对性的通知。您可以使用“推送”仪表板上的“标记”选项卡或使用 REST API 来创建和管理标记。您可以使用以下部分中的代码片段来管理和查询移动应用程序的标记预订。还可以使用这些代码片段来获取预订、预订标记、取消预订标记，以及获取可用标记的列表。您可将这些代码片段复制并粘贴到移动应用程序中。

## Android

**getTags** API 会返回设备可预订的可用标记的列表。在预订特定标记后，设备可以接收针对该标记发送的任何推送通知。

将以下代码片段复制到 Android 移动应用程序中，以获取设备所预订的标记的列表以及获取可用标记的列表。

使用以下 **getTags** API 可获取设备可预订的可用标记的列表。

```
// Get a list of available tags to which the device can subscribe
push.getTags(new MFPPushResponseListener<List<String>>(){  
@Override
    public void onSuccess(List<String> tags) {
    updateTextView("Retrieved available tags: " + tags);  
   System.out.println("Available tags are: "+tags);
   availableTags = tags;   
subscribeToTag();
   
  }    
@Override
    
public void onFailure(MFPPushException ex) {

     updateTextView("Error getting available tags.. " + ex.getMessage());
  }
})  
```

使用以下 **getSubscriptions** API 可获取设备所预订的标记的列表。

```
// Get a list of tags that to which the device is subscribed.
push.getSubscriptions(new MFPPushResponseListener<List<String>>() {

    @Override
    public void onSuccess(List<String> tags) {
    updateTextView("Retrieved subscriptions : " + tags);
    System.out.println("Subscribed tags are: "+tags);
    subscribedTags = tags;
    subscribeToTag();
    }
    @Override
    public void onFailure(MFPPushException ex) {
         updateTextView("Error getting subscriptions.. " + ex.getMessage());
    }
})
```

## Cordova

将以下代码片段复制到移动应用程序中，以获取设备所预订的标记的列表以及获取设备可预订的可用标记的列表。

检索可供预订的标记的数组。

```
//Get a list of available tags to which the device can subscribe
MFPPush.retrieveAvailableTags(function(tags) {
    alert(tags);
}, null);


```

```
//Get a list of available tags to which the device is subscribed.
MFPPush.getSubscriptionStatus(function(tags) {

    alert(tags);
}, null);
```

## Objective-C

将以下代码片段复制到使用 Objective-C 开发的 iOS 应用程序中，以获取设备所预订的标记的列表以及获取设备可预订的可用标记的列表。

使用以下 **retrieveAvailableTags** API 可获取设备可预订的可用标记的列表。

```
//Get a list of available tags to which the device can subscribe 
[push retrieveAvailableTagsWithCompletionHandler:
^(IMFResponse *response, NSError *error){ 
 if(error){    
[self updateMessage:error.description];
  
} else {
[self updateMessage:@"Successfully retrieved available tags."];
 NSDictionary *availableTags = [[NSDictionary alloc]init];
 availableTags = [response tags];
[self.appDelegateVC updateMessage:availableTags.description];
}
}];
```
       
使用以下 **retrieveSubscriptions** API 可获取设备所预订的标记的列表。


```
// Get a list of tags that to which the device is subscribed.
[push retrieveSubscriptionsWithCompletionHandler:
^(IMFResponse *response, NSError *error) {
  if(error){
     [self updateMessage:error.description];
   } else {
     [self updateMessage:@"Successfully retrieved subscriptions."];
 NSDictionary *subscribedTags = [[NSDictionary alloc]init];
subscribedTags = [response subscriptions];
[self.appDelegateVC updateMessage:subscribedTags.description];
}
}];
```

## Swift

**retrieveAvailableTagsWithCompletionHandler** API 会返回设备可预订的可用标记的列表。在预订特定标记后，设备可以接收针对该标记发送的任何推送通知。

调用推送服务来预订标记。

将以下代码片段复制到 Swift 移动应用程序中，以获取设备所预订的标记的列表以及获取设备可预订的可用标记的列表。


```
//Get a list of available tags to which the device can subscribe
push.retrieveAvailableTagsWithCompletionHandler({ (response, statusCode, error) -> Void in

    if error.isEmpty {

        print( "Response during retrieve tags : \(response)")
        print( "status code during retrieve tags : \(statusCode)")
    }
    else{
        print( "Error during retrieve tags \(error) ")
        Print( "Error during retrieve tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```

```
//Get a list of available tags to which the device is subscribed
push.retrieveSubscriptionsWithCompletionHandler { (response, statusCode, error) -> Void in
    if error.isEmpty {

        print( "Response during retrieving subscribed tags : \(response.description)")
        print( "status code during retrieving subscribed tags : \(statusCode)")
    }
    else {
print( "Error during retrieving subscribed tags \(error) ")
        Print( "Error during retrieving subscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```

# 预订和取消预订标记
{: #Subscribe_tags}

使用以下代码片段可允许设备获取预订、预订某个标记以及取消预订某个标记。

## Android

将以下代码片段复制并粘贴到 Android 移动应用程序中。

```
push.subscribe(allTags.get(0),
new MFPPushResponseListener<String>() {
  @Override
  public void onFailure(MFPPushException ex) {
    updateTextView("Error subscribing to Tag1.."
           + ex.getMessage());
  }
  @Override
  public void onSuccess(String arg0) {
   updateTextView("Succesfully Subscribed to: "+ arg0);
   unsubscribeFromTags(arg0);
   }
});
```

```
push.unsubscribe(tag, new MFPPushResponseListener<String>() {
@Override
 public void onSuccess(String s) {
   updateTextView("Unsubscribing from tag");
   updateTextView("Successfully unsubscribed from tag . "+ tag);
 }
 @Override
 public void onFailure(MFPPushException e) {
 updateTextView("Error while unsubscribing from tags. "+ e.getMessage());
 }
});
```

## Cordova

将以下代码片段复制并粘贴到 Cordova 移动应用程序中。

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

将以下代码片段复制并粘贴到 Objective-C 移动应用程序中。

使用 **subscribeToTags** API，可以预订标记。

```
[push subscribeToTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
  if(error){
     [self updateMessage:error.description];
  }else{
      NSDictionary* subStatus = [[NSDictionary alloc]init];
      subStatus = [response subscribeStatus];
      [self updateMessage:@"Parsed subscribe status is:"];
      [self updateMessage:subStatus.description];
  }
}];
```

使用 **unsubscribeFromTags** API，可以取消预订标记。

```
[push unsubscribeFromTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
   if (error){
       [self updateMessage:error.description];
 } else {
       NSDictionary* subStatus = [[NSDictionary alloc]init];
       subStatus = [response unsubscribeStatus];
       [self updateMessage:subStatus.description];
  }
}];
```

## Swift

将以下代码片段复制并粘贴到 Swift 移动应用程序中。

**预订可用标记**

使用 **subscribeToTags** API，可以预订标记。

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in

	if (error != nil) {
//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus();
	}
} 
```

**取消预订标记**

使用 **unsubscribeFromTags** API，可以取消预订标记。

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in

    if error.isEmpty {
        print( "Response during unsubscribed tags : \(response.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
    else {
print( "Error during  unsubscribed tags \(error) ")
        print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```


# 使用基于标记的通知
{: #using_tags}


基于标记的通知是针对预订了特定标记的所有设备的通知消息。每个设备都可以预订任意数量的标记。本部分描述了如何发送基于标记的通知。预订通过 Push Notification Service Bluemix 实例进行维护。删除标记时，与该标记关联的所有信息（包括其订户和设备）都会一并删除。无需对此标记自动取消预订，因为此标记不再存在，因此也不需要从客户机端执行进一步的操作。

**开始之前**

在**标记**屏幕上创建标记。有关如何创建标记的信息，请参阅[创建标记](t_manage_tags.html)。

1. 在**推送通知**仪表板中，单击**通知**选项卡。
1. 选择**标记**选项，以发送基于标记的通知。
1. 在**搜索标记**字段中，搜索要使用的标记，然后单击 **+添加**按钮。![“通知”屏幕](images/tag_notification.jpg)
1. 转至**创建通知**区域，然后在**消息文本**字段中输入要在通知中发送的文本。
1. 单击**发送**按钮。
