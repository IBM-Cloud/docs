---

copyright:
  years: 2015, 2016

---

<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 扩展 {{site.data.keyword.deliverypipeline}} 服务
{: #deliverypipeline_extending}
上次更新时间：2016 年 8 月 29 日
{: .last-updated}

通过配置作业使用受支持的服务，您可以扩展 {{site.data.keyword.deliverypipeline}} 服务的功能。例如，测试作业可以运行静态代码扫描，而构建作业可以全球化字符串。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

以下任务描述如何将所选工具与 Delivery Pipeline 相集成。

## 使用管道运行静态代码扫描

{: #deliverypipeline_scan}

想要在部署代码之前，查找代码中的安全问题？当您使用 IBM® Static Analyzer for Bluemix™ 作为管道的一部分时，您可以针对 Java™ 应用程序的静态 `.war`、`.ear`、`.jar` 或 `.class` 构建二进制文件，来运行自动检查。

使用 Static Analyzer 服务的管道通常包括以下阶段：

+ 构建阶段，用于构建源文件
+ 处理阶段，包括以下作业：
  + 用于运行 Static Analyzer 服务的构建作业
  + 用于运行容器构建的构建作业
+ 部署阶段，用于部署容器


### 创建静态代码扫描

开始之前，请[查看服务的使用条款](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01)。

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. 创建处理阶段。

  a. 单击**添加阶段**。

  b. 对阶段进行命名，例如 `Processing`。

  c. 对于输入类型，选择**构建工件**。

  d. 对于阶段和作业，验证并更新值（如果需要的话）。

2. 在处理阶段中，添加构建作业以运行代码扫描。

  a. 在**作业**选项卡上，单击**添加作业**。

  b. 对于作业类型，选择**测试**。

  c. 对于测试程序类型，选择 **IBM Security Static Analyzer**。

  d. 对于组织和空间，验证并更新值（如果需要的话）。

  e. 根据需要，选中或清除**为我设置服务和空间**复选框。

    * 如果您想要管道针对服务和将服务绑定到容器的应用程序，检查 Bluemix 空间，请选中此复选框。如果服务或绑定的应用程序不存在，那么管道会将服务的免费套餐添加到空间。所创建的绑定应用程序名为 `pipeline_bridge_app`。之后，管道会使用 pipeline_bridge_app 中的凭证访问绑定的服务。

    * 如果您已在 Bluemix 空间中配置服务和绑定的应用程序，或者如果您想要[手动配置这些需求](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline)，请使该复选框保留清除状态。

  f. 在**等待分析完成的时间（分钟）**字段中，键入值 0 - 59 分钟。缺省值为 5 分钟。
Static Analyzer 仪表板的 URL 位于作业结尾的控制台日志中。

     如果在您所指定的时间之前 Static Analyzer 扫描未完成，那么作业会失败。但是，扫描分析会继续运行，而您可以在 Static Analyzer 仪表板上对其进行查看。在 Static Analyzer 扫描完成之后，如果您重新运行该作业，那么不会重新提交扫描请求，而管道作业可以完成。或者，您可以配置在产生成功扫描结果时，不会封锁管道。有关指示信息，请参阅下一步。

  g. 根据此作业失败或超时时您希望执行的操作，选中或清除**此作业失败时停止运行此阶段**复选框。当漏洞高时，作业可能会失败。

    * 如果您选中该复选框而作业失败，那么该阶段中的后续作业和后续阶段不会运行。

    * 如果您清除该复选框而作业失败，那么该阶段会继续而不会阻止后续作业和阶段。例如，如果您了解报告包含许多问题要处理，那么您可能会配置阶段继续运行，因为扫描可能会花费很长时间。在此情况下，您可能并不希望仅仅因为执行扫描需要很长时间而停止剩余作业和阶段。

  h. 单击**保存**。

3. 作业完成时，单击**查看日志和历史记录**，以查看结果。如果分析成功或超时，那么会在扫描结果中显示 URL。如果扫描状态为暂挂，请等待直到扫描完成，以查看完整结果。

4. 如果在分析完成之前，您需要重新运行处理阶段，那么您可以这样做。但是，在以下情况下，不会重新提交新分析而会使用之前的结果：
  * 当您启动新分析时，处理阶段仍在运行。
  * 已经提交构建的扫描
  * 新源构建尚未运行

5. 要启动新分析，请完成以下其中一个步骤：
  * 运行输入到处理阶段的构建阶段，然后重新运行处理阶段。
  * 打开扫描结果的 URL 并单击**废纸篓**图标。然后，重新运行处理阶段。

控制台输出示例：

**成功扫描**
![成功扫描示例](images/analyzer_success.png)

**暂挂扫描**
![暂挂扫描示例](images/analyzer_pending.png)

有关使用 Static Analyzer 服务的更多信息，请参阅 [Static Analyzer 服务文档](https://console.ng.bluemix.net/docs/services/ApplicationSecurityonCloud/index.html)。

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## 针对管道中的构建创建 Slack 通知
{: #deliverypipeline_slack}

您可以将有关 IBM Container Service、IBM Security Static Analyzer 和 IBM Globalization 构建结果的通知，从 Delivery Pipeline 发送到 Slack 通道。

开始之前，先创建或复制 Slack WebHook URL：

1. 打开适合于您团队的“Slack 集成”页面：`https://_project_name_.slack.com/services`
2. 在集成的列表中，找到**入局 WebHook**，并单击**添加**。
3. 选择通道，然后单击**添加入局 WebHook 集成**。
4. 添加 **WebHook URL** 或复制现有 URL。

有关更多信息，请参阅 [Slack 文档中的入局 WebHook](https://api.slack.com/incoming-webhooks)。

要创建 Slack 通知，请执行以下操作：

1. 在管道中，打开阶段的配置。
2. 在**环境属性**选项卡中，单击**添加属性**。
3. 选择**文本属性**。
4. 输入环境属性的名称和值。重复上述步骤以创建多个环境属性。

  *表 1. 用于配置 Slack 通知的环境属性*

  <table>
  <tr>
  <th>名称</th>
  <th>值</th>
  <th>描述</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>URL</td>
    <td>必要。保存在 Slack 项目设置中的 WebHook URL。</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>可以输入下列其中一个值：<ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>任何十六进制颜色，如 #439FEO</li></ul></td>
    <td>可选。Slack 中沿消息边显示的边框的颜色。缺省颜色如下：成功消息为绿色，失败消息为红色，参考消息为灰色。</td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>要只接收部分消息类型，请输入以下某个值：<ul>
      <li><code>good</code>：仅获取 unknown、good 和 info 消息。不发送失败消息。</li>
      <li><code>bad</code>：获取所有消息。</li>
      <li><code>info</code>：仅获取 info 消息。不发送 Good、bad 和 unknown 消息。</li>
      <li><code>unknown</code>：获取所有消息。</li></ul>
示例：如果您设置 <code>NOTIFY_FILTER = bad</code>，那么仅会在 Slack 通道中显示错误通知。</td>
    <td>可选。决定要发送通知的消息类型。缺省情况下，会发送成功和失败消息，但不会发送参考消息。<ul><li><code>good</code>：成功的构建结果。</li>
      <li><code>bad</code>：失败的构建结果。</li>
      <li><code>info</code>：构建过程的参考消息。</li>
      <li><code>unknown</code>：未分配类型的未知消息。</li></ul></td>
   </table>

5. 单击**保存**。

6. 重复上述步骤，以针对包含 IBM Container Service、IBM Security Analyzer 和 IBM Globalization 作业的其他阶段，发送 Slack 消息。

在 Slack 中显示的构建通知包括指向 DevOps Services 项目的链接，有时是指向项目仪表板的链接。Slack 用户要想打开这些链接，该用户必须已在 DevOps Services服务中注册，成为管道配置所在的项目的成员。

## 针对管道中的构建创建 HipChat 通知
{: #deliverypipeline_hipchat}

您可以将有关 IBM Container Service、IBM Security Static Analyzer 和 IBM Globalization 构建结果的通知，从 Delivery Pipeline 发送到 HipChat 聊天室。

开始之前，先创建或复制现有的 HipChat 令牌：

1. 转至适合于您团队的“HipChat 页面”页面：`https://_project_name_.hipchat.com/account/api`
2. 创建新令牌或使用现有令牌。

要创建 HipChat 通知，请执行以下操作：

1. 在管道中，打开阶段的配置。
2. 在**环境属性**选项卡中，单击**添加属性**。
3. 选择**文本属性**。
4. 输入环境属性的名称和值。重复上述步骤以创建多个环境属性。

  *表 2. 用于配置 HipChat 通知的环境属性*

  <table>
  <tr>
  <th>名称</th>
  <th>值</th>
  <th>描述</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>字母数字字符串</td>
    <td>必要。请参阅“开始之前”，以获取创建或复制现有 HipChat 令牌的指示信息。</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>聊天室名称</td>
    <td>必要。</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>输入以下某个值：<ul><li><code>yellow</code></li>
      <li><code>red</code></li>
      <li><code>green</code></li>
      <li><code>purple</code></li>
      <li><code>gray</code></li>
      <li><code>random</code></li></ul>
    </td>
    <td>可选：指定 HipChat 通知的背景色和边框颜色。如果您设置 <code>HIP_CHAT_COLOR</code>，那么在您调用脚本时无需指定颜色。
<p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>输入以下某个值：<ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
此变量适用于 HipChat 和 Clack 通知颜色。如果指定
<code>NOTIFICATION_COLOR</code>，那么不需要指定 <code>HIP_CHAT_COLOR</code> 或
<code>SLACK_COLOR</code>。</td>
    <td>可选：指定 HipChat 和 Slack 通知的背景色和边框颜色。如果您设置 <code>NOTIFICATION_COLOR</code>，那么在您调用脚本时无需指定颜色。
<p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>输入以下某个值：<ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>可选：指定通知级别。请参阅 <code>NOTIFICATION_FILTER</code>，以获取有关会触发通知的内容的更多详细信息。</td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>输入以下某个值：<ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>可选：指定通知过滤级别。满足以下参数时将发送通知：<ul><li><code>NOTIFICATION_FILTER = good</code> 和 <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code> 或 <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = info</code> 和 <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code>、<code>info</code> 或 <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = bad</code> 和 <code>NOTIFICATION_LEVEL = bad</code> 或 <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = unknown</code> 和 <code>NOTIFICATION_LEVEL = bad</code>、<code>good</code> 或 <code>unknown</code></li></ul></td>
    </tr>
  </table>

5. 单击**保存**。

6. 重复上述步骤，以针对包含 IBM Container Service、IBM Security Static Analyzer 和 IBM Globalization 作业的其他阶段，发送 HipChat 消息。

## 使用 Active Deploy 在管道中实现零停机时间部署
{: #deliverypipeline_activedeploy}

您可以使用 Bluemix® DevOps Services Delivery Pipeline 中的 IBM® Active Deploy 服务，自动化应用程序或容器组的连续部署。有关入门的更多信息，请参阅 [Active Deploy 文档](https://new-console.ng.bluemix.net/docs/services/ActiveDeploy/updatingapps.html#adpipeline)。

## 使用管道构建和部署容器映像
{: #deliverypipeline_containers}

您可以使用 IBM® Continuous Delivery Pipeline for Bluemix，自动化 Bluemix® 的应用程序构建和容器部署。DevOps Services 中的 Delivery Pipeline 服务支持：
  - 构建 Docker 映像
  - 将容器中的映像部署至 Bluemix

有关入门的更多信息，请参阅 [Delivery Pipeline 和容器概述](https://new-console.ng.bluemix.net/docs/containers/container_pipeline_ov.html#container_pipeline_ov)。
