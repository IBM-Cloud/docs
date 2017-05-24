---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 管理使用者存取權
{: #managing-user-access}

從成員儀表板中，您可以控制及管理對 {{site.data.keyword.iot_full}} 組織的存取權。您可以透過新增、邀請<!--, registering-->或匯入的方式來新增使用者。您也可以透過指派角色，授與使用者不同的存取權層次。
{:shortdesc}

## 新增使用者
{: #adding-new-users}

從儀表板的**成員**標籤中，您可以使用<!--Add, Invite, or Register-->「新增」或「邀請」功能來新增個別成員。您也可以使用「匯入」功能，同時<!--add, invite, or register-->新增或邀請多位成員。

依預設，成員帳戶不會到期。將使用者新增至 {{site.data.keyword.iot_short_notm}} 組織時，您可以選擇性地設定其帳戶的到期日。

### 將成員新增至您的 {{site.data.keyword.iot_short_notm}} 組織

若要將成員新增至組織，您將需要成員的 IBM ID。新增成員時，您不需要成員的確認。

若要將單一成員新增至您的 {{site.data.keyword.iot_short_notm}} 組織，請執行下列動作：
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**成員**。
2. 按一下**新增成員**，然後選取**新增**標籤。
3. 輸入成員的 IBM ID。
4. 選取成員的角色。
5. 選用項目：設定成員的到期日。
6. 按一下**新增**。

若要同時新增多位成員，您必須上傳 `.csv` 檔案，其中包含每一位成員的 IBM ID、角色及選用性的到期日。如需相關資訊，請參閱[建構 CSV 檔案](#constructing-your-csv)。
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**成員**。
2. 按一下**新增成員**，然後選取**匯入**標籤。
3. 瀏覽您的檔案，或將 `.csv` 檔案拖曳至**上傳 CSV** 視窗。
4. 選取在無法辨識 CSV 檔案中指定的角色時，所要使用的預設角色。
5. 將 CSV 檔案中的直欄號碼對映至相對應的 IBM ID、角色和（選用）到期日項目。
6. 配合 `.csv` 檔案中使用的分隔字元，選取適當的逗點或分號直欄分隔字元。
7. 按一下**匯入**，以匯入 IBM ID 並建立成員。


### 邀請成員加入您的 {{site.data.keyword.iot_short_notm}} 組織

當您邀請使用者成為 {{site.data.keyword.iot_short_notm}} 組織的成員時，使用者會收到一封包含邀請鏈結的電子郵件。邀請鏈結會在傳送後的 48 小時到期。如果未在 48 小時內使用邀請鏈結，則必須重新邀請使用者，才會收到新的邀請鏈結。

**重要事項：**邀請功能需要有已配置的郵件服務。如需相關資訊，請參閱[外部服務整合](reference/extensions/index.html#email)主題中的「電子郵件」小節。

若要邀請成員加入您的 {{site.data.keyword.iot_short_notm}} 組織，請執行下列動作：
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**成員**。
2. 選取**邀請**標籤。
2. 按一下**邀請成員**，然後選取**邀請**標籤。
3. 輸入成員的電子郵件位址。
4. 選取此成員的角色。
5. 選用項目：設定成員的到期日。
6. 按一下**邀請成員**。

若要同時邀請多位成員，您必須上傳 `.csv` 檔案，其中包含每一位成員的電子郵件位址、角色及選用性的到期日。如需相關資訊，請參閱[建構 CSV 檔案](#constructing-your-csv)。
1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，移至**成員**。
2. 選取**邀請**標籤。
2. 按一下**邀請成員**，然後選取**匯入**標籤。
3. 瀏覽您的檔案，或將 `.csv` 檔案拖曳至**上傳 CSV** 視窗。
4. 選取在無法辨識 CSV 檔案中指定的角色時，所要使用的預設角色。
5. 將 CSV 檔案中的直欄號碼對映至相對應的電子郵件位址、角色和（選用）到期日項目。
6. 配合 `.csv` 檔案中使用的分隔字元，選取適當的逗點或分號直欄分隔字元。
7. 按一下**匯入**，以送出邀請。

<!-- ### Registering a member with your {{site.data.keyword.iot_short_notm}} organization

If your organization is using {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, you can add individual members to your organization by registering them, which does not require an IBMid.

To register a member with your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Select the **Invitations** tab.
2. Click **Invite Members** and select **Invite**.
3. Enter the email address of the member.
4. Select a role for this member.
5. Enter the subject, realm name, and issuer.
   **Important:** Ensure that the `Subject`, `Realm Name`, and `Issuer` fields comply with the OpenID Connect recommendations and standards. For more information, see the [OpenID Connect ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://openid.net/connect/){: new_window} website.
6. Optional: Set an expiry date for the member.
7. Click **Register Member**.

To register multiple members simultaneously, you must upload a CSV (`.csv`) file that contains the email address, role, subject, realm name, issuer, and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Register**.
4. Select a default role and ensure that the column numbers on your CSV file match the column numbers in the CSV settings.
5. Ensure the column separator in your CSV file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the CSV file into the **Upload CSV** window. -->

### 建構 CSV 檔案
{: #constructing-your-csv}

建構 CSV 檔案以將成員匯入至您的組織時，請確保您在所使用的方法中包含必要資訊。使用逗點或分號來區隔直欄。  
**重要事項：**上傳 CSV 檔案時，請在 **CSV 設定**下，確定您選取正確的直欄分隔字元。

以逗點定界的 CSV 檔案範例：  
```
user1@sample.com,PD_DEVELOPER_USER,1489505652152
user2@sample.com,PD_OPERATOR_USER,1489505652152
user3@sample.com,PD_ADMIN_USER,1489505652152
```

使用下列直欄項目的位置：  
- 直欄 1：使用者的電子郵件位址。  
如果您要新增成員，請確定您使用的電子郵件位址對應於有效的 IBM ID。如果您要邀請成員，可以使用任何有效的電子郵件位址。
- 直欄 2：要指派給使用者的角色。  
請輸入下列其中一個角色：
 - PD_ADMIN_USER
 - PD_OPERATOR_USER
 - PD_DEVELOPER_USER
 - PD_ANALYST_USER
 - PD_READER_USER  
如需使用者角色的相關資訊，請參閱[使用者、應用程式及閘道角色](roles_index.html#user_roles)。
- 直欄 3：對應於使用者到期日的 Unix 時間戳記（自 1970 年 1 月 1 日 00:00 UTC 開始的毫秒數）。

## 編輯使用者
{: #editing-users}

您可以編輯使用者以變更其角色；新增、移除或變更存取到期日，或是新增或移除組織的存取權。

1. 從 {{site.data.keyword.iot_short_notm}} 儀表板中，按一下左側導覽列中的**成員**。
2. 按一下您想要編輯之使用者旁的**編輯**圖示。
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
2. 按一下要移除之使用者旁的**刪除**圖示。
3. 按一下確認對話框中的**刪除**。
