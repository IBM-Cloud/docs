---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Gateway Access Control (BETA)

**Important**: This feature is currently available as part of a limited beta.

Gateway devices are empowered to act on behalf of other devices. Gateway resource groups define which devices within an organization that each gateway can act on behalf of. Gateways can be assigned the *Standard Gateway* role. Standard gateways can only publish or subscribe to messages on behalf of devices in their resource group.
{: #shortdesc}


## Assigning a role to a gateway

Assigning a role to a gateway is mandatory for the gateway to have a resource group. Gateways without a resource group can act on behalf of all devices in the organization. Assigning the *Standard Gateway* role automatically creates a new resource group for the gateway. Once a gateway is assigned to a resource group, it can only act on behalf of the devices in that resource group and itself, even if its role is changed.

To assign a role to a gateway, use the following API:

```
PUT /authorization/devices/{deviceId}/roles
```

For details of the request schema, see the [{{site.data.keyword.iot_full}} API documentation](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles).

## Adding devices to and removing devices from a resource group

Before a gateway with the *Standard Gateway* role can act on behalf of a device, the device must be a member of the resource group assigned to the gateway. To add many devices to a resource group at the same time, use the following API:

```
 PUT /bulk/devices/{groupId}/add
```

The group to add devices to must be specified in the path of the request, and the devices to be added must be specified in the body of the request. For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_bulk_devices_groupId_add).

To remove multiple devices from a resource group, use the following API:

```
PUT /bulk/devices/{groupId}/remove
```

The devices specified in the body of the request will be removed from the group specified in the path of the request. For more information on the request schema and response, see the [{{site.data.keyword.iot_short_notm}} API documentation](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_bulk_devices_groupId_remove).

## Finding a resource group

Resource groups can have associated search tags. Search tags can be used to retrieve the details of a resource group by using the following API:

```
GET /groups
```

This API returns the resource groups associated with the search tag used. If no search tag is specified, all resource groups are returned. <!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

A resource group's ID can be found by using the following API:

```
GET /authorization/devices/{deviceId}
```

This API returns the unique identifier of the resource group(s) this device is a member of. More information on this API can be found in the [{{site.data.keyword.iot_short_notm}} API documentation](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/get_authorization_devices_deviceId).

## Querying a resource group

Resource groups can be queried within various parameters to return either the full properties of all devices in the group, the unique identifiers of all devices in the group, or the properties of the resource group.

To return the full properties of all devices in the specified resource group, use the following API:

```
GET /bulk/devices/{groupId}
```

This API returns the full properties list for all members of the specified resource group. For more information on the request schema, responses, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/get_bulk_devices_groupId).

To return only the unique identifiers of the members of the resource group, use the following API:

```
GET /bulk/devices/{groupId}/ids
```

This API returns the unique identifiers of all devices that are members of the resource group. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

To return the properties of the resource group, use the following API:

```
GET /groups/{groupId}
```

This API returns the properties of the resource group (name, description, search tags, and unique identifier) specified in the path, but does not return the list of members of the resource group. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Creating and deleting a resource group.

Resource groups can be created and deleted independently of connecting gateways. To create a resource group, use the following API:

```
POST /groups
```

This API creates a resource group, and returns the group details. <!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

To delete a resource group, use the following API:

```
DELETE /groups/{groupId}
```

This API deletes the specified resource group. Devices which were a member of the group are removed from the group, but the devices themselves are not otherwise affected. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Updating group properties



  - /groups/{groupId}
    - PUT: updates the properties of the specified group.

## Retrieving and updating device properties.

There are several ways to retrieve device properties using the API, each API returns different information. To retrieve the device properties of all devices connected to your {{site.data.keyword.iot_short_notm}} organization, use the following API:

```
GET /authorization/devices:

```

This API returns the properties of all device connected to the organization, including their access control relevant properties (role, status, expiration date). <!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

To retrieve device properties without retrieving the access control relevant information, use the following API:

```
GET /authorization/devices/{deviceId}
```

This API returns all device properties of the specified device, without returning the access control information. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

To retrieve the access control information of a specific device, use the following API:

```
GET /authorization/devices/{deviceId}/roles:
```

This API retrieves the access control relevant information for the specified device without returning other device properties. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Device properties can be updated in two ways. Properties can be updated without changing the access control properties, or access control properties can be updated directly.

To update device properties without affecting the access control properties, use the following API:

```
PUT /authorization/devices/{deviceId}
```

This API will only update properties of the device which are not associated with access control. <!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

To update only the access control properties of the specified device, use the following API:

```
PUT /authorization/devices/{deviceId}/withroles:
```

This API will only update the access control properties of the specified device. <!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
