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
