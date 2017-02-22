---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 管理標籤
{: #manage_tags}
前次更新：2017 年 1 月 11 日
{: .last-updated}

使用 {{site.data.keyword.mobilepushshort}} 儀表板來建立及刪除您應用程式的標籤，然後起始標籤型通知。標籤型通知是在訂閱標籤的裝置上接收。


## 建立標籤
{: #create_tags}

標籤型通知是指以所有訂閱特定標籤之裝置為目標的訊息。每一個裝置都可以訂閱任意數目的標籤。刪除標籤時，會刪除與該標籤相關聯的資訊（包括其訂閱者及裝置）。不需要自動取消訂閱，因為標籤不再存在。用戶端不需要採取任何進一步動作。

1. 在 {{site.data.keyword.mobilepushshort}} 儀表板上，選取**標籤**標籤。
1. 按一下 + **建立標籤**按鈕。   
   1. 在**名稱**欄位中，輸入標籤的名稱。例如，"coupons"。
   1. 在**說明**欄位中，輸入標籤說明。
   1. 按一下**儲存**。

1. 在**程式碼 Snippet** 區域中，選取您行動應用程式的平台。
1. 修改程式碼 Snippet 來處理錯誤，然後將每一個標籤的程式碼 Snippet 複製到行動應用程式。

## 刪除標籤
{: #delete_tags}

1. 從**標籤**標籤中，選取您要刪除的標籤，然後按一下**刪除**圖示。
1. 按一下**確定**。

## 編輯標籤說明
{: #edit_tags}

1. 從**標籤**標籤中，選取您要編輯的標籤。
1. 按一下**編輯**圖示。
1. 編輯標籤說明，然後按一下**儲存**按鈕。

# 取得標籤
{: #get_tags}

標籤提供的方法是根據使用者的興趣將目標通知傳送給使用者，與傳送給所有應用程式的一般播送不同。您可以使用 {{site.data.keyword.mobilepushshort}} 儀表板上的「標籤」標籤或使用 REST API 來建立及管理標籤。您可以使用程式碼 Snippet 來管理及查詢行動應用程式的標籤訂閱。您可以使用這些程式碼 Snippet 來取得訂閱、訂閱標籤、取消訂閱標籤，或取得可用標籤清單。請將這些程式碼 Snippet 複製到行動應用程式中。

## 在 Android 上取得標籤
{: android-get-tags}

**getTags** API 會傳回裝置可訂閱的可用標籤清單。在裝置訂閱特定標籤之後，該裝置就可以接收針對該標籤傳送的 {{site.data.keyword.mobilepushshort}}。

將下列程式碼 Snippet 複製到 Android 行動應用程式來取得裝置訂閱的標籤清單，以及取得可用標籤清單。

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
	{: codeblock}

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
	{: codeblock}

## 在 Cordova 上取得標籤
{: cordova-get-tags}

將下列程式碼 Snippet 複製到行動應用程式來取得裝置訂閱的標籤清單，以及取得可用標籤清單。

擷取可供訂閱的標籤陣列。

```
//Get a list of available tags to which the device can subscribe
BMSPush.retrieveAvailableTags(function(tags) {
  alert(tags);
}, failure); 
```
	{: codeblock}

```
//Get a list of available tags to which the device is subscribed.
BMSPush.retrieveSubscriptions(function(tags) {
   alert(tags); 
}, failure); 
```
	{: codeblock}


## 在 Swift 上取得標籤
{: swift-get-tags}

**retrieveAvailableTagsWithCompletionHandler** API 會傳回裝置可訂閱的可用標籤清單。在裝置訂閱特定標籤之後，該裝置就可以接收針對該標籤傳送的 {{site.data.keyword.mobilepushshort}}。

呼叫 {{site.data.keyword.mobilepushshort}} 來取得標籤的訂閱。

將下列程式碼 Snippet 複製到 Swift 行動應用程式，來取得裝置訂閱的可用標籤清單，以及取得裝置可訂閱的可用標籤清單。
```
//Get a list of available tags to which the device can subscribe
	push.retrieveAvailableTagsWithCompletionHandler({ (response, statusCode, error) -> Void in
    if error.isEmpty 
		{
        print( "Response during retrieve tags : \(response)")
        print( "status code during retrieve tags : \(statusCode)")
    }
    else
	{
    print( "Error during retrieve tags \(error) ")
        Print( "Error during retrieve tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    	}
		}
```
		{: codeblock}

```
//Get a list of available tags to which the device is subscribed
push.retrieveSubscriptionsWithCompletionHandler { (response, statusCode, error) -> Void in
    if error.isEmpty {

        print( "Response during retrieving subscribed tags : \(response?.description)")
        print( "status code during retrieving subscribed tags : \(statusCode)")
    }
    else 
	{
    print( "Error during retrieving subscribed tags \(error) ")
        Print( "Error during retrieving subscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
	   }
```
	{: codeblock}

## Google Chrome、Safari 及 Mozilla Firefox
{: web-get-tags}

若要取得客戶可以訂閱的可用標籤清單，請使用下列程式碼。

```
  var bmsPush = new BMSPush();
  bmsPush.retrieveAvailableTags(function(response) 
	{
    alert(response.response)
    var json = JSON.parse(response.response);
    var tagsA = []
    for (i in json.tags)
	{
      tagsA.push(json.tags[i].name)
    }
    alert(tagsA)
  })
```
	{: codeblock}


## Google Chrome Apps and Extensions
{: web-get-tags}

若要取得客戶可以訂閱的可用標籤清單，請使用下列程式碼。

```
  var bmsPush = new BMSPush();
  bmsPush.retrieveAvailableTags(function(response) 
	{
    alert(response.response)
    var json = JSON.parse(response.response);
    var tagsA = []
    for (i in json.tags)
	{
      tagsA.push(json.tags[i].name)
    }
    alert(tagsA)
  })
```
	{: codeblock}

將下列程式碼 Snippet 複製到 Google Chrome Apps and Extensions，以取得客戶已訂閱的標籤清單。

```
  var bmsPush = new BMSPush();
  bmsPush.retrieveSubscriptions(function(response) 
	{
    alert(response.response)
})
```
	{: codeblock}


# 訂閱及取消訂閱標籤
{: #Subscribe_tags}

使用下列程式碼 Snippet，可容許裝置取得訂閱、訂閱標籤，以及取消訂閱標籤。

## 在 Android 上訂閱及取消訂閱標籤
{: android-subscribe-tags}

複製下列程式碼 Snippet，並將其貼入 Android 行動應用程式。

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
	{: codeblock}

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
	{: codeblock}

## 在 Cordova 上訂閱及取消訂閱標籤
{: cordova-subscribe-tags}

複製下列程式碼 Snippet，並將其貼入 Cordova 行動應用程式。

```
var tag = "YourTag";
BMSPush.subscribe(tag, success, failure);
BMSPush.unsubscribe(tag, success, failure);
```
	{: codeblock}


## 在 Swift 上訂閱及取消訂閱標籤
{: swift-subscribe-tags}

複製下列程式碼 Snippet，並將其貼入 Swift 行動應用程式。

使用 **subscribeToTags** API 來訂閱標籤。

```
push.subscribeToTags(tagsArray: ["MyTag"], completionHandler: { (response, statusCode, error) -> Void in
    if error.isEmpty {
        print("Response when subscribing to tags: \(response?.description)")
        print("Status code when subscribing to tags: \(statusCode)")
    } else {
        print("Error when subscribing to tags: \(error) ")
        print("Error status code when subscribing to tags: \(statusCode)")
    }
})
```
	{: codeblock}

使用 **unsubscribeFromTags** API 來取消訂閱標籤。

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in
    if error.isEmpty {
        print( "Response during unsubscribed tags : \(response?.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
    else {
        print( "Error during  unsubscribed tags \(error) ")
        print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```
	{: codeblock}

## Google Chrome 及 Mozilla Firefox
{: web-subscribe-tags}

若要從 Web 應用程式訂閱標籤，請使用下列程式碼 Snippet：

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

取消訂閱標籤會使用 **unSubscribe** 方法。

```
var tagsArray = ["tag1", "Tag2"]
  bmsPush.unSubscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

# 使用標籤型通知
{: #using_tags}

標籤型通知是指以所有訂閱特定標籤之裝置為目標的訊息。每一個裝置都可以訂閱任意數目的標籤。本主題說明如何傳送標籤型通知。訂閱透過 {{site.data.keyword.mobilepushshort}} Service Bluemix 實例進行維護。刪除標籤時，會刪除與該標籤相關聯的所有資訊（包括其訂閱者及裝置）。無需對此標籤進行自動取消訂閱，因為此標籤已不存在，因此也不需要從用戶端採取進一步的動作。

在**標籤**畫面上建立標籤。如需如何建立標籤的相關資訊，請參閱[建立標籤](t_manage_tags.html)。

1. 從 **Push Notification** 儀表板中，按一下**傳送通知**。
1. 選取**傳送至**下拉清單中的**依標籤的裝置**選項。
1. 搜尋您要使用的標籤，然後選取它們。
![通知畫面](images/tag_notification.jpg)
1. 在**訊息文字**欄位中，輸入將當作通知傳送給已訂閱讀者的文字。
1. 按一下**傳送**。
