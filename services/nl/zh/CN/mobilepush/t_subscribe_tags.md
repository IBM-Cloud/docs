---

copyright:
 years: 2015, 2016

---

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
