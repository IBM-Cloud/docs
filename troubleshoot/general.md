


# General services problems
{: #general}

{{site.data.keyword.Bluemix}} services problems might include a gateway time out error that occurs when you delete a service instance. However, in many cases, you can recover from these problems by following a few easy steps.

## A gateway timeout error message is displayed when you delete a service instance
{: #ts_service_broker}

You might receive an error message when you try to delete a service instance that is already deleted from the cloud controller.

**What's happening**

When you try to delete a service instance, you see the service broker error message, ```Gateway timeout```.


**Why it's happening**

This problem happens if the service instance is already deleted from the cloud controller.


**How to fix it**

To resolve this problem, create a service instance with the same service name, and then bind it to your applications. After that, you can delete the service instance and the applications that use the service.
