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



