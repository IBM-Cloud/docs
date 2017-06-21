---

copyright:

  years: 2015, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestión de organizaciones 
Como propietario de una cuenta o como un gestor de una organización, puede realizar tareas de gestión de la organización como, por ejemplo, cambiar el nombre de la misma, suprimir la organización, suprimir un espacio, actualizar la organización, actualizar roles de espacio y gestionar dominios o cuotas.
{:shortdesc}

Desde la barra de menús, pulse **Gestionar > Cuenta > Organizaciones** para gestionar sus organizaciones.  

**Nota:** Solo puede ver los recursos de una organización a la vez. Si es miembro de varias organizaciones, puede conmutar entre organizaciones desde el enlace de preferencias de cuenta de usuario en la barra de menús de la consola. 

## Cambiar el nombre de las organizaciones
{: #orgrename}

Siga los pasos siguientes para cambiar el nombre de la organización:
1. Pulse **Gestionar** > **Cuenta** > **Organizaciones**.
2. Identifique la organización que desea renombrar y pulse **Ver detalles**.
3. Pulse **Editar organización**.
4. Pulse **Editar** junto al nombre de la organización. 
5. Escriba el nuevo nombre de la organización, y pulse **Guardar**.

## Supresión de organizaciones y espacios
{: #deleteorgs}

Como propietario de la cuenta, póngase en contacto con el [equipo de soporte de {{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} para suprimir una organización.

**Nota**: La supresión de operaciones no se puede revertir. Perderá todas las apps y los servicios asociados a la organización. 

Siga estos pasos para suprimir una organización o un espacio: 
1. Pulse **Gestionar** > **Cuenta** > **Organizaciones**.
2. Identifique la organización que desea editar y pulse **Ver detalles**.
3. Identifique el espacio que desea suprimir y pulse **Editar espacio**.
4. Pulse **Suprimir espacio**.

## Edición de roles de usuario
{: #listmembers}

Siga los siguientes pasos para editar los roles de usuario de una organización específica: 
1. Pulse **Gestionar** &gt; **Cuenta** &gt; **Organizaciones**.
2. Identifique la organización para la que desea ver los miembros y pulse **Ver detalles**.
3. Pulse **Editar organización**.
4. Puede ver los miembros de su organización y sus roles en el separador **USUARIOS**.

Siga los siguientes pasos para editar los roles de usuario de un espacio específico: 
1. Pulse **Gestionar** &gt; **Cuenta** &gt; **Organizaciones**.
2. Identifique la organización para la que desea ver los miembros y pulse **Ver detalles**.
3. Identifique el espacio para el que desea ver los miembros y pulse **Editar espacio**.
4. Puede ver los miembros de su espacio y sus roles en el separador **USUARIOS**.

## Gestión de cuota
{: #managequota}

Como propietario de cuenta o gestor de organización de {{site.data.keyword.Bluemix_notm}}, puede ver la cuota utilizada y asignada para una organización. La cuota representa los límites de recursos para la organización que está asignada cuando se crea la organización. Según si tiene una cuenta de prueba o una cuenta facturable, los recursos que están disponibles para una organización varían. Cualquier aplicación o servicio de un espacio de la organización contribuye al uso de la cuota asignada.

Para ver la cuota utilizada y asignada a una organización, realice los pasos siguientes:
1. Pulse **Gestionar** &gt; **Cuenta** &gt; **Organizaciones**.
2. Identifique la organización para la que desea ver la cuota y pulse **Ver detalles**.
3. Pulse **Editar organización**.
4. Si tiene espacios definidos en más de una región, seleccione la región específica que desee ver.
5. Pulse **CUOTA**. 
6. De forma predeterminada, se abrirá la página de cuota de **Cloud Foundry**. Puede ver los detalles de la cuota para los siguientes recursos:
 * MEMORIA
 * SERVICIOS
 * PLAN
 * PRECIO
7. Pulse **Contenedores** para ver la asignación de cuota de contenedor utilizada y disponible. La asignación de contenedor varía en función del plan de precios. Puede ver los detalles de la cuota para los siguientes recursos:
 * MEMORIA
 * IP PÚBLICA
 * COMPARTICIONES DE ARCHIVOS
8. Pulse **Servidores virtuales** para ver las máquinas virtuales.

**Nota:** Los contenedores no están disponibles en la región Sídney de {{site.data.keyword.Bluemix_notm}}. 

Para obtener más información sobre los contenedores, consulte [Cuota](/docs/containers/container_planning.html#container_planning_quota) en la documentación de Contenedores.
Para cambiar la cuota asignada para una organización, debe abrir una incidencia de soporte. Para obtener más información sobre la apertura de una incidencia de soporte, consulte [Obtención de soporte al cliente](/docs/support/index.html#contacting-support). 

## Gestión de dominios
{: #managedomains}

Como propietario de cuenta o gestor de organización, puede ver el dominio del sistema y añadir dominios personalizados para aplicaciones que están incluidas dentro una organización y sus espacios. Como gestor de espacios, el separador **Dominios** para un espacio es una lista de solo lectura de los dominios asignados al espacio.

1. Pulse **Gestionar** &gt; **Cuenta** &gt; **Organizaciones**.
2. Identifique la organización para la que desea ver o editar los dominios.
3. Seleccione **Ver detalles** para esa organización.
4. Pulse **Editar organización**.
5. Pulse **DOMINIOS**.

Si añade un dominio personalizado, debe configurar el servidor DNS para resolver el dominio personalizado para que apunte al dominio del sistema de {{site.data.keyword.Bluemix_notm}}. De este modo, cuando {{site.data.keyword.Bluemix_notm}} recibe una solicitud para el dominio personalizado, puede direccionarlo correctamente a la app. El dominio del sistema siempre está disponible en un espacio y también se pueden asignar dominios personalizados a un espacio. Las apps creadas en un espacio pueden utilizar cualquiera de los dominios listados para ese espacio. Para obtener más información sobre cómo crear y utilizar dominios personalizados, consulte [Utilización de un dominio personalizado](/docs/manageapps/updapps.html#domain).
