---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# {{site.data.keyword.Bluemix_notm}} 存取疑難排解 
{: #accessing}

前次更新：2016 年 8 月 18 日
{: .last-updated} 

一般在存取 {{site.data.keyword.Bluemix}} 時發生的問題，可能包括使用者無法登入 {{site.data.keyword.Bluemix_notm}}、帳戶陷入擱置狀態，等等。然而，在許多情況下，您可以依照下列一些簡單的步驟，從這些問題中回復。
{:shortdesc}

## 無法登入 {{site.data.keyword.Bluemix_notm}}
{: #ts_logintobm}

您必須具有有效的 IBM ID 及密碼才能登入 {{site.data.keyword.Bluemix_notm}}。


嘗試登入 {{site.data.keyword.Bluemix_notm}} 時，您看到下列錯誤訊息：
{: tsSymptoms} 

`The password that you entered is not correct.`


您用來登入 {{site.data.keyword.Bluemix_notm}} 的 IBM ID 及密碼無效。
{: tsCauses} 
 

若要取得有效的 IBM ID 及密碼，請移至「我的 IBM 設定檔」頁面，然後完成下列其中一個步驟：
{: tsResolve}
  * 如果您已登錄一個 IBM ID，而想要檢查您的 ID 及密碼是否有效，請按一下**登入**，並在「登入」頁面上輸入您的 IBM ID 及密碼。如果您忘記密碼，請按一下「登入」頁面上的**忘記密碼**來重設密碼。如果您忘記 IBM ID 或是持續發生密碼問題，請聯絡 Worldwide IBM Registration Help Desk 以取得協助。 
  * 如果您沒有 IBM ID，請按一下**登錄**來登錄一個 IBM ID 及密碼。 
  
**附註：**對於 IBM 員工而言，IBM ID 可能與內部網路登入 ID 不同。 



<!-- begin STAGING ONLY --> 

## 存取外部網站時發生問題
{: #ts_bmlinkid}

除非您鏈結內部網路 ID 與 IBM ID，否則無法使用 IBM 內部網路 ID 來登入 {{site.data.keyword.Bluemix_notm}}。


在您從「{{site.data.keyword.Bluemix_notm}} 登入」頁面中選取**使用內部網路 ID 登入**之後，可能會看到下列錯誤訊息：
{: tsSymptoms} 

`存取外部網站時發生問題`



當您使用未鏈結至 IBM ID 的 IBM 內部網路 ID 登入 {{site.data.keyword.Bluemix_notm}} 時發生此問題。IBM ID 是您用來登入 www.ibm.com 的 ID。
{: tsCauses}


身為 IBM 員工，您必須先鏈結內部網路 ID 與外部 IBM ID，才能使用 IBM 內部網路 ID 來登入 {{site.data.keyword.Bluemix_notm}}。若要鏈結兩個 ID，請完成下列步驟：
{: tsResolve} 

  1. 在[中央登入](https://w3-03.sso.ibm.com/tools/cso/index.jsp){: new_window}頁面上，按一下**我的登入**。
  2. 在「我的登入」頁面上，按一下**鏈結 ID**，然後在「{{site.data.keyword.Bluemix_notm}} 登入」頁面上輸入您的 IBM ID 及密碼。之後，即會自動鏈結您的內部網路 ID 與 IBM ID。
  

<!-- end STAGING ONLY -->




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



## 帳戶擱置
{: #ts_accntpding}

如果您的帳戶擱置，您便無法登入 {{site.data.keyword.Bluemix_notm}}。

 
在登錄取得 {{site.data.keyword.Bluemix_notm}} 試用帳戶之後，您可能無法登入 {{site.data.keyword.Bluemix_notm}}。相反地，您看到下列訊息：
{: tsSymptoms}

<code>您的帳戶處於擱置狀態。請稍候，最晚 24 小時即會收到電子郵件確認信，同時也請檢查垃圾郵件資料夾。如果您仍未收到電子郵件確認，請聯絡 <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Bluemix 支援中心</a>。</code>


在登錄取得 {{site.data.keyword.Bluemix_notm}} 試用帳戶之後，您會收到一封確認電子郵件。您必須按一下此封確認電子郵件中的鏈結，才能完成登錄程序。
{: tsCauses} 

確認電子郵件會寄送到您提供的電子郵件位址。請檢查您的收件匣以及垃圾郵件資料夾。如果您尚未收到確認電子郵件，請與 [{{site.data.keyword.Bluemix_notm}} 支援中心](http://ibm.biz/bluemixsupport.com){: new_window}聯絡。  
{: tsResolve}



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

 

如果您無法邀請使用者加入您的組織，而需要不同的角色來完成這項動作，請與組織管理員聯絡，以變更角色。若要識別您的組織管理員，請完成下列步驟：
{: tsResolve}

  1. 移至「{{site.data.keyword.Bluemix_notm}} 儀表板」，按一下功能表列中的{{site.data.keyword.avatar}}圖示 ![「虛擬人像」圖示](images/account_support.svg)，然後選取**管理組織**。
  2. 移至您的組織，然後檢視**使用者**標籤上的組織管理員資訊。  
  
如果您因自己是合作人員（而非成員）而無法邀請使用者，則您必須刪除先前的 {{site.data.keyword.Bluemix_notm}} 帳戶，然後受邀以組織成員的身分加入帳戶。若要刪除先前的帳戶並以成員的身分加入帳戶，請完成下列步驟： 

  1. 聯絡 [{{site.data.keyword.Bluemix_notm}} 支援](http://ibm.biz/bluemixsupport){: new_window}，以開啟一個支援問題單，並要求刪除您的帳戶。如果您的資料與要儲存並移至新帳戶的舊帳戶相關聯，請在電子郵件中包含此資訊。 
  2. 刪除您的帳戶之後，請讓具有組織管理員角色的使用者，邀請您以組織管理員的身分加入組織。然後，透過該邀請註冊 {{site.data.keyword.Bluemix_notm}}。 




## 不支援批次登錄使用者
{: #ts_batchregistration}

當您向 {{site.data.keyword.Bluemix_notm}} 登錄使用者時，必須個別登錄每一個使用者。
 

{{site.data.keyword.Bluemix_notm}} 不提供同時登錄多個使用者的功能。
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} 不支援批次登錄使用者。若要向 {{site.data.keyword.Bluemix_notm}} 登錄使用者，必須個別登錄每一個使用者。
{: tsCauses}
 

若要向 {{site.data.keyword.Bluemix_notm}} 登錄多個使用者，您必須為每個使用者完成下列步驟：
{: tsResolve}

  1. 按一下 {{site.data.keyword.Bluemix_notm}} 使用者介面中的**註冊**。
  2. 遵循精靈指示來完成步驟。

    

## 無法載入 {{site.data.keyword.Bluemix_notm}} 頁面
{: #ts_err}

當您使用 {{site.data.keyword.Bluemix_notm}} 使用者介面時，您可能無法載入 {{site.data.keyword.Bluemix_notm}} 頁面。反之，可能會看到錯誤訊息 BXNUI0001E 或 BXNUI0016E。
 

當您使用 {{site.data.keyword.Bluemix_notm}} 使用者介面時，您可能會看到下列其中一則錯誤訊息：
{: tsSymptoms}

`BXNUI0001E: 由於 Bluemix 未偵測到階段作業是否存在，因此未載入頁面。`


`BXNUI0016E: 由於未載入 Bluemix 頁面，因此未擷取應用程式及服務。`

 

您可以視需要完成下列其中一個以上的動作：
{: tsResolve}

  * 重新整理或重新啟動瀏覽器。
  * 登出 {{site.data.keyword.Bluemix_notm}} 然後再重新登入。
  * 使用瀏覽器的專用瀏覽模式。 
  * 清除瀏覽器的 Cookie 及快取。
  * 使用不同的瀏覽器。如需 {{site.data.keyword.Bluemix_notm}} 支援的瀏覽器版本的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}。
  * 如果您已安裝 cf 指令行介面，請輸入 `cf apps` 指令來查看您的應用程式是否正在執行中。
  
  
  
  
  

