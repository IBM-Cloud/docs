---

copyright:
 years: 2015, 2016

---

# Managing tags
{: #manage_tags}

Use the Push dashboard to create and delete tags for your application and then initiate tag-based notifications. The tag-based notification is received on the device that is subscribed to the tag.


## Creating tags
{: #create_tags}

Tag-based notifications are notification messages that are targeted to all the devices that are subscribed to a particular tag. Each device can subscribe to any number of tags. When a tag is deleted, all the information associated with that tag, including its subscribers and devices are deleted. No automatic unsubscribe is needed for this tag since it no longer exists and no further action is required from the client side.

1. On the Push dashboard, select the **Tags** tab.
1. Click the + **Create Tag** button.   

   a. In the **Name** field, enter the name of the tag. For example, "coupons".
   
   b. In the **Description** field, enter a tag description.
   
   c. Click  **Save**.
   
1. In the **Code Snippets** area, select the platform for your mobile application.
1. Modify the code snippets to handle errors and then copy the code snippets for each tag into your mobile application.

## Deleting tags
{: #delete_tags}

1. From the **Tag** tab, select the tag that you want to delete and click the delete icon.
1. Click **OK**.

## Editing a tag description
{: #edit_tags}

1. From the **Tag** tab, select the tag that you want to edit.
1. Click the edit icon.
1. Edit the tag description and then click the **Save** button.

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

# Subscribing and unsubscribing tags
{: #Subscribe_tags}

Use the following code snippets to allow your devices to get subscriptions, subscribe to a tag, and unsubscribe from a tag.

## Android

Copy and paste this code snippet into your Android mobile application.

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

Copy and paste this code snippet into your Cordova mobile application.

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

Copy and paste this code snippet into your Objective-C mobile application.

Use the **subscribeToTags** API to subscribe to a tag.

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

Use the **unsubscribeFromTags** API to unsubscribe from a tag.

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

Copy and paste this code snippet into your Swift mobile application.

**Subscribe to Available Tags**

Use the **subscribeToTags** API to subscribe to a tag.

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in
	if (error != nil) { 
		//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus(); 
	}
} 
```

**Unsubscribe Tags**

Use the **unsubscribeFromTags** API to unsubscribe from a tag.

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


# Using tag-based notifications
{: #using_tags}


Tag-based notifications are notification messages that are targeted to all the devices that are subscribed to a particular tag. Each device can be subscribed to any number of tags. This section describes how to send tag-based notifications. Subscriptions are maintained by the Push Notifications service Bluemix instance. When a tag is deleted, all the information associated with that tag, including its subscribers and devices are deleted. No automatic unsubscribe is needed for this tag since it no longer exists and no further action is required from the client side.

**Before you begin**

Create tags on the **Tag** screen. For information about how to create tags, see [Creating tags](t_manage_tags.html).

1. From the **Push Notification** dashboard, click the **Notifications** tab.
1. Select the **Tags** option to send tag-based notifications.
1. In the **Search** tags field, search for the tags that want to use and then click the **+Add** button.![Notifications Screen](images/tag_notification.jpg)
1. Go to the **Create Your Notifications** area and in the **Message Text** field, enter text that want to send in your notification.
1. Click the **Send** button.
