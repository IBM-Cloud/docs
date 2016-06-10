---

copyright:
 years: 2015, 2016

---

# 管理標籤
{: #manage_tags}

使用 Push 儀表板來建立及刪除您應用程式的標籤，然後起始標籤型通知。標籤型通知是在訂閱標籤的裝置上接收。


## 建立標籤
{: #create_tags}

標籤型通知是指以所有訂閱特定標籤之裝置為目標的通知訊息。每一個裝置都可以訂閱任意數目的標籤。刪除標籤時，會刪除與該標籤相關聯的所有資訊，包括其訂閱者及裝置。無需對此標籤進行自動取消訂閱，因為此標籤已不存在，因此也不需要從用戶端採取進一步的動作。

1. 在 Push 儀表板上，選取**標籤**標籤。
1. 按一下 + **建立標籤**按鈕。   

   a. 在**名稱**欄位中，輸入標籤的名稱。例如，"coupons"。
   
   b. 在**說明**欄位中，輸入標籤說明。
   
   
   c. 按一下**儲存**。
   
1. 在**程式碼 Snippet** 區域中，選取您行動式應用程式的平台。
1. 修改程式碼 Snippet 來處理錯誤，然後將每一個標籤的程式碼 Snippet 複製到行動式應用程式。

## 刪除標籤
{: #delete_tags}

1. 從**標籤**標籤中，選取您要刪除的標籤，然後按一下「刪除」圖示。
1. 按一下**確定**。

## 編輯標籤說明
{: #edit_tags}

1. 從**標籤**標籤中，選取您要編輯的標籤。
1. 按一下編輯圖示。
1. 編輯標籤說明，然後按一下**儲存**按鈕。

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

# 訂閱及取消訂閱標籤
{: #Subscribe_tags}

使用下列程式碼 Snippet，可容許裝置取得訂閱、訂閱標籤，以及取消訂閱標籤。

## Android

複製下列程式碼 Snippet，並將其貼入 Android 行動式應用程式。

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

複製下列程式碼 Snippet，並將其貼入 Cordova 行動式應用程式。

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

複製下列程式碼 Snippet，並將其貼入 Objective-C 行動式應用程式。

使用 **subscribeToTags** API 來訂閱標籤。

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

使用 **unsubscribeFromTags** API 來取消訂閱標籤。

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

複製下列程式碼 Snippet，並將其貼入 Swift 行動式應用程式。

**訂閱可用的標籤**

使用 **subscribeToTags** API 來訂閱標籤。

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in

	if (error != nil) {
//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus();
	}
} 
```

**取消訂閱標籤**

使用 **unsubscribeFromTags** API 來取消訂閱標籤。

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


# 使用標籤型通知
{: #using_tags}


標籤型通知是指以所有訂閱特定標籤之裝置為目標的通知訊息。每一個裝置都可以訂閱任意數目的標籤。本節說明如何傳送標籤型通知。訂閱透過 Push Notification Service Bluemix 實例進行維護。刪除標籤時，會刪除與該標籤相關聯的所有資訊，包括其訂閱者及裝置。無需對此標籤進行自動取消訂閱，因為此標籤已不存在，因此也不需要從用戶端採取進一步的動作。

**開始之前**

在**標籤**畫面上建立標籤。如需如何建立標籤的相關資訊，請參閱[建立標籤](t_manage_tags.html)。

1. 從**推送通知**儀表板中，按一下**通知**標籤。
1. 選取**標籤**選項，以傳送標籤型通知。
1. 在**搜尋標籤**欄位中，搜尋您要使用的標籤，然後按一下 **+ 新增**按鈕。![通知畫面](images/tag_notification.jpg)
1. 移至**建立您的通知**區域，然後在**訊息文字**欄位中輸入要在通知中傳送的文字。
1. 按一下**傳送**按鈕。
