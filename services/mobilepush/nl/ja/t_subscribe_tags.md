---

copyright:
 years: 2015, 2016

---

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
