---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 管理翻译
{: #globalizationpipeline_managingtranslations}


在您创建束并开始生成应用程序的翻译之后，可按原样使用机器生成的内容或进一步修改之后使用。您还可以选择使用非缺省的机器翻译。本节描述如何更改执行束翻译的机器翻译引擎、如何执行人类翻译后编辑，以及您可以如何向需要访问翻译的人员分配用户角色和访问限制。
{:shortdesc}

## 机器翻译配置
{: #globalizationpipeline_service_to_service}

{{site.data.keyword.GlobalizationPipeline_full}} 支持集成替代机器翻译服务，以对束执行机器翻译的能力。如果 {{site.data.keyword.GlobalizationPipeline_short}} 使用的缺省引擎不提供您所需的特定语言，或者如果您更愿意使用不同引擎所生成的机器翻译，那么添加替代服务会很有益处。替代服务的使用和收费涵盖在那些服务的条款下。

要添加并配置 {{site.data.keyword.GlobalizationPipeline_short}} 的替代机器翻译服务，请从 {{site.data.keyword.GlobalizationPipeline_short}} 仪表板选择**机器翻译配置**选项卡。

* 要添加 {{site.data.keyword.Bluemix_notm}} 目录中的机器翻译服务（**Watson 语言转换程序**），必须首先将该服务添加到您的 {{site.data.keyword.Bluemix_notm}} 空间。

* 要添加第三方服务，请在**机器翻译配置**选项卡上选择该服务的按钮，然后提供访问该服务所需的用户凭证。

在向 {{site.data.keyword.GlobalizationPipeline_short}} 添加了机器翻译服务之后，请完成其余的步骤，以完成该服务的集成。

1. 单击**启用**，以开启与该服务的集成。

2. 单击**更新语言**，以查看受支持目标语言的更新列表。

3. 从目标语言列表中，选择应该执行翻译的机器翻译引擎。

4. 单击**保存**，以返回到**机器翻译配置**选项卡。

在使用 {{site.data.keyword.GlobalizationPipeline_short}} 配置替代服务之后，将会使用该引擎开始生成分配给该引擎的所有目标语言。 

要停止使用替代机器翻译引擎：

1. 从**机器翻译配置**选项卡中，单击您要停止使用的服务的**禁用**按钮。

在禁用替代机器翻译服务之后，该服务所生成的所有翻译仍会在您的束中。但是，如果目前启用的机器翻译引擎不再支持特定目标语言，那么可能无法进一步更新该目标语言的翻译。

<!-- Review comment: When you disable an engine, do you need to go back and reconfigure the languages?? Does it go back to the default engine? What happens? -->

## 查看和编辑翻译
{: #globalizationpipeline_translations}

{{site.data.keyword.GlobalizationPipeline_short}} 服务提供人类翻译后编辑功能。专业的翻译人员或精通任何目标语言的人都可以对已生成的翻译进行编辑。您可以进行编辑，以改进翻译质量或一致性，或者替换想要的措词。例如，您可能想要改写产品名称的翻译。

要查看和编辑目标语言的翻译：

1. 从**束详细信息**页面中，选择目标语言，或者单击“操作”列中的**查看翻译**图标 ![选择“查看翻译”图标，以查看目标语言的翻译](images/viewProjectDetailIcon.png)。
2. 翻译会以表格形式呈现，其中会显示键、源和翻译信息。
 * **键：**代表资源文件中具有关联值的属性。
 * **源：**代表已上传资源文件中所包含的可翻译的字符串。
 * **翻译：**代表源值的已翻译版本。
3. 在“操作”列中，单击**修改翻译**图标 ![选择“修改翻译”图标，以编辑特定键值对的翻译。](images/editIcon.png)，以编辑机器翻译的值。
4. 编辑翻译并单击**更新**，以将原始翻译值更新为您编辑的值。

![修改翻译对话框窗口提供一种简单的方法可用于编辑翻译。](images/editTranslation.png) 

***提示：***当您使用包含许多可翻译键的大型束时，查找特定值可能非常困难。在目标语言翻译页面上，您可以使用**搜索...** 方框，在所有键、源和翻译中快速进行搜索。

![使用目标语言翻译页面上提供的搜索框，可在目标语言中搜索键、源、翻译或所有这三项。](images/search.png) 


## 添加 API 用户
{: #globalizationpipeline_users}

当您管理翻译时，您可能希望基于其他 API 用户需要执行的任务，来授予他们访问权。例如，您可能想要使得某位翻译人员能够编辑翻译，但无法修改束信息。

| 角色类型 | 查看翻译？ | 编辑翻译？ | 修改束信息？ |
|-----------|--------------------|--------------------|----------------------------|
| 读者 | 是 | 否 | 否 |
| 翻译人员 | 是 | 是 | 否 |
| 管理员 | 是 | 是 | 是 |

如果您创建更多的 API 用户，那么您可以限制他们对一个或多个特定束的访问，或者授予他们对所有可用束的访问权。

要授予 API 用户访问 {{site.data.keyword.GlobalizationPipeline_short}} 服务实例中束的权限：

1. 在 {{site.data.keyword.GlobalizationPipeline_short}} 仪表板上，单击 **API 用户**选项卡。
2. 单击**新建 API 用户**。
3. 输入**显示名称**和**注释**，以描述新 API 用户。
4. 选择新 API 用户的**类型**。
5. 选择授予 API 用户对所有束还是仅所选择束的访问权。
6. 单击**保存**。

![填写表单以创建新的 API 用户。](images/newUser.png)

此时将生成并显示 API 用户标识和密码。复制并保存那些凭证；在您关闭窗口之后，您无法再访问它们。通过 [SDK](https://github.com/IBM-Bluemix/gp-common)，凭证可用于 RESTful 服务。 

要重置 API 用户密码：

1. 在 {{site.data.keyword.GlobalizationPipeline_short}} 仪表板上，单击 **API 用户**选项卡。
2. 单击**重置密码**图标 ![选择此图表以重置 API 用户密码](images/resetPW.png)，以重置特定用户标识的密码。 
3. 单击**是**。 
