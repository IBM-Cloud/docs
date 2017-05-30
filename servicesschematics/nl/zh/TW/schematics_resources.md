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

# Terraform 外掛程式提供者的資源
{: #terraform-resources}

{{site.data.keyword.IBM}} Cloud 資源提供為 Terraform 外掛程式提供者。您可以結合不同的資源來建立自己的配置，再部署至環境。
{: shortdesc}

您可以檢視 GitHub 中<a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">資料來源文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 及<a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">資源文件 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 裡的使用範例、必要的引數及匯出的屬性。配置可以用 JSON 或 <a href="https://www.terraform.io/docs/configuration/index.html">HashiCorp 配置語言 (HCL) <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 撰寫。

## 本端開發
{: #developing}

如果您想要在本端系統開發，請完成下列步驟：

1. <a href="https://www.terraform.io/intro/getting-started/install.html">為您的系統下載及安裝 Terraform。<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">下載適用於 {{site.data.keyword.IBM_notm}} Cloud 提供者的 Terraform 二進位檔。<img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>

3. 建立 `.terraformrc` 檔案，此檔案指向 Terraform 二進位檔。 

  在下列範例中，`/opt/provider/terraform-provider-ibmcloud` 是目錄的路徑。

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. 配置外掛程式提供者和您的 {{site.data.keyword.IBM_notm}} 認證，以便使用 Terraform。 

  若要以環境變數的形式提供認證，您可以在 `.tf` 檔案中使用下列程式碼。
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  然後，您可以在終端機匯出認證。
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## 資料來源
{: #data}

下列是可用的資料來源，可用來擷取關於資源的唯讀資訊。 

<table summary="Bluemix 資料來源">
<caption>表 1. 可用的平台資料來源。
</caption>
 <thead>
 <th colspan="5">Bluemix 資料來源</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Bluemix 帳戶 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Bluemix 組織 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Bluemix 空間 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Cloud Foundry 服務實例 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Cloud Foundry 服務金鑰 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Cloud Foundry 服務方案 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Kubernetes 叢集 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Kubernetes 叢集配置 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Kubernetes 工作者節點 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Bluemix 基礎架構 (SoftLayer) 資料來源">
<caption>表 2. 可用的基礎架構資料來源。
</caption>
<thead>
<th colspan="4">Bluemix 基礎架構 (SoftLayer) 資料來源</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">DNS 網域 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">映像檔範本 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">SSH 金鑰 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
 <t/r>
</tbody></table>


## 資源
{: #resources}

下列是可用的資源，可用來定義基礎架構的元件。 

 <table summary="Bluemix 資源">
 <caption>表 3. 可用的平台資源。
 </caption>
  <thead>
  <th colspan="5">Bluemix 資源</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Cloud Foundry 服務實例 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Cloud Foundry 服務金鑰 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Kubernetes 叢集 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Kubernetes 服務連結 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">使用者 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  </tr>
</tbody></table>

<table summary="Bluemix 基礎架構 (SoftLayer) 資源">
<caption>表 4. 可用的基礎架構資源。
 </caption>
 <thead>
 <th colspan="5">Bluemix 基礎架構 (SoftLayer) 資源</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">裸機伺服器 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">基本監視器 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">Block Storage <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">DNS 網域 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">DNS 網域記錄 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">File Storage <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">專用硬體防火牆 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">專用硬體防火牆規則 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">廣域 IP <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">本端負載平衡器 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">本端負載平衡器服務 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">本端負載平衡器服務群組 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">負載平衡器 VPX <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">負載平衡器 VPX HA <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">負載平衡器 VPX 服務 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">負載平衡器 VPX 虛擬 IP <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">Object Storage 帳戶 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">佈建 hook <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">擴充群組 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">擴充原則 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">安全憑證 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">SSH 金鑰 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">使用者 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">虛擬客體 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a></td>
  <tr>
</tbody></table>
