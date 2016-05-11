---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 管理使用者 {: #manage-users}

{{site.data.keyword.iotrtinsights_short}} 是針對小組協同作業所設計，可讓管理者新增更多使用者來存取 {{site.data.keyword.iotrtinsights_short}} 主控台。
{: shortdesc}

角色說明：
- 操作員
操作員可直接登入 {{site.data.keyword.iotrtinsights_short}} 主控台，來監視其裝置及一組裝置的即時資料流程。操作員也可以啟動及停用規則，以及修改可編輯的儀表板。  
- 管理者
除了操作員可執行的作業之外，管理者還可以新增使用者、管理儀表板佈置、新增資料來源，以及管理裝置類型。  
- 擁有者
擁有者角色是指派給已在 Bluemix 中部署 {{site.data.keyword.iotrtinsights_short}} 服務實例的 IBM ID。擁有者的專用權與管理者相同，但無法予以刪除。

若要新增使用者，請執行下列動作：
1. 將使用者新增至 {{site.data.keyword.iot_short}}。  
>**重要事項：**如果您是新增具有管理者角色的使用者，則也必須將該使用者新增至 {{site.data.keyword.iot_short}}。  

  1. 登入為 {{site.data.keyword.iotrtinsights_short}} 服務之資料來源的 {{site.data.keyword.iot_short}} 服務儀表板。  
  2. 導覽至**存取 > 成員**，然後按一下**新增成員**。
  3. 輸入您要新增之使用者的 IBM ID，然後按一下**新增成員**。
2. 將使用者新增至 {{site.data.keyword.iotrtinsights_short}}。
  1. 以具有管理者角色或擁有者角色的使用者身分，登入 {{site.data.keyword.iotrtinsights_short}} 主控台。
  2. 移至**設定 > 管理使用者**。
  3. 按一下**新增使用者**。
  4. 輸入您要邀請之使用者的電子郵件位址，選取使用者的角色，然後按一下 ![「建立」圖示](images/create.png "「建立」圖示")。
即會將包含 Web 主控台鏈結的電子郵件傳送給使用者。如果電子郵件位址已與 IBM ID 相關聯，使用者可以直接登入並存取主控台。否則，系統會提示使用者先建立免費的 IBM ID，然後再存取主控台。  
>**選取 Real-Time Insights 實例：**能夠以操作員或管理者身分存取多個 Real-Time Insights 實例的使用者，可以在這些實例之間快速地進行切換。在 Real-Time Insights 主控台中，他們可以按一下其使用者名稱，然後選取要存取的實例。  
