---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Sending basic notifications to web browsers
{: #web_notifications}
Last updated: 11 January 2017
{: .last-updated}

After you have developed your applications, you can send a push notification. 

1. Select **Send Notifications**, and compose a message by choosing **Web Notifications** as the **Send To** option. 
2. Type the message that needs to be delivered in the **Message** field.
3. You can choose to provide optional settings:
  - **Notification Title**: This is the text that would be displayed as message alert heading.
  - **Notification Icon URL**: If your message needs to be delivered with an app notification icon, provide the link to your icon in the field.
  - **Time to live**: Notifies the server on the validity of the messages.
4. For web notifications sent to Safari browser, there are some additional information required:
  - **Action**: This is the label of the action button.
  - **URL Arguments**: The URL arguments that need to be used with this notification. Ensure that this is provided in the form of a JSON array. 
 
The following image shows the web notifications option in the dashboard.

  ![Notifications screen](images/DashboardWebpush.jpg)


## Next steps
  {: #next_steps_tags}

After you have successfully set up basic notifications, you can choose to configure tag-based notifications and advanced options.

Add these {{site.data.keyword.mobilepushshort}} service features to your app. To use tag-based notifications, see [Tag-based Notifications](c_tag_basednotifications.html). To use advanced notifications options, see [Advanced notifications](t_advance_badge_sound_payload.html).



