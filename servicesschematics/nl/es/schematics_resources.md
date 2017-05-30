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

# Recursos para el proveedor de plugins de Terraform
{: #terraform-resources}

Los recursos de {{site.data.keyword.IBM}} Cloud están disponibles como proveedor de plugins de Terraform. Combine distintos recursos para crear sus propias configuraciones, que podrá desplegar en sus entornos.
{: shortdesc}

Consulte los <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">documentos de orígenes de datos <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> y los <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">documentos de recursos <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> en GitHub para obtener ejemplos de uso, argumentos necesarios y atributos exportados. Las configuraciones se pueden escribir en JSON o <a href="https://www.terraform.io/docs/configuration/index.html">HashiCorp Configuration Language (HCL) <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

## Desarrollo de forma local
{: #developing}

Si desea realizar el desarrollo de forma local en su sistema, realice los siguientes pasos:

1. <a href="https://www.terraform.io/intro/getting-started/install.html">Descargue e instale Terraform para su sistema. <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">Descargue el binario de Terraform para el proveedor de {{site.data.keyword.IBM_notm}} Cloud. <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>

3. Cree un archivo `.terraformrc` que apunte al binario de Terraform. 

  En el siguiente ejemplo, `/opt/provider/terraform-provider-ibmcloud` es la ruta al directorio. 

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. Configure el proveedor de plugins y sus credenciales de {{site.data.keyword.IBM_notm}} para trabajar con Terraform. 

  Para proporcionar las credenciales como variables de entorno, puede utilizar el código siguiente en el archivo `.tf`.
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  A continuación, puede exportar las credenciales al terminal.
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## Orígenes de datos
{: #data}

Los siguientes orígenes de datos están disponibles y se pueden utilizar para extraer información de solo lectura sobre el recurso.  

<table summary="Orígenes de datos de Bluemix">
<caption>Tabla 1. Orígenes de datos de plataforma disponibles.
</caption>
 <thead>
 <th colspan="5">Orígenes de datos de Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Cuenta de Bluemix <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Organización de Bluemix <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Espacio de Bluemix <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Instancia de servicio de Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Clave de servicio de Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Plan de servicio de Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Clúster de Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Configuración de clústeres de Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Nodo de trabajador de Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Orígenes de datos de infraestructura de Bluemix (SoftLayer)">
<caption>Tabla 2. Orígenes de datos de infraestructura disponible.
</caption>
<thead>
<th colspan="4">Orígenes de datos de infraestructura de Bluemix (SoftLayer)</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">Dominio DNS <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">Plantilla de imagen
<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">Clave SSH <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
 <t/r>
</tbody></table>


## Recursos
{: #resources}

Los siguientes recursos están disponibles y se pueden utilizar para definir componentes de su infraestructura. 

 <table summary="Recursos de Bluemix">
 <caption>Tabla 3. Recursos de plataforma disponibles.</caption>
  <thead>
  <th colspan="5">Recursos de Bluemix</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Instancia de servicio de Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Clave de servicio de Cloud Foundry <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Clúster de Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Enlace de servicio de Kubernetes <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Usuario <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  </tr>
</tbody></table>

<table summary="Recursos de la infraestructura de Bluemix (SoftLayer)">
<caption>Tabla 4. Recursos de infraestructura disponibles.
</caption>
 <thead>
 <th colspan="5">Recursos de la infraestructura de Bluemix (SoftLayer)</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">Servidor nativo <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">Supervisor básico <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">Almacenamiento de bloques <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">Dominio DNS <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">Registro de dominios DNS <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">Almacenamiento de archivos <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">Cortafuegos de hardware dedicado <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">Reglas de cortafuegos de hardware dedicado <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">IP global <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">Equilibrador de carga local <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">Servicio local de equilibrador de carga <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">Grupo de servicios locales de equilibrador de carga <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">VPX de equilibrador de carga <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">VPX HA de equilibrador de carga <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">Servicio VPX de equilibrador de carga del servicio VPX <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">IP virtual de VPX de equilibrador de carga <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">Cuenta de almacenamiento de objetos <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">Gancho de suministro <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">Grupo de escalado <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">Política de escalado <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">Certificado de seguridad <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">Clave SSH <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">Usuario <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">Invitado virtual <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a></td>
  <tr>
</tbody></table>
