---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Uso de cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} Público
{: #toolchains-using}

Última actualización: 9 de noviembre de 2016
{: .last-updated}

Puede utilizar una cadena de herramientas para que sea productiva en su trabajo diario de desarrollo, despliegue y operaciones. Una vez que se ha configurado una cadena de herramientas, es posible añadir, eliminar o configurar integraciones de herramientas y gestionar el acceso a la cadena de herramientas. Las cadenas de herramientas están disponibles únicamente en el sur de EE. UU.
{: shortdesc}

## Configuración de una integración de herramienta
{: #configuring_a_tool_integration}

Si ha aplazado la configuración de una integración de herramientas al crear una cadena de herramientas, se mostrará un botón **Configure** en su mosaico. Si ha configurado una integración de herramientas al crear una cadena de herramientas, puede actualizar los valores de configuración.

1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Visión general correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Visión general**.
1. Si necesita configurar una integración de herramienta por primera vez, en su mosaico, pulse **Configure**.

  ![Botón de configuración](images/toolchain_tile_configure.png)

 Cuando haya terminado de configurar la integración de la herramienta, pulse **Save Integration**.
 
1. Si necesita actualizar la configuración de una integración de herramienta, en su mosaico, pulse el menú para acceder a las opciones de configuración.

  ![Menú de configuración](images/toolchain_tile_menu.png)
 
 Cuando haya terminado de configurar los ajustes, pulse **Save Integration**.

## Adición de una integración de herramienta
{: #adding_a_tool_integration}

Puede añadir y configurar integraciones de herramientas para su cadena de herramientas.

1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Visión general correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Visión general**.
1. Para ver una lista de integraciones de herramientas que añadir, pulse **Añadir una herramienta**.
1. Pulse en la integración de herramientas que desee añadir.
1. Introduzca la información necesaria para configurar la integración de la herramienta. 
1. Pulse **Create Integration** para añadir la integración de la herramienta en su cadena de herramientas.

## Eliminación de una integración de herramienta
{: #deleting_a_tool_integration}

Si suprime una integración de herramientas desde su cadena de herramientas, la supresión no se podrá deshacer. 

1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Visión general correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Visión general**.
1. En el mosaico de la integración de herramienta que desea eliminar, pulse el menú para acceder a las opciones de configuración.
1. Para eliminar la integración de herramienta de su cadena de herramientas, pulse **Delete**.
1. Confirme la acción pulsando **Delete**.  

## Gestión del acceso
{: #managing_access}

Puede conceder acceso a los usuarios a una cadena de herramientas si los añade a la organización con la que está asociada la cadena de herramientas. Cada cadena de herramientas está asociada con una organización específica, y cualquier usuario que sea miembro de dicha organización puede acceder a las cadenas de herramientas asociadas. La organización en la que está trabajando actualmente se muestra en la barra de menús. Pulse la organización y, a continuación, cambie de organización para acceder a un conjunto distinto de cadenas de herramientas.

1. En el panel de control de DevOps, en la página **Toolchains**, pulse la cadena de herramientas que desee gestionar y pulse **Manage**. Como alternativa, en la página de visión general de la aplicación, en el mosaico Continuous Delivery, pulse **View Toolchain** y luego pulse **Manage**.  
1. Pulse el enlace de su organización. 
1. En la página Manage Organizations, pulse **Invite a User** y escriba la dirección de correo electrónico del usuario.
1. Si desea conceder permisos avanzados para gestionar usuarios en las organizaciones de {{site.data.keyword.Bluemix_notm}}, seleccione uno o varios de los recuadros de selección **Manager**, **Billing Manager** o **Auditor**.
1. Pulse **INVITE**.
1. Pulse **GUARDAR**.

## Eliminación de una cadena de herramientas
{: #deleting_a_toolchain}

Puede eliminar una cadena de herramientas y especificar qué integraciones de herramienta asociadas desea eliminar. Al suprimir una cadena de herramientas, la supresión no se podrá deshacer.

1. En el panel de control de DevOps, en la página **Toolchains**, pulse la cadena de herramientas que desee eliminar y pulse **Manage**. Como alternativa, en la página de visión general de la aplicación, en el mosaico Continuous Delivery, pulse **View Toolchain** y luego pulse **Manage**.
1. Pulse **Delete Toolchain** y revise o ajuste las integraciones de herramientas que se dispone a eliminar.
1. Para confirmar la eliminación, escriba el nombre de la cadena de herramientas y pulse **Delete**.  

 **Consejo**: cuando elimine la integración de una herramienta GitHub, el repositorio de GitHub asociado no se eliminará de GitHub. Deberá eliminar el repositorio manualmente.


# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [Crear y utilizar su primera cadena de herramientas (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Crear una cadena de herramientas personalizada (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Crear una aplicación con tres microservicios (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Crear una cadena de herramientas desde una plantilla en {{site.data.keyword.Bluemix_notm}} Dedicado (Beta) (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Crear una cadena de herramientas desde una app en {{site.data.keyword.Bluemix_notm}} Dedicado (Beta) (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Enlaces relacionados
{: #general}

* [Cadena de herramientas de microservicios (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadena de herramientas simple (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [Método IBM Bluemix Garage (el enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method){:new_window}
