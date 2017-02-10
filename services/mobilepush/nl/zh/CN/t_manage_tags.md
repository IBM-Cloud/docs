---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 管理标记
{: #manage_tags}
上次更新时间：2017 年 1 月 11 日
{: .last-updated}

使用 {{site.data.keyword.mobilepushshort}} 仪表板，可以创建和删除应用程序的标记，然后初始化基于标记的通知。预订了标记的设备会收到基于标记的通知。


## 创建标记
{: #create_tags}

基于标记的通知是针对预订了特定标记的所有设备的消息。每个设备都可以预订任意数量的标记。删除标记时，与该标记关联的信息（包括其订户和设备）都会一并删除。不需要自动取消预订，因为该标记不存在。客户端不需要任何进一步操作。

1. 在 {{site.data.keyword.mobilepushshort}} 仪表板上，选择**标记**选项卡。
1. 单击 + **创建标记**按钮。   
   1. 在**名称**字段中，输入标记的名称。例如，“coupons”。
   1. 在**描述**字段中，输入标记描述。
   1. 单击**保存**。

1. 在**代码片段**区域中，选择移动应用程序的平台。
1. 修改代码片段以处理错误，然后将每个标记的代码片段复制到移动应用程序中。

## 删除标记
{: #delete_tags}

1. 从**标记**选项卡，选择要删除的标记，并单击**删除**图标。
1. 单击**确定**。

## 编辑标记描述
{: #edit_tags}

1. 在**标记**选项卡中，选择要编辑的标记。
1. 单击**编辑**图标。
1. 编辑标记描述，然后单击**保存**按钮。

# 获取标记
{: #get_tags}

不同于发送给所有应用程序的一般性广播，通过标记，可以根据用户的兴趣发送有针对性的通知。您可以使用 {{site.data.keyword.mobilepushshort}} 仪表板上的“标记”选项卡或使用 REST API 来创建和管理标记。您可以使用代码片段来管理和查询移动应用程序的标记预订。还可以使用这些代码片段来获取预订、预订标记、取消预订标记，或者获取可用标记的列表。将这些代码片段复制到移动应用程序中。

## 在 Android 上获取标记
{: android-get-tags}

**getTags** API 会返回设备可预订的可用标记的列表。在设备预订特定标记后，该设备可以接收针对该标记发送的 {{site.data.keyword.mobilepushshort}}。

将以下代码片段复制到 Android 移动应用程序中，以获取设备所预订的标记的列表以及获取可用标记的列表。

使用以下 **getTags** API 可获取设备可预订的可用标记的列表。

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
	{: codeblock}

## 在 Cordova 上获取标记
{: cordova-get-tags}

将以下代码片段复制到移动应用程序中，以获取设备所预订的标记的列
表以及可用标记的列表。

检索可供预订的标记的数组。

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


## 在 Swift 上获取标记
{: swift-get-tags}

**retrieveAvailableTagsWithCompletionHandler** API 会返回设备可预订的可用标记的列表。在设备预订特定标记后，该设备可以接收针对该标记发送的 {{site.data.keyword.mobilepushshort}}。

调用 {{site.data.keyword.mobilepushshort}} 来预订标记。

将以下代码片段复制到 Swift 移动应用程序中，以获取设备所预订的标记的列表以及获取设备可预订的可用标记的列表。
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

## Google Chrome、Safari 和 Mozilla Firefox
{: web-get-tags}

要获取客户可以预订的可用标记列表，请使用以下代码。

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

要获取客户可以预订的可用标记列表，请使用以下代码。

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

将以下代码片段复制到 Google Chrome Apps and Extensions 中，以获取客户所预订的标记列表。

```
  var bmsPush = new BMSPush();
  bmsPush.retrieveSubscriptions(function(response) 
	{
    alert(response.response)
  })
```
	{: codeblock}


# 预订和取消预订标记
{: #Subscribe_tags}

使用以下代码片段可允许设备获取预订、预订某个标记以及取消预订某个标记。

## 在 Android 上预订和取消预订标记
{: android-subscribe-tags}

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

## 在 Cordova 上预订和取消预订标记
{: cordova-subscribe-tags}

将以下代码片段复制并粘贴到 Cordova 移动应用程序中。

```
var tag = "YourTag";
BMSPush.subscribe(tag, success, failure);
BMSPush.unsubscribe(tag, success, failure);
```
	{: codeblock}


## 在 Swift 上预订和取消预订标记
{: swift-subscribe-tags}

将以下代码片段复制并粘贴到 Swift 移动应用程序中。

使用 **subscribeToTags** API，可以预订标记。

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

使用 **unsubscribeFromTags** API，可以取消预订标记。

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in
    if error.isEmpty {
        print( "Response during unsubscribed tags : \(response?.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
    else 
	{
    print( "Error during  unsubscribed tags \(error) ")
        print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```
	{: codeblock}

## Google Chrome 和 Mozilla Firefox
{: web-subscribe-tags}

要从 Web 应用程序预订标记，请使用以下代码片段：

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

要取消预订标记，请使用 **unSubscribe** 方法。

```
var tagsArray = ["tag1", "Tag2"]
  bmsPush.unSubscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

# 使用基于标记的通知
{: #using_tags}

基于标记的通知是针对预订了特定标记的所有设备的消息。每个设备都可以预订任意数量的标记。本主题描述了如何发送基于标记的通知。预订通过 {{site.data.keyword.mobilepushshort}} 服务 Bluemix 实例进行维护。删除标记时，与该标记关联的所有信息（包括其订户和设备）都会一并删除。无需对此标记自动取消预订，因为此标记不再存在，因此也不需要从客户机端执行进一步的操作。

在**标记**屏幕上创建标记。有关如何创建标记的信息，请参阅[创建标记](t_manage_tags.html)。

1. 从 **Push Notification** 仪表板，单击**发送通知**。
1. 在**发送到**下拉列表中，选择**按标记列出设备**选项。
1. 搜索您要使用的标记并选择它们。
![通知屏幕](images/tag_notification.jpg)
1. 在**消息文本**字段中，输入将作为通知发送给订阅受众的文本。
1. 单击**发送**。
