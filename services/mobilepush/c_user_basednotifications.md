---

Title: Enabling user-based Push Notifications

Keywords: User-based Push Notifications, userId
copyright:
 years: 2015, 2016

---

# Enabling user-based notifications
{: #user_based_notifications}
Last updated: 13 July 2016
{: .last-updated}

User ID-based push notifications are targeted at mobile app users with customized messages. User-based notifications can assist engaging specific individuals in taking advantage of their personal preferences and choices.  

## Register device with User ID
To enable push notifications targeted by User ID, ensure that you register the device with a User ID and also pass the 'clientSecret' that is allocated when the Push Notifications services is provisioned. The device registration will fail without a valid 'clientSecret'.  

The User ID can be any string that the application provides to the device registration API. Typically, a mobile application will first run an authentication cycle where the mobile app user is authenticated against a authentication service [like Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). On successful authentication, the authenticated user ID is then passed into the Push Device Registration API along with a 'clientSecret'.  The presence of a 'clientSecret' enforces only authorized association of User IDs with mobile device registrations.

The 'clientSecret' should be kept confidential and should never be hard-coded into the mobile app. There are various application initialization patterns that can be used to pull in the 'clientSecret' dynamically during the application's runtime. The sequence diagram outlines such a pattern.

![Enable_Push](images/init_client_secret.jpg) 

You may also register a device to be associated with a 'anonymous' user. This requires that you use a variant of the device registration API that does not require the user ID and 'clientSecret' arguments.   

## Synchronizing user login/logout and enabling push notifications 

You can choose to send notifications only if the user is logged in. 

For example, if a device is shared by a family or shared by a team at work, and you need to address specific users in the family or team.  In such a use case, there would be a user log-in and log out sequence that guards the application to track the identity of the present user of the application. To ensure that notifications targeted to a specific user is always received by that user only, after a successful log-in, invoke the device registration API passing the User ID of the logged-in user. Likewise, before logging out, invoke the device unregistration API. Sequencing these Push APIs with log-in and log out will ensure that push notifications meant to a specific user is sent to that user only.