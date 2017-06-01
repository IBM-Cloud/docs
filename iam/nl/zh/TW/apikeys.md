---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 管理 API 金鑰
{: #manapikey}

應用程式設計介面金鑰（API 金鑰）是由電腦程式所傳入的代碼，而這些電腦程式會呼叫應用程式設計介面 (API) 來識別網站的呼叫端程式、其開發人員或其使用者。API 金鑰是用來追蹤及控制 API 的使用方式，例如，防止惡意使用或濫用 API（可能是由服務條款所定義）。API 金鑰通常作為進行鑑別的唯一 ID 及機密記號，而且一般具有其相關聯 API 的一組存取權。API 金鑰是以通用唯一 ID (UUID) 系統為基礎，確保它們對每一位使用者而言都是唯一的。

身為 {{site.data.keyword.Bluemix_notm}} 使用者，在啟用程式或 Script 而不將密碼配送至 Script 時，您可能想要使用 API 金鑰。使用 API 金鑰的好處在於使用者或組織可以為不同的程式建立數個 API 金鑰，而且，如果已受損而不干擾其他 API 金鑰甚至使用者，則可以個別刪除 API 金鑰。此外，身為[聯合使用者](/docs/admin/adminpublic.html#federatedid)，您可以使用 API 金鑰來登入。如需使用 API 金鑰登入的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} CLI `bluemix login` 指令](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login)及 [cf CLI `cf login` 指令](/docs/cli/reference/cfcommands/index.html#cf_login)的文件。

您可以從「Bluemix API 金鑰」視窗來管理 {{site.data.keyword.Bluemix_notm}} API 金鑰。移至**管理** &gt; **安全** &gt; **Bluemix API 金鑰**，以查看具有說明及日期的 API 金鑰清單。您可以從這個頁面建立、編輯或刪除 API 金鑰。

若要建立 API 金鑰，請執行下列動作：

1. 移至**管理** &gt; **安全** &gt; **Bluemix API 金鑰**。
2. 按一下**建立 API 金鑰**。
3. 輸入 API 金鑰的名稱及說明。
4. 按一下**建立 API 金鑰**。
5. 然後，按一下**顯示**以顯示要複製的 API 金鑰，並儲存它以供日後使用，或按一下**下載 API 金鑰**。

**附註**：API 金鑰只適用於在建立時顯示或下載。如果 API 金鑰遺失，您必須建立新的 API 金鑰。

若要編輯 API 金鑰，請執行下列動作：

1. 移至**管理** &gt; **安全** &gt; **Bluemix API 金鑰**。
2. 從表格中所列 API 金鑰的**動作**功能表中，按一下**編輯名稱及說明** 
3. 更新 API 金鑰的資訊。
4. 按一下**更新 API 金鑰**。

若要刪除 API 金鑰，請執行下列動作： 

1. 移至**管理** &gt; **安全** &gt; **Bluemix API 金鑰**。
2. 從表格中所列 API 金鑰的**動作**功能表中，按一下以**刪除**。
3. 然後，按一下**刪除金鑰**來確認刪除。

您也可以使用 {{site.data.keyword.Bluemix_notm}} CLI，透過列出金鑰、建立金鑰、更新金鑰或刪除金鑰來管理 API 金鑰。如需相關資訊，請參閱 [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam) 指令區段。

