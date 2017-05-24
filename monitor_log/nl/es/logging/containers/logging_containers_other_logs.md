---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Recopilación de datos de registro no predeterminado desde un contenedor
{: #logging_containers_collect_data}

Para capturar de ubicaciones de registro que no sean la predeterminada dentro de un contenedor, establezca la variable de entorno **LOG_LOCATIONS** cuando cree un contenedor. 
{:shortdesc}

* Añada la variable de entorno de **LOG_LOCATIONS** con una vía de acceso al archivo de registro cuando cree el contenedor. 
* Puede añadir varios archivos de registro separándolos con comas. 

## Recopilación de datos de registro no predeterminado mediante la consola de Bluemix
{: #logging_containers_collect_data_ui}

Siga los pasos siguientes para recopilar datos de registro no predeterminado mediante la consola:

1. Desde el catálogo, seleccione **Contenedores** y elija una imagen. 

    La lista de imágenes que se muestra incluye imágenes proporcionadas por {{site.data.keyword.IBM}} e imágenes almacenadas en su registro privado de {{site.data.keyword.Bluemix_notm}}. 

2. Defina un contenedor. Elija el tipo, escriba un nombre para el contenedor, seleccione su tamaño y defina otros atributos, como detalles de la dirección IP y puertos. Para obtener más información, consulte [Crear y desplegar un único contenedor mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}](/docs/containers/container_single_ui.html#gui). 

3. Expanda la sección **Opciones avanzadas** y seleccione **Añadir una variable de entorno nueva**.

4. Añada la variable **LOG_LOCATIONS** y establezca su valor en el registro que desea analizar.

    Por ejemplo, cuando añada un contenedor basado en la última imagen de Liberty, para analizar el archivo de registro *dpkg.log* establezca el valor de entorno en el valor siguiente:
    
    <table>
      <caption>Tabla 1. Valor de ejemplo de ubicaciones de registro</caption>
      <tbody>
        <tr>
          <th align="center">Nombre de variable</th>
          <th align="center">Valor</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. Pulse **Crear**.

Se abre el panel de control del contenedor. Compruebe que el estado del contenedor sea *En ejecución* y consulte los registros en el separador **Supervisión y registros**.


## Recopilación de datos de registro no predeterminado mediante la CLI
{: #logging_containers_collect_data_cli}

Siga los pasos siguientes para recopilar datos de registro no predeterminado mediante la CLI:

1. Configure un terminal para que utilice la CLI de {{site.data.keyword.containershort}}. Para obtener más información, consulte [Configuración de la CLI del servicio IBM Bluemix Container](/docs/containers/container_cli_cfic_install.html).

2. Inicie una sesión en la CLI de Cloud Foundry con el siguiente mandato: `cf login`. Escriba el ID, la contraseña, la organización, el espacio de {{site.data.keyword.Bluemix_notm}} cuando se le solicite. 

    De forma predeterminada, la sesión se inicia en la región del sur de Estados Unidos o en la última región en la que se ha iniciado una sesión. 
    
    Puede incluir la opción **–a** para iniciar la sesión en una región específica en {{site.data.keyword.Bluemix_notm}}. Por ejemplo, en la siguiente tabla se muestran los mandatos por región:

    <table>
      <caption>Tabla 2. Mandatos por región</caption>
      <tbody>
        <tr>
          <th align="center">Región</th>
          <th align="center">Mandato</th>
        </tr>
        <tr>
          <td align="left">EE.UU. sur</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">Reino Unido</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
	 <tr>
          <td align="left">Frankfurt</td>
          <td align="left">cf login -a api.eu-de.bluemix.net</td>
        </tr>
       </tbody>
    </table>
    

3. Inicie la sesión en {{site.data.keyword.containershort}} con el siguiente mandato: `cf ic login`

4. Crear un único contenedor a partir de una imagen. Incluya la variable de entorno LOG_LOCATIONS para incluir las ubicaciones de registros no predeterminados.  

    Para añadir una ubicación personalizada para poder ver la información de registro en Kibana, añada la variable de entorno **LOG_LOCATIONS** cuando cree el contenedor. Escriba este mandato:
    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    donde
    
     <table>
      <caption>Tabla 3. Opciones de mandato</caption>
      <tbody>
        <tr>
          <th align="center">Opción</th>
          <th align="center">Descripción</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> Si desea que se pueda acceder a la app desde Internet, tiene que exponer un puerto público. Incluya los puertos especificados en el archivo de Docker para la imagen que está utilizando. <br> Puede elegir entre UDP y TCP para indicar el protocolo IP que desea utilizar. Si no especifica ningún protocolo, el puerto se expone automáticamente para el tráfico TCP. <br> Cuando exponga un puerto público, cree un Grupo de seguridad de red pública para el contenedor que le permita enviar y recibir datos públicos únicamente en el puerto expuesto. Los demás puertos públicos están cerrados y no pueden utilizarse para acceder a la app desde Internet. <br> Puede incluir varios puertos con varias opciones -p. </td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">Establece una variable de entorno. <br> Puede listar varias claves por separado. Especifique el nombre y el valor de la variable de entorno entre comillas. <br> Para añadir un archivo de registro para su supervisión en el contenedor, incluya la variable de entorno LOG_LOCATIONS con una vía de acceso al archivo de registro.</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">Define el nombre del contenedor.</td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">Registro en la región pública. Por ejemplo, para la región EE.UU. Sur, el nombre de dominio predeterminado es: `ng.bluemix.net` y para el Reino Unido, el nombre de dominio predeterminado es: `eu-gb.bluemix.net` </td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">Nombre de la imagen que desea añadir.</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">Etiqueta de la imagen que desea añadir.</td>
        </tr>
      </tbody>
    </table>
    
    Por ejemplo, para crear un contenedor basado en la última imagen de Liberty e incluir el archivo de registro `/var/log/dpkg.log`, utilice el mandato siguiente: 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    El archivo dpkg.log es un archivo de registro Ubuntu estándar que se suele generar durante la creación de un contenedor, pero no que se traslada automáticamente a Kibana.

Para comprobar el estado del contenedor, ejecute el mandato `docker ps`. Cuando el estado sea *En ejecución*, consulte los registros en la consola de {{site.data.keyword.Bluemix_notm}}, a través de la línea de mandatos o a través de Kibana.



