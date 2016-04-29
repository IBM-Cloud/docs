---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Managing assets {: #manage-assets}

One of the powers of {{site.data.keyword.iotrtinsights_full}} is to map your devices to your managed assets and to create rules that apply to all devices that are mapped to an asset.
{: shortdesc}

For example, a single asset that you are interested in monitoring might include several devices and a large number of sensors.

**Tip:** You can repeat the mapping procedure when your assets are updated or modified. The `action`  parameter in the context and mapping files lets you add and remove assets and devices.

To map your devices to your assets:
1. Create a list of assets and save as a CSV file.  
This file includes asset data from your asset management software.
Sample file format:  
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION  
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+    
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  Where:  
  - ASSETNUM - **Required:** The asset ID number in your system. (12)
  - ASSETTYPE - The type of asset. (15)
  - AS_DESCRIPTION - A brief description of the asset. (100)
  - AS_DESCRIPTION_LD - A complete description of the asset. (32,000)
  - INSTALLDATE - (Date in the format yyyy-MM-dd) The date that the asset was installed.
  - AS_ITEMNUM - A related item number for the asset. (30)
  - AS_ITEMSETID - The item set number for the asset. (8)
  - AS_LOCATION - The location of the asset. (12)
  - PRIORITY - (Integer) The asset priority. (12)
  - PURCHASEPRICE - (Decimal) The purchase price of the asset. (10.2)
  - REPLACECOST - (Decimal) The cost to replace the asset. (10.2)
  - SERIALNUM - The asset serial number. (64)
  - AS_SITEID - The ID of the site that the asset is installed in. (8)
  - AS_STATUS - The status of the asset. (20)
  - ACTION - A `+` symbol means that the asset is added, and a `-` symbol means that the asset is removed.  
  **Tip:** The number in parentheses indicates the maximum length of the string. Unless indicated, the parameter format is alphanumeric characters, mixed case.

5. Create an asset and devices mapping list and save as a CSV file.  
  This file is used to map the imported assets in the asset list to your {{site.data.keyword.iot_short}} devices.  
  Sample file format:  
  ```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  Where:
    - sourceType - Consists of the following {{site.data.keyword.iot_short}} data for your device:
      - orgid - Your {{site.data.keyword.iot_short}} organization ID
      - iot-device-type - Your {{site.data.keyword.iot_short}} Device Type  
    - sourceID - Your {{site.data.keyword.iot_short}} Device ID  
    - targetType - Use the word `asset` to create an asset mapping.
    - targetID - The ASSETNUM entry for the asset from the context file that you created
    - action - A `+` symbol means that the asset is mapped, and a `-` symbol means that the asset is removed from mapping.
2. Log in to the {{site.data.keyword.iotrtinsights_short}}  console as an administrator user.
2. Go to **Devices > Manage Device Groups** and click **Import Asset**.  
3. Browse for and select the asset file that you created.
4. Click ![Create icon.](images/create.png "Create icon") to create the asset list.
3. Browse for and select the assets and devices mapping file that you created.
4. Click ![Create icon.](images/create.png "Create icon") to create the asset list.
5. Go to **Devices > Manage Device Groups** and click one of your assets to see a list of the devices that you mapped to the asset.
