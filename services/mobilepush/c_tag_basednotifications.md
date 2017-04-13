---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Enabling tag-based notifications
{: #tag_based_notifications}
Last updated: 12 April 2017
{: .last-updated}

Tag-based notification messages are targeted to all devices subscribed to a particular tag. 

You can define tags and then send and receive messages using tags. You must first create the tags for the application, set up the tag subscriptions and then initiate the tag-based notifications. To send a Tag-based notification using the [REST API](https://mobile.{DomainName}/imfpush/){: new_window}, ensure that the "tagNames" are provided when posting to the message resource.


## Managing tags
{: #manage_tags}

Use the {{site.data.keyword.mobilepushshort}} dashboard to create and delete tags for your application and then initiate tag-based notifications. The tag-based notification is received on devices that are subscribed to tags.


### Creating tags
{: #create_tags}

Tag-based notifications are messages targeted to all devices subscribed to a particular tag. Each device can subscribe to any number of tags. When a tag is deleted, information associated with that tag, including its subscribers and devices, are deleted. Automatic unsubscribe is not required, as the tag no longer exists. No further action is required from the client side.

1. On the {{site.data.keyword.mobilepushshort}} dashboard, select the **Tags** tab.
1. Click the + **Create Tag** button.   
   1. In the **Name** field, enter the name of the tag. For example, "coupons".
   1. In the **Description** field, enter a tag description.
   1. Click  **Save**.

1. In the **Code Snippets** area, select the platform for your mobile application.
1. Modify the code snippets to handle errors and then copy the code snippets for each tag into your mobile application.

### Deleting tags
{: #delete_tags}

1. From the **Tag** tab, select the tag that you want to delete and click **Delete** icon.
1. Click **OK**.

### Editing a tag description
{: #edit_tags}

1. From the **Tag** tab, select the tag that you want to edit.
1. Click the **Edit** icon.
1. Edit the tag description and then click the **Save** button.

## Getting tags
{: #get_tags}

Tags provide a way to send targeted notifications to users based on their interests, unlike general broadcasts that are sent to all applications. You can create and manage tags by using the Tag tab on the {{site.data.keyword.mobilepushshort}} dashboard or use REST APIs. You can use code snippets to manage and query your tag subscriptions for your mobile application. You can use these code snippets to get subscriptions, subscribe to a tag, unsubscribe from a tag, or get a list of available tags. Copy these code snippets to your mobile application.

### Getting tags on Android
{: #android-get-tags}

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

### Getting tags on Cordova
{: #cordova-get-tags}

Copy the following code snippets to your mobile application to get a list of tags to which the device is subscribed and to a list of available tags.

Retrieve an array of tags that are available for subscription.

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


### Getting tags on Swift
{: #swift-get-tags}

The **retrieveAvailableTagsWithCompletionHandler** API returns the list of available tags to which the device can subscribe. After the device is subscribed to a particular tag, the device can receive {{site.data.keyword.mobilepushshort}} sent for that tag.

Call the {{site.data.keyword.mobilepushshort}} to get subscriptions for a tag.

Copy the following code snippets into your Swift mobile application to get a list of available tags to which the device is subscribed and get a list of available tags to which the device can subscribe.
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

### Getting tags on Google Chrome, Safari and Mozilla Firefox
{: #web-get-tags}

To obtain the list of available tags to which customers can subscribe, use the following code.

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


### Getting tags on Google Chrome Apps and Extensions
{: #ext-get-tags}

To obtain the list of available tags to which customers can subscribe, use the following code.

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

Copy the following code snippet to your Google Chrome Apps and Extensions to get a list of tags to which customers have subscribed.

```
var bmsPush = new BMSPush();
bmsPush.retrieveSubscriptions(function(response) 
{
   alert(response.response)
 })
```
	{: codeblock}


## Subscribing and unsubscribing to tags
{: #Subscribe_tags}

Use the following code snippets to allow your devices to get subscriptions, subscribe to a tag, and unsubscribe from a tag.

### Subscribing and unsubscribing to tags on Android
{: #android-subscribe-tags}

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

### Subscribing and unsubscribing to tags on Cordova
{: #cordova-subscribe-tags}

Copy and paste this code snippet to your Cordova mobile application.

```
var tag = "YourTag";
BMSPush.subscribe(tag, success, failure);
BMSPush.unsubscribe(tag, success, failure);
```
	{: codeblock}


### Subscribing and unsubscribing to tags on Swift
{: #swift-subscribe-tags}

Copy and paste this code snippet to your Swift mobile application.

Use the **subscribeToTags** API to subscribe to a tag.

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

### Subscribing and unsubscribing to tags on Google Chrome and Mozilla Firefox
{: #web-subscribe-tags}

To subscribe to tags from web applications, use the following code snippet:

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

Unsubscribing from the tags uses **unSubscribe** method.

```
var tagsArray = ["tag1", "Tag2"]
 bmsPush.unSubscribe(tagsArray,function(response) {
 alert(response.response)
})
```
	{: codeblock}

## Using tag-based notifications
{: #using_tags}

Tag-based notifications are messages targeted to all devices that are subscribed to a particular tag. Each device can be subscribed to any number of tags. This topic describes how to send tag-based notifications. Subscriptions are maintained by the {{site.data.keyword.mobilepushshort}} service Bluemix instance. When a tag is deleted, all information associated with that tag, including its subscribers and devices are deleted. No automatic unsubscribe is needed for this tag since it no longer exists and no further action is required from the client side.

Create tags using the **Manage Tags** option. 

1. From the **Push Notification** dashboard, click **Send Notifications**.
1. Select the **Device by Tag** option in the **Send To** drop-down list.
1. Search for the tags that want to use and select them.
![Notifications Screen](images/tag_notification.jpg)
1. In the **Message Text** field, enter text that would be sent as a notification to the subscribed audience.
1. Click **Send**.