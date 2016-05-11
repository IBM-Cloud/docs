# Getting tags
{: #get_tags}

Tags provide a way to send targeted notifications to users based their interests, unlike general broadcasts that are sent to all applications. You can create and manage tags by using the Tag tab on the Push dashboard or use REST APIs. You can use code snippets in the following sections to manage and query your tag subscriptions for your mobile application. You can use these code snippets to get subscriptions, subscribed to a tag, unsubscribed from a tag, get a list of available tags. You copy and paste these code snippets into your mobile application.

## Android

The **getTags** API returns the list of available tags to which the device can subscribe. After the device is subscribed to a particular tag, the device can receive any push notifications that are sent for that tag.

Copy the following code snippets into your Android mobile application to get a list of tags to which the device is subscribed and to get a list of available tags.

Use the following **getTags** API to get a list of available tags to which the device can subscribe.

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

Use the **getSubscriptions** API to get a list of tags that to which the device is subscribed.

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

Copy the following code snippets into your mobile application to get a list of tags to which the device is subscribed and to get a list of available tags to which the device can subscribe.

Retrieve an array of tags that are available to subscribe to.

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

Copy the following code snippets into your iOS application developed using Objective-C to get a list of tags to which the device is subscribed and get a list of available tags to which the device can subscribe.

Use the following **retrieveAvailableTags** API to get a list of available tags to which the device can subscribe.

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
       
Use the **retrieveSubscriptions** API to get a list of tags that to which the device is subscribed.


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

The **retrieveAvailableTagsWithCompletionHandler** API returns the list of available tags to which the device can subscribe. After the device is subscribed to a particular tag, the device can receive any push notifications that are sent for that tag.

Call the push service to get subscriptions for a tag.

Copy the following code snippets into your Swift mobile application to get a list of available tags to which the device is subscribed and get a list of available tags to which the device can subscribe.


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



