---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Sandbox and production modes

{: #push-sandboxandproduction-modes}

You can use the Push Notifications in one of the following modes: sandbox or production. Sandbox is a self-contained test environment to develop and test push API integration with the server application push service. You first configure sandbox and production modes by using the Push Dashboard. You switch the mode of operation of push service between sandbox and production by using the [Push REST API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} . By default, the sandbox mode is enabled. However, when you switch between modes, the tags, devices, and subscriptions are not shared between these modes.


When you are ready to deploy the application to a live environment, select PRODUCTION mode, by using the Push REST API. For information about the REST API, see REST API.

To switch the mode of operation of the push service from sandbox to production:

1. Use the PUT ApplicationID Settings REST API call
2. In the JSON body, confirm that the mode was switched by using the [GET ApplicationID Settings REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} API call. The expected response is "mode": "PRODUCTION
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. After your environment mode has been switched, run your client code again to register your device in PRODUCTION mode.

For information about the REST API, see REST API.