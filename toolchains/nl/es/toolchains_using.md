---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Uso de cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} público
{: #toolchains-using}

*Última actualización: 12 de agosto de 2016*
{: .last-updated}

Puede utilizar una cadena de herramientas para ser productivo en sus actividades diarias de desarrollo, despliegue y operaciones. Tras configurar una cadena de herramientas, puede añadir, suprimir o configurar integraciones de herramientas y gestionar el acceso a la cadena de herramientas.
{: shortdesc}

**Importante**: esta funcionalidad es experimental. Las cadenas de herramientas pueden no ser estables y es posible que cambien de modo que no sean compatibles con versiones anteriores. No se recomienda utilizarlas en entornos de producción. Las cadenas de herramientas están disponibles solo en la región EE.UU. sur.

## Configuración de una integración de herramientas
{: #configuring_a_tool_integration}

Si ha aplazado la configuración de una integración de herramientas al crear una cadena de herramientas, se mostrará un botón **Configurar** en el mosaico correspondiente. Si ha configurado una integración de herramientas al crear una cadena de herramientas, puede actualizar los valores de configuración.

1. En el panel de control de DevOps, en la pestaña **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Integraciones de herramientas**.
1. Si necesita configurar una integración de herramientas por primera vez, en el mosaico correspondiente, pulse **Configurar**.

  ![Botón Configurar](images/toolchain_tile_configure.png)

 Cuando haya terminado de configurar la integración de herramientas, pulse **Guardar integración**.
 
1. Si necesita actualizar la configuración de una integración de herramientas, en el mosaico correspondiente, pulse el menú para acceder a las opciones de configuración.

  ![Menú de configuración](images/toolchain_tile_menu.png)
 
 Cuando haya terminado de actualizar los valores, pulse **Guardar integración**.

## Adición de una integración de herramientas
{: #adding_a_tool_integration}

Puede añadir y configurar las integraciones de herramientas para su cadena de herramientas.

1. En el panel de control de DevOps, en la pestaña **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Integraciones de herramientas**.
1. Para ver una lista de integraciones para añadir, pulse el botón (+).
1. Pulse una integración de herramientas que desee añadir.
1. Indique la información necesaria para configurar la integración de herramientas. 
1. Pulse **Crear integración** para añadir la integración de herramientas a su cadena de herramientas.

## Supresión de una integración de herramientas
{: #deleting_a_tool_integration}

Si suprime una integración de herramientas de la cadena de herramientas, la supresión no se puede deshacer. 

1. En el panel de control de DevOps, en la pestaña **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Integraciones de herramientas**.
1. En el mosaico de la integración de herramientas que desea suprimir, pulse el menú para acceder a las-opciones de configuración.
1. Para suprimir la integración de herramientas de la cadena de herramientas, pulse **Suprimir**.
1. Confirme pulsando **Suprimir**.  

## Gestión de acceso
{: #managing_access}

Puede conceder a los usuarios acceso a una cadena de herramientas añadiéndolos a la organización (org) con la que está asociada la cadena de herramientas. Cada cadena de herramientas está asociada con una organización específica y cualquier usuario que sea miembro de la organización en cuestión puede acceder a las cadenas de herramientas asociadas. Pulse el icono **{{site.data.keyword.avatar}}** ![icono Avatar](../icons/i-avatar-icon.svg) en la barra de menús para abrir el widget Cuenta y soporte y ver la organización con la que está trabajando actualmente. Cambie de organización para acceder a otro conjunto de cadenas de herramientas.

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. En el panel de control de DevOps, pestaña **Cadenas de herramientas**, pulse la cadena de herramientas que se gestionará y, a continuación, pulse **Gestionar**. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Gestionar**.  
1. Pulse el enlace de su organización. 
1. En la página Gestionar organizaciones, pulse **Invitar a usuario** y escriba la dirección de correo electrónico del usuario.
1. Si desea conceder permisos avanzados para gestionar usuarios en organizaciones de {{site.data.keyword.Bluemix_notm}}, seleccione una o varias de las casillas **Gestor**, **Gestor de facturación** o **Auditor**.
1. Pulse **INVITAR**.
1. Pulse **GUARDAR**.

## Supresión de una cadena de herramientas
{: #deleting_a_toolchain}

Puede suprimir una cadena de herramientas y especificar cuál de las integraciones de herramientas asociadas desea suprimir. Cuando se suprime una cadena de herramientas, la supresión no se puede deshacer.

1. En el panel de control de DevOps, pestaña **Cadenas de herramientas**, pulse la cadena de herramientas que se suprimirá y, a continuación, pulse **Gestionar**. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas** y, a continuación, **Gestionar**.
1. Pulse **Suprimir cadena de herramientas** y revise o ajuste las integraciones de herramientas que se está suprimiendo.
1. Confirme la supresión escribiendo el nombre de la cadena de herramientas y pulsando **Suprimir**.  

 **Consejo**: cuando suprima una integración de herramientas GitHub, el repositorio de GitHub asociado no se suprimirá de GitHub. Debe eliminar manualmente el repositorio de GitHub.
