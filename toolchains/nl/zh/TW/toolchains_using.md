---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 使用工具鏈
{: #toolchains-using}

*前次更新：2016 年 5 月 4 日*
{: .last-updated}

在每日開發、部署及操作工作中，使用工具鏈較具生產力。設定工具鏈之後，即可新增、刪除或配置工具整合，以及管理對工具鏈的存取。
{: shortdesc}

**重要事項**：這是實驗性功能。工具鏈可能不穩定，與舊版本不相容的部分也可能會變更。建議不要將它們用於正式作業環境。若要使用工具鏈，您必須進行一次性的[存取要求](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}。工具鏈只適用於美國南部地區。

## 配置工具整合
{: #configuring_a_tool_integration}

您可以配置首次工具整合，或更新已屬於工具鏈一部分之工具整合的配置設定。

1. 在 DevOps 儀表板的**工具鏈**標籤上，按一下工具鏈來開啟它的「工具整合」頁面。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**工具整合**。
1. 如果您需要配置首次工具整合，請在其磚上按一下**配置**。

  ![「配置」按鈕](images/toolchain_tile_configure.png)

 完成工具整合的配置後，請按一下**儲存整合**。
 
1. 如果您需要更新工具整合的配置，請在其磚上按一下功能表來存取配置選項。

  ![「配置」功能表](images/toolchain_tile_menu.png)
 
 完成設定的更新後，請按一下**儲存整合**。

 **附註**：配置 GitHub 工具整合的儲存庫之後，即可更新儲存庫 URL，但無法變更儲存庫本身。若要使用不同的儲存庫，請從工具鏈中刪除現行 GitHub 工具整合，並將 GitHub 工具整合新增至工具鏈，然後配置該工具整合來使用新的儲存庫。

## 新增工具整合
{: #adding_a_tool_integration}

您可以新增及配置工具鏈的工具整合。

1. 在 DevOps 儀表板的**工具鏈**標籤上，按一下工具鏈來開啟它的「工具整合」頁面。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**工具整合**。
1. 若要查看要新增的工具整合清單，請按一下新增按鈕 (+)。
1. 按一下您要新增的工具整合。
1. 輸入用來配置工具整合的任何必要資訊。 
1. 按一下**建立整合**，以將工具整合新增至您的工具鏈。

## 刪除工具整合
{: #deleting_a_tool_integration}

您可以從工具鏈中刪除工具整合。 

1. 在 DevOps 儀表板的**工具鏈**標籤上，按一下工具鏈來開啟它的「工具整合」頁面。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**工具整合**。
1. 在您要刪除之工具整合的磚上，按一下功能表來存取配置選項。
1. 若要從工具鏈中刪除工具整合，請按一下**刪除**。
1. 按一下**刪除**來進行確認。

## 管理存取權
{: #managing_access}

將使用者新增至與工具鏈相關聯的組織，即可將工具鏈存取權授與使用者。每一個工具鏈都會與特定組織相關聯，而且任何屬於該組織成員的使用者都可以存取相關聯的工具鏈。如果您切換至不同的組織，則可以存取一組不同的工具鏈。

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. 在 DevOps 儀表板的**工具鏈**標籤上，按一下要管理的工具鏈，然後按一下**管理**。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**管理**。  
1. 按一下您組織的鏈結。 
1. 在「管理組織」頁面上，按一下**邀請使用者**，然後鍵入使用者的電子郵件位址。
1. 如果您要將進階許可權授與使用者，請選取一個以上的**管理員**、**帳單管理員**或**審核員**勾選框。
1. 按一下**邀請**。
1. 按一下**儲存**。

## 刪除工具鏈
{: #deleting_a_toolchain}

您可以刪除工具鏈，以及指定您要刪除的相關聯工具整合。

1. 在 DevOps 儀表板的**工具鏈**標籤上，按一下要刪除的工具鏈，然後按一下**管理**。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**管理**。
1. 按一下**刪除工具鏈**，然後檢閱所刪除的工具整合。
1. 鍵入工具鏈名稱，然後按一下**刪除**，來確認刪除。

 **提示**：當您刪除 GitHub 工具整合時，不會從 GitHub 中刪除相關聯的 GitHub 儲存庫。您必須從 GitHub 中手動移除儲存庫。
