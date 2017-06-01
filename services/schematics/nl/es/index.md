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

# Iniciación a {{site.data.keyword.bpfull_notm}} (Beta)
{: #gettingstarted}

{{site.data.keyword.bplong}} es una herramienta de automatización que puede utilizar para definir y desplegar la infraestructura de nube como una única unidad, y utilizar estas definiciones de nube en cualquier número de entornos.
{:shortdesc}

{{site.data.keyword.bpshort}} utiliza Terraform, de HashiCorp, para codificar la infraestructura. Los componentes de su infraestructura se dividen en recursos individuales, que pueden ser cualquier cosa, desde hardware físico hasta cuentas de usuario. Esta separación de recursos de alto y bajo nivel le permite tratar la infraestructura como si fuera software, como código.  

Cuando trabaja con {{site.data.keyword.bpshort}}, escribe configuraciones para su entorno en una sintaxis declarativa. Indica el aspecto que quiere para su entorno, como tener 10 {{site.data.keyword.virtualmachinesshort}} en producción. El servicio compara su configuración con la creada anteriormente por Terraform y añade o elimina recursos, según sea necesario.

{{site.data.keyword.bpshort}} es una herramienta de DevOps colaborativa que proporciona una única fuente fiable para la infraestructura. Puede almacenar las configuraciones de entorno en el control de origen, proporcionando a su equipo la capacidad de realizar revisiones de código, versionar la infraestructura, realizar el seguimiento de los cambios a través del historial de confirmación y revertir los cambios más fácilmente. 

{{site.data.keyword.bpshort}} está disponible automáticamente para todos los usuarios en su cuenta de {{site.data.keyword.Bluemix_notm}}.


## Creación de una configuración
{: #configuration}

Al crear una configuración, está codificando los recursos de nube que componen su entorno.
{:shortdesc}


Si quiere probar una configuración de ejemplo con {{site.data.keyword.bpshort}}, complete los siguientes pasos. En el ejemplo, puede suministrar una clave SSH para utilizar en {{site.data.keyword.BluSoftlayer}}. 

**Nota:** La configuración de ejemplo requiere una cuenta de {{site.data.keyword.BluSoftlayer}}. Consulte el [documento Enlace de sus cuentas de usuario de {{site.data.keyword.Bluemix_notm}} y SoftLayer](../../pricing/linking_accounts.html#unifyingaccounts) si tiene una cuenta existente, o bien puede [registrarse para una cuenta](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

1. Genere un par de claves SSH de forma local.
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. Bifurque la configuración de ejemplo en <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. 

  Los ejemplos siguientes muestran los distintos tipos de bloques que se encuentran en la configuración de ejemplo. Puede ver la configuración completa en el archivo `main.tf` del repositorio de GitHub.
  
  * El bloque de proveedores configura el proveedor de {{site.data.keyword.IBM_notm}} Cloud y las credenciales de inicio de sesión.

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * El bloque recursos define un componente de su infraestructura, que en este ejemplo es una clave SSH. 
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * El bloque variables define sus variables, que puede especificar en la interfaz gráfica de usuario de {{site.data.keyword.bpshort}} para este ejemplo.
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * El bloque de salidas define lo que se muestra en la salida de Terraform después de utilizar la configuración para crear su entorno y de crear el recurso (clave SSH). 
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
Ahora puede crear un entorno desde su configuración.  

{:codeblock}

## Creación de un entorno
{: #environment}

Cuando crea un entorno, el servicio debe apuntar a su configuración para que dicho servicio pueda extraer las últimas modificaciones de código.
{:shortdesc}

Utilizando la configuración de ejemplo, complete los pasos siguientes para crear un entorno. 

1. En el menú, seleccione **Servicios** y, a continuación, **{{site.data.keyword.bpshort}}**. Se le dirigirá al panel de control de {{site.data.keyword.bpshort}}.

2. En el menú de navegación izquierdo, seleccione **Entornos** y pulse **Crear entorno** para describir propiedades sobre su configuración. La creación de un entorno define cómo {{site.data.keyword.bpshort}} suministra y actualiza los recursos de nube, pero no crea recursos todavía. 

3. Especifique los detalles sobre su entorno. La configuración de ejemplo requiere los valores que se enumeran en la tabla siguiente:

  <table summary="Los valores que son necesarios para poder utilizar la configuración de ejemplo como el origen de su entorno.">
  <caption>Tabla 1. Los valores que son necesarios para poder utilizar la configuración de ejemplo como el origen de su entorno.</caption>
  <thead>
  <th colspan="1">Valor</th>
  <th colspan="1">Descripción</th>
  </thead>
  <tbody>
  <tr>
  <td>URL de control de origen</td>
  <td>Especifique el URL de GitHub donde ha bifurcado la configuración de ejemplo.</td>
  </tr>
  <tr>
  <td>Nombre</td>
  <td>Especifique un nombre exclusivo para asignar a su entorno.</td>
  </tr>
  <td>Versión de Terraform</td>
  <td>Especifique la versión de Terraform para garantizar que se ejecute una versión de Terraform compatible con su entorno. Para la configuración de ejemplo, utilice la versión <code>0.9.1</code>.</td>
  </tr>
  <tr>
  <td>Variables</td>
  <td>Puede definir variables en el servicio o alterar temporalmente las variables de entorno que están en sus archivos <code>.tf</code>. Puede enmascarar variables sensibles si pulsa el icono de bloqueo. El enmascaramiento de variables impide que otros usuarios vean los valores ocultos en la página de detalles del entono. <p>
  <p>Añada las siguientes variables y valores para trabajar con la configuración de ejemplo:<ul>
  <li><code>ibmid</code> - Especifique su {{site.data.keyword.ibmid}} completo como valor.</li>
  <li><code>ibmidpw</code> - Especifique la contraseña asociada a su {{site.data.keyword.ibmid}} y pulse el icono de bloqueo para enmascarar el valor.</li>
  <li><code>slaccountnum</code> - Especifique su número de cuenta de {{site.data.keyword.BluSoftlayer}}.
   <li><code>datacenter</code> - Especifique el centro de datos en el que desea desplegar el recurso de clave SSH. Consulte el <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">archivo readme <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para obtener una lista completa de los valores disponibles.</li> 
   <li><code>public_key</code> - Especifique la clave SSH pública. Para copiar la clave pública en su portapapeles, puede ejecutar el mandato <code>pbcopy < ~/.ssh/id_rsa.pub</code>.
   <li><code>key_label</code> - Identifique la clave con un nombre exclusivo.
   <li><code>key_note</code> - Opcional: Añada texto descriptivo sobre la clave SSH.</ul></td>
   </tr></tbody></table>

4. Cuando haya completado los detalles del entorno, pulse **Crear**. Se muestra el entorno recién creado.  
5. Para ver una vista previa de los recursos suministrados o eliminados al desplegar el entorno, pulse **Plan**. 
6. Consulte el registro del plan para comprobar que no haya errores la salida. 
7. Cuando esté listo para desplegar el entorno, pulse **Aplicar**. Puede supervisar el archivo de aplicación para ver si la clave se ha desplegado correctamente. Un despliegue correcto muestra la siguiente línea hacia el final de la salida:

  ```
  ¡Aplicación completa! Recursos: 1 añadido, 0 cambiados, 0 destruidos.
  ```
  {: screen}

  También puede ver la clave SSH en el [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys).
8. Opcional: Para eliminar la clave SSH y eliminar el entorno de {{site.data.keyword.Bluemix_notm}}, seleccione **Destruir recursos** en el menú de acciones.

### Qué hacer a continuación
{: #next}

* Para encontrar más información sobre cómo desplegar sus entornos mediante programación, [consulte la CLI o la API](schematics_deploying.html).
* Para crear sus propias configuraciones desde cero, consulte los <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">Recursos de {{site.data.keyword.IBM_notm}} Cloud <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>. Los recursos de {{site.data.keyword.IBM_notm}} Cloud están disponibles como proveedor de plugins de Terraform.
