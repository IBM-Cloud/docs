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

# Recursos para o provedor de plug-in do Terraform
{: #terraform-resources}

Os recursos do {{site.data.keyword.IBM}} Cloud ficam disponíveis como um provedor de plug-in do Terraform. Será possível combinar diferentes recursos para criar suas próprias configurações que poderão então ser implementadas em seus ambientes.
{: shortdesc}

É possível visualizar os <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">docs de origem de dados <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e os <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">docs de recursos <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> no GitHub para obter exemplos de uso, argumentos necessários e atributos exportados. As configurações podem ser gravadas em JSON ou <a href="https://www.terraform.io/docs/configuration/index.html">HashiCorp Configuration Language (HCL) <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. 

## Desenvolvendo localmente
{: #developing}

Se desejar desenvolver localmente no sistema, conclua as etapas a seguir:

1. <a href="https://www.terraform.io/intro/getting-started/install.html">Faça download e instale o Terraform no sistema. <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">Faça download do binário do Terraform para o provedor {{site.data.keyword.IBM_notm}}. <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>

3. Crie um arquivo `.terraformrc` que aponte para o binário do Terraform. 

  No exemplo a seguir, `/opt/provider/terraform-provider-ibmcloud` é a rota para o diretório.

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. Configure o provedor de plug-in e as credenciais do {{site.data.keyword.IBM_notm}} para trabalhar com o Terraform. 

  Para fornecer suas credenciais como variáveis de ambiente, será possível usar o código a seguir no arquivo `.tf`.
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  Será possível então exportar suas credenciais em seu terminal.
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## Origem de dados
{: #data}

As origens de dados a seguir estão disponíveis e podem ser usadas para extrair informações somente leitura sobre seu recurso. 

<table summary="Origens de dados do Bluemix">
<caption>Tabela 1. Origens de dados de plataforma disponíveis.
</caption>
 <thead>
 <th colspan="5">Origens de dados do Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Conta do Bluemix <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Organização do Bluemix <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Espaço do Bluemix <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Instância de serviço do Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Chave de serviço do Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Plano de serviço do Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Cluster do Kubernetes <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Configuração de cluster do Kubernetes <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Nó do trabalhador do Kubernetes <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Origens de dados de infraestrutura do Bluemix (SoftLayer)">
<caption>Tabela 2. Origens de dados de infraestrutura disponíveis.
</caption>
<thead>
<th colspan="4">Origens de dados de infraestrutura do Bluemix (SoftLayer)</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">Domínio do DNS <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">Modelo de imagem <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">Chave SSH <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
 <t/r>
</tbody></table>


## Recursos
{: #resources}

Os recursos a seguir estão disponíveis e podem ser usados para definir componentes de sua infraestrutura. 

 <table summary="Recursos do Bluemix">
 <caption>Tabela 3. Recursos de plataforma disponíveis.
 </caption>
  <thead>
  <th colspan="5">Recursos do Bluemix</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Instância de serviço do Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Chave de serviço do Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Cluster do Kubernetes <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Ligação de serviços do Kubernetes <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Usuário <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  </tr>
</tbody></table>

<table summary="Recursos de infraestrutura do Bluemix (SoftLayer)">
<caption>Tabela 4. Recursos de infraestrutura disponíveis.
</caption>
 <thead>
 <th colspan="5">Recursos de infraestrutura do Bluemix (SoftLayer)</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">Servidor bare metal <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">Monitor básico <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">Armazenamento de bloco <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">Domínio do DNS <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">Registro de domínio do DNS <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">Armazenamento de arquivo <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">Firewall de hardware dedicado <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">Regras dedicadas do firewall de hardware <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">IP global <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">Balanceador de carga local <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">Serviço local do balanceador de carga <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">Grupo de serviços locais do balanceador de carga <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">VPX do balanceador de carga <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">VPX HA do balanceador de carga <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">Serviço VPX do balanceador de carga <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">IP virtual do VPX do balanceador de carga <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">Conta do armazenamento de objeto <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">Gancho de fornecimento <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">Grupo de ajuste de escala <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">Política de ajuste de escala <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">Certificado de segurança <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">Chave SSH <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Usuário <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">Guest virtual <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a></td>
  <tr>
</tbody></table>
