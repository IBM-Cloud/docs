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

# Resources for the Terraform plug-in provider
{: #terraform-resources}

{{site.data.keyword.IBM}} Cloud resources are available as a Terraform plug-in provider. You can combine different resources to create your own configurations that can then be deployed to your environments.
{: shortdesc}

You can view the <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">data source docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> and <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">resource docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> in GitHub for usage examples, required arguments, and exported attributes. Configurations can be written in JSON or <a href="https://www.terraform.io/docs/configuration/index.html">HashiCorp Configuration Language (HCL) <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Developing locally
{: #developing}

If you want to develop locally on your system, complete the following steps:

1. <a href="https://www.terraform.io/intro/getting-started/install.html">Download and install Terraform for your system. <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">Download the Terraform binary for the {{site.data.keyword.IBM_notm}} Cloud provider. <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>

3. Create a `.terraformrc` file that points to the Terraform binary. 

  In the following example, `/opt/provider/terraform-provider-ibmcloud` is the route to the directory.

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. Configure the plug-in provider and your {{site.data.keyword.IBM_notm}} credentials to work with Terraform. 

  To provide your credentials as environment variables, you can use the following code in your `.tf` file.
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  You can then export your credentials in your terminal.
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## Data sources
{: #data}

The following data sources are available and can be used to extract read-only information about your resource. 

<table summary="Bluemix data sources">
<caption>Table 1. Available platform data sources.
</caption>
 <thead>
 <th colspan="5">Bluemix data sources</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Bluemix account <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Bluemix org <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Bluemix space <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Cloud Foundry service instance <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Cloud Foundry service key <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Cloud Foundry service plan <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Kubernetes cluster <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Kubernetes cluster configuration <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Kubernetes worker node <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Bluemix Infrastructure (SoftLayer) data sources">
<caption>Table 2. Available infrastructure data sources.
</caption>
<thead>
<th colspan="4">Bluemix Infrastructure (SoftLayer) data sources</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">DNS domain <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">Image template <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">SSH key <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
 <t/r>
</tbody></table>


## Resources
{: #resources}

The following resources are available and can be used to define components of your infrastructure. 

 <table summary="Bluemix resources">
 <caption>Table 3. Available platform resources.
 </caption>
  <thead>
  <th colspan="5">Bluemix resources</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Cloud Foundry service instance <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Cloud Foundry service key <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Kubernetes cluster <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Kubernetes service binding <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">User <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  </tr>
</tbody></table>

<table summary="Bluemix Infrastructure (SoftLayer) resources">
<caption>Table 4. Available infrastructure resources.
</caption>
 <thead>
 <th colspan="5">Bluemix Infrastructure (SoftLayer) resources</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">Bare metal server <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">Basic monitor <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">Block storage <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">DNS domain <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">DNS domain record <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">File storage <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">Hardware firewall dedicated <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">Hardware firewall dedicated rules <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">Global IP <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">Load balancer local <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">Load balancer local service <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">Load balancer local service group <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">Load balancer VPX <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">Load balancer VPX HA <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">Load balancer VPX service <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">Load balancer VPX virtual IP <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">Object Storage account <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">Provisioning hook <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">Scaling group <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">Scaling policy <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">Security certificate <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">SSH key <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">User <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">Virtual guest <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="External link icon"></a></td>
  <tr>
</tbody></table>
