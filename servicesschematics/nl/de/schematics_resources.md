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

# Ressourcen für den Terraform-Plug-in-Provider
{: #terraform-resources}

{{site.data.keyword.IBM}} Cloudressourcen stehen als Terraform-Plug-in-Provider zur Verfügung. Sie können verschiedene Ressourcen kombinieren, um Ihre eigenen Konfigurationen zu erstellen, die dann in Ihrer Umgebung bereitgestellt werden können.
{: shortdesc}

Anschließend können Sie die <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">Datenquellendokumentation<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> und <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">Ressourcendokumentation<img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> in GitHub für Verwendungsbeispiele, erforderliche Argumente und exportierte Attribute anzeigen. Konfigurationen können in JSON oder <a href="https://www.terraform.io/docs/configuration/index.html">HashiCorp Configuration Language (HCL) <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> geschrieben werden.

## Lokale Entwicklung
{: #developing}

Wenn Sie lokal auf Ihrem System entwickeln möchten, führen Sie die folgenden Schritte aus:

1. <a href="https://www.terraform.io/intro/getting-started/install.html">Laden Sie Terraform für Ihr System herunter und installieren Sie es. <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">Laden Sie die Terraform-Binärdatei für den {{site.data.keyword.IBM_notm}} Cloud-Provider herunter. <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>

3. Erstellen Sie eine `.terraformrc `-Datei, die auf die Terraform-Binärdatei verweist. 

  Im folgenden Beispiel ist `/opt/provider/terraform-Provider-ibmcloud` die Route zum Verzeichnis.

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. Konfigurieren Sie den Plug-in-Provider und Ihre {{site.data.keyword.IBM_notm}} Berechtigungsnachweise für die Arbeit mit Terraform. 

  Um Ihre Berechtigungsnachweise als Umgebungsvariablen angeben, können Sie den folgenden Code in Ihrer `.tf`-Datei verwenden.
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  Anschließend können Sie Ihre Berechtigungsnachweise in Ihr Terminal exportieren.
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## Datenquellen
{: #data}

Die folgenden Datenquellen sind verfügbar und können verwendet werden, um schreibgeschützte Informationen zu Ihrer Ressource zu extrahieren. 

<table summary="Bluemix-Datenquellen">
<caption>Tabelle 1. Verfügbare Plattformdatenquellen.
</caption>
 <thead>
 <th colspan="5">Bluemix-Datenquellen</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Bluemix-Konto <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Bluemix-Organisation <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Bluemix-Bereich <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Cloud Foundry-Serviceinstanz <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Cloud Foundry-Serviceschlüssel <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Cloud Foundry-Serviceplan <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Kubernetes-Cluster <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Kubernetes-Clusterkonfiguration <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Kubernetes-Workerknoten <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Datenquellen für Bluemix-Infrastruktur (SoftLayer)">
<caption>Tabelle 2. Verfügbare Infrastruktur-Datenquellen.
</caption>
<thead>
<th colspan="4">Datenquellen für Bluemix-Infrastruktur (SoftLayer)</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">DNS-Domäne <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">Imagevorlage <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">SSH-Schlüssel <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
 <t/r>
</tbody></table>


## Ressourcen
{: #resources}

Die folgenden Ressourcen sind verfügbar und können verwendet werden, um Komponenten Ihrer Infrastruktur zu definieren. 

 <table summary="Bluemix-Ressourcen">
 <caption>Tabelle 3. Verfügbare Plattformressourcen.
 </caption>
  <thead>
  <th colspan="5">Bluemix-Ressourcen</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Cloud Foundry-Serviceinstanz <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Cloud Foundry-Serviceschlüssel <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Kubernetes-Cluster <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Kubernetes-Servicebindung <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Benutzer <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  </tr>
</tbody></table>

<table summary="Ressourcen für Bluemix-Infrastruktur (SoftLayer)">
<caption>Tabelle 4. Verfügbare Infrastrukturressourcen.
</caption>
 <thead>
 <th colspan="5">Ressourcen für Bluemix-Infrastruktur (SoftLayer)</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">Bare-Metal-Server <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">Basic-Überwachung <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">Blockspeicher <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">DNS-Domäne <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">DNS-Domänendatensatz <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">Dateispeicherung <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">Dedizierte Hardware-Firewall <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">Regeln für die dedizierte Hardware-Firewall <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">Globale IP <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">Lokale Lastausgleichsfunktion <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">Lokaler Service für die Lastausgleichsfunktion <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">Lokale Servicegruppe für die Lastausgleichsfunktion <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">Lastausgleichsfunktion VPX <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">Lastausgleichsfunktion VPX HA <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">Lastausgleichsfunktion VPX-Service <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">Lastausgleichsfunktion VPX virtuelle IP <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">Objektspeicherkonto <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">Bereitstellungs-Hook <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">Skalierungsgruppe <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">Skalierungsrichtlinie <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">Sicherheitszertifikat <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">SSH-Schlüssel <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Benutzer <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">Virtueller Gast <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a></td>
  <tr>
</tbody></table>
