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

# Ressources pour le fournisseur de plug-in Terraform 
{: #terraform-resources}

Les ressources de cloud {{site.data.keyword.IBM}} sont disponibles sous la forme d'un fournisseur de plug-in Terraform. Vous pouvez combiner différentes ressources afin de créer vos propres configurations que vous pouvez ensuite déployer dans vos environnements.
{: shortdesc}

Vous pouvez afficher la <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">documentation relative aux sources de données <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> et la <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">documentation relative aux ressources <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> dans GitHub pour des exemples d'utilisation et prendre connaissance des arguments requis et des attributs exportés. Les configurations peuvent être écrites en langage JSON ou <a href="https://www.terraform.io/docs/configuration/index.html">HashiCorp Configuration Language (HCL) <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>.

## Développement en local
{: #developing}

Si vous voulez procéder au développement localement sur votre système, procédez comme suit : 

1. <a href="https://www.terraform.io/intro/getting-started/install.html">Téléchargez et installez Terraform pour votre système. <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">Téléchargez le fichier binaire Terraform pour le fournisseur de cloud {{site.data.keyword.IBM_notm}}. <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a>

3. Créez un fichier `.terraformrc` qui pointe vers le fichier binaire Terraform.  

  Dans l'exemple suivant, `/opt/provider/terraform-provider-ibmcloud` est le chemin d'accès au répertoire : 

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. Configurez le fournisseur de plug-in et vos données d'identification {{site.data.keyword.IBM_notm}} en vue de leur utilisation avec Terraform.  

  Pour fournir vos données d'identification sous forme de variables d'environnement, vous pouvez utiliser le code ci-dessous dans votre fichier `.tf`. 
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  Ensuite, vous pouvez exporter vos données d'identification dans votre terminal. 
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## Sources de données 
{: #data}

Les sources de données ci-après sont disponibles et peuvent être utilisées pour extraire des informations en lecture seule sur votre ressource.  

<table summary="Sources de données Bluemix">
<caption>Tableau 1. Sources de données de plateforme disponibles.
</caption>
 <thead>
 <th colspan="5">Sources de données Bluemix </th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Compte Bluemix <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Organisation Bluemix<img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Espace Bluemix <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Instance de service Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Clé de service Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Plan de service Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Cluster Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Configuration de cluster Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Noeud de travail Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Sources de données de l'infrastructure Bluemix (SoftLayer)">
<caption>Tableau 2. Sources de données d'infrastructure disponibles.
</caption>
<thead>
<th colspan="4">Sources de données de l'infrastructure Bluemix (SoftLayer) </th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">Domaine DNS <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">Modèle d'image <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">Clé SSH <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">Réseau local virtuel <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
 <t/r>
</tbody></table>


## Ressources
{: #resources}

Les ressources ci-après sont disponibles et peuvent être utilisées pour définir des composants de votre infrastructure.  

 <table summary="Ressources Bluemix">
 <caption>Tableau 3. Ressources de plateforme disponibles.
</caption>
  <thead>
  <th colspan="5">Ressources Bluemix </th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Instance de service Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Clé de service Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Cluster Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Liaison de service Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Utilisateur <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  </tr>
</tbody></table>

<table summary="Ressources de l'infrastructure Bluemix (SoftLayer)">
<caption>Tableau 4. Ressources d'infrastructure disponibles.
</caption>
 <thead>
 <th colspan="5">Ressources de l'infrastructure Bluemix (SoftLayer) </th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">Serveur Bare Metal <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">Moniteur de base <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">Stockage par blocs <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">Domaine DNS <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">Enregistrement de domaine DNS <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">Stockage de fichier <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">Pare-feu matériel dédié <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">Règles de pare-feu matériel dédié <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">Adresse IP globale <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">Equilibreur de charge local <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">Service d'équilibreur de charge local <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">Groupe de services de l'équilibreur de charge local <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">Equilibreur de charge VPX <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">Equilibreur de charge VPX à haute disponibilité <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">Service d'équilibreur de charge VPX <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">Adresse IP virtuelle d'équilibreur de charge VPX <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">Compte Object Storage <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">Point d'ancrage de mise à disposition <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">Groupe de mise à l'échelle <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">Stratégie de mise à l'échelle <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">Certificat de sécurité <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">Clé SSH <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Utilisateur <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">Invité virtuel <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">Réseau local virtuel <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a></td>
  <tr>
</tbody></table>
