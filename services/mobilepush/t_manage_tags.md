---

copyright:
 years: 2015, 2016

---

# Managing tags
{: #manage_tags}
Last updated: 29 August 2016
{: .last-updated}

Use the {{site.data.keyword.mobilepushshort}} dashboard to create and delete tags for your application and then initiate tag-based notifications. The tag-based notification is received on devices that are subscribed to tags.


## Creating tags
{: #create_tags}

Tag-based notifications are messages targeted to all devices subscribed to a particular tag. Each device can subscribe to any number of tags. When a tag is deleted, information associated with that tag, including its subscribers and devices, are deleted. Automatic unsubscribe is not required, as the tag no longer exists. No further action is required from the client side.

1. On the {{site.data.keyword.mobilepushshort}} dashboard, select the **Tags** tab.
1. Click the + **Create Tag** button.   
   1. In the **Name** field, enter the name of the tag. For example, "coupons".
   1. In the **Description** field, enter a tag description.
   1. Click  **Save**.

1. In the **Code Snippets** area, select the platform for your mobile application.
1. Modify the code snippets to handle errors and then copy the code snippets for each tag into your mobile application.

## Deleting tags
{: #delete_tags}

1. From the **Tag** tab, select the tag that you want to delete and click **Delete** icon.
1. Click **OK**.

## Editing a tag description
{: #edit_tags}

1. From the **Tag** tab, select the tag that you want to edit.
1. Click the **Edit** icon.
1. Edit the tag description and then click the **Save** button.

# Getting tags
{: #get_tags}

Tags provide a way to send targeted notifications to users based on their interests, unlike general broadcasts that are sent to all applications. You can create and manage tags by using the Tag tab on the {{site.data.keyword.mobilepushshort}} dashboard or use REST APIs. You can use code snippets to manage and query your tag subscriptions for your mobile application. You can use these code snippets to get subscriptions, subscribe to a tag, unsubscribe from a tag, or get a list of available tags. Copy these code snippets to your mobile application.

## Android
{: android-get-tags}

The **getTags** API returns the list of available tags to which the device can subscribe. After the device is subscribed to a particular tag, the device can receive {{site.data.keyword.mobilepushshort}} that are sent for that tag.

Copy the following code snippets to your Android mobile application to get a list of tags to which the device is subscribed and to get a list of available tags.

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
	{: codeblock}

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
	{: codeblock}

## Cordova
{: cordova-get-tags}

Copy the following code snippets to your mobile application to get a list of tags to which the device is subscribed and to a list of available tags.

Retrieve an array of tags that are available to subscribe to.

	```
	//Get a list of available tags to which the device can subscribe
	MFPPush.retrieveAvailableTags(function(tags) {
    alert(tags);
	}, null);

	```
	{: codeblock}

	```
	//Get a list of available tags to which the device is subscribed.
	MFPPush.getSubscriptionStatus(function(tags) {
    alert(tags);
	}, null);
	```
	{: codeblock}

## Objective-C
{: objc-get-tags}

Copy the following code snippets to your iOS application, developed using Objective-C to get a list of tags to which the device is subscribed and get a list of available tags to which the device can subscribe.

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
	{: codeblock}

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
	{: codeblock}

## Swift
{: swift-get-tags}

The **retrieveAvailableTagsWithCompletionHandler** API returns the list of available tags to which the device can subscribe. After the device is subscribed to a particular tag, the device can receive {{site.data.keyword.mobilepushshort}} sent for that tag.

Call the {{site.data.keyword.mobilepushshort}} to get subscriptions for a tag.

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
	{: codeblock}

	```
	//Get a list of available tags to which the device is subscribed
	push.retrieveSubscriptionsWithCompletionHandler { (response, statusCode, error) -> Void in
    if error.isEmpty {

        print( "Response during retrieving subscribed tags : \(response?.description)")
        print( "status code during retrieving subscribed tags : \(statusCode)")
    }
    else {
        print( "Error during retrieving subscribed tags \(error) ")
        Print( "Error during retrieving subscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
	}
	```
	{: codeblock}


# Subscribing and unsubscribing tags
{: #Subscribe_tags}

Use the following code snippets to allow your devices to get subscriptions, subscribe to a tag, and unsubscribe from a tag.

## Android
{: android-subscribe-tags}

Copy and paste this code snippet to your Android mobile application.

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

## Cordova
{: cordova-subscribe-tags}

Copy and paste this code snippet to your Cordova mobile application.

	```
	var tag = "YourTag";
	MFPPush.subscribe(tag, success, failure);
	MFPPush.unsubscribe(tag, success, failure);
	```
	{: codeblock}

## Objective-C
{: objc-subscribe-tags}

Copy and paste this code snippet to your Objective-C mobile application.

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
	{: codeblock}

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
	{: codeblock}

## Swift
{: swift-subscribe-tags}

Copy and paste this code snippet to your Swift mobile application.

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
	{: codeblock}

**Unsubscribe Tags**

Use the **unsubscribeFromTags** API to unsubscribe from a tag.

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

# Using tag-based notifications
{: #using_tags}

Tag-based notifications are messages targeted to all devices that are subscribed to a particular tag. Each device can be subscribed to any number of tags. This topic describes how to send tag-based notifications. Subscriptions are maintained by the {{site.data.keyword.mobilepushshort}} service Bluemix instance. When a tag is deleted, all information associated with that tag, including its subscribers and devices are deleted. No automatic unsubscribe is needed for this tag since it no longer exists and no further action is required from the client side.

###Before you begin
{: before-you-begin}

Create tags on the **Tag** screen. For information about how to create tags, see [Creating tags](t_manage_tags.html).

1. From the **Push Notification** dashboard, click the **Notifications** tab.
1. Select the **Tags** option to send tag-based notifications.
1. In the **Search** tags field, search for the tags that want to use and then click the **+Add** button.![Notifications Screen](images/tag_notification.jpg)
1. In the **Message Text** field, enter text that would be sent as a notification to the subscribed audience.
1. Click the **Send** button.
