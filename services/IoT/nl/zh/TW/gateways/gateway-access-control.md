---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# 閘道存取控制（測試版）

**重要事項**：此特性目前是受限測試版的一部分。

閘道裝置獲授權可代表其他裝置作業。閘道資源群組定義組織內每一個閘道都可以代表作業的裝置。閘道可獲指派*標準閘道* 角色。標準閘道只能代表其資源群組中的裝置來發佈或訂閱訊息。
{: #shortdesc}


如需使用 API 來發佈閘道裝置事件的相關資訊，請參閱[閘道裝置的 HTTP 傳訊 API](../gateways/gw_intro_api.html)。

## 將角色指派給某閘道
{: #gw_roles}

必須將角色指派給某閘道，閘道才會有資源群組。沒有資源群組的閘道可以代表組織中的所有裝置作業。自動指派*標準閘道* 角色，會建立閘道的新資源群組。將閘道指派給某資源群組之後，此閘道只能代表該資源群組的裝置及本身作業，即使其角色變更也是一樣。

若要將角色指派給某閘道，請使用下列 API：

```
PUT /authorization/devices/{deviceId}/roles
```

如需要求綱目的詳細資訊，請參閱 [{{site.data.keyword.iot_full}} API 文件 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles){: new_window}。

## 將裝置新增至某資源群組以及從中移除裝置
{: #devices_groups}

裝置必須是指派給閘道的資源群組的成員，具有*標準閘道* 角色的閘道才能代表裝置作業。若要同時將多個裝置新增至資源群組，請使用下列 API：

```
 PUT /bulk/devices/{groupId}/add
```

要在其中新增裝置的群組必須指定於要求路徑中，而且要新增的裝置必須指定於要求主體中。如需要求綱目及回應的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} API 文件 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_add){: new_window}。

若要移除資源群組中的多個裝置，請使用下列 API：

```
PUT /bulk/devices/{groupId}/remove
```

將會從要求路徑中所指定的群組中，移除要求主體所指定的裝置。如需要求綱目及回應的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}}API 文件 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_remove){: new_window}。

## 尋找資源群組
{: #finding_groups}

資源群組可以有關聯的搜尋標籤。使用下列 API，可以使用搜尋標籤來擷取資源群組的詳細資料：

```
GET /groups
```

此 API 會傳回與所使用搜尋標籤相關聯的資源群組。如果未指定搜尋標籤，則會傳回所有資源群組。<!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

使用下列 API，可以找到資源群組的 ID：

```
GET /authorization/devices/{deviceId}
```

此 API 會傳回此裝置所屬之資源群組的唯一 ID。您可以在 [{{site.data.keyword.iot_short_notm}} API 文件![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_authorization_devices_deviceId){: new_window} 中找到此 API 的相關資訊。


## 查詢資源群組
{: #querying_groups}

您可以在各種參數內查詢資源群組，以傳回群組中所有裝置的完整內容、群組中所有裝置的唯一 ID，或是資源群組的內容。

若要傳回所指定資源群組中所有裝置的完整內容，請使用下列 API：

```
GET /bulk/devices/{groupId}
```

此 API 會傳回所指定資源群組的所有成員的完整內容清單。如需要求綱目、回應以及如何翻看結果的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} API 文件![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_bulk_devices_groupId){: new_window}。

若只要傳回資源群組成員的唯一 ID，請使用下列 API：

```
GET /bulk/devices/{groupId}/ids
```

此 API 會傳回隸屬於資源群組的所有裝置的唯一 ID。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

若要傳回資源群組的內容，請使用下列 API：

```
GET /groups/{groupId}
```

此 API 會傳回路徑中所指定資源群組的內容（名稱、說明、搜尋標籤及唯一 ID），但不會傳回資源群組成員清單。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## 建立及刪除資源群組。
{: #crt_del_groups}

您可以在不使用連接閘道的情況下建立及刪除資源群組。若要建立資源群組，請使用下列 API：

```
POST /groups
```

此 API 會建立資源群組，並傳回群組詳細資料。<!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

若要刪除資源群組，請使用下列 API：

```
DELETE /groups/{groupId}
```

此 API 會刪除指定的資源群組。隸屬於群組的裝置將從群組中予以移除，但不會影響裝置本身。<!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## 更新群組內容
{: #update_groups}

  - /groups/{groupId}
    - PUT：更新所指定群組的內容。

## 擷取及更新裝置內容。
{: #fdevice_group_props}

有數種方法可以使用 API 來擷取裝置內容，而每一個 API 都會傳回不同的資訊。若要擷取所有連接至 {{site.data.keyword.iot_short_notm}} 組織的裝置的裝置內容，請使用下列 API：

```
GET /authorization/devices:

```

此 API 會傳回所有連接至組織的裝置的內容，包括其存取控制相關內容（角色、狀態、到期日）。<!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

若要擷取裝置內容，而不擷取存取控制相關資訊，請使用下列 API：

```
GET /authorization/devices/{deviceId}
```

此 API 會傳回指定裝置的所有裝置內容，而不傳回存取控制資訊。<!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

若要擷取特定裝置的存取控制資訊，請使用下列 API：

```
GET /authorization/devices/{deviceId}/roles:
```

此 API 會擷取指定裝置的存取控制相關資訊，而不傳回其他裝置內容。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

裝置內容可以使用兩種方式進行更新。您可以更新內容，而不變更存取控制內容，也可以直接更新存取控制內容。

若要更新裝置內容，而不影響存取控制內容，請使用下列 API：

```
PUT /authorization/devices/{deviceId}
```

此 API 只會更新與存取控制無關的裝置的內容。<!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

若只要更新指定裝置的存取控制內容，請使用下列 API：

```
PUT /authorization/devices/{deviceId}/withroles:
```

此 API 只會更新指定裝置的存取控制內容。<!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
