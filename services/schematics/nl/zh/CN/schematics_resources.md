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

# Terraform 插件提供程序的资源
{: #terraform-resources}

{{site.data.keyword.IBM}} Cloud 资源作为 Terraform 插件提供程序提供。您可以组合使用不同的资源来创建自己的配置，然后可以将这些配置部署到环境。
{: shortdesc}

有关用法示例、必需自变量和导出的属性，可以查看 GitHub 中的<a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">数据源文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 和<a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">资源文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。配置可以使用 JSON 或 <a href="https://www.terraform.io/docs/configuration/index.html">HashiCorp 配置语言 (HCL) <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 进行编写。

## 本地开发
{: #developing}

如果要在系统本地进行开发，请完成以下步骤：

1. <a href="https://www.terraform.io/intro/getting-started/install.html">下载并安装适合您系统的 Terraform。<img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">下载 {{site.data.keyword.IBM_notm}} Cloud 提供者的 Terraform 二进制文件。<img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>

3. 创建指向 Terraform 二进制文件的 `.terraformrc` 文件。 

  在以下示例中，`/opt/provider/terraform-provider-ibmcloud` 是该目录的路径。

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. 配置插件提供程序和您的 {{site.data.keyword.IBM_notm}} 凭证以使用 Terraform。 

  要将凭证作为环境变量提供，可以在 `.tf` 文件中使用以下代码。
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  然后，可以在终端中导出凭证。
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## 数据源
{: #data}

提供了以下数据源，可用于抽取有关资源的只读信息。 

<table summary="Bluemix 数据源">
<caption>表 1. 可用的平台数据源。
</caption>
 <thead>
 <th colspan="5">Bluemix 数据源</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Bluemix 帐户 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Bluemix 组织 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Bluemix 空间 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Cloud Foundry 服务实例 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Cloud Foundry 服务密钥 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Cloud Foundry 服务套餐 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Kubernetes 集群 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Kubernetes 集群配置 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Kubernetes 工作程序节点 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Bluemix Infrastructure (SoftLayer) 数据源">
<caption>表 2. 可用的 Infrastructure 数据源。
</caption>
<thead>
<th colspan="4">Bluemix Infrastructure (SoftLayer) 数据源</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">DNS 域 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">映像模板 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">SSH 密钥 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
 <t/r>
</tbody></table>


## 资源
{: #resources}

提供了以下资源，可用于定义基础架构的组件。 

 <table summary="Bluemix 资源">
 <caption>表 3. 可用的平台资源。
 </caption>
  <thead>
  <th colspan="5">Bluemix 资源</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Cloud Foundry 服务实例 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Cloud Foundry 服务密钥 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Kubernetes 集群 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Kubernetes 服务绑定 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">用户 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  </tr>
</tbody></table>

<table summary="Bluemix Infrastructure (SoftLayer) 资源">
<caption>表 4. 可用的 Infrastructure 资源。
</caption>
 <thead>
 <th colspan="5">Bluemix Infrastructure (SoftLayer) 资源</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">裸机服务器 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">基本监视 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">块存储器 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">DNS 域 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">DNS 域记录 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">文件存储器 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">专用硬件防火墙 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">专用硬件防火墙规则 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">全局 IP <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">本地负载均衡器 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">负载均衡器本地服务 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">负载均衡器本地服务组 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">负载均衡器 VPX <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">负载均衡器 VPX HA <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">负载均衡器 VPX 服务 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">负载均衡器 VPX 虚拟 IP <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">对象存储器帐户 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">供应 Hook <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">扩展组 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">扩展策略 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">安全证书 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">SSH 密钥 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">用户 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">虚拟访客 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a></td>
  <tr>
</tbody></table>
