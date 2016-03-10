{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} troubleshooting
{: #troubleshooting}

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
