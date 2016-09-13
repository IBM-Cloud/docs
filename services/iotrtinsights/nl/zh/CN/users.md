---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 管理用户{: #manage-users}

{{site.data.keyword.iotrtinsights_short}} 专为团队协作而设计，支持管理员添加更多用户来访问 {{site.data.keyword.iotrtinsights_short}} 控制台。
{: shortdesc}

角色描述：
- 操作员
操作员可直接登录到 {{site.data.keyword.iotrtinsights_short}} 控制台来监视自己的设备和设备组的实时数据流。操作员还可以激活和停用规则，以及修改可编辑的仪表板。  
- 管理员
除了操作员可以执行的任务外，管理员还可以添加用户、管理仪表板布局、添加数据源以及管理设备类型。  
- 所有者
“所有者”角色分配给在 Bluemix 中部署了 {{site.data.keyword.iotrtinsights_short}} 服务实例的 IBM 标识。所有者具有与管理员相同的特权，但不能将所有者删除。

要添加新用户，请执行以下步骤：
1. 将用户添加到 {{site.data.keyword.iot_short}}。  
>**重要信息：**如果要添加具有“管理员”角色的用户，那么还必须将该用户添加到 {{site.data.keyword.iot_short}}。  

  1. 登录到作为 {{site.data.keyword.iotrtinsights_short}} 服务数据源的 {{site.data.keyword.iot_short}} 服务的仪表板。  
  2. 浏览至**访问 > 成员**，然后单击**添加成员**。
  3. 输入要添加的用户的 IBM 标识，然后单击**添加成员**。
2. 将用户添加到 {{site.data.keyword.iotrtinsights_short}}。
  1. 以具有“管理员”角色或“所有者”角色的用户身份登录到 {{site.data.keyword.iotrtinsights_short}} 控制台。
  2. 转至**设置 > 管理用户**。
  3. 单击**添加新用户**。
  4. 输入要邀请的用户的电子邮件地址，为该用户选择角色，然后单击 ![“创建”图标](images/create.png "“创建”图标")。
将向该用户发送包含 Web 控制台链接的电子邮件。如果电子邮件地址已经与 IBM 标识关联，那么该用户可以直接登录并访问控制台。否则，系统会提示用户在访问控制台之前，先创建免费 IBM 标识。  
>**选择 Real-Time Insights 实例：**有权以操作员或管理员身份访问多个 Real-Time Insights 实例的用户可以迅速在这些实例之间进行切换。在 Real-Time Insights 控制台中，这些用户可以单击自己的用户名，然后选择要访问的实例。  
