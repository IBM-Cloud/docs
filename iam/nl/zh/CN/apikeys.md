---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 管理 API 密钥
{: #manapikey}

应用程序编程接口密钥（API 密钥）是由调用应用程序编程接口 (API) 的计算机程序传入的代码，用于确定调用程序、其开发者或其 Web 站点用户。API 密钥用于跟踪和控制 API 的使用情况，例如阻止恶意使用或滥用 API（可能如服务方面所定义）。API 密钥通常充当进行认证的唯一标识和密码提示令牌，并且一般有一组访问权用于与其关联的 API。API 密钥可以基于通用唯一标识 (UUID) 系统来确保它们对每个用户唯一。

作为 {{site.data.keyword.Bluemix_notm}} 用户，您可能希望在启用程序或脚本时使用 API 密钥，而不将密码分发到脚本。使用 API 密钥的优点是用户或组织可以针对不同的程序创建多个 API 密钥，并且如果 API 密钥泄露，可以将其单独删除，而不影响其他 API 密钥，甚至不会影响到用户。此外，作为[联合用户](/docs/admin/adminpublic.html#federatedid)，您可以使用 API 密钥来登录。有关使用 API 密钥登录的更多信息，请参阅文档中的 [{{site.data.keyword.Bluemix_notm}} CLI `bluemix login` 命令](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login)和 [cf CLI `cf login` 命令](/docs/cli/reference/cfcommands/index.html#cf_login)。

可以在 Bluemix“API 密钥”窗口中管理 {{site.data.keyword.Bluemix_notm}} API 密钥。转至**管理** &gt; **安全性** &gt; **Bluemix API 密钥**可查看 API 密钥及其描述和日期。可以在此页面中创建、编辑或删除 API 密钥。

要创建 API 密钥，请执行以下操作：

1. 转至**管理** &gt; **安全性** &gt; **Bluemix API 密钥**。
2. 单击**创建 API 密钥**。
3. 为 API 密钥输入名称和描述。
4. 单击**创建 API 密钥**。
5. 然后，单击**显示**以显示 API 密钥，以便复制并保存供日后使用，或者单击**下载 API 密钥**。

**注**：API 密钥仅在创建时才可显示或下载。如果 API 密钥丢失，必须创建新的 API 密钥。

要编辑 API 密钥，请执行以下操作：

1. 转至**管理** &gt; **安全性** &gt; **Bluemix API 密钥**。
2. 在表中列出的 API 密钥的**操作**菜单中，单击**编辑名称和描述**。 
3. 更新 API 密钥的信息。
4. 单击**更新 API 密钥**。

要删除 API 密钥，请执行以下操作： 

1. 转至**管理** &gt; **安全性** &gt; **Bluemix API 密钥**。
2. 在表中列出的 API 密钥的**操作**菜单中，单击**删除**。
3. 然后，通过单击**删除密钥**来确认删除操作。

您还可以使用 {{site.data.keyword.Bluemix_notm}} CLI 通过列出密钥、创建密钥、更新密钥或删除密钥来管理 API 密钥。有关更多信息，请参阅 [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam) 命令部分。

