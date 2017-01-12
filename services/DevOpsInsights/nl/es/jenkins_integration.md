---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integración de {{site.data.keyword.DRA_short}} con Jenkins
{: #toolchain_configure_jenkins}

Cuando haya terminado de definir las políticas que {{site.data.keyword.DRA_full}} debe supervisar, el siguiente paso es añadir {{site.data.keyword.DRA_short}} a una cadena de herramientas y, a configuración, configurar un conducto de entrega continua.
{:shortdesc}

<!--##Configuring a Jenkins project-->

Puede integrar {{site.data.keyword.DRA_short}} en un proyecto de Jenkins o en varios proyectos de Jenkins relacionados. Esto le permite establecer puertas de calidad, así como recibir datos de calidad de las compilaciones en el panel de control de {{site.data.keyword.DRA_short}}.

##Requisitos previos    
{: #DI_jenkins_prereqs}

* Debe tener acceso a un proyecto de Jenkins local o al servidor que ejecuta un proyecto de Jenkins.

##Instalación del plugin de {{site.data.keyword.DRA_short}}
{: #DI_jenkins_install}

Para instalar el plugin de {{site.data.keyword.DRA_short}} en su proyecto de Jenkins, siga estos pasos:

  1. [Descargue el archivo de instalación del plugin de IBM DevOps Insight (.hpi)](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi) desde el repositorio de GitHub del plugin.
  2. En su instalación de Jenkins, pulse **Gestionar Jenkins**, seleccione **Gestionar plugins** y pulse el separador **Avanzado**.
  3. Pulse **Elegir archivo** y seleccione el archivo de instalación del plugin de DevOps Insight.
  4. Pulse **Cargar**.
  5. Reinicie Jenkins y verifique se ha instalado el plugin.

##Integración de {{site.data.keyword.DRA_short}} con Jenkins    
{: #DI_jenkins_integrate}

Tras instalar el plugin, pero antes de integrar {{site.data.keyword.DRA_short}} en su instalación de Jenkins, vaya al [centro de control](https://control-center.stage1.ng.bluemix.net/) y cree al menos una política.

Para cada uno de los trabajos que ya tiene y en los que desea utilizar {{site.data.keyword.DRA_short}}:

1. Añada una acción posterior a la compilación de tipo **Publicar información de compilación en {{site.data.keyword.DRA_short}}**, **Publicar información de despliegue en {{site.data.keyword.DRA_short}}** o **Publicar resultado de prueba en {{site.data.keyword.DRA_short}}**. El tipo específico debe coincidir con el tipo de trabajo (compilar, desplegar o probar). Complete los campos necesarios.
  * En el campo Credencial, escriba su ID y su contraseña de Bluemix. Si no están guardados en Jenkins, pulse el botón **Añadir** para añadirlos y guardarlos.
  * En el campo Nombre de trabajo de compilación, especifique el nombre del trabajo exactamente como aparece en Jenkins. Si la compilación se realiza juntamente con el trabajo de prueba, deje este campo vacío. Si el trabajo de compilación se realiza fuera de Jenkins, marque **Las compilaciones se realizan fuera de Jenkins** y especifique el número de compilación y el URL de compilación.
  * Para el campo Ubicación del archivo de resultados, especifique la ubicación del archivo de resultados. Si la prueba no genera ningún archivo de resultados, deje este campo vacío. El plugin cargará un archivo de resultados de prueba predeterminado en el estado del trabajo de prueba actual.
3. *Opcional*: Si desea que las puertas de política DRA del trabajo de prueba controlen el trabajo de despliegue en sentido descendente, añada otra acción posterior a la compilación de tipo **Puerta de DevOps Risk Analytics** y complete los campos necesarios. La puerta impedirá que se ejecute el trabajo en sentido descendente si el trabajo de prueba no cumple las políticas asociadas.
4. Pulse **Aplicar** y, a continuación, pulse **Guardar**.

Puede pulsar **Compilar ahora** en la página de proyecto para ejecutar el proyecto.

Tras ejecutarse la compilación, vaya al [centro de control](https://control-center.stage1.ng.bluemix.net/) para comprobar el estado de la compilación en el panel de control. Si ha configurado puertas de política, también puede ver los resultados de {{site.data.keyword.DRA_short}} en la página Estado de la compilación actual.
