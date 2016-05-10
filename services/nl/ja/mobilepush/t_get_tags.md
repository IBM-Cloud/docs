# タグの取得
{: #get_tags}

タグは、ユーザーの関心に基づいてユーザーにターゲット通知を送信する手段となります。この点は、すべてのアプリケーションに送信される一般ブロードキャストと異なります。タグを作成および管理するには、Push ダッシュボードの「タグ」タブを使用するか、または REST API を使用します。以下のセクションのコード・スニペットを使用して、モバイル・アプリケーションのタグ・サブスクリプションを管理および照会できます。これらのコード・スニペットを使用して、サブスクリプションの取得、タグへのサブスクライブ、タグからのアンサブスクライブ、使用可能なタグのリストの取得を行うことができます。
これらのコード・スニペットは、モバイル・アプリケーションにコピー・アンド・ペーストします。

## Android

**getTags** API は、デバイスをサブスクライブできる対象として使用可能なタグのリストを返します。デバイスを特定のタグにサブスクライブすると、そのタグに送られるすべてのプッシュ通知をそのデバイスは受け取ることができるようになります。

デバイスのサブスクライブ対象タグ・リストを取得し、使用可能なタグのリストを取得するには、Android モバイル・アプリケーションに以下のコード・スニペットをコピーします。


以下の **getTags** API を使用して、デバイスをサブスクライブできる使用可能なタグのリストを取得します。

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
    
  public void onFailure(MFPPushException ex){
     updateTextView("Error getting available tags.. " + ex.getMessage());
  }
})  
```

**getSubscriptions** API を使用して、デバイスがサブスクライブする対象タグのリストを取得します。


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

デバイスがサブスクライブする対象タグのリストを取得し、デバイスをサブスクライブできる対象として使用可能なタグのリストを取得するには、モバイル・アプリケーションに以下のコード・スニペットをコピーします。

サブスクライブ対象として使用可能なタグの配列を取得します。

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

デバイスがサブスクライブする対象タグのリストを取得し、デバイスをサブスクライブできる対象として使用可能なタグのリストを取得するには、Objective-C を使用して開発された iOS アプリケーションに以下のコード・スニペットをコピーします。

以下の **retrieveAvailableTags** API を使用して、デバイスをサブスクライブできる対象として使用可能なタグのリストを取得します。

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
       
**retrieveSubscriptions** API を使用して、デバイスがサブスクライブする対象タグのリストを取得します。



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

**retrieveAvailableTagsWithCompletionHandler** API は、デバイスをサブスクライブできる対象として使用可能なタグのリストを返します。デバイスを特定のタグにサブスクライブすると、そのタグに送られるすべてのプッシュ通知をそのデバイスは受け取ることができるようになります。

タグのサブスクリプションを取得するためにプッシュ・サービスを呼び出します。

デバイスがサブスクライブする使用可能なタグのリストを取得し、デバイスをサブスクライブできる対象として使用可能なタグのリストを取得するには、Swift モバイル・アプリケーションに以下のコード・スニペットをコピーします。


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



