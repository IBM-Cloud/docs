# 取得標籤
{: #get_tags}

標籤提供的方法是根據使用者的興趣將目標通知傳送給使用者，與傳送給所有應用程式的一般播送不同。您可以使用 Push 儀表板上的「標籤」標籤或使用 REST API 來建立及管理標籤。您可在下列區段中使用程式碼 Snippet 來管理及查詢行動式應用程式的標籤訂閱。您可以使用這些程式碼 Snippet 來取得訂閱、訂閱標籤、取消訂閱標籤，以及取得可用標籤清單。您可以複製這些程式碼 Snippet，並將其貼入行動式應用程式中。

## Android

**getTags** API 會傳回裝置可訂閱的可用標籤清單。在裝置訂閱特定標籤之後，該裝置就可以接收針對該標籤傳送的任何推送通知。

將下列程式碼 Snippet 複製到 Android 行動式應用程式來取得裝置訂閱的標籤清單，以及取得可用標籤清單。

使用下列 **getTags** API 來取得裝置可訂閱的可用標籤清單。

```
// Get a list of available tags to which the device can subscribe
push.getTags(new MFPPushResponseListener<List<String>>(){  
   @Override
   public void onSuccess(List<String> tags){
   updateTextView("Retrieved available tags: " + tags);  
   System.out.println("Available tags are: "+tags);
   availableTags = tags;   
   subscribeToTag();   
  }    
  @Override    
  public void onFailure(MFPPushException ex){
     updateTextView("Error getting available tags.. " + ex.getMessage());
  }
})  
```

使用 **getSubscriptions** API 來取得裝置訂閱的標籤清單。

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

將下列程式碼 Snippet 複製到行動式應用程式來取得裝置訂閱的標籤清單，以及取得裝置可訂閱的可用標籤清單。

擷取可供訂閱的標籤陣列。

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

將下列程式碼 Snippet 複製到使用 Objective-C 所開發的 iOS 應用程式來取得裝置訂閱的標籤清單，以及取得裝置可訂閱的可用標籤清單。

使用下列 **retrieveAvailableTags** API 來取得裝置可訂閱的可用標籤清單。

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
       
使用 **retrieveSubscriptions** API 來取得裝置訂閱的標籤清單。


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

**retrieveAvailableTagsWithCompletionHandler** API 會傳回裝置可訂閱的可用標籤清單。在裝置訂閱特定標籤之後，該裝置就可以接收針對該標籤傳送的任何推送通知。

呼叫 Push 服務來取得標籤的訂閱。

將下列程式碼 Snippet 複製到 Swift 行動式應用程式，來取得裝置訂閱的可用標籤清單，以及取得裝置可訂閱的可用標籤清單。


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



