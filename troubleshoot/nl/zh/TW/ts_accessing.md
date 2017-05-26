---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# {{site.data.keyword.Bluemix_notm}} 存取疑難排解 
{: #accessing}


在存取 {{site.data.keyword.Bluemix}} 時發生的一般問題，可能包括無法登入 {{site.data.keyword.Bluemix_notm}}，或是帳戶處於擱置狀態。在許多情況下，您可以遵照一些簡單的步驟，從這些問題回復。
{:shortdesc}

## 無法登入 {{site.data.keyword.Bluemix_notm}}：密碼不正確
{: #ts_logintobm}

您必須要有與 IBM ID 相關聯的有效密碼，才能登入 {{site.data.keyword.Bluemix_notm}} 主控台。

您必須要有與 IBM ID 或 SoftLayer ID 相關聯的有效密碼，才能透過[客戶入口網站](https://control.softlayer.com)來登入。

當您嘗試登入 {{site.data.keyword.Bluemix_notm}} 時，顯示下列錯誤訊息：
{: tsSymptoms} 

`The password that you entered is not correct.`

您用來登入 {{site.data.keyword.Bluemix_notm}} 的 IBM ID 和密碼無效。
{: tsCauses} 
 
使用下列其中一個解決方案：
{: tsResolve}
 * 輸入正確的密碼。若要檢查您的 IBM ID 和密碼是否有效，您可以移至「我的 IBM 設定檔」頁面，按一下**登入**，然後在「登入」頁面上輸入您的 IBM ID 和密碼。 
 * 如果您忘記密碼，請按一下**忘記密碼**來重設密碼。然後，回到 [Bluemix 主控台](https://console.{DomainName})或[客戶入口網站](https://control.softlayer.com)，再重新登入。
 * 如果您忘記 IBM ID 或是持續發生密碼問題，請與 Worldwide IBM Registration Help Desk 聯絡以取得協助。 
 * 若要取得有效的 IBM ID 和密碼，請移至「我的 IBM 設定檔」頁面，然後按一下**登錄**。
  
**附註：**如果您在「登入 IBM」頁面上，而登入處理程序因為任何原因（例如，正在重設密碼）中斷，請回到 [Bluemix 主控台](https://console.{DomainName})或[客戶入口網站](https://control.softlayer.com)，再重新開始登入處理程序。
 

## 無法登入 {{site.data.keyword.Bluemix_notm}}：登入認證無效
{: #ts_login_invalid_credentials}

當您使用 IBM ID 登入時，顯示下列訊息：
{: tsSymptoms}

`提供的登入認證無效。如果您有與帳戶相關聯的 IBM ID，請在這裡登入` 

* 您已切換至 IBM ID，但嘗試使用先前的 SoftLayer 使用者名稱和密碼，透過[客戶入口網站](https://control.softlayer.com)來登入。
{: tsCauses}

* 您嘗試透過[客戶入口網站](https://control.softlayer.com)來登入，卻在「使用者名稱」和「密碼」欄位中輸入您的 IBM ID 和密碼。 

按一下訊息中的**在這裡登入**，或移至「IBM ID 帳戶登入」區段，然後按一下**使用 IBM ID 登入**。
{: tsResolve}

請不要使用您之前用於 Softlayer ID 的**使用者名稱**和**密碼**欄位。


## 無法登入 {{site.data.keyword.Bluemix_notm}}：無法辨識的 IBM ID 或電子郵件
{: #ts_softlayer_username}

當您登入 {{site.data.keyword.Bluemix_notm}} 主控台時，顯示下列訊息：
{: tsSymptoms} 

`We didn't recognize this IBMid or email.`

您嘗試登入 {{site.data.keyword.Bluemix_notm}} 主控台，但未使用有效的 IBM ID。例如，您未輸入 IBM ID 的完整電子郵件位址，或是嘗試使用 SoftLayer 使用者名稱和密碼。
{: tsCauses}
 
您必須具有有效的 IBM ID 及密碼才能登入 {{site.data.keyword.Bluemix_notm}}。

 * 確定您輸入的是 IBM ID 的完整電子郵件位址。
 {: tsResolve}
 * 如果您是具有 SoftLayer ID 的 SoftLayer 使用者，必須先在「客戶入口網站」中，於您可存取的每一個帳戶中切換至 IBM ID 鑑別，才能使用 IBM ID 鑑別登入。如需相關資訊，請參閱[切換至 IBM ID](/docs/admin/softlayerlink.html#ibmid_switch)。


## 無法登入 {{site.data.keyword.Bluemix_notm}}：IBM ID 未與任何 IBM Cloud 帳戶相關聯
{: #ts_login_noswitch}

當您使用 IBM ID 登入時，顯示下列訊息：
{: tsSymptoms}

`You have reached this page because your authentication was successful, however, this IBMid is not associated with any IBM Cloud accounts. If you believe this to be in error, contact your Account Owner or Master User.`

您已從[客戶入口網站](https://control.softlayer.com)使用有效的 IBM ID 登入，但未於 SoftLayer 中切換至 IBM ID 鑑別。
{: tsCauses} 
 
請視情況完成下列檢查：
{: tsResolve}
 * 與主要使用者或帳戶管理者聯絡，確定您可以切換至 IBM ID 鑑別。
 * 確定您已經在 SoftLayer 帳戶中完成「切換至 IBM ID」步驟。請參閱[切換至 IBM ID](/docs/admin/softlayerlink.html#ibmid_switch)。
 * 確定您已遵循**建立 SoftLayer 使用者與 IBM ID 的關聯**電子郵件中的動作。檢查您的收件匣和垃圾郵件資料夾，以尋找此電子郵件。若要重新取得電子郵件（例如它已過期），請移至「控制入口網站」中的「編輯使用者設定檔」頁面，然後按一下**重新傳送電子郵件**。或者，請聯絡 [{{site.data.keyword.Bluemix_notm}} 支援中心 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://ibm.biz/bluemixsupport.com){: new_window}。

**附註：**如果您是直接以 IBM ID 來建立您的 IBM ID，您會收到兩封要處理的電子郵件；一封來自 IBM ID 登錄，另一封來自 Softlayer。請務必遵循這兩封電子郵件中的動作。

視帳戶的設定方式而定，您可能可以使用其中一些登入選項： 
 * 具有 SoftLayer ID 的 SoftLayer 使用者必須透過[客戶入口網站](https://control.softlayer.com)登入。
 * 具有 IBM ID 並且具有（或沒有）已鏈結 Bluemix 帳戶的 SoftLayer 使用者，可以透過[客戶入口網站](https://control.softlayer.com)登入，以開啟「SoftLayer 客戶入口網站」，或透過 [Bluemix 主控台](https://console.{DomainName})來開啟「基礎架構」儀表板。 


## 無法登入 {{site.data.keyword.Bluemix_notm}}：IBM ID 未與任何 {{site.data.keyword.Bluemix_notm}} 帳戶相關聯
{: #ts_unabletologin}

當您登入 {{site.data.keyword.Bluemix_notm}} 時，顯示下列訊息：
{: tsSymptoms} 
 
`You have reached this page because your authentication was successful, however, this IBMid is not associated with any  {{site.data.keyword.Bluemix_notm}} accounts.`

您已從 [Bluemix 主控台](https://console.{DomainName})使用有效的 IBM ID 登入，但尚未建立 {{site.data.keyword.Bluemix_notm}} 帳戶。
{: tsCauses} 

若要建立 {{site.data.keyword.Bluemix_notm}} 帳戶，請遵循註冊處理程序。
{: tsResolve}

視帳戶的設定方式而定，您可能可以使用其中一些登入選項： 
 * 沒有已鏈結 SoftLayer 帳戶的 Bluemix 使用者必須透過 Bluemix 主控台登入。
 * 具有已鏈結 SoftLayer 帳戶的 Bluemix 使用者可以透過 [Bluemix 主控台](https://console.{DomainName})或[客戶入口網站](https://control.softlayer.com)登入。
 

## 無法登入 {{site.data.keyword.Bluemix_notm}}：主控台未開啟
{: #ts_login_stalls}

當您使用 IBM ID 登入時，顯示登入成功訊息，但您未回到 [Bluemix 主控台](https://console.{DomainName})或[客戶入口網站](https://control.softlayer.com)。
{: tsSymptoms}

使用下列其中一個解決方案：
{: tsResolve}
 * 關閉您的瀏覽器，清除快取和 Cookie，然後嘗試重新登入。
 * 確定您是從 [Bluemix 主控台](https://console.{DomainName})或[客戶入口網站](https://control.softlayer.com)登入，而不是直接從 IBM ID 鑑別服務登入。
 
 
## 無法登入 {{site.data.keyword.Bluemix_notm}}：IBM ID 登入未完成
{: #ts_login_ibmid}

當您登入 {{site.data.keyword.Bluemix_notm}} 時，未完成以 IBM ID 進行鑑別。
{: tsSymptoms}

IBM ID 鑑別服務可能有問題。
{: tsCauses}

在 [IBM BlueID ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window} 檢查服務狀態，然後重試。
{: tsResolve}


## 無法登入 {{site.data.keyword.Bluemix_notm}}：帳戶處於擱置狀態
{: #ts_accntpding}

如果您的帳戶處於擱置狀態，即無法登入 {{site.data.keyword.Bluemix_notm}}。
 
在登錄取得 {{site.data.keyword.Bluemix_notm}} 試用帳戶之後，您可能無法登入 {{site.data.keyword.Bluemix_notm}}。系統會顯示下列訊息：
{: tsSymptoms}

<code>您的帳戶處於擱置狀態。請稍候，最晚 24 小時即會收到電子郵件確認信，同時也請檢查垃圾郵件資料夾。如果您仍未收到確認電子郵件，請與 <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix 支援中心</a>聯絡。</code>

在登錄取得 {{site.data.keyword.Bluemix_notm}} 試用帳戶之後，您會收到一封確認電子郵件。您必須按一下此封確認電子郵件中的鏈結，才能完成登錄程序。
{: tsCauses} 

確認電子郵件會寄送到您提供的電子郵件位址。檢查您的收件匣和垃圾郵件資料夾。如果您尚未收到確認電子郵件，請與 [{{site.data.keyword.Bluemix_notm}} 支援中心 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://ibm.biz/bluemixsupport.com){: new_window} 聯絡。  
{: tsResolve}


## 您有未儲存的變更
{: #ts_unsaved_changes}

在應用程式詳細資料頁面上進行瀏覽時，可能無法執行任何動作，系統可能會提示您儲存變更後才能繼續。 

在應用程式詳細資料頁面上嘗試檢查應用程式或服務時，總是收到下列錯誤訊息：
{: tsSymptoms} 

`您在頁面 app_name 中有未儲存的變更。請儲存或取消這些變更。`

在運行環境窗格的**實例**或**記憶體配額**欄位上捲動滑鼠時，值就會變更。這是有意這樣設計的；但是，當您要離開該頁面時，會有錯誤訊息提示您儲存記憶體或實例設定。
{: tsCauses}

關閉訊息視窗，然後按一下運行環境窗格中的**重設**按鈕。
{: tsResolve} 
  
    
## {{site.data.keyword.Bluemix_notm}} 地區之間的自動失效接手無法使用
{: #ts_failover}

您無法在 {{site.data.keyword.Bluemix_notm}} 地區之間使用自動失效接手。不過，您可以使用支援在多個 IP 位址之間進行失效接手的 DNS 提供者，作為暫行解決方法。

當 {{site.data.keyword.Bluemix_notm}} 地區變成無法使用時，在該地區中執行的應用程式也會無法使用，即使相同應用程式正在另一個 {{site.data.keyword.Bluemix_notm}} 地區中執行亦然。
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} 尚未提供從一個地區到另一個地區的自動失效接手。
{: tsCauses}
 
您可以使用支援在多個 IP 位址之間進行智慧型失效接手的 DNS 提供者，並且手動配置 DNS 設定，以啟用 {{site.data.keyword.Bluemix_notm}} 地區之間的自動失效接手。具有此功能的 DNS 提供者包括 NSONE、Akamai、Dyn。
{: tsResolve}

當您配置 DNS 設定時，必須指定應用程式執行所在之 {{site.data.keyword.Bluemix_notm}} 地區的公用 IP 位址。若要取得 {{site.data.keyword.Bluemix_notm}} 地區的公用 IP 位址，請使用 `nslookup` 指令。例如，您可以在指令行視窗鍵入下列指令：

```
nslookup stage1.mybluemix.net
```

## 無法將使用者新增至組織
{: #ts_adduser}

您可以邀請多位使用者在相同的組織下工作。唯有您是帳戶擁有者，或同時為組織的管理員與成員時，才能邀請使用者加入您的組織。
 
您無法在**管理組織**區段中看到**邀請新使用者**鏈結。
{: tsSymptoms}

只有下列 {{site.data.keyword.Bluemix_notm}} 使用者可以邀請使用者加入組織：
{: tsCauses}
  * 組織的帳戶擁有者
  * 同時為組織成員（非合作人員）的組織管理員
  
在 {{site.data.keyword.Bluemix_notm}} 中，您可以是組織的成員或合作人員：

<dl><dt>合作人員</dt>
<dd>如果您已有 {{site.data.keyword.Bluemix_notm}} 帳戶，而別人邀請加入組織，則您是組織的合作人員。</dd>
<dt>成員</dt>
<dd>如果您沒有 {{site.data.keyword.Bluemix_notm}} 帳戶，但某人邀請您加入組織，且您透過該邀請註冊 {{site.data.keyword.Bluemix_notm}}，則您是組織的成員。</dd>
</dl>

如果您是組織的合作人員，即使已將您指派為組織管理員，您也無法邀請使用者加入您的組織。

**附註：**所有組織管理員（包括身為組織合作人員者）都可以新增、修改及移除已經在組織中的使用者。

如果無法邀請使用者加入您的組織，而需要不同的角色來完成這項動作，請與組織管理員聯絡，以變更您的角色。若要識別您的組織管理員，請完成下列步驟：
{: tsResolve}

  1. 移至 {{site.data.keyword.Bluemix_notm}}「儀表板」。從功能表列中，按一下**帳戶**功能表項目，然後按一下**管理組織**。
  2. 移至您的組織，然後檢視**使用者**標籤上的組織管理員資訊。  
  
如果您因自己是合作人員（而非成員）而無法邀請使用者，則必須刪除您先前的 {{site.data.keyword.Bluemix_notm}} 帳戶，然後受邀以組織成員的身分加入帳戶。若要刪除先前的帳戶並以成員的身分加入帳戶，請完成下列步驟： 

  1. 與 [{{site.data.keyword.Bluemix_notm}} 支援中心聯絡 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://ibm.biz/bluemixsupport){: new_window}，以開啟支援問題單，並要求刪除您的帳戶。如果您的資料與要儲存並移至新帳戶的舊帳戶相關聯，請在電子郵件中包含此資訊。 
  2. 刪除您的帳戶之後，請讓具有組織管理員角色的使用者，邀請您以組織管理員的身分加入組織。然後，透過該邀請註冊 {{site.data.keyword.Bluemix_notm}}。 

## 不支援將使用者批次登錄
{: #ts_batchregistration}

當您向 {{site.data.keyword.Bluemix_notm}} 登錄使用者時，必須個別登錄每一個使用者。

{{site.data.keyword.Bluemix_notm}} 未提供同時登錄多位使用者的功能。
{: tsSymptoms}
 
{{site.data.keyword.Bluemix_notm}} 不支援批次登錄使用者。若要向 {{site.data.keyword.Bluemix_notm}} 登錄使用者，必須個別登錄每一個使用者。
{: tsCauses}
 
若要向 {{site.data.keyword.Bluemix_notm}} 登錄多位使用者，請為每一位使用者完成下列步驟：
{: tsResolve}

  1. 按一下 {{site.data.keyword.Bluemix_notm}} 主控台中的**註冊**。
  2. 遵循精靈指示來完成步驟。
    

## 無法載入 {{site.data.keyword.Bluemix_notm}} 頁面
{: #ts_err}

當您使用 {{site.data.keyword.Bluemix_notm}} 主控台時，可能無法載入 {{site.data.keyword.Bluemix_notm}} 頁面。反之，可能會看到錯誤訊息 BXNUI0001E 或 BXNUI0016E。
 
當您使用 {{site.data.keyword.Bluemix_notm}} 主控台時，可能會看到下列其中一則錯誤訊息：
{: tsSymptoms}

`BXNUI0001E: 由於 Bluemix 未偵測到階段作業是否存在，因此未載入頁面。`

`BXNUI0016E: 由於未載入 Bluemix 頁面，因此未擷取應用程式及服務。`

請視需要完成下列一個以上的動作：
{: tsResolve}

  * 重新整理或重新啟動瀏覽器。
  * 登出 {{site.data.keyword.Bluemix_notm}} 然後再重新登入。
  * 使用瀏覽器的專用瀏覽模式。 
  * 清除瀏覽器的 Cookie 及快取。
  * 使用不同的瀏覽器。如需 {{site.data.keyword.Bluemix_notm}} 支援的瀏覽器版本相關資訊，請參閱 [Bluemix 必要條件](/docs/overview/whatisbluemix.html#prereqs)。
  * 如果您已安裝 cf 指令行介面，請輸入 `cf apps` 指令，以查看您的應用程式是否正在執行中。
