---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Uso de cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} Dedicado
{: #toolchains-using_dedicated}

Última actualización: 13 de septiembre de 2016
{: .last-updated}

Puede utilizar una cadena de herramientas para que sea productiva en su trabajo diario de desarrollo, despliegue y operaciones. Una vez que se ha configurado una cadena de herramientas, es posible añadir, eliminar o configurar integraciones de herramientas y gestionar el acceso a la cadena de herramientas.
{: shortdesc}

## Configuración de una integración de herramienta
{: #configuring_a_tool_integration_dedicated}

Si ha aplazado la configuración de una integración de herramientas al crear una cadena de herramientas, se mostrará un botón **Configure** en su mosaico. Si ha configurado una integración de herramientas al crear una cadena de herramientas, puede actualizar los valores de configuración.

1. En el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Tool Integrations. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**.
1. Si necesita configurar una integración de herramienta por primera vez, en su mosaico, pulse **Configure**.

  ![Botón de configuración](images/toolchain_tile_configure.png)

 Cuando haya terminado de configurar la integración de la herramienta, pulse **Save Integration**.
 
1. Si necesita actualizar la configuración de una integración de herramienta, en su mosaico, pulse el menú para acceder a las opciones de configuración.

  ![Menú de configuración](images/toolchain_tile_menu.png)
 
 Cuando haya terminado de configurar los ajustes, pulse **Save Integration**.

## Adición de una integración de herramienta
{: #adding_a_tool_integration_dedicated}

Puede añadir y configurar integraciones de herramientas para su cadena de herramientas.

1. En el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Tool Integrations. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**.
1. Para ver una lista de las integraciones de herramientas que se deben añadir, pulse el botón de adición (+).
1. Pulse en la integración de herramientas a añadir.
1. Introduzca la información necesaria para configurar la integración de la herramienta. 
1. Pulse **Create Integration** para añadir la integración de la herramienta en su cadena de herramientas.

## Eliminación de una integración de herramienta
{: #deleting_a_tool_integration}

Si suprime una integración de herramientas desde su cadena de herramientas, la supresión no se podrá deshacer. 

1. En el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Tool Integrations. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**.
1. En el mosaico de la integración de herramientas a suprimir, pulse el menú para acceder a las opciones de configuración.
1. Para eliminar la integración de herramienta de su cadena de herramientas, pulse **Delete**.
1. Confirme la acción pulsando **Delete**. 

## Gestión del acceso
{: #managing_access_dedicated}

Puede conceder acceso a los usuarios a una cadena de herramientas si los añade a la organización con la que está asociada la cadena de herramientas. Cada cadena de herramientas está asociada con una organización específica, y cualquier usuario que sea miembro de dicha organización puede acceder a las cadenas de herramientas asociadas. Para ver la organización en la que está trabajando en este momento, pulse el icono **{{site.data.keyword.avatar}}** ![Icono de avatar](../icons/i-avatar-icon.svg) en la barra de menús. Para acceder a un conjunto distinto de cadenas de herramientas, cambie a una organización distinta.

Al añadir usuarios a la organización y a los espacios de {{site.data.keyword.Bluemix}}, los usuarios pueden iniciar sesión en GitHub Enterprise utilizando su ID y contraseña de {{site.data.keyword.Bluemix_notm}}. Cuando los usuarios inician sesión, se les crearán cuentas. Al añadir usuarios a la organización y a los espacios de {{site.data.keyword.Bluemix_notm}}, no se añadirán automáticamente al repositorio de GitHub Enterprise. Debe añadirlos alguien que tenga privilegios de administración para el repositorio. Para obtener más información, consulte [Uso de GitHub Enterprise Dedicado (El enlace se abre en una ventana nueva)](../services/ghededicated/index.html){: new_window}.

Para añadir un usuario, siga estos pasos: 

1. En el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Tool Integrations. A continuación, pulse **Manage**. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**. A continuación, pulse **Manage**.  
1. Pulse el enlace de su organización. 
1. En la página Manage Organizations, pulse **Invite a User** y escriba la dirección de correo electrónico del usuario.
1. Si desea conceder permisos avanzados para gestionar usuarios en las organizaciones de {{site.data.keyword.Bluemix_notm}}, seleccione uno o varios de los recuadros de selección **Manager**, **Billing Manager** o **Auditor**.
1. Pulse **INVITE**.
1. Pulse **SAVE**.

## Eliminación de una cadena de herramientas
{: #deleting_a_toolchain_dedicated}

Puede eliminar una cadena de herramientas y especificar qué integraciones de herramienta asociadas desea eliminar. Al suprimir una cadena de herramientas, la supresión no se podrá deshacer.

1. En el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Tool Integrations. A continuación, pulse **Manage**. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**. A continuación, pulse **Manage**.
1. Pulse **Delete Toolchain** y revise o ajuste las integraciones de herramientas que se dispone a eliminar.
1. Para confirmar la eliminación, escriba el nombre de la cadena de herramientas y pulse **Delete**.

 **Consejo**: cuando elimine la integración de una herramienta GitHub Enterprise, el repositorio de GitHub Enterprise asociado no se eliminará de GitHub Enterprise. Deberá eliminar el repositorio manualmente de GitHub Enterprise.
