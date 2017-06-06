---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.bpfull_notm}} (Beta) 入门
{: #gettingstarted}

{{site.data.keyword.bplong}} 是一种自动化工具，可用于定义云基础架构并将其作为单个单元进行部署，然后在任意数量的环境中复用这些云资源定义。
{:shortdesc}

{{site.data.keyword.bpshort}} 使用 HashiCorp 公司的 Terraform 来对基础架构编码。基础架构的组件可分解成从物理硬件到用户帐户等各种不同的资源。通过提取高级别和低级别资源，可以像处理软件一样，将基础架构作为代码进行处理。 

使用 {{site.data.keyword.bpshort}} 时，可采用声明式语法为环境编写配置。您可声明所需的环境外观，例如在生产中具有 10 个{{site.data.keyword.virtualmachinesshort}}。此服务会将您的配置与 Terraform 先前创建的内容进行比较，然后根据需要添加或除去资源。

{{site.data.keyword.bpshort}} 是一种协作式 DevOps 工具，为基础架构提供了单一的真实源。可以将环境配置存储在源代码控制中，这将让团队有能力执行代码复审，控制基础架构的版本，通过落实历史记录来跟踪更改，以及更轻松地还原更改。

{{site.data.keyword.bpshort}} 自动可用于 {{site.data.keyword.Bluemix_notm}} 帐户中的所有用户。


## 创建配置
{: #configuration}

创建配置时，要对构成环境的云资源进行编码。
{:shortdesc}


如果要试用 {{site.data.keyword.bpshort}} 的样本配置，请完成以下步骤。在样本中，可以供应 SSH 密钥以在 {{site.data.keyword.BluSoftlayer}} 中使用。 

**注**：样本配置需要 {{site.data.keyword.BluSoftlayer}} 帐户。请参阅[链接 {{site.data.keyword.Bluemix_notm}} 和 SoftLayer 帐户文档](../../pricing/linking_accounts.html#unifyingaccounts)（如果您有现有帐户），或者可以[注册帐户](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)。

1. 在本地生成 SSH 密钥对。
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. 在 <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 中派生样本配置。 

  以下示例显示了样本配置中不同类型的块。可以在 GitHub 存储库的 `main.tf` 文件中查看完整配置。
  
  * provider 块用于设置 {{site.data.keyword.IBM_notm}} Cloud 提供者和登录凭证。

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * resource 块用于定义基础架构的组件，在此样本中为 SSH 密钥。
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * variable 块用于定义变量，针对此样本，您可以在 {{site.data.keyword.bpshort}} GUI 中输入变量。
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * output 块用于定义在使用配置来创建环境以及创建资源（SSH 密钥）后，Terraform 输出中显示的内容。
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
现在，可以通过您的配置来创建环境。 

{:codeblock}

## 创建环境
{: #environment}

创建环境时，请将此服务指向配置，以便服务可以提取最新的代码更改。
{:shortdesc}

使用样本配置，完成以下步骤来创建环境。

1. 在菜单中，选择**服务**，然后选择 **{{site.data.keyword.bpshort}}**。这将转至 {{site.data.keyword.bpshort}} 仪表板。

2. 在左侧导航菜单中，选择**环境**，然后单击**创建环境**来描述有关配置的属性。创建环境将定义 {{site.data.keyword.bpshort}} 如何供应和更新云资源，但此时还不会创建资源。

3. 输入有关环境的详细信息。样本配置需要下表中列出的值。

  <table summary="为了能将样本配置用作环境的源而必需的值。">
  <caption>表 1. 为了能将样本配置用作环境的源而必需的值。</caption>
  <thead>
  <th colspan="1">设置</th>
  <th colspan="1">描述</th>
  </thead>
  <tbody>
  <tr>
  <td>源代码控制 URL</td>
  <td>输入在其中派生了样本配置的 GitHub URL。</td>
  </tr>
  <tr>
  <td>名称</td>
  <td>输入要为环境指定的唯一名称。</td>
  </tr>
  <td>Terraform 版本</td>
  <td>输入 Terraform 的版本，以确保对环境运行的是兼容版本的 Terraform。对于样本配置，请使用版本 <code>0.9.1</code>。</td>
  </tr>
  <tr>
  <td>变量</td>
  <td>可以在服务中定义变量，或覆盖 <code>.tf</code> 文件中的环境变量。您可以通过单击“锁定”图标来掩盖敏感变量。掩盖变量可阻止其他用户在“环境详细信息”页面上看到隐藏值。<p>
  <p>添加以下变量和值以使用样本配置：<ul>
  <li><code>ibmid</code> - 输入您的完整 {{site.data.keyword.ibmid}}作为值。</li>
  <li><code>ibmidpw</code> - 输入与您的 {{site.data.keyword.ibmid}}关联的密码，然后单击“锁定”图标以掩盖此值。</li>
  <li><code>slaccountnum</code> - 输入您的 {{site.data.keyword.BluSoftlayer}} 帐号。
   <li><code>datacenter</code> - 输入要将 SSH 密钥资源部署到的数据中心。有关可用值的完整列表，请参阅<a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">自述文件 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。</li> 
   <li><code>public_key</code> - 输入公共 SSH 密钥。要将公用密钥复制到剪贴板，可以运行 <code>pbcopy < ~/.ssh/id_rsa.pub</code> 命令。
   <li><code>key_label</code> - 使用唯一名称标识密钥。
   <li><code>key_note</code> - 可选：添加关于 SSH 密钥的描述性文本。</ul></td>
   </tr></tbody></table>

4. 填写环境详细信息完成后，单击**创建**。这将显示新创建的环境。 
5. 要查看在部署环境时会供应或除去的资源的预览，请单击**计划**。 
6. 查看计划日志以检查输出中是否有任何错误。 
7. 准备好部署环境时，单击**应用**。可以监视应用日志以查看密钥是否已成功部署。如果成功部署，会在输出末尾附近显示以下行：

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  您还可以在 [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys) 中查看 SSH 密钥。
8. 可选：要从 {{site.data.keyword.Bluemix_notm}} 中除去 SSH 密钥并除去环境，请从“操作”菜单中选择**销毁资源**。

### 后续工作
{: #next}

* 要了解有关以编程方式部署环境的更多信息，请[检查 CLI 或 API](schematics_deploying.html)。
* 要从头开始创建自己的配置，请检查 <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud 资源 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。{{site.data.keyword.IBM_notm}} Cloud 资源作为 Terraform 插件提供程序提供。
