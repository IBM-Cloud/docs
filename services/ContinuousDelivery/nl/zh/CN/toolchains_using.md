---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 在 {{site.data.keyword.Bluemix_notm}} Public 中使用工具链
{: #toolchains-using}

上次更新时间：2016 年 11 月 9 日
{: .last-updated}

您可以使用工具链，以使您的每日开发、部署和操作工作更富成效。设置工具链之后，您可以添加、删除或配置工具集成，并管理工具链的访问。
工具链仅在美国南部区域可用。
{: shortdesc}

## 配置工具集成
{: #configuring_a_tool_integration}

如果创建工具链时延迟了工具集成的配置，那么其磁贴上会显示**配置**按钮。如果创建工具链时配置了工具集成，可以更新配置设置。

1. 在 DevOps 仪表板的**工具链**页面上，单击工具链，以打开其“概述”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**概述**。
1. 如果您需要全新配置工具集成，请在其磁贴上，单击**配置**。

  ![“配置”按钮](images/toolchain_tile_configure.png)

 完成配置工具集成时，单击**保存集成**。
 
1. 如果您需要更新工具集成的配置，请在其磁贴上，单击菜单以访问配置选项。

  ![配置菜单](images/toolchain_tile_menu.png)
 
 完成更新设置时，单击**保存集成**。

## 添加工具集成
{: #adding_a_tool_integration}

您可以为工具链添加和配置工具集成。

1. 在 DevOps 仪表板的**工具链**页面上，单击工具链，以打开其“概述”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**概述**。
1. 要查看要添加的工具集成列表，请单击**添加工具**。
1. 单击要添加的工具集成。
1. 输入配置工具集成所需的任何信息。 
1. 单击**创建集成**，以向工具链添加工具集成。

## 删除工具集成
{: #deleting_a_tool_integration}

如果从工具链删除工具集成，那么该删除操作无法撤销。 

1. 在 DevOps 仪表板的**工具链**页面上，单击工具链，以打开其“概述”页面。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**概述**。
1. 在要删除的工具集成的磁贴上，单击菜单以访问配置选项。
1. 要从工具链删除工具集成，请单击**删除**。
1. 单击**删除**以确认。  

## 管理访问权
{: #managing_access}

您可以通过将用户添加到与工具链相关联的组织，对用户授予工具链的访问权。每一个工具链都与特定组织相关联，且属于该组织成员的任何用户都可以访问相关联的工具链。您当前正在哪个组织中工作会显示在菜单栏中。单击该组织，然后切换到不同的组织以访问不同的工具链集。

1. 在 DevOps 仪表板的**工具链**页面上，单击要管理的工具链，然后单击**管理**。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**管理**。  
1. 单击指向组织的链接。 
1. 在“管理组织”页面上，单击**邀请用户**，并输入用户的电子邮件地址。
1. 如果您想要授予高级许可权以管理 {{site.data.keyword.Bluemix_notm}} 组织中的用户，请选中**管理员**、**记帐管理员**或**审计员**复选框中的一个或多个。
1. 单击**邀请**。
1. 单击**保存**。

## 删除工具链
{: #deleting_a_toolchain}

您可以删除工具链，并指定您要删除的相关联工具集成。如果删除工具链，那么该删除操作无法撤销。

1. 在 DevOps 仪表板的**工具链**页面上，单击要删除的工具链，然后单击**管理**。或者，在应用程序“概述”页面的“持续交付”磁贴上，单击**查看工具链**，然后单击**管理**。
1. 单击**删除工具链**，并复查或调整要删除的工具集成。
1. 通过输入工具链的名称并单击**删除**，以确认删除。  

 **提示**：当您删除 GitHub 工具集成时，不会从 GitHub 删除相关联的 GitHub 存储库。您必须手动从 GitHub 除去存储库。


# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}

* [Create and use your first toolchain（在新窗口中打开链接）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Create a custom toolchain（在新窗口中打开链接）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Create an application with three microservices（在新窗口中打开链接）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [在 {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) 上从模板创建工具链（在新窗口中打开链接）](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [在 {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) 上从应用程序创建工具链（在新窗口中打开链接）](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## 相关链接
{: #general}

* [Microservices toolchain（在新窗口中打开链接）](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain（在新窗口中打开链接）](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method（在新窗口中打开链接）](https://www.ibm.com/devops/method){:new_window}
