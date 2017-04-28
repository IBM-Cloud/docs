---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 태그 기반 알림 사용
{: #tag_based_notifications}
마지막 업데이트 날짜: 2017년 4월 12일
{: .last-updated}

태그 기반 알림 메시지는 특정 태그를 구독하는 모든 디바이스가 대상입니다.  

태그를 정의한 다음 태그를 사용하여 메시지를 전송 및 수신할 수 있습니다. 먼저 애플리케이션에 대한 태그를 작성하고, 태그 구독을 설정한 다음, 태그 기반 알림을 시작해야 합니다. [REST API](https://mobile.{DomainName}/imfpush/){: new_window}를 사용하여 태그 기반 알림을 전송하려면 메시지 리소스에 게시하는 중에 "tagNames"가 제공되는지 확인하십시오. 


## 태그 관리
{: #manage_tags}

{{site.data.keyword.mobilepushshort}} 대시보드를 사용하여 애플리케이션의 태그를 작성 및 삭제하고 태그 기반 알림을 시작합니다. 태그를 구독하는 디바이스에서 태그 기반 알림이 수신됩니다.


### 태그 작성
{: #create_tags}

태그 기반 알림은 특정 태그를 구독하는 모든 디바이스를 대상으로 하는 메시지입니다. 각 디바이스는 수에 관계 없이 태그를 구독할 수 있습니다. 태그가 삭제되면 태그 구독자와 디바이스를 비롯한 해당 태그와 연관된 정보가 삭제됩니다. 태그가 더 이상 존재하지 않으므로 자동 구독 해지가 필요하지 않습니다. 클라이언트 측에서 추가 조치가 필요하지 않습니다.

1. {{site.data.keyword.mobilepushshort}} 대시보드에서 **태그** 탭을 선택하십시오. 
1.  + **태그 작성** 단추를 클릭하십시오.    
   1. **이름** 필드에 태그의 이름을 입력하십시오. 예를 들어, "coupons"를 입력하십시오. 
   1. **설명** 필드에 태그 설명을 입력하십시오. 
   1. **저장**을 클릭하십시오.

1. **코드 스니펫** 영역에서 모바일 애플리케이션에 대한 플랫폼을 선택하십시오. 
1. 코드 스니펫을 수정하여 오류를 수정한 다음 각 태그의 코드 스니펫을 모바일 애플리케이션에 복사하십시오. 

### 태그 삭제
{: #delete_tags}

1. **태그** 탭에서 삭제할 태그를 선택하고 **삭제** 아이콘을 클릭하십시오.
1. **확인**을 클릭하십시오. 

### 태그 설명 편집
{: #edit_tags}

1. **태그** 탭에서 편집할 탭을 선택하십시오. 
1. **편집** 아이콘을 클릭하십시오. 
1. 태그 설명을 편집하고 **저장** 단추를 클릭하십시오. 

## 태그 가져오기
{: #get_tags}

태그는 모든 애플리케이션에 전송되는 일반 브로드캐스트와 달리 관심사를 기반으로 수신인에게 맞춤형 알림을 전송하는 방법을 제공합니다. {{site.data.keyword.mobilepushshort}} 대시보드의 태그 탭을 사용하여 태그를 작성 및 관리하거나 REST API를 사용할 수 있습니다. 코드 스니펫을 사용하여 모바일 애플리케이션에 대한 태그 구독을 관리 및 조회할 수 있습니다. 이러한 코드 스니펫을 사용하여 구독을 가져오고 태그를 구독하며 태그 구독을 취소하고 사용 가능한 태그 목록을 가져올 수 있습니다. 이러한 코드 스니펫을 모바일 애플리케이션에 복사하십시오. 

### Android에서 태그 가져오기
{: #android-get-tags}

**getTags** API는 디바이스를 구독할 수 있는 사용 가능한 태그 목록을 리턴합니다. 디바이스에서 특정 태그를 구독하면 디바이스가 해당 태그와 관련하여 전송되는 {{site.data.keyword.mobilepushshort}}를 수신할 수 있습니다. 

디바이스가 구독하는 태그 목록을 가져오고 사용 가능한 태그 목록을 가져오려면 다음 코드 스니펫을 Android 모바일 애플리케이션에 복사하십시오. 

디바이스가 구독할 수 있는 사용 가능 태그 목록을 가져오려면 다음 **getTags** API를 사용하십시오.

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
	{: codeblock}

### Cordova에서 태그 가져오기
{: #cordova-get-tags}

디바이스가 구독하는 태그 목록과 사용 가능한 태그 목록을 가져오려면 다음 코드 스니펫을 모바일 애플리케이션에 복사하십시오. 

구독에 사용할 수 있는 태그의 배열을 검색하십시오. 

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


### Swift에서 태그 가져오기
{: #swift-get-tags}

**retrieveAvailableTagsWithCompletionHandler** API는 디바이스가 구독하는 데 사용할 수 있는 모든 태그의 목록을 리턴합니다. 디바이스에서 특정 태그를 구독하면 디바이스가 해당 태그와 관련하여 전송되는 {{site.data.keyword.mobilepushshort}}를 수신할 수 있습니다. 

태그를 구독하려면 {{site.data.keyword.mobilepushshort}}를 호출하십시오. 

디바이스가 구독된 사용 가능한 태그 목록을 가져오고 디바이스가 구독할 수 있는 사용 가능한 태그 목록을 가져오려면 다음 코드 스니펫을 Swift 모바일 애플리케이션에 복사하십시오. 
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

### Google Chrome, Safari 및 Mozilla Firefox의 태그 가져오기
{: #web-get-tags}

고객이 구독할 수 있는 사용 가능한 태그 목록을 가져오려면 다음 코드를 사용하십시오. 

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


### Google Chrome 앱 및 확장 프로그램의 태그 가져오기
{: #ext-get-tags}

고객이 구독할 수 있는 사용 가능한 태그 목록을 가져오려면 다음 코드를 사용하십시오. 

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

고객이 구독한 태그의 목록을 가져오려면 다음 코드 스니펫을 Google Chrome 앱 및 확장 프로그램에 복사하십시오. 

```
var bmsPush = new BMSPush();
bmsPush.retrieveSubscriptions(function(response)
{
   alert(response.response)
 })
```
	{: codeblock}


## 태그 구독 및 구독 해지
{: #Subscribe_tags}

다음 코드 스니펫을 사용하여 사용자 디바이스가 구독을 가져오고, 태그를 구독하고, 태그를 구독 해지할 수 있도록 합니다.

### Android에서 태그 구독 및 구독 해지
{: #android-subscribe-tags}

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

### Cordova에서 태그 구독 및 구독 해지
{: #cordova-subscribe-tags}

다음 코드 스니펫을 복사하여 Cordova 모바일 애플리케이션에 붙여넣으십시오. 

```
var tag = "YourTag";
BMSPush.subscribe(tag, success, failure);
BMSPush.unsubscribe(tag, success, failure);
```
	{: codeblock}


### Swift에서 태그 구독 및 구독 해지
{: #swift-subscribe-tags}

다음 코드 스니펫을 복사하여 Swift 모바일 애플리케이션에 붙여넣으십시오. 

태그를 구독하려면 **subscribeToTags** API를 사용하십시오.


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

태그 구독을 취소하려면 **unsubscribeFromTags** API를 사용하십시오.

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

### Google Chrome 및 Mozilla Firefox에서 태그 구독 및 구독 해지
{: #web-subscribe-tags}

웹 애플리케이션에서 태그를 구독하려면 다음 코드 스니펫을 사용하십시오. 

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

태그 구독을 취소하려면 **unSubscribe** 메소드를 사용합니다. 

```
var tagsArray = ["tag1", "Tag2"]
  bmsPush.unSubscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

## 태그 기반 알림 사용
{: #using_tags}

태그 기반 알림은 특정 태그를 구독하는 모든 디바이스를 대상으로 하는 메시지입니다. 각 디바이스는 원하는 수만큼의 태그에 대해 구독이 가능합니다. 이 주제에서는 태그 기반 알림의 전송 방법에 대해 설명합니다. {{site.data.keyword.mobilepushshort}} 서비스 Bluemix 인스턴스에서 구독을 유지보수합니다. 태그가 삭제되면 태그 구독자와 디바이스를 비롯한 해당 태그와 연관된 모든 정보가 삭제됩니다. 이 태그가 더 이상 존재하지 않고 클라이언트측에서 추가 조치가 필요하지 않으므로 이 태그에 대해 자동 구독 해지 조치가 필요하지 않습니다. 

**태그 관리** 옵션을 사용하여 태그를 작성하십시오.  

1. **Push Notification** 대시보드에서 **알림 전송**을 클릭하십시오. 
1. **받는 사람** 드롭 다운 목록에서 **태그별 디바이스** 옵션을 선택하십시오. 
1. 사용할 태그를 검색하여 선택하십시오.
![알림 화면](images/tag_notification.jpg)
1. **메시지 텍스트** 필드에서 알림으로 구독자에게 전송될 텍스트를 입력하십시오. 
1. **전송**을 클릭하십시오. 
