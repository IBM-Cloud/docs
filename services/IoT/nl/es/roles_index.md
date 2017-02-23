---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Roles de usuario, aplicación y pasarela

Los roles son conjuntos de permisos que se pueden utilizar para otorgar o restringir el acceso a operaciones específicas. Los roles se pueden utilizar para gestionar permisos para grupos de usuarios, aplicaciones y pasarelas.
{:shortdesc}

## Roles de usuario
{: #user_roles}

Puede asignar roles de usuario cuando se añade, invita o registra un usuario al {{site.data.keyword.iot_full}}. También se puede asignar o cambiar los roles de usuario en cualquier momento utilizando el panel de instrumentos de {{site.data.keyword.iot_short_notm}}. Para obtener más información sobre cómo asignar un rol a un usuario, consulte [Gestión de roles de usuario](managing_user_roles.html).

Están disponibles los siguientes roles de usuario estándares:

Rol de usuario | Descripción
------------- | -------------
Administrador | Un rol 'superusuario' que otorga acceso a todas las API relacionadas con el usuario. Los administradores no pueden acceder a operaciones restringidas a dispositivos y aplicaciones.
Operador | Pensado para usuarios de organizaciones frontales. Otorga acceso a la mayoría de las operaciones de organización, operaciones de control de acceso, operaciones de analíticas, operaciones de terceros y operaciones de gestión de riesgos.
Desarrollador | Otorga acceso no restringido a operaciones de dispositivo, operaciones de registro, operaciones de memoria caché, operaciones de historian, operaciones de analíticas y operaciones de servicio de terceros. El rol proporciona acceso limitado a las operaciones de la organización, control de acceso y gestión de riesgos.
Analista | Otorga acceso a las operaciones de analíticas, incluidas la creación, actualización y supresión de reglas, acciones y esquemas.
Lector | El rol de usuario predeterminado. Otorga un acceso limitado a operaciones que están disponibles para todos los usuarios.

Para obtener más información sobre los roles de usuario, consulte [Roles de usuario](reference/roles_access.html).

## Roles de aplicación
{: #application_roles}
Puede asignar roles de aplicación para otorgar o denegar acceso a las aplicaciones a operaciones específicas. Todos los roles de aplicación deniegan el acceso a las siguientes operaciones:

- Todas las operaciones de gestión de riesgos
- Configurar parámetros de almacenamiento
- Configurar proveedores de autenticación
- Crear, actualizar o suprimir configuración de correo electrónico

Están disponibles los siguientes roles de aplicación estándares:

Rol de aplicación | Descripción
------------- | -------------
Estándar | El rol de aplicación predeterminado. Otorga acceso a la mayor parte de las operaciones de las aplicaciones, pero no a las operaciones de usuario o de rol.   
Operaciones | Otorga acceso a la gama más amplia de operaciones, pero deniega el acceso para suscribirse o publicar operaciones.
Programa de fondo de confianza | Está pensado para aplicaciones que no requieren interacción desde el operador de sistemas. Deniega el acceso a las operaciones de gestión de dispositivos, organizaciones, roles o extensión.
Procesador de datos | Está pensado para las aplicaciones que realizan el proceso de analíticas y de datos. Se ha otorgado acceso limitado a las aplicaciones del procesador de datos a operaciones de organizaciones y de usuarios, pero tienen acceso completo a las operaciones de analíticas, incluidas las reglas de creación y de gestión, las reglas, acciones y esquemas.
Visualización | Está pensada para aplicaciones que son responsables de generar visualizaciones de datos. Las aplicaciones de visualización tienen acceso a operaciones activas y almacenadas y a operaciones de panel de instrumentos.
Dispositivo | Pensado para aplicaciones que toman el rol de dispositivos; es decir, que proporcionan un origen de los datos que se envían al {{site.data.keyword.iot_short_notm}} como si se tratara de un dispositivo. Sólo se otorga a las aplicaciones de dispositivo acceso limitado a las operaciones.

Para obtener más información sobre el acceso de las operaciones de los roles de aplicación, consulte [Roles de aplicación](reference/app_roles_access.html).

## Roles de pasarela
{: #gateway_roles}
Las pasarelas tienen un número limitado de roles que rigen la definición de la pasarela y la habilidad de registrar dispositivos en el {{site.data.keyword.iot_short_notm}}.

Están disponibles los siguientes roles de pasarela estándares:

Rol de pasarela | Descripción
------------- | -------------
Estándar | El rol de pasarela predeterminado. Otorga acceso restringido a las operaciones.
Privilegiado | Pensado para pasarelas de confianza y permite a las pasarelas privilegiadas añadir dispositivos al {{site.data.keyword.iot_short_notm}}. Otorga acceso a las operaciones relevantes para añadir, actualizar y gestionar dispositivos y propiedades de dispositivos, pero no tiene acceso a otras operaciones.  

Para obtener más información sobre el acceso de las operaciones de los roles de pasarela, consulte [Roles de pasarela](reference/gateway_roles_access.html).
