---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Sandbox and production modes
{: #push-sandboxandproduction-modes}
Last updated: 11 January 2017
{: .last-updated}

You can use {{site.data.keyword.mobilepushshort}} in either of the following modes: sandbox or production. Sandbox is a self-contained test environment to develop and test push API integration with the server application push service. 

Configure the sandbox and production modes by using the Push Dashboard. You can switch between the mode of operations of the push service - between sandbox and production using the [Push REST API](https://mobile.{DomainName}/imfpush/){: new_window}. By default, sandbox mode is enabled. However, when you switch between modes, the tags, devices, and subscriptions are not shared between these modes.

When you are ready to deploy the application to a live environment, select PRODUCTION mode, by using the [Push REST API](https://mobile.{DomainName}/imfpush/){: new_window}. 

To switch the mode of operation of the push service from sandbox to production:

1. Use the PUT ApplicationID Settings REST API call
2. In the JSON body, confirm that the mode was switched by using the [GET ApplicationID Settings REST](https://mobile.{DomainName}/imfpush/){: new_window} API call. The expected response is "mode": "PRODUCTION
```{ 
    "mode": "PRODUCTION"
    }
```
	{: codeblock}
1. After your environment mode has been switched, run your client code again to register your device in PRODUCTION mode.

For information about the REST API, see [Using REST APIs](t_restapi.html).