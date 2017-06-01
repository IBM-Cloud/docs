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

# Risorse per il provider del plug-in Terraform
{: #terraform-resources}

Le risorse {{site.data.keyword.IBM}} Cloud sono disponibili come provider di plug-in Terraform. Puoi combinare risorse diverse per creare le tue proprie configurazioni che possono essere quindi distribuite ai tuoi ambienti.
{: shortdesc}

Puoi visualizzare le <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">documentazioni delle origini dati <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> e le <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">documentazioni delle risorse <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a> in GitHub per gli esempi di utilizzo, gli argomenti richiesti e gli attributi esportati. Le configurazioni possono essere scritte in JSON o <a href="https://www.terraform.io/docs/configuration/index.html">HCL (HashiCorp Configuration Language) <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>.

## Sviluppo in locale
{: #developing}

Se vuoi sviluppare in locale sul tuo sistema, completa la seguente procedura:

1. <a href="https://www.terraform.io/intro/getting-started/install.html">Scarica e installa Terraform per il tuo sistema. <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">Scarica il file binario Terraform per il provider {{site.data.keyword.IBM_notm}} Cloud. <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a>

3. Crea un file `.terraformrc` che punti al file binario Terraform. 

  Nel seguente esempio, `/opt/provider/terraform-provider-ibmcloud` è la rotta della directory.

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. Configura il provider di plug-in e le tue credenziali {{site.data.keyword.IBM_notm}} per lavorare con Terraform. 

  Per fornire le tue credenziali come variabili di ambiente, puoi utilizzare il seguente codice nel file `.tf`.
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  Puoi quindi esportare le credenziali nel tuo terminale.
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## Origini dati
{: #data}

Le seguenti origini dati sono disponibili e possono essere utilizzate per estrarre le informazioni di sola lettura sulla tua risorsa. 

<table summary="Bluemix data sources">
<caption>Tabella 1. Origini dati della piattaforma disponibili.
</caption>
 <thead>
 <th colspan="5">Origini dati Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Account Bluemix<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Organizzazione Bluemix <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Spazio Bluemix <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Istanza del servizio Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Chiave del servizio Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Piano del servizio Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Cluster Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Configurazione del cluster Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Nodo di lavoro Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Bluemix Infrastructure (SoftLayer) data sources">
<caption>Tabella 2. Origini dati dell'infrastruttura disponibili.
</caption>
<thead>
<th colspan="4">Origini dati dell'infrastruttura Bluemix (SoftLayer)</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">Dominio DNS<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">Template immagine <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">Chiave SSH <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
 <t/r>
</tbody></table>


## Risorse
{: #resources}

Le seguenti risorse sono disponibili e possono essere utilizzate per definire i componenti della tua infrastruttura. 

 <table summary="Bluemix resources">
 <caption>Tabella 3. Risorse della piattaforma disponibili.
 </caption>
  <thead>
  <th colspan="5">Risorse Bluemix</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Istanza del servizio Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Chiave del servizio Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Cluster Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Bind del servizio Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Utente <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  </tr>
</tbody></table>

<table summary="Bluemix Infrastructure (SoftLayer) resources">
<caption>Tabella 4. Risorse dell'infrastruttura disponibili.
</caption>
 <thead>
 <th colspan="5">Risorse dell'infrastruttura Bluemix (SoftLayer)</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">Server bare metal <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">Monitor di base <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">Archivio blocchi <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">Dominio DNS<img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">Record del dominio DNS <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">Archiviazione file <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">Firewall hardware dedicato <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">Regole del firewall hardware dedicato <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">IP globale <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">Programma di bilanciamento del carico locale <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">Servizio locale del programma di bilanciamento del carico <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">Gruppo di servizi locali del programma di bilanciamento del carico <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">VPX del programma di bilanciamento del carico <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">HA VPX del programma di bilanciamento del carico <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">Servizio VPX del programma di bilanciamento del carico <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">IP virtuale VPX del programma di bilanciamento del carico <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">Account Object Storage <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">Hook di provisioning <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">Gruppo di ridimensionamento <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">Politica di ridimensionamento <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">Certificato di sicurezza <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">Chiave SSH <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Utente <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">Guest virtuale <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="Icona link esterno"></a></td>
  <tr>
</tbody></table>
