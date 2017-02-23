---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-24"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 管理使用者存取權

從存取儀表板中，您可以控制及管理對 {{site.data.keyword.iot_full}} 組織的存取權。您可以透過新增、邀請、登錄或匯入，來新增使用者。您也可以透過指派角色，給與使用者不同的存取權層次。
{:shortdesc}

- [新增使用者](#adding-new-users)
- [編輯使用者](#editing-users)
- [封鎖使用者存取權](#blocking-users)
- [移除使用者](#removing-users)

## 新增使用者
{: #adding-new-users}

從儀表板的**存取**標籤中，您可以使用「新增」、「邀請」或「登錄」功能來新增個別成員。您也可以使用「匯入」功能，同時新增、邀請或登錄多位成員。

依預設，成員帳戶不會到期。將使用者新增至 {{site.data.keyword.iot_short_notm}} 組織時，您可以選擇性地設定其帳戶的到期日。

### 將成員新增至您的 {{site.data.keyword.iot_short_notm}} 組織

若要將成員新增至組織，您將需要成員的 IBM ID。新增成員時，您不需要成員的確認。

若要將單一成員新增至您的 {{site.data.keyword.iot_short_notm}} 組織，請執行下列動作：
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**存取**。
2. 按一下**新增成員**，然後選取**新增**。
3. 輸入成員的 IBM ID。
4. 選取成員的角色。
5. 選用項目：設定成員的到期日。
6. 按一下**新增成員**。

若要同時新增多位成員，您必須上傳 `.csv` 檔案，其中包含每一位成員的 IBM ID、角色及選用性的到期日。
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**存取**。
2. 按一下**新增成員**，然後選取**匯入**。
3. 按一下**大量新增**。
4. 選取預設角色，並確保 `.csv` 檔案上的直欄號碼符合 CSV 設定中的直欄號碼。
5. 確保 `.csv` 檔案中的直欄分隔字元符合 CSV 設定中的直欄分隔字元。
6. 按一下**瀏覽您的檔案**，或將 `.csv` 檔案拖曳至**上傳 CSV** 視窗。

### 邀請成員加入您的 {{site.data.keyword.iot_short_notm}} 組織

當您邀請使用者成為 {{site.data.keyword.iot_short_notm}} 組織的成員時，使用者會收到一封包含邀請鏈結的電子郵件。邀請鏈結會在傳送後的 48 小時到期。如果未在 48 小時內使用邀請鏈結，則必須重新邀請使用者，才會收到新的邀請鏈結。

若要邀請成員加入您的 {{site.data.keyword.iot_short_notm}} 組織，請執行下列動作：
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**存取**。
2. 按一下**新增成員**，然後選取**邀請**。
3. 輸入成員的電子郵件位址。
4. 選取此成員的角色。
5. 選用項目：設定成員的到期日。
6. 按一下**邀請成員**。

若要同時邀請多位成員，您必須上傳 `.csv` 檔案，其中包含每一位成員的電子郵件位址、角色及選用性的到期日。
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**存取**。
2. 按一下**新增成員**，然後選取**匯入**。
3. 按一下**大量邀請**。
4. 選取預設角色，並確保 `.csv` 檔案上的直欄號碼符合 CSV 設定中的直欄號碼。
5. 確保 `.csv` 檔案中的直欄分隔字元符合 CSV 設定中的直欄分隔字元。
6. 按一下**瀏覽您的檔案**，或將 `.csv` 檔案拖曳至**上傳 CSV** 視窗。

### 向您的 {{site.data.keyword.iot_short_notm}} 組織登錄成員

如果您的組織不使用 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}，您可以透過登錄將個別成員新增至組織中，這樣做並不需要 IBM ID。

若要向您的 {{site.data.keyword.iot_short_notm}} 組織登錄成員，請執行下列動作：
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**存取**。
2. 按一下**新增成員**，然後選取**邀請**。
3. 輸入成員的電子郵件位址。
4. 選取此成員的角色。
5. 輸入主旨、領域名稱及發出者。  
   **重要事項：**確保 `Subject`、`Realm Name` 及 `Issuer` 欄位符合 OpenID Connect 的建議及標準。如需相關資訊，請參閱 [OpenID Connect](http://openid.net/connect/) 網站。
6. 選用項目：設定成員的到期日。
7. 按一下**登錄成員**。

若要同時登錄多位成員，您必須上傳 CSV (`.csv`) 檔案，其中包含每一位成員的電子郵件位址、角色、主旨、領域名稱、發出者及選用性的到期日。
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**存取**。
2. 按一下**新增成員**，然後選取**匯入**。
3. 按一下**大量登錄**。
4. 選取預設角色，並確保 CSV 檔案上的直欄號碼符合 CSV 設定中的直欄號碼。
5. 確保 CSV 檔案中的直欄分隔字元符合 CSV 設定中的直欄分隔字元。
6. 按一下**瀏覽您的檔案**，或將 CSV 檔案拖曳至**上傳 CSV** 視窗。

### 建構 CSV 檔案

建構 CSV 檔案以將成員匯入至您的組織時，請確保您在所使用的方法中包含必要資訊。使用逗點或分號來區隔直欄。上傳 CSV 檔案時，請在 **CSV 設定**下，確保您選取正確的直欄分隔字元。

## 編輯使用者
{: #editing-users}

您可以編輯使用者以變更其角色；新增、移除或變更存取到期日，或是新增或移除組織的存取權。

1. 從 {{site.data.keyword.iot_short_notm}} 儀表板中，按一下左側導覽列中的**成員**。
2. 按一下您想要編輯之使用者旁的**編輯**圖示 ![編輯](/docs/images/edit_32.svg)。
3. 對使用者進行想要的變更。
4. 按一下**儲存**。

## 封鎖使用者存取權
{: #blocking-users}

您可以封鎖使用者存取 {{site.data.keyword.iot_short_notm}} 組織，同時仍然維護組織成員資格。

1. 從 {{site.data.keyword.iot_short_notm}} 儀表板中，按一下左側導覽列中的**成員**。
2. 按一下您想要封鎖存取 {{site.data.keyword.iot_short_notm}} 組織之使用者旁的切換按鈕。


## 移除使用者
{: #removing-users}

您可以從 {{site.data.keyword.iot_short_notm}} 組織中完全移除使用者。移除使用者是無法復原的作業，而且必須將使用者[新增至平台](#adding-new-users)才能還原存取權。

1. 從 {{site.data.keyword.iot_short_notm}} 儀表板中，按一下左側導覽列中的**成員**。
2. 按一下要移除之使用者旁的**刪除**圖示 ![刪除](/docs/images/trash_32.svg)。
3. 按一下確認對話框中的**刪除**。
