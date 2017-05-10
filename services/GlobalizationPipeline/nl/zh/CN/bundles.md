---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 使用束
{: #globalizationpipeline_workingwithbundles}


您所创建的每个束都包含资源文件的键值对，以及生成的完整翻译集。
{:shortdesc}

您所上传的资源文件可以是以下格式中的任何一种，且必须以代表应用程序中 UI 字符串的键值对形式包含内容。


* 文件类型：*Java™ 属性文件 (.properties)*<br>
示例：
```js
logout=Logout 
back=Back 
examples=Menu 
home=Home 
web=Web 
enterprise=Enterprise 
extra=Resources 
about=About 
settings=Settings 
help=Help 
support=Support 
topics=Topics 
appExitMsg=Are you sure you want to quit the application?
```
* 文件类型：*AMD I18N (.js)*<br>
示例：
```js
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
``` 
* 文件类型：*JSON (.json)*<br>
示例：
```js
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
``` 

此外，资源文件还必须遵循以下准则：
* 每个键最多可为 255 个字符。
* 每个值最多可为 8191 个字符。
* 每个束最多可包含 500 个键值对。


## 翻译束
{: #globalizationpipeline_translatingabundle}

仅会翻译已上传的资源文件。当[创建束](index.html#globalizationpipeline_creatingbundles)或[修改束详细信息](bundles.html#globalizationpipeline_modifyingbundles)时，您可以上传资源文件。

上传资源文件后，您可以将其内容翻译为缺省机器翻译引擎所提供的任何语言。或者，您可以选择替代的机器翻译引擎，如[机器翻译配置](managing_translations.html#globalizationpipeline_service_to_service)一节中所述。缺省引擎支持以下目标语言

<table>
<thead>
<tr>
<th>目标语言</th>
</tr>
</thead>
<tbody>
<tr>
<td>中文（简体）</td>
</tr>
<tr>
<td>中文（繁体）</td>
</tr>
<tr>
<td>法语</td>
</tr>
<tr>
<td>德语</td>
</tr>
<tr>
<td>意大利语</td>
</tr>
<tr>
<td>日语</td>
</tr>
<tr>
<td>韩语</td>
</tr>
<tr>
<td>葡萄牙语（巴西）</td>
</tr>
<tr>
<td>西班牙语</td>
</tr>
</tbody>
</table>

**注：**{{site.data.keyword.GlobalizationPipeline_short}} 的缺省机器翻译引擎仅提供对将英语作为源语言的支持。但可在 {{site.data.keyword.GlobalizationPipeline_short}} 中配置替代的机器翻译引擎来支持其他非英语源语言/语言对。

当您创建束时，它们会添加到**束**选项卡中，以便您可以轻松地对它们进行访问。从那里，可以对翻译执行其他任务。


## 选择要使用的束
{: #globalizationpipeline_selectingabundle}

1. 单击**束**选项卡，以查看已创建的所有束。
2. 单击列表中的**束标识**，以查看该束的更多详细信息，或者在“操作”列中单击**查看束详细信息**图标 ![选择“查看束详细信息”图标，以打开束并使用其翻译](images/viewProjectDetailIcon.png)。

![从“束”选项卡查看所有可用的束。](images/translationBundles.png)

在您选择要使用的束之后，您可以查看其翻译的状态、添加或移除语言、编辑翻译或提供资源文件的更新。

如果您不再需要某个束，那么您可以将其从**束**选项卡中删除。同时也会删除与该束相关联的所有翻译。

## 修改束详细信息
{: #globalizationpipeline_modifyingbundles}

打开束时，可以查看有关该束的所有详细信息。该束中的所有目标语言都会列出，同时还包括每一种语言的当前翻译状态。

![束详细信息页面显示束及其翻译的相关信息。](images/bundleDetails.png)

束中每一种语言的状态可以是“进行中”、“已失败”或“已翻译”：

| 状态 | 描述 |
|--------|-------------|
| 进行中 | 机器翻译仍在进行中。 |
| 已失败 | 在将资源文件翻译为目标语言时发生错误。 |
| 已翻译 | 到目标语言的翻译已完成。 |

您可以更新束所使用的资源文件、向束中添加目标语言、从束中删除目标语言，以及下载已生成的目标语言翻译。

### 更新束所使用的资源文件

1. 在源语言的旁边，单击“操作”列中的**上传资源**图标 ![选择此图标以上传新资源文件](images/uploadIcon.png)。
2. 单击**浏览**并选择要上传的新资源文件。
3. 选择要上传的资源文件类型
 * Java 属性文件
 * AMD I18N
 * JSON
4. 单击**更新**，以上传新资源文件。

新的或更新的资源文件中的键值对会与已上传的值同步。只会翻译新的或更改的内容。

### 向束中添加目标语言

1. 单击**添加语言**按钮。
2. 此时将显示所有可用的目标语言。选择要添加到束的语言。

此时将立即开始所选择语言的翻译。

### 从束中删除目标语言

当您从束中删除目标语言时，您会从项目移除目标语言及所有相关联的翻译。在要移除的目标语言的“操作”列中，单击**移除此目标语言**图示 ![选择“移除此目标语言”废纸箱图标](images/trashIcon.png)。

### 下载生成的目标语言翻译

{{site.data.keyword.GlobalizationPipeline_short}} 提供多种方法，可将目标语言的翻译引入到您的应用程序中。您可以将翻译下载为资源文件，并在您的应用程序构建中包含该资源文件。您还可以通过 {{site.data.keyword.GlobalizationPipeline_short}}，使用其中一个开放式源代码 [SDK](https://github.com/IBM-Bluemix/gp-common)，动态地参考翻译。 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

要将翻译下载为资源文件： 

1. 在要下载的目标或源语言的**操作**列中，单击**下载翻译**图标 ![选择下载图标以下载目标语言的源键或翻译](images/downloadIcon.png)。
2. 选择文件格式。
3. 单击**下载**。
