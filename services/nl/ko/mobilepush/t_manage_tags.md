---

copyright:
 years: 2015, 2016

---

# 태그 관리
{: #manage_tags}

푸시 대시보드를 사용하여 사용자 애플리케이션의 태그를 작성 및 삭제하고 태그 기반 알림을 시작합니다. 태그에 등록된 디바이스에서 태그 기반 알림이 수신됩니다. 


## 태그 작성
{: #create_tags}

태그 기반 알림은 특정 태그를 구독하는 모든 디바이스를 대상으로 하는 알림 메시지입니다. 각 디바이스는 수에 관계 없이 태그를 구독할 수 있습니다. 태그가 삭제되면 구독자와 디바이스를 포함하여 해당 태그와 연관된 모든 정보가 삭제됩니다. 이 태그가 더 이상 존재하지 않고 클라이언트측에서 추가 조치가 필요하지 않으므로 이 태그에 대해 자동 구독 해지 조치가 필요하지 않습니다. 

1. 푸시 대시보드에서 **태그** 탭을 선택하십시오. 
1. + **태그 작성** 단추를 클릭하십시오.    

   a. **이름** 필드에 태그 이름을 입력하십시오. 예를 들어, "coupons"를 입력하십시오. 
   
   b. **설명** 필드에 태그 설명을 입력하십시오. 
   
   c. **저장**을 클릭하십시오.
   
1. **코드 스니펫** 영역에서 모바일 애플리케이션에 대한 플랫폼을 선택하십시오. 
1. 코드 스니펫을 수정하여 오류를 수정한 다음 각 태그의 코드 스니펫을 모바일 애플리케이션에 복사하십시오. 

## 태그 삭제
{: #delete_tags}

1. **태그** 탭에서 삭제할 탭을 선택하고 삭제 아이콘을 클릭하십시오. 
1. **확인**을 클릭하십시오. 

## 태그 설명 편집
{: #edit_tags}

1. **태그** 탭에서 편집할 탭을 선택하십시오. 
1. 편집 아이콘을 클릭하십시오. 
1. 태그 설명을 편집하고 **저장** 단추를 클릭하십시오. 

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

# 태그 구독 및 구독 해지
{: #Subscribe_tags}

다음 코드 스니펫을 사용하여 사용자 디바이스가 구독을 가져오고, 태그를 구독하고, 태그를 구독 해지할 수 있도록 합니다.

## Android

다음 코드 스니펫을 복사하여 Android 모바일 애플리케이션에 붙여넣으십시오. 

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

다음 코드 스니펫을 복사하여 Cordova 모바일 애플리케이션에 붙여넣으십시오. 

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

다음 코드 스니펫을 복사하여 Objective-C 모바일 애플리케이션에 붙여넣으십시오. 

태그를 구독하려면 **subscribeToTags** API를 사용하십시오.

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

태그 구독을 취소하려면 **unsubscribeFromTags** API를 사용하십시오.

```
[push unsubscribeFromTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
   if(error){
       [self updateMessage:error.description];
 } else {
       NSDictionary* subStatus = [[NSDictionary alloc]init];
       subStatus = [response unsubscribeStatus];
       [self updateMessage:subStatus.description];
  }
}];
```

## Swift

다음 코드 스니펫을 복사하여 Swift 모바일 애플리케이션에 붙여넣으십시오. 

**사용 가능한 태그 구독**

태그를 구독하려면 **subscribeToTags** API를 사용하십시오.

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in
	if (error != nil) {
//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus();
	}
} 
```

**태그 구독 해지**

태그 구독을 취소하려면 **unsubscribeFromTags** API를 사용하십시오.

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


# 태그 기반 알림 사용
{: #using_tags}


태그 기반 알림은 특정 태그를 구독하는 모든 디바이스를 대상으로 하는 알림 메시지입니다. 각 디바이스는 원하는 수만큼의 태그에 대해 구독이 가능합니다. 여기서는 태그 기반 알림의 전송 방법에 대해 설명합니다. 구독은 푸시 알림 서비스 Bluemix 인스턴스에서 유지보수됩니다. 태그가 삭제되면 구독자와 디바이스를 포함하여 해당 태그와 연관된 모든 정보가 삭제됩니다. 이 태그가 더 이상 존재하지 않고 클라이언트측에서 추가 조치가 필요하지 않으므로 이 태그에 대해 자동 구독 해지 조치가 필요하지 않습니다. 

**시작하기 전에**

**태그** 화면에서 태그를 작성하십시오. 태그 작성 방법에 대한 정보는 [태그 작성](t_manage_tags.html)을 참조하십시오. 

1. **푸시 알림** 대시보드에서 **알림** 탭을 클릭하십시오. 
1. 태그 기반 알림을 전송할 **태그** 옵션을 선택하십시오. 
1. **검색** 태그 필드에서 사용할 태그를 검색하고 **+추가** 단추를 클릭하십시오. ![알림 화면](images/tag_notification.jpg)
1. **메시지 텍스트** 필드의 **알림 작성** 영역으로 이동하여 알림에서 전송할 텍스트를 입력하십시오. 
1. **전송** 단추를 클릭하십시오. 
