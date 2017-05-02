---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# タグの管理
{: #manage_tags}
最終更新日: 2017 年 1 月 11 日
{: .last-updated}

{{site.data.keyword.mobilepushshort}}ダッシュボードを使用して、ご使用のアプリケーション向けのタグを作成および削除し、タグ・ベースの通知を開始します。タグ・ベースの通知は、タグにサブスクライブしているデバイスが受け取ります。


## タグの作成
{: #create_tags}

タグ・ベースの通知は、特定のタグにサブスクライブしているすべてのデバイスをターゲットとするメッセージです。各デバイスは、任意の数のタグにサブスクライブできます。タグが削除されると、そのタグに関連付けられている情報 (サブスクライバーやデバイスを含む) が削除されます。タグが存在しなくなることから、自動アンサブスクライブは不要です。クライアント・サイドではそれ以上のアクションは不要です。

1. {{site.data.keyword.mobilepushshort}}ダッシュボードで、**「タグ」**タブを選択します。
1. **「+ タグを作成 (+ Create Tag)」**ボタンをクリックします。   
   1. **「名前」**フィールドで、タグの名前を入力します。例えば、「クーポン」と入力します。
   1. **「説明」**フィールドで、タグの説明を入力します。
   1. **「保存」**をクリックします。

1. **「コード・スニペット (Code Snippets)」**エリアで、ご使用のモバイル・アプリケーションのプラットフォームを選択します。
1. エラー処理をするコード・スニペットを変更し、各タグに対するコード・スニペットをご使用のモバイル・アプリケーションにコピーします。

## タグの削除
{: #delete_tags}

1. **「タグ」**タブで、削除するタグを選択し**「削除」**アイコンをクリックします。
1. **「OK」**をクリックします。

## タグの説明の編集
{: #edit_tags}

1. **「タグ」**タブで、編集するタグを選択します。
1. **「編集」**アイコンをクリックします。
1. タグの説明を編集し、**「保存」**ボタンをクリックします。

# タグの取得
{: #get_tags}

タグは、ユーザーの関心に基づいてターゲットを絞った通知をユーザーに送信する手段となります。この点は、すべてのアプリケーションに送信される一般ブロードキャストと異なります。タグを作成および管理するには、{{site.data.keyword.mobilepushshort}}ダッシュボードの「タグ」タブを使用するか、または REST API を使用します。コード・スニペットを使用して、モバイル・アプリケーションのタグ・サブスクリプションを管理および照会できます。以下のコード・スニペットを使用して、サブスクリプションの取得、タグへのサブスクライブ、タグからのアンサブスクライブ、または使用可能なタグのリストの取得を行うことができます。以下のコード・スニペットをモバイル・アプリケーションにコピーしてください。

## Android 上でのタグの取得
{: android-get-tags}

**getTags** API は、デバイスをサブスクライブできる対象として使用可能なタグのリストを返します。デバイスを特定のタグにサブスクライブすると、そのタグに送られる{{site.data.keyword.mobilepushshort}}をそのデバイスは受け取ることができるようになります。

デバイスがサブスクライブしているタグのリストを取得したり、使用可能なタグのリストを取得したりするには、Android モバイル・アプリケーションに以下のコード・スニペットをコピーします。

以下の **getTags** API を使用して、デバイスをサブスクライブできる使用可能なタグのリストを取得します。

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
	{: codeblock}

## Cordova 上でのタグの取得
{: cordova-get-tags}

デバイスがサブスクライブしているタグのリストを取得したり、使用可能なタグのリストを取得したりするには、モバイル・アプリケーションに以下のコード・スニペットをコピーします。

サブスクリプションに使用可能なタグの配列を取得します。

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


## Swift 上でのタグの取得
{: swift-get-tags}

**retrieveAvailableTagsWithCompletionHandler** API は、デバイスをサブスクライブできる対象として使用可能なタグのリストを返します。デバイスを特定のタグにサブスクライブすると、そのタグに送られる{{site.data.keyword.mobilepushshort}}をそのデバイスは受け取ることができるようになります。

タグのサブスクリプションを取得するために{{site.data.keyword.mobilepushshort}}を呼び出します。

デバイスがサブスクライブする使用可能なタグのリストを取得し、デバイスをサブスクライブできる対象として使用可能なタグのリストを取得するには、Swift モバイル・アプリケーションに以下のコード・スニペットをコピーします。
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
  if error.isEmpty
	{
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

## Google Chrome、Safari、および Mozilla Firefox
{: web-get-tags}

お客様がサブスクライブできる、使用可能なタグのリストを取得するには、以下のコードを使用します。

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


## Google Chrome アプリケーションおよびエクステンション
{: web-get-tags}

お客様がサブスクライブできる、使用可能なタグのリストを取得するには、以下のコードを使用します。

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

お客様がサブスクライブしているタグのリストを取得するには、以下のコード・スニペットを Google Chrome アプリケーションおよびエクステンションにコピーします。

```
var bmsPush = new BMSPush();
bmsPush.retrieveSubscriptions(function(response)
{
   alert(response.response)
 })
```
	{: codeblock}


# タグへのサブスクライブとアンサブスクライブ
{: #Subscribe_tags}

以下のコード・スニペットを使用して、デバイスのサブスクリプションの取得、タグへのサブスクライブ、およびタグからのアンサブスクライブを可能にします。

## Android 上でのタグのサブスクライブとアンサブスクライブ
{: android-subscribe-tags}

このコード・スニペットを Android モバイル・アプリケーションにコピー・アンド・ペーストします。

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

## Cordova 上でのタグのサブスクライブとアンサブスクライブ
{: cordova-subscribe-tags}

このコード・スニペットを Cordova モバイル・アプリケーションにコピー・アンド・ペーストします。

```
var tag = "YourTag";
BMSPush.subscribe(tag, success, failure);
BMSPush.unsubscribe(tag, success, failure);
```
	{: codeblock}


## Swift 上でのタグのサブスクライブとアンサブスクライブ
{: swift-subscribe-tags}

このコード・スニペットを Swift モバイル・アプリケーションにコピー・アンド・ペーストします。

タグにサブスクライブするには、**subscribeToTags** API を使用します。

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

タグからアンサブスクライブするには、**unsubscribeFromTags** API を使用します。

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

## Google Chrome と Mozilla Firefox
{: web-subscribe-tags}

Web アプリケーションからタグにサブスクライブするには、以下のコード・スニペットを使用します。

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

タグをアンサブスクライブするには、**unSubscribe** メソッドを使用します。

```
var tagsArray = ["tag1", "Tag2"]
 bmsPush.unSubscribe(tagsArray,function(response) {
 alert(response.response)
})
```
	{: codeblock}

# タグ・ベースの通知の使用
{: #using_tags}

タグ・ベースの通知は、特定のタグにサブスクライブしているすべてのデバイスをターゲットとするメッセージです。各デバイスは、任意の数のタグにサブスクライブできます。このトピックでは、タグ・ベースの通知の送信方法を説明します。サブスクリプションは、{{site.data.keyword.mobilepushshort}}サービス Bluemix インスタンスによって維持されます。タグが削除されると、そのタグに関連付けられているすべての情報 (サブスクライバーやデバイスを含む) が削除されます。このタグはもはや存在せず、クライアント・サイドから必要な追加アクションはないので、このタグの自動アンサブスクライブは必要ありません。

**「タグ」**画面でタグを作成します。タグの作成方法については、[「タグの作成」](t_manage_tags.html)を参照してください。

1. **「Push Notification」**ダッシュボードで、**「通知の送信 (Send Notifications)」**をクリックします。
1. **「送信先 (Send To)」**ドロップダウン・リストで、**「タグ指定によるデバイス  (Device by Tag)」**オプションを選択します。
1. 使用するタグを検索して、タグを選択します。
![「通知」画面](images/tag_notification.jpg)
1. **「メッセージ・テキスト」**フィールドに、サブスクライブした対象者に通知として送信されるテキストを入力します。
1. **「送信」**をクリックします。
