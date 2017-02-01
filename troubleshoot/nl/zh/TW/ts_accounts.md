---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# 管理帳戶疑難排解
{: #managingaccounts}


您可能會在管理帳戶時遇到問題，例如不同的應用程式共用相同的網域名稱、管理者無法檢視所有組織等等。然而，在許多情況下，您可以依照下列一些簡單的步驟，從這些問題中回復。
{:shortdesc}


## 帳戶處於非作用中
{: #ts_accnt_inactive}

如果帳戶處於非作用中，則您無法在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式。您必須與支援團隊聯絡以修正此問題。



嘗試在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式時，您看到下列錯誤訊息：
{: tsSymptoms} 

`BXNUI0096E: 未建立應用程式。您的帳戶處於非作用中狀態，因為它已取消或已暫停。`


當帳戶遭到取消或暫停時，{{site.data.keyword.Bluemix_notm}} 帳戶的狀態會變成非作用中。
{: tsCauses}

 

若要重新啟動您的帳戶，請聯絡 [{{site.data.keyword.Bluemix_notm}} 支援中心 ![外部鏈結圖示](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window}。在電子郵件中，您必須包含下列資訊：
{: tsResolve}

  * 您用來登入 {{site.data.keyword.Bluemix_notm}} 的 IBM ID。
  * 您的應用程式建立所在的組織名稱。此資訊可幫助支援團隊判斷您是否已在組織內獲指派正確的角色或成員資格。



## 沒有與現行組織相關聯的空間
{: #ts_no_space}

如果沒有空間與您的現行組織相關聯，則您無法建立應用程式。



嘗試在 {{site.data.keyword.Bluemix_notm}} 中建立應用程式時，您看到下列錯誤訊息：
{: tsSymptoms} 


`BXNUI0097E: 在新增應用程式之前，必須至少有一個空間與您的組織和地區相關聯。在「儀表板」上，按一下「建立空間」。建立空間後，請重試。`



{{site.data.keyword.Bluemix_notm}} 中的應用程式必須在組織下的空間內建立。
{: tsCauses} 

 

若要建立空間，請使用下列其中一種方法：
{: tsResolve}
 
  * 在 {{site.data.keyword.Bluemix_notm}}「儀表板」上，選取您要在其中建立空間的組織，然後按一下**建立空間**。
  * 在 cf 指令行介面中，鍵入 `cf create-space <space_name> -o <organization_name>`。
  
  
  
  
## 應用程式共用相同的網域名稱
{: #ts_domain_diff}

您可能注意到 {{site.data.keyword.Bluemix_notm}} 中有數個應用程式共用相同的 URL。

 

將相同的 URL 路徑指派給空間內的不同應用程式時，可能會發生此問題。
{: tsCauses}

例如，您將 myApp1 應用程式推送至 {{site.data.keyword.Bluemix_notm}}，並將網域設為 "mynewapp.stage1.mybluemix.net"。然後，將另一個 myApp2 應用程式推送至相同的空間，並將它的其中一個 URL 路徑設為 "mynewapp.stage1.mybluemix.net"。路徑現在對映至兩個應用程式。

 

這是 {{site.data.keyword.Bluemix_notm}} 的支援行為，而且您可以使用此作法，讓應用程式升級達到零中斷時間。如需相關資訊，請參閱藍綠部署。
{: tsResolve}
  
	
	
<!-- begin STAGING ONLY --> 
	
	
## 管理者無法使用 {{site.data.keyword.Bluemix_notm}} 使用者介面來檢視所有組織
{: #ts_ui_org}

身為管理者，當您使用 {{site.data.keyword.Bluemix_notm}} 使用者介面時，無法顯示每個組織來進行管理。您只能顯示及管理您所屬的那些組織。

 

身為管理者，您無法使用 {{site.data.keyword.Bluemix_notm}} 使用者介面來查看所有組織。
{: tsSymptoms}

 

這是 {{site.data.keyword.Bluemix_notm}} 使用者介面的限制。
{: tsCauses}

 

您可以從 cf 指令行介面使用 `cf orgs`、`cf create-org` 及 `cf delete-org` 這類指令來管理所有組織。如需完整的 cf 指令清單，請輸入 `cf help`。
{: tsResolve}
	
<!-- end STAGING ONLY -->




## 無法新增信用卡
{: #ts_addcc}

您無法提交信用卡資訊，以將試用帳戶轉換為「隨收隨付制」帳戶。

 

「新增信用卡」頁面上的「提交」按鈕會被停用。
{: tsSymptoms}

 

若您的資訊未正確地填入「新增信用卡」頁面中，即會發生此問題。
{: tsCauses}

 

請完成下列步驟，以解決此問題：
{: tsResolve}

  1. 在「新增信用卡」頁面上，填入聯絡資訊、聯絡地址及帳單地址區段中的所有必要欄位。
  2. 選取**我已閱讀並同意 IBM 條款**，然後按一下**提交**。即會顯示**選取付款方法**區段。
  3. 輸入信用卡上的信用卡號碼、信用卡到期日及安全碼。然後，按一下**提交**。


