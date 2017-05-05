---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.contdelivery_short}} 疑難排解
{: #ts_cd}

取得使用 {{site.data.keyword.contdelivery_full}} 之一般疑難排解問題的答案。
{:shortdesc}


## 無法授權使用 GitHub
{: #cannot_authorize_github}

您未獲授權使用 GitHub。
{:shortdesc}

如果您未獲授權 {{site.data.keyword.Bluemix_notm}} 存取 GitHub 帳戶，則可能會發生下列任何問題：
{: tsSymptoms}

 * 當您嘗試將 GitHub 工具整合新增至工具鏈時，未新增工具整合。
 * 當您將變更推送至 GitHub 或 GitHub Enterprise 儲存庫時，未自動執行管線。

{{site.data.keyword.Bluemix_notm}} 未獲授權存取 GitHub。  
{: tsCauses}
 
如果您要在建立工具鏈時配置 GitHub 工具整合，請遵循下列步驟：
{: tsResolve}
 
  1. 在「可配置的整合」區段中，按一下 **GitHub**。 
  1. 如果您在「{{site.data.keyword.Bluemix_notm}} 公用」上建立工具鏈，但並未授權 {{site.data.keyword.Bluemix_notm}} 存取 GitHub，請按一下**授權**來移至 GitHub 網站。 
  1. 如果您沒有作用中的 GitHub 階段作業，則系統會提示您登入。按一下**授權應用程式**，以容許 {{site.data.keyword.Bluemix_notm}} 存取 GitHub 帳戶。如果您有作用中的 GitHub 階段作業，但最近未輸入過密碼，則系統可能會提示您輸入 GitHub 密碼進行確認。
  
如果您已有工具鏈，請更新 GitHub 工具整合的配置：

 1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**，然後按一下**概觀**。
 1. 在 GitHub 卡上，按一下功能表，然後按一下**配置**。
 1. 更新配置設定，以授權 {{site.data.keyword.Bluemix_notm}} 存取 GitHub。按一下**授權**，以移至 GitHub 網站。如果您沒有作用中的 GitHub 階段作業，則系統會提示您登入。按一下**授權應用程式**，以容許 {{site.data.keyword.Bluemix_notm}} 存取 GitHub 帳戶。如果您有作用中的 GitHub 階段作業，但最近未輸入過密碼，則系統可能會提示您輸入 GitHub 密碼進行確認。
 1. 完成設定的更新後，請按一下**儲存整合**。


## 未配置工具整合
{: #tool_integration_error}

配置工具鏈的工具整合之後，其工具卡上顯示 `Setup failed` 錯誤。
{:shortdesc}

配置工具整合之後，檢視其在工具鏈之「概觀」頁面上的工具卡，並注意到設定失敗。
{: tsSymptoms}

 ![設定失敗錯誤](images/tool_setup_failed.png)
 
新增工具整合時，工具鏈會與工具整合所代表的工具進行通訊，來佈建任何必要資源，以及建立它們與工具鏈的關聯。如果在設定處理程序期間發生錯誤，或工具鏈與工具之間的通訊未適當地完成，則工具整合會進入錯誤狀態。
{: tsCauses}

重新配置工具整合：
{: tsResolve}

1. 在其工具卡上，將游標移至 `Setup failed` 訊息上方，然後按一下**重新配置**。

 ![「重新配置」按鈕](images/tool_reconfigure.png)
 
1. 確定您使用的是有效的配置參數。如果是無效的配置導致錯誤，則會顯示錯誤訊息；例如，`The integration could not be set up. Check the settings and try again. Reason: Invalid api_key:fakeKey`。更新工具整合的設定，然後按一下**儲存整合**。
1. 如果是通訊問題導致錯誤，請按一下**儲存整合**以重試。
