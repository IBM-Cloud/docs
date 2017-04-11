---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# 网关访问控制 (Beta)

**重要信息**：此功能目前作为受限 Beta 版的一部分提供。

网关设备有权代表其他设备执行操作。网关资源组定义每个网关可以代表组织内的哪些设备执行操作。可以向网关分配*标准网关*角色。标准网关只能代表其资源组中的设备来发布或预订消息。
{: #shortdesc}


有关使用 API 从网关设备发布事件的信息，请参阅[针对网关设备的 HTTP 消息传递 API](../gateways/gw_intro_api.html)。

## 向网关分配角色
{: #gw_roles}

必须向网关分配角色之后，该网关才能拥有资源组。没有资源组的网关可以代表组织中的所有设备执行操作。分配*标准网关*角色会自动为网关创建新的资源组。一旦向网关分配了资源组，该网关就只能代表该资源组中的设备及其自身执行操作，即便更改其角色后也是如此。

要向网关分配角色，请使用以下 API：

```
PUT /authorization/devices/{deviceId}/roles
```

有关请求模式的详细信息，请参阅 [{{site.data.keyword.iot_full}} API 文档 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles){: new_window}。

## 向资源组添加设备以及从资源组中除去设备
{: #devices_groups}

要使具有*标准网关*角色的网关能够代表设备执行操作，该设备必须是分配给该网关的资源组的成员。要同时向某个资源组添加多个设备，请使用以下 API：

```
 PUT /bulk/devices/{groupId}/add
```

要向其添加设备的组必须在请求路径中指定，并且要添加的设备必须在请求主体中指定。有关请求模式和响应的更多信息，请参阅 [{{site.data.keyword.iot_short_notm}} API 文档 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_add){: new_window}。

要从资源组中除去多个设备，请使用以下 API：

```
PUT /bulk/devices/{groupId}/remove
```

在请求主体中指定的设备将从请求路径中指定的组中除去。有关请求模式和响应的更多信息，请参阅 [{{site.data.keyword.iot_short_notm}} API 文档 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_remove){: new_window}。

## 查找资源组
{: #finding_groups}

资源组可以具有关联的搜索标签。搜索标签可用于通过以下 API 来检索资源组的详细信息：

```
GET /groups
```

此 API 将返回与使用的搜索标签关联的资源组。如果未指定任何搜索标签，那么将返回所有资源组。<!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

可以使用以下 API 来查找资源组的标识：

```
GET /authorization/devices/{deviceId}
```

此 API 将返回此设备所属的资源组的唯一标识。有关此 API 的更多信息位于 [{{site.data.keyword.iot_short_notm}} API 文档 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_authorization_devices_deviceId){: new_window} 中。


## 查询资源组
{: #querying_groups}

可以通过各种参数查询资源组，以返回组中所有设备的完整属性、组中所有设备的唯一标识或资源组的属性。

要返回指定资源组中所有设备的完整属性，请使用以下 API：

```
GET /bulk/devices/{groupId}
```

此 API 将返回指定资源组的所有成员的完整属性列表。有关请求模式、响应以及如何逐页浏览结果的更多信息，请参阅 [{{site.data.keyword.iot_short_notm}} API 文档 ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_bulk_devices_groupId){: new_window}。

要仅返回资源组中成员的唯一标识，请使用以下 API：

```
GET /bulk/devices/{groupId}/ids
```

此 API 将返回属于资源组的所有设备的唯一标识。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

要返回资源组的属性，请使用以下 API：

```
GET /groups/{groupId}
```

此 API 将返回路径中所指定资源组的属性（名称、描述、搜索标签和唯一标识），但不会返回资源组中成员的列表。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## 创建和删除资源组
{: #crt_del_groups}

资源组可以独立于连接网关进行创建和删除。要创建资源组，请使用以下 API：

```
POST /groups
```

此 API 将创建资源组，并返回该组的详细信息。<!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

要删除资源组，请使用以下 API：

```
DELETE /groups/{groupId}
```

此 API 将删除指定的资源组。属于该组的设备会从组中除去，但这些设备本身在其他方面并不受影响。<!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## 更新组属性
{: #update_groups}

  - /groups/{groupId}
    - PUT：更新指定组的属性。

## 检索和更新设备属性。
{: #fdevice_group_props}

有多种方式可使用 API 来检索设备属性，每个 API 会返回不同的信息。要检索连接到您 {{site.data.keyword.iot_short_notm}} 组织的所有设备的设备属性，请使用以下 API：

```
GET /authorization/devices:

```

此 API 将返回连接到该组织的所有设备的属性，包括其访问控制相关属性（角色、状态和到期日期）。<!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

要检索设备属性而不检索访问控制相关信息，请使用以下 API：

```
GET /authorization/devices/{deviceId}
```

此 API 将返回指定设备的所有设备属性，而不返回访问控制信息。<!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

要检索特定设备的访问控制信息，请使用以下 API：

```
GET /authorization/devices/{deviceId}/roles:
```

此 API 将检索指定设备的访问控制相关信息，而不返回其他设备属性。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

设备属性可以通过两种方式更新。可以更新属性而不更改访问控制属性，也可以直接更新访问控制属性。

要更新设备属性而不影响访问控制属性，请使用以下 API：

```
PUT /authorization/devices/{deviceId}
```

此 API 将仅更新设备的不与访问控制相关联的属性。<!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

要仅更新指定设备的访问控制属性，请使用以下 API：

```
PUT /authorization/devices/{deviceId}/withroles:
```

此 API 将仅更新指定设备的访问控制属性。<!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
