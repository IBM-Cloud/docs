---

copyright:
 years: 2015, 2016

---

# Creating a Push service instance
{: #create-push-instance}

To get started with {{site.data.keyword.IBM}} {{site.data.keyword.mobilepushshort}}, you first create a {{site.data.keyword.Bluemix}} application; for example, a Node.js app. You then create an instance of a Push service, {{site.data.keyword.mobilepushfull}} , which needs to be bound to this Bluemix application. You can also do this by going to the Boilerplate section of the Bluemix catalog and clicking the MobileFirst Services Starter.

**Note**: If you configured organizations to manage your environment, select the organization in which you want to create the runtime and services for your mobile app.


1. If do you not have a Bluemix application, you need to create one; for example, Node.js app. To create a Bluemix application, go to the Bluemix Dashboard and click **Create App**.
	
	**Note**: If you have an application, go to step 7 to add a service.![Create a service instance](images/create_service_instance1.jpg "Create a Service Instance")

1. From **Choose Your App Template**, click **WEB**

3. In the **Choose Starting Point** area, select **SDK for Node.js** and then click **CONTINUE**.![Starting Point](images/create_service_nodejs2.jpg) 

4. From the **Space** pulldown menu, select your organization space.

	![
Select organization space](images/create_a_service3.jpg)
1. In **Name**, enter the name of your app and in the host, enter the name of the host.

1. From the **Selected Plan** pull-down menu, select a plan then click the **CREATE** button. Wait for the application to stage.

1. Click the **Overview** link.![Add a service](images/create_service_add4.jpg)
1. Click **Add a Service**. The CATALOG screen is displayed.

1. Select **IBM Push Notifications:** and from the **Space** pull-down menu, select your organization.

	![Organization space pull-down menu](images/create_service_org.jpg)
1. In the **Service** name, enter the Push Notification service nme.

1. In the **Selected Plan**, select a plan and click the **CREATE** button.

1. Click **Yes** to restage the application.

	![IBM Push Notification Service](images/create_service_notification5.jpg)

1. Click **Push Notifications** to display the Push Notification dashboard.
