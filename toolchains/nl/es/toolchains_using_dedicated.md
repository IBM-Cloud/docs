---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Sudo de cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} dedicado
{: #toolchains-using_dedicated}

Última actualización: 26 de agosto de 2016
{: .last-updated}

Puede utilizar una cadena de herramientas para ser productivo en sus actividades diarias de desarrollo, despliegue y operaciones. Tras configurar una cadena de herramientas, puede añadir, suprimir o configurar integraciones de herramientas y gestionar el acceso a la cadena de herramientas.
{: shortdesc}

**Importante**: esta funcionalidad es experimental. Las cadenas de herramientas pueden no ser estables y es posible que cambien de modo que no sean compatibles con versiones anteriores. No se recomienda utilizarlas en entornos de producción.   

## Configuración de una integración de herramientas
{: #configuring_a_tool_integration_dedicated}

Si ha aplazado la configuración de una integración de herramientas al crear una cadena de herramientas, se mostrará un botón **Configurar** en el mosaico correspondiente. Si ha configurado una integración de herramientas al crear una cadena de herramientas, puede actualizar los valores de configuración.

1. En el panel de control, en la pestaña **DEVOPS**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**.A continuación, pulse **Integraciones de herramientas**.
1. Si necesita configurar una integración de herramientas por primera vez, en el mosaico correspondiente, pulse **Configurar**.

  ![Botón Configurar](images/toolchain_tile_configure.png)

 Cuando haya terminado de configurar la integración de herramientas, pulse **Guardar integración**.
 
1. Si necesita actualizar la configuración de una integración de herramientas, en el mosaico correspondiente, pulse el menú para acceder a las opciones de configuración.

  ![Menú de configuración](images/toolchain_tile_menu.png)
 
 Cuando haya terminado de actualizar los valores, pulse **Guardar integración**.

## Adición de una integración de herramientas
{: #adding_a_tool_integration_dedicated}

Puede añadir y configurar las integraciones de herramientas para su cadena de herramientas.

1. En el panel de control, en la pestaña **DEVOPS**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**.A continuación, pulse **Integraciones de herramientas**.
1. Para ver una lista de integraciones para añadir, pulse el botón (+).
1. Pulse la integración de herramientas que desee añadir.
1. Indique la información necesaria para configurar la integración de herramientas. 
1. Pulse **Crear integración** para añadir la integración de herramientas a su cadena de herramientas.

## Supresión de una integración de herramientas
{: #deleting_a_tool_integration}

Si suprime una integración de herramientas de la cadena de herramientas, la supresión no se puede deshacer. 

1. En el panel de control, en la pestaña **DEVOPS**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**.A continuación, pulse **Integraciones de herramientas**.
1. En el mosaico de la integración de herramientas que desea suprimir, pulse el menú para acceder a las-opciones de configuración.
1. Para suprimir la integración de herramientas de la cadena de herramientas, pulse **Suprimir**.
1. Confirme pulsando **Suprimir**. 

## Gestión de acceso
{: #managing_access_dedicated}

Puede conceder a los usuarios acceso a una cadena de herramientas añadiéndolos a la organización (org) con la que está asociada la cadena de herramientas. Cada cadena de herramientas está asociada con una organización específica y cualquier usuario que sea miembro de la organización en cuestión puede acceder a las cadenas de herramientas asociadas. Para ver la organización en la que está trabajando, pulse el icono **{{site.data.keyword.avatar}}** ![icono de Avatar](../icons/i-avatar-icon.svg) en la barra de menús. Para acceder a otro conjunto de cadenas de herramientas, cambie de organización.

Cuando se añaden usuarios a la organización y los espacios de {{site.data.keyword.Bluemix}}, los usuarios puede indicar sesión en GitHub Enterprise utilizando su ID y contraseña de {{site.data.keyword.Bluemix_notm}}. Cuando los usuarios inician sesión, se les crean cuentas. Cuando se añaden usuarios a la organización y los espacios de {{site.data.keyword.Bluemix_notm}}, también se añaden automáticamente al repositorio de GitHub Enterprise. El usuario que los añada debe disponer de privilegios administrativos.Para obtener más información, consulte [Uso de Dedicated GitHub Enterprise](../services/ghededicated/index.html){: new_window}.

Para añadir un usuario, siga estos pasos: 

1. En el panel de control, en la pestaña **DEVOPS**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. A continuación, pulse **Gestionar**. Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**. A continuación, pulse **Gestionar**.  
1. Pulse el enlace de su organización. 
1. En la página Gestionar organizaciones, pulse **Invitar a usuario** y escriba la dirección de correo electrónico del usuario.
1. Si desea conceder permisos avanzados para gestionar usuarios en organizaciones de {{site.data.keyword.Bluemix_notm}}, seleccione una o varias de las casillas **Gestor**, **Gestor de facturación** o **Auditor**.
1. Pulse **INVITAR**.
1. Pulse **GUARDAR**.

## Supresión de una cadena de herramientas
{: #deleting_a_toolchain_dedicated}

Puede suprimir una cadena de herramientas y especificar cuál de las integraciones de herramientas asociadas desea suprimir. Cuando se suprime una cadena de herramientas, la supresión no se puede deshacer.

1. En el panel de control, en la pestaña **DEVOPS**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. A continuación, pulse **Gestionar**. Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**. A continuación, pulse **Gestionar**.
1. Pulse **Suprimir cadena de herramientas** y revise o ajuste las integraciones de herramientas que se está suprimiendo.
1. Confirme la supresión escribiendo el nombre de la cadena de herramientas y pulsando **Suprimir**.

 **Consejo**: cuando suprima una integración de herramientas GitHub Enterprise, el repositorio de GitHub Enterprise asociado no se suprimirá de GitHub Enterprise. Debe eliminar manualmente el repositorio de GitHub Enterprise.
