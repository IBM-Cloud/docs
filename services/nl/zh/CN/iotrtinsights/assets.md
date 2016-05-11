---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 管理资产
{: #manage-assets}

{{site.data.keyword.iotrtinsights_full}} 的其中一个功能是将设备映射到受管资产，并创建应用于已映射到某个资产的所有设备的规则。
{: shortdesc}

例如，您有兴趣监视的单个资产可能包含多个设备和大量传感器。

>**提示：**更新或修改资产后，可以重复映射过程。通过上下文和映射文件中的 `action` 参数，可以添加和除去资产和设备。
要将设备映射到资产，请执行以下步骤：
1. 创建资产列表，并另存为 CSV 文件。
此文件包含资产管理软件中的资产数据。
样本文件格式：
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  其中：  
  - ASSETNUM - **必需：**系统中的资产标识号。(12)
  - ASSETTYPE - 资产类型。(15)
  - AS_DESCRIPTION - 资产的简短描述。(100)
  - AS_DESCRIPTION_LD - 资产的完整描述。(32,000)
  - INSTALLDATE -（格式为 yyyy-MM-dd 的日期）资产安装日期。
  - AS_ITEMNUM - 资产的相关项目编号。(30)
  - AS_ITEMSETID - 资产的项目集编号。(8)
  - AS_LOCATION - 资产的位置。(12)
  - PRIORITY -（整数）资产优先级。(12)
  - PURCHASEPRICE -（小数）资产的采购价格。(10.2)
  - REPLACECOST -（小数）更换资产的成本。(10.2)
  - SERIALNUM - 资产序列号。(64)
  - AS_SITEID - 资产安装所在站点的标识。(8)
  - AS_STATUS - 资产的状态。(20)
  - ACTION - `+` 号表示添加了资产，`-` 号表示除去了资产。  
  >**提示：**括号中的数字指示字符串的最大长度。除非另有指示，否则参数格式为大小写混合的字母数字字符。

5. 创建资产和设备映射列表，并另存为 CSV 文件。
  此文件用于将资产列表中导入的资产映射到 {{site.data.keyword.iot_short}} 设备。
样本文件格式：
  ```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  其中：
    - sourceType - 由设备的以下 {{site.data.keyword.iot_short}} 数据构成：
      - orgid - 您的 {{site.data.keyword.iot_short}} 组织标识
      - iot-device-type - {{site.data.keyword.iot_short}} 设备类型  
    - sourceID - {{site.data.keyword.iot_short}} 设备标识  
    - targetType - 使用词 `asset` 来创建资产映射。
    - targetID - 已创建的上下文文件中资产的 ASSETNUM 条目。
    - action - `+` 号表示映射了资产，`-` 号表示从映射中除去了资产。
2. 以管理员用户身份登录到 {{site.data.keyword.iotrtinsights_short}} 控制台。
2. 转至**设备 > 管理设备组**，然后单击**导入资产**。  
3. 浏览并选择已创建的资产文件。
4. 单击 ![“创建”图标。](images/create.png "“创建”图标") 以创建资产列表。
3. 浏览并选择已创建的资产和设备映射文件。
4. 单击 ![“创建”图标。](images/create.png "“创建”图标") 以创建资产列表。
5. 转至**设备 > 管理设备组**，然后单击其中一个资产以查看映射到该资产的设备的列表。
