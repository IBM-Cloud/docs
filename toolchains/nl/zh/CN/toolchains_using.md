---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 在 {{site.data.keyword.Bluemix_notm}} Public 上使用工具链
{: #toolchains-using}

*上次更新时间：2016 年 8 月 12 日*
{: .last-updated}

您可以通过工具链使日常开发、部署和操作工作更富有成效。设置工具链后，可以添加、删除或配置工具集成，并管理对工具链的访问权。
{: shortdesc}

**重要信息**：此功能是试验性的。工具链可能不稳定，并且可能会发生变化而与较低版本不兼容。因此，不建议在生产环境中使用工具链。工具链只能在美国（南部）区域中使用。

## 配置工具集成
{: #configuring_a_tool_integration}

如果创建工具链时未立即配置工具集成，那么会在其磁贴上显示**配置**按钮。如果创建工具链时配置了工具集成，那么可以更新配置设置。

1. 在 DevOps 仪表板的**工具链**选项卡上，单击工具链来打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**工具集成**。
1. 如果是首次需要配置工具集成，请单击其磁贴上的**配置**。

  ![“配置”按钮](images/toolchain_tile_configure.png)

 完成配置工具集成后，单击**保存集成**。
 
1. 如果需要更新工具集成的配置，请单击其磁贴上的菜单来访问配置选项。

  ![配置菜单](images/toolchain_tile_menu.png)
 
 完成更新设置后，单击**保存集成**。

## 添加工具集成
{: #adding_a_tool_integration}

可以向工具链添加工具集成并对工具集成进行配置。

1. 在 DevOps 仪表板的**工具链**选项卡上，单击工具链来打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**工具集成**。
1. 要查看要添加的工具集成的列表，请单击添加按钮 (+)。
1. 单击要添加的工具集成。
1. 输入配置工具集成所必需的所有信息。 
1. 单击**创建集成**以将工具集成添加到工具链。

## 删除工具集成
{: #deleting_a_tool_integration}

如果从工具链中删除工具集成，此删除操作将无法撤销。 

1. 在 DevOps 仪表板的**工具链**选项卡上，单击工具链来打开其“工具集成”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**工具集成**。
1. 在要删除的工具集成对应的磁贴上，单击菜单以访问配置选项。
1. 要从工具链中删除工具集成，请单击**删除**。
1. 通过单击**删除**以确认。  

## 管理访问权
{: #managing_access}

可以通过将用户添加到工具链关联的组织来授予用户对工具链的访问权。每个工具链都与一个特定组织相关联，属于该组织的任何用户都可以访问关联的工具链。单击菜单栏中的 **{{site.data.keyword.avatar}}** 图标 ![Avatar 图标](../icons/i-avatar-icon.svg) 以打开“帐户和支持”窗口小部件，并查看您当前在其中工作的组织。切换到其他组织可访问另一组不同的工具链。

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. 在 DevOps 仪表板的**工具链**选项卡上，单击要管理的工具链，然后单击**管理**。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**管理**。  
1. 单击组织的链接。 
1. 在“管理组织”页面上，单击**邀请用户**，然后输入用户的电子邮件地址。
1. 如果要授予高级许可权来管理 {{site.data.keyword.Bluemix_notm}} 组织中的用户，请选中**管理员**、**记帐管理员**或**审计员**复选框中的一个或多个复选框。
1. 单击**邀请**。
1. 单击**保存**。

## 删除工具链
{: #deleting_a_toolchain}

可以删除工具链，并指定要删除哪些关联的工具集成。删除工具链时，此删除操作无法撤销。

1. 在 DevOps 仪表板的**工具链**选项卡上，单击要删除的工具链，然后单击**管理**。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**管理**。
1. 单击**删除工具链**，然后查看或调整要删除的工具集成。
1. 通过输入工具链的名称并单击**删除**以确认删除。  

 **提示**：删除 GitHub 工具集成时，不会从 GitHub 中删除关联的 GitHub 存储库。您必须手动从 GitHub 中除去该存储库。
