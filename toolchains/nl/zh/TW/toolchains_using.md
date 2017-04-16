---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 在 {{site.data.keyword.Bluemix_notm}} 公用上使用工具鏈
{: #toolchains-using}

前次更新：2016 年 10 月 7 日
{: .last-updated}

在每日開發、部署及操作工作中，使用工具鏈較具生產力。設定工具鏈之後，即可新增、刪除或配置工具整合，以及管理對工具鏈的存取。工具鏈只適用於美國南部地區。
{: shortdesc}

**附註**：請透過檢查頂端橫幅來確定您是以「全新 Bluemix」體驗進行工作。

 * 如果看到有關試用新的 Bluemix 的訊息，則表示您是以「傳統 Bluemix」體驗進行工作。請按一下鏈結，以開啟「全新 Bluemix」體驗。
 * 如果未看到該訊息，則表示您已經以「全新 Bluemix」體驗進行工作。

## 配置工具整合
{: #configuring_a_tool_integration}

如果您已在建立工具鏈時延遲配置工具整合，則會在其磚上顯示**配置**按鈕。如果您已在建立工具鏈時配置工具整合，則可以更新配置設定。

1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟它的「工具整合」頁面。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**工具整合**。
1. 如果您需要配置首次工具整合，請在其磚上按一下**配置**。

  ![「配置」按鈕](images/toolchain_tile_configure.png)

 完成工具整合的配置後，請按一下**儲存整合**。
 
1. 如果您需要更新工具整合的配置，請在其磚上按一下功能表來存取配置選項。

  ![「配置」功能表](images/toolchain_tile_menu.png)
 
 完成設定的更新後，請按一下**儲存整合**。

## 新增工具整合
{: #adding_a_tool_integration}

您可以新增及配置工具鏈的工具整合。

1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟它的「工具整合」頁面。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**工具整合**。
1. 若要查看要新增的工具整合清單，請按一下新增按鈕 (+)。
1. 按一下您要新增的工具整合。
1. 輸入用來配置工具整合的任何必要資訊。 
1. 按一下**建立整合**，以將工具整合新增至您的工具鏈。

## 刪除工具整合
{: #deleting_a_tool_integration}

如果您從工具鏈中刪除工具整合，則無法復原刪除。 

1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟它的「工具整合」頁面。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**工具整合**。
1. 在您要刪除之工具整合的磚上，按一下功能表來存取配置選項。
1. 若要從工具鏈中刪除工具整合，請按一下**刪除**。
1. 按一下**刪除**來進行確認。  

## 管理存取權
{: #managing_access}

將使用者新增至與工具鏈相關聯的組織，即可將工具鏈存取權授與使用者。每一個工具鏈都會與特定組織相關聯，而且任何屬於該組織成員的使用者都可以存取相關聯的工具鏈。您目前在其中工作的組織顯示在功能表列中。請按一下該組織，然後切換至不同的組織來存取一組不同的工具鏈。

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下要管理的工具鏈，然後按一下**管理**。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**管理**。  
1. 按一下您組織的鏈結。 
1. 在「管理組織」頁面上，按一下**邀請使用者**，然後鍵入使用者的電子郵件位址。
1. 如果您要授與管理 {{site.data.keyword.Bluemix_notm}} 組織中使用者的進階許可權，請選取一個以上的**管理員**、**帳單管理員**或**審核員**勾選框。
1. 按一下**邀請**。
1. 按一下**儲存**。

## 刪除工具鏈
{: #deleting_a_toolchain}

您可以刪除工具鏈，以及指定您要刪除的相關聯工具整合。當您刪除工具鏈時，無法復原刪除。

1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下要刪除的工具鏈，然後按一下**管理**。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**管理**。
1. 按一下**刪除工具鏈**，然後檢閱或調整所刪除的工具整合。
1. 鍵入工具鏈名稱，然後按一下**刪除**，來確認刪除。  

 **提示**：當您刪除 GitHub 工具整合時，不會從 GitHub 中刪除相關聯的 GitHub 儲存庫。您必須從 GitHub 中手動移除儲存庫。
