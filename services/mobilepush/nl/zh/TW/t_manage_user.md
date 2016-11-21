---

copyright:
 years: 2015, 2016

---


# 使用 userId 登錄裝置
{: #register_device_with_userId}
前次更新：2016 年 10 月 17 日
{: .last-updated}

若要登錄 userId 型通知，請完成下列步驟：

## Android
{: android-register}

使用 {{site.data.keyword.mobilepushshort}} Service 的 `AppGUID` 及 `clientSecret` 金鑰，來起始設定 MFPPush 類別。
```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```
	{: codeblock}

####AppGUID
{: push-app-guid}

這是 {{site.data.keyword.mobilepushshort}} Service 的 AppGUID 金鑰。

####clientSecret
{: android-client-secret}

這是 {{site.data.keyword.mobilepushshort}} Service 的 clientSecret 金鑰。

使用 **registerDeviceWithUserId** API 登錄裝置，以取得 {{site.data.keyword.mobilepushshort}}。
```
// Register the device to {{site.data.keyword.mobilepushshort}}.
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
	           Log.d("Device is registered with Push Service.");
  }
  @Override
  public void onFailure(MFPPushException ex) {
    Log.d("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
  }
});
```
	{: codeblock}

####userId
{: android-user-id}

傳遞唯一 userId 值，以登錄 {{site.data.keyword.mobilepushshort}}。

**附註：**若要啟用 userId 設為目標的 {{site.data.keyword.mobilepushshort}}，請確定您使用 userId 登錄裝置，同時也傳遞佈建 {{site.data.keyword.mobilepushshort}} Service 時所配置的 'clientSecret'。若沒有有效的 clientSecret，裝置登錄會失敗。


## Objective-C
{: objc-register}

使用下列 API 來登錄使用者 ID 型 {{site.data.keyword.mobilepushshort}}。
```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
```
	{: codeblock}

###AppGUID
{: objc-pushappguid}

這是 {{site.data.keyword.mobilepushshort}} Service 的 AppGUID 金鑰。

####clientSecret
{: objc-client-secret}

這是 {{site.data.keyword.mobilepushshort}} Service 的 clientSecret 金鑰。

使用 **registerWithUserId** API 登錄裝置，以取得 {{site.data.keyword.mobilepushshort}}。
```
// Register the device to push notifications service.
[push registerWithDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
    NSString *message=@"";
	if (error){
        message = [NSString stringWithFormat:@"Error registering for push notifications: %@", error.description];
        NSLog(@"%@",message);
    } else {
        message=@"Successfully registered for push notifications";
        NSLog(@"%@",message);
    }
}];
```
	{: codeblock}

####userId
{: objc-user-id}

傳遞唯一 userId 值，以登錄 {{site.data.keyword.mobilepushshort}}。

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}

####AppGUID
{: swift-pushappguid}
這是 {{site.data.keyword.mobilepushshort}} Service 的 AppGUID 金鑰。

####clientSecret
{: swift-client-secret}

這是 {{site.data.keyword.mobilepushshort}} Service 的 clientSecret 金鑰。

使用 **registerWithUserId** API 登錄裝置，以取得 {{site.data.keyword.mobilepushshort}}。

```
// Register the device to Push Notifications service.
push.registerWithDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")
        print( "status code during device registration : \(statusCode)")
    } else {
        print( "Error during device registration \(error) ")
    }
    }
```
	{: codeblock}

####userId
{: swift-user-id}

傳遞唯一 userId 值，以登錄 {{site.data.keyword.mobilepushshort}}。

## Google Chrome 及 Mozilla Firefox
{: web-register}

使用下列 API 來登錄 userId 型通知。使用 `app GUID`、`app Region` 及 `Client Secret` 來起始設定 SDK。

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
      })
```
	{: codeblock}
  
順利起始設定之後，請使用 userId 登錄 Web 應用程式。

```
    bmsPush.registerWithUserId("UserId", function(response) {
      alert(response.response)
  })
```
	{: codeblock}

## Google Chrome Apps and Extensions
{: web-register-new}

使用下列 API 來登錄 userId 型通知。使用 `app GUID`、`app Region` 及 `Client Secret` 來起始設定 SDK。

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
      })
```
	{: codeblock}
  
順利起始設定之後，請使用 userId 登錄 Web 應用程式。

```
    bmsPush.registerWithUserId("UserId", function(response) {
      alert(response.response)
  })
```
	{: codeblock}

# 使用 userId 型通知
{: #using_userid}


userId 型通知是以特定使用者為目標的通知訊息。可向一個使用者登錄多個裝置。下列步驟說明如何傳送使用者 ID 型通知。

1. 從 **Push Notification** 儀表板中，選取**傳送通知**選項。
1. 在**傳送至**選項清單中，選取**使用者 ID**。
1. 在**使用者 ID** 欄位中，搜尋您要使用的使用者 ID，然後按一下 **+ 新增**。![通知畫面](images/user_notification.jpg)
1. 在**訊息**欄位中，輸入要在通知中傳送的文字。
1. 按一下**傳送**。
