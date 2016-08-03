---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilización de cadenas de herramientas
{: #toolchains-using}

*Última actualización: 4 de mayo de 2016*
{: .last-updated}

Puede utilizar una cadena de herramientas para que sea productiva en su trabajo diario de desarrollo, despliegue y operaciones. Una vez que se ha configurado una cadena de herramientas, es posible añadir, eliminar o configurar integraciones de herramientas y gestionar el acceso a la cadena de herramientas.
{: shortdesc}

**Importante**: esta capacidad es experimental. Es posible que las cadenas de herramientas no sean estables y que cambien de tal modo que no sean compatibles con versiones anteriores. No se recomienda su uso en entornos de producción. Para utilizar cadenas de herramientas, debe realizar una [solicitud única de acceso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}. Las cadenas de herramientas están disponibles únicamente en el sur de EE. UU. 

## Configuración de una integración de herramienta
{: #configuring_a_tool_integration}

Puede configurar una integración de herramienta por primera vez o actualizar los ajustes de la configuración para una integración de herramienta que ya forme parte de su cadena de herramientas. 

1. En el panel de control de DevOps, en la pestaña **Toolchains**, pulse una cadena de herramientas para abrir la página Tool Integrations correspondiente. Como alternativa, en la página de visión general de la app, en el título Continuous Delivery, pulse **View Toolchain** y, a continuación, pulse **Tool Integrations**.
1. Si necesita configurar una integración de herramienta por primera vez, en su título, pulse **Configure**.

  ![Botón de configuración](images/toolchain_tile_configure.png)

 Cuando haya terminado de configurar la integración de la herramienta, pulse **Save Integration**.
 
1. Si necesita actualizar la configuración de una integración de herramienta, en su título, pulse el menú para acceder a las opciones de configuración. 

  ![Menú de configuración](images/toolchain_tile_menu.png)
 
 Cuando haya terminado de configurar los ajustes, pulse **Save Integration**.

 **Nota**: una vez que haya configurado el repositorio para la integración de una herramienta GitHub, el URL del repositorio podrá actualizarse, pero no podrá modificar el repositorio. Para utilizar otro repositorio, elimine la integración de herramienta GitHub actual de su cadena de herramientas, añada una integración de la herramienta GitHub a su cadena de herramientas y configure dicha integración para utilizar el nuevo repositorio. 

## Adición de una integración de herramienta
{: #adding_a_tool_integration}

Puede añadir y configurar integraciones de herramientas para su cadena de herramientas. 

1. En el panel de control de DevOps, en la pestaña **Toolchains**, pulse una cadena de herramientas para abrir la página Tool Integrations correspondiente. Como alternativa, en la página de visión general de la app, en el título Continuous Delivery, pulse **View Toolchain** y, a continuación, pulse **Tool Integrations**.
1. Para ver una lista de las integraciones de herramientas que se deben añadir, pulse el botón de adición (+).
1. Pulse en la integración de herramientas que desee añadir. 
1. Introduzca la información necesaria para configurar la integración de la herramienta.  
1. Pulse **Create Integration** para añadir la integración de la herramienta en su cadena de herramientas. 

## Eliminación de una integración de herramienta
{: #deleting_a_tool_integration}

Puede eliminar una integración de herramienta de su cadena de herramientas.  

1. En el panel de control de DevOps, en la pestaña **Toolchains**, pulse una cadena de herramientas para abrir la página Tool Integrations correspondiente. Como alternativa, en la página de visión general de la app, en el título Continuous Delivery, pulse **View Toolchain** y, a continuación, pulse **Tool Integrations**.
1. En el título de la integración de herramienta que desea eliminar, pulse el menú para acceder a las opciones de configuración. 
1. Para eliminar la integración de herramienta de su cadena de herramientas, pulse **Delete**.
1. Confirme la acción pulsando **Delete**.

## Gestión del acceso
{: #managing_access}

Puede conceder acceso a los usuarios a una cadena de herramientas si los añade a la organización con la que está asociada la cadena de herramientas. Cada cadena de herramientas está asociada con una organización específica, y cualquier usuario que sea miembro de dicha organización puede acceder a las cadenas de herramientas asociadas. Si cambia de organización, puede acceder a un conjunto de cadenas de herramientas distinto. 

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. En el panel de control de DevOps, en la pestaña **Toolchains**, pulse la cadena de herramientas que desee gestionar y pulse **Manage**. Como alternativa, en la página de visión general de la aplicación, en el título Continuous Delivery, pulse **View Toolchain** y luego pulse **Manage**.  
1. Pulse el enlace de su organización.  
1. En la página Manage Organizations, pulse **Invite a User** y escriba la dirección de correo electrónico del usuario.
1. Si desea conceder permisos avanzados al usuario, seleccione las casillas **Manager**, **Billing Manager** o **Auditor** que corresponda. 
1. Pulse **INVITE**.
1. Pulse **SAVE**.

## Eliminación de una cadena de herramientas
{: #deleting_a_toolchain}

Puede eliminar una cadena de herramientas y especificar qué integraciones de herramienta asociadas desea eliminar. 

1. En el panel de control de DevOps, en la pestaña **Toolchains**, pulse la cadena de herramientas que desee eliminar y pulse **Manage**. Como alternativa, en la página de visión general de la aplicación, en el título Continuous Delivery, pulse **View Toolchain** y luego pulse **Manage**.
1. Pulse **Delete Toolchain** y revise las integraciones de herramientas que se dispone a eliminar. 
1. Para confirmar la eliminación, escriba el nombre de la cadena de herramientas y pulse **Delete**.

 **Consejo**: cuando elimine la integración de una herramienta GitHub, el repositorio de GitHub asociado no se eliminará de GitHub. Deberá eliminar el repositorio manualmente. 
