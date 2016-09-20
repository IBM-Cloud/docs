---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} troubleshooting
{: #troubleshooting}

*Last updated: 17 August 2016*
{: .last-updated}

Here are the answers to common troubleshooting questions about using {{site.data.keyword.objectstoragefull}}.

## Unrecognized token contentpack returned when using openstack4J with Liberty Profile
{: #unrecognized_token}

### Symptom

The following stacktrace might occur when using openstack4j with the Liberity Profile:

    Exception thrown by application class 'org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity:124'
    org.openstack4j.api.exceptions.ClientResponseException: Unrecognized token 'contentpack': was expecting ('true', 'false' or 'null') at [Source: contentpack ; line: 1, column: 12]
    at org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity(HttpResponseImpl.java:124)
    at org.openstack4j.core.transport.HttpEntityHandler.handle(HttpEntityHandler.java:56)
    at org.openstack4j.connectors.okhttp.HttpResponseImpl.getEntity(HttpResponseImpl.java:68)
    at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:169)
    at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:163)
    at org.openstack4j.openstack.storage.object.internal.ObjectStorageContainerServiceImpl.list(ObjectStorageContainerServiceImpl.java:41)
    at com.mimotic.SecureMessageApp.HelloResource.getInformation(HelloResource.java:47)
    at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    at sun.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)
    at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
    at java.lang.reflect.Method.invoke(Unknown Source)

### Solution

This problem results from a class-loading issue, where the openstack4j library contains some of the same packages that are provided in the Liberty profile.  For example, OpenStack4j uses JERSEY, which might collide with the Wink libs.

To resolve the problem, follow these steps:

1. Use reverse classloading (parentLast).
2. Exclude jaxrs from the enabled features.

## Getting help and support for {{site.data.keyword.objectstorageshort}}
{: #gettinghelp}

If you have problems or questions when using {{site.data.keyword.objectstoragefull}}, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.

* If you have technical questions about {{site.data.keyword.objectstorageshort}}, post your question on [Stack Overflow](http://stackoverflow.com/search?q=object-storage+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "object-storage".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/object-storage/?smartspace=bluemix){:new_window} forum. Include the  "object-storage" and "bluemix" tags.

See [Getting help](https://console.ng.bluemix.net/docs/support/index.html#getting-help) for more details about using the forums.

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](https://console.ng.bluemix.net/docs/support/index.html#contacting-support).
