---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-24"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 管理用户访问权

在“访问权”仪表板中，可以控制和管理对 {{site.data.keyword.iot_full}} 组织的访问权。您可以通过添加、邀请、注册或导入用户来添加用户。还可以通过分配角色来向用户授予不同的访问级别。
{:shortdesc}

- [添加新用户](#adding-new-users)
- [编辑用户](#editing-users)
- [阻止用户访问](#blocking-users)
- [除去用户](#removing-users)

## 添加新用户
{: #adding-new-users}

在仪表板的**访问权**选项卡中，可以使用“添加”、“邀请”或“注册”功能来添加单个成员。还可以使用“导入”功能来同时添加、邀请或注册多个成员。

缺省情况下，成员帐户不会到期。向 {{site.data.keyword.iot_short_notm}} 组织添加用户时，可以选择为其帐户设置到期日期。

### 向 {{site.data.keyword.iot_short_notm}} 组织添加成员

要向组织添加成员，您将需要该成员的 IBM 标识。添加成员时，无需得到该成员的确认。

要向 {{site.data.keyword.iot_short_notm}} 组织添加单个成员，请执行以下操作：
1. 在 {{site.data.keyword.iot_short_notm}} 仪表板中，转至**访问权**。
2. 单击**添加成员**，然后选择**添加**。
3. 输入成员的 IBM 标识。
4. 为成员选择角色。
5. 可选：为成员设置到期日期。
6. 单击**添加成员**。

要同时添加多个成员，必须上传 `.csv` 文件，此文件包含每个成员的 IBM 标识、角色和可选的到期日期。
1. 在 {{site.data.keyword.iot_short_notm}} 仪表板中，转至**访问权**。
2. 单击**添加成员**，然后选择**导入**。
3. 单击**批量添加**。
4. 选择缺省角色，并确保 `.csv` 文件中的列编号与 CSV 设置中的列编号相匹配。
5. 确保 `.csv` 文件中的列分隔符与 CSV 设置中的列分隔符相匹配。
6. 单击**浏览文件**或将 `.csv` 文件拖入**上传 CSV** 窗口中。

### 邀请成员加入 {{site.data.keyword.iot_short_notm}} 组织

邀请用户成为 {{site.data.keyword.iot_short_notm}} 组织的成员时，该用户会收到一封包含邀请链接的电子邮件。邀请链接在发送 48 小时后到期。如果未在 48 小时内使用邀请链接，那么必须重新邀请该用户以使其收到新的邀请链接。

要邀请成员加入 {{site.data.keyword.iot_short_notm}} 组织，请执行以下操作：
1. 在 {{site.data.keyword.iot_short_notm}} 仪表板中，转至**访问权**。
2. 单击**添加成员**，然后选择**邀请**。
3. 输入成员的电子邮件地址。
4. 为此成员选择角色。
5. 可选：为成员设置到期日期。
6. 单击**邀请成员**。

要同时邀请多个成员，必须上传 `.csv` 文件，此文件包含每个成员的电子邮件地址、角色和可选的到期日期。
1. 在 {{site.data.keyword.iot_short_notm}} 仪表板中，转至**访问权**。
2. 单击**添加成员**，然后选择**导入**。
3. 单击**批量邀请**。
4. 选择缺省角色，并确保 `.csv` 文件中的列编号与 CSV 设置中的列编号相匹配。
5. 确保 `.csv` 文件中的列分隔符与 CSV 设置中的列分隔符相匹配。
6. 单击**浏览文件**或将 `.csv` 文件拖入**上传 CSV** 窗口中。

### 向 {{site.data.keyword.iot_short_notm}} 组织注册成员

如果组织未使用 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}，那么可以通过注册成员来向组织添加单个成员，此操作无需 IBM 标识。

要向 {{site.data.keyword.iot_short_notm}} 组织注册成员，请执行以下操作：
1. 在 {{site.data.keyword.iot_short_notm}} 仪表板中，转至**访问权**。
2. 单击**添加成员**，然后选择**邀请**。
3. 输入成员的电子邮件地址。
4. 为此成员选择角色。
5. 输入主题、域名和签发者。
   **重要信息：**确保`主题`、`域名`和`签发者`字段符合 OpenID Connect 的建议和标准。有关更多信息，请参阅 [OpenID Connect](http://openid.net/connect/) Web 站点。
6. 可选：为成员设置到期日期。
7. 单击**注册成员**。

要同时注册多个成员，必须上传 CSV (`.csv`) 文件，此文件包含每个成员的电子邮件地址、角色、主题、域名、签发者和可选的到期日期。
1. 在 {{site.data.keyword.iot_short_notm}} 仪表板中，转至**访问权**。
2. 单击**添加成员**，然后选择**导入**。
3. 单击**批量注册**。
4. 选择缺省角色，并确保 CSV 文件中的列编号与 CSV 设置中的列编号相匹配。
5. 确保 CSV 文件中的列分隔符与 CSV 设置中的列分隔符相匹配。
6. 单击**浏览文件**或将 CSV 文件拖入**上传 CSV** 窗口中。

### 构造 CSV 文件

构造用于将成员导入组织中的 CSV 文件时，确保包含所用方法的必需信息。请使用逗号或分号来分隔列。上传 CSV 文件时，确保在 **CSV 设置**下选择正确的列分隔符。

## 编辑用户
{: #editing-users}

可以对用户进行编辑，以更改其角色，添加、除去或更改访问权到期日期，或者添加或除去对组织的访问权。

1. 在 {{site.data.keyword.iot_short_notm}} 仪表板左侧的导航栏中，单击**成员**。
2. 单击要编辑的用户旁的**编辑**图标 ![编辑](/docs/images/edit_32.svg)。
3. 对用户进行所需的更改。
4. 单击**保存**。

## 阻止用户访问
{: #blocking-users}

可以阻止用户访问 {{site.data.keyword.iot_short_notm}} 组织，同时仍保留其组织成员资格。

1. 在 {{site.data.keyword.iot_short_notm}} 仪表板左侧的导航栏中，单击**成员**。
2. 单击要阻止其访问 {{site.data.keyword.iot_short_notm}} 组织的用户旁的切换开关。


## 除去用户
{: #removing-users}

可以从 {{site.data.keyword.iot_short_notm}} 组织中完全除去用户。除去用户的操作不可撤销，要恢复已除去用户的访问权，必须将相应用户[添加到平台](#adding-new-users)。

1. 在 {{site.data.keyword.iot_short_notm}} 仪表板左侧的导航栏中，单击**成员**。
2. 单击要除去的用户旁的**删除**图标 ![删除](/docs/images/trash_32.svg)。
3. 单击确认对话框中的**删除**。
