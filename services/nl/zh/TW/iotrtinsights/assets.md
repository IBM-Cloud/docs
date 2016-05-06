---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 管理資產 {: #manage-assets}

{{site.data.keyword.iotrtinsights_full}} 的其中一個功能是將裝置對映至受管理資產，以及建立適用於對映至資產之所有裝置的規則。
{: shortdesc}

例如，您要監視的單一資產可能包括數台裝置以及大量的感應器。

>**提示：**更新或修改資產時，您可以重複對映程序。環境定義及對映檔中的 `action` 參數可讓您新增及移除資產和裝置。

若要將裝置對映至資產，請執行下列動作：
1. 建立資產清單，並儲存為 CSV 檔。
此檔案包括來自資產管理軟體的資產資料。
檔案格式範例：
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION  
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+    
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  其中：  
  - ASSETNUM - **必要項目：**系統中的資產 ID 號碼。(12)
  - ASSETTYPE - 資產的類型。(15)
  - AS_DESCRIPTION - 資產的簡要說明。(100)
  - AS_DESCRIPTION_LD - 資產的完整說明。(32,000)
  - INSTALLDATE -（yyyy-MM-dd 格式的日期）資產的安裝日期。
  - AS_ITEMNUM - 資產的相關項目號碼。(30)
  - AS_ITEMSETID - 資產的項目集號碼。(8)
  - AS_LOCATION - 資產的位置。(12)
  - PRIORITY -（整數）資產優先順序。(12)
  - PURCHASEPRICE -（小數）資產的購買價格。(10.2)
  - REPLACECOST -（小數）更換資產的成本。(10.2)
  - SERIALNUM - 資產序號。(64)
  - AS_SITEID - 在其中安裝資產的網站 ID。(8)
  - AS_STATUS - 資產的狀態。(20)
  - ACTION - `+` 符號表示已新增資產，而 `-` 符號表示已移除資產。  
  >**提示：**括弧中的數字指出字串的長度上限。除非指出，否則參數格式是英數字元，且大小寫混合。

5. 建立資產及裝置對映清單，並儲存為 CSV 檔。
  此檔案用來將資產清單中的已匯入資產對映至 {{site.data.keyword.iot_short}} 裝置。
  檔案格式範例：
  ```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  其中：
    - sourceType - 包含裝置的下列 {{site.data.keyword.iot_short}} 資料：
      - orgid - {{site.data.keyword.iot_short}} 組織 ID
      - iot-device-type - {{site.data.keyword.iot_short}} 裝置類型  
    - sourceID - {{site.data.keyword.iot_short}} 裝置 ID  
    - targetType - 使用 `asset` 這個字來建立資產對映。
    - targetID - 來自您建立之環境定義檔案的資產的 ASSETNUM 項目
    - action - `+` 符號表示已對映資產，而 `-` 符號表示已從對映中移除資產。
2. 以管理者使用者身分登入 {{site.data.keyword.iotrtinsights_short}} 主控台。
2. 移至**裝置 > 管理裝置群組**，然後按一下**匯入資產**。  
3. 瀏覽並選取您已建立的資產檔案。
4. 按一下 ![「建立」圖示](images/create.png "「建立」圖示")，以建立資產清單。
3. 瀏覽並選取您已建立的資產及裝置對映檔。
4. 按一下 ![「建立」圖示](images/create.png "「建立」圖示")，以建立資產清單。
5. 移至**裝置 > 管理裝置群組**，然後按一下您的其中一個資產，以查看您已對映至資產的裝置清單。
