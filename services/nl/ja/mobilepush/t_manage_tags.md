---

copyright:
 years: 2015, 2016

---

# タグの管理
{: #manage_tags}

Push ダッシュボードを使用して、ご使用のアプリケーションのタグを作成および削除し、タグ・ベースの通知を開始します。
タグをサブスクライブしているデバイスでタグ・ベースの通知を受け取るようになります。


## タグの作成
{: #create_tags}

タグ・ベースの通知は、特定のタグにサブスクライブしているすべてのデバイスをターゲットとする通知メッセージです。
各デバイスは、任意の数のタグにサブスクライブできます。タグが削除されると、そのタグに関連付けられているすべての情報 (サブスクライバーやデバイスを含む) が削除されます。このタグはもはや存在せず、クライアント・サイドから必要な追加アクションはないので、このタグの自動アンサブスクライブは必要ありません。

1. Push ダッシュボードで、**「タグ」**タブを選択します。
1. **「+ タグを作成 (+ Create Tag)」**ボタンをクリックします。   

   a. **「名前」**フィールドで、タグの名前を入力します。例えば、「クーポン」と入力します。
   
   b. **「説明」**フィールドで、タグの説明を入力します。
   
   
   c. **「保存」**をクリックします。
   
1. **「コード・スニペット (Code Snippets)」**エリアで、ご使用のモバイル・アプリケーションのプラットフォームを選択します。

1. エラー処理をするコード・スニペットを変更し、各タグに対するコード・スニペットをご使用のモバイル・アプリケーションにコピーします。


## タグの削除
{: #delete_tags}

1. **「タグ」**タブで、削除するタグを選択し「削除」アイコンをクリックします。

1. **「OK」**をクリックします。

## タグの説明の編集
{: #edit_tags}

1. **「タグ」**タブで、編集するタグを選択します。
1. 「編集」 アイコンをクリックします。
1. タグの説明を編集し、**「保存」**ボタンをクリックします。

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

# タグのサブスクライブとアンサブスクライブ
{: #Subscribe_tags}

以下のコード・スニペットを使用して、デバイスのサブスクリプションの取得、タグへのサブスクライブ、およびタグからのアンサブスクライブを可能にします。

## Android

このコード・スニペットを Android モバイル・アプリケーションにコピーして貼り付けます。

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

このコード・スニペットを Cordova モバイル・アプリケーションにコピーして貼り付けます。

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

このコード・スニペットを Objective-C モバイル・アプリケーションにコピーして貼り付けます。

タグにサブスクライブするには、**subscribeToTags** API を使用します。

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

タグからアンサブスクライブするには、**unsubscribeFromTags** API を使用します。

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

このコード・スニペットを Swift モバイル・アプリケーションにコピーして貼り付けます。

**使用可能なタグへのサブスクライブ**

タグにサブスクライブするには、**subscribeToTags** API を使用します。

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in

	if (error != nil) { 
//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus();
	}
} 
```

**タグからのアンサブスクライブ**

タグからアンサブスクライブするには、**unsubscribeFromTags** API を使用します。

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in

    if error.isEmpty {print( "Response during unsubscribed tags : \(response.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
    else {
        print( "Error during  unsubscribed tags \(error) ")
        print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```


# タグ・ベースの通知の使用
{: #using_tags}


タグ・ベースの通知は、特定のタグにサブスクライブしているすべてのデバイスをターゲットとする通知メッセージです。
各デバイスは、任意の数のタグにサブスクライブできます。このセクションでは、タグ・ベースの通知の送信方法を説明します。サブスクリプションは、Push Notifications Service Bluemix インスタンスによって維持されます。タグが削除されると、そのタグに関連付けられているすべての情報 (サブスクライバーやデバイスを含む) が削除されます。このタグはもはや存在せず、クライアント・サイドから必要な追加アクションはないので、このタグの自動アンサブスクライブは必要ありません。

**始めに**

**「タグ」**画面でタグを作成します。タグの作成方法については、[「タグの作成」](t_manage_tags.html)を参照してください。

1. **「Push Notification」**ダッシュボードで、**「通知」**タブをクリックします。
1. タグ・ベースの通知を送信する**「タグ」**オプションを選択します。
1. **「タグの検索 (Search tags)」**フィールドで、使用するタグを検索し**「+ 追加 (+Add)」**ボタンをクリックします。![「通知」画面](images/tag_notification.jpg)
1. **「通知の作成 (Create Your Notifications)」**エリアに移動し、**「メッセージ・テキスト (Message Text)」**フィールドで、通知で送信したいテキストを入力します。

1. **「送信」**ボタンをクリックします。
