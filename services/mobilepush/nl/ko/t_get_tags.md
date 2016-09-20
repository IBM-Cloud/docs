# 태그 가져오기
{: #get_tags}

태그는 모든 애플리케이션에 전송되는 일반 브로드캐스트와 달리 관심사를 기반으로 수신인에게 맞춤형 알림을 전송하는 방법을 제공합니다. 푸시 대시보드의 태그 탭을 사용하여 태그를 작성 및 관리하거나 REST API를 사용할 수 있습니다. 다음 섹션의 코드 스니펫을 사용하여 모바일 애플리케이션에 대한 태그 구독을 관리 및 조회할 수 있습니다. 이 코드 스니펫을 사용하여 구독을 가져오고 태그를 구독하며 태그 구독을 취소하고 사용 가능한 태그 목록을 가져올 수 있습니다. 코드 스니펫을 모바일 애플리케이션에 복사하고 붙여넣으십시오. 

## Android

**getTags** API는 디바이스를 구독할 수 있는 사용 가능한 태그 목록을 리턴합니다. 디바이스가 특정 태그에 구독되면 디바이스는 해당 태그에 대해 전송되는 모든 푸시 알림을 수신할 수 있습니다. 

디바이스가 구독된 사용 가능한 태그 목록을 가져오려면 다음 코드 스니펫을 Android 모바일 애플리케이션에 복사하십시오. 

디바이스가 구독할 수 있는 사용 가능 태그 목록을 가져오려면 다음 **getTags** API를 사용하십시오.

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
  public void onFailure(MFPPushException ex) {
     updateTextView("Error getting available tags.. " + ex.getMessage());
  }
})  
```

디바이스가 구독된 태그 목록을 가져오려면 **getSubscriptions** API를 사용하십시오. 

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

디바이스가 구독된 사용 가능한 태그 목록을 가져오고 디바이스가 구독할 수 있는 사용 가능한 태그 목록을 가져오려면 다음 코드 스니펫을 모바일 애플리케이션에 복사하십시오. 

구독에 사용할 수 있는 태그의 배열을 검색하십시오. 

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

디바이스가 구독된 사용 가능한 태그 목록을 가져오고 디바이스가 구독할 수 있는 사용 가능한 태그 목록을 가져오려면 Objective-C를 사용하여 개발된 iOS 애플리케이션으로 다음 코드 스니펫을 복사하십시오. 

디바이스가 구독할 수 있는 사용 가능 태그 목록을 가져오려면 다음 **retrieveAvailableTags** API를 사용하십시오.

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
       
디바이스가 구독된 태그 목록을 가져오려면 **retrieveSubscriptions** API를 사용하십시오.



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

**retrieveAvailableTagsWithCompletionHandler** API는 디바이스가 구독하는 데 사용할 수 있는 모든 태그의 목록을 리턴합니다. 디바이스가 특정 태그에 구독되면 디바이스는 해당 태그에 대해 전송되는 모든 푸시 알림을 수신할 수 있습니다. 

태그 구독을 위해 푸시 서비스를 호출합니다. 

디바이스가 구독된 사용 가능한 태그 목록을 가져오고 디바이스가 구독할 수 있는 사용 가능한 태그 목록을 가져오려면 다음 코드 스니펫을 Swift 모바일 애플리케이션에 복사하십시오. 


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



