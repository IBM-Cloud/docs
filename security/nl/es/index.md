---

 

copyright:

  years: 2014, 2017
  
lastupdated: "2017-01-11"

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Seguridad de {{site.data.keyword.Bluemix_notm}}
{: #security}

Diseñada con prácticas de ingeniería seguras, la plataforma {{site.data.keyword.Bluemix}} dispone de controles de seguridad de varios niveles de la red y de la infraestructura. {{site.data.keyword.Bluemix_notm}} ofrece una serie de servicios de seguridad que pueden utilizar los desarrolladores de apps para proteger sus apps móviles y web. Estos elementos se combinan para convertir {{site.data.keyword.Bluemix_notm}} en una plataforma con opciones claras para el desarrollo de apps seguras.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} garantiza la seguridad mediante el cumplimiento con las políticas de seguridad derivadas de prácticas recomendadas en IBM para sistemas, redes e ingeniería segura. Estas políticas incluyen prácticas como exploración de código, exploración dinámica, modelado de amenazas y pruebas de penetración. {{site.data.keyword.Bluemix_notm}} sigue el proceso IBM Product Security Incident Response Team (PSIRT) en cuanto a la gestión de incidentes relacionados con la seguridad. Consulte el sitio [IBM Security Vulnerability Management (PSIRT)![icono de enlace externo](../icons/launch-glyph.svg)](http://www-03.ibm.com/security/secure-engineering/process.html){: new_window} para ver detalles.

{{site.data.keyword.Bluemix_notm}} público y dedicado utiliza los servicios de nube de {{site.data.keyword.BluSoftlayer}} Infrastructure-as-a-Service (IaaS) y aprovecha su arquitectura de seguridad. {{site.data.keyword.BluSoftlayer}} IaaS proporciona varias capas de protección solapadas para sus apps y datos. En {{site.data.keyword.Bluemix_notm}} local, usted es el propietario de la seguridad física y proporciona
la infraestructura alojando {{site.data.keyword.Bluemix_notm}} local en su propio centro de datos detrás de un cortafuegos de la empresa. Además, {{site.data.keyword.Bluemix_notm}} incorpora funciones de seguridad en la capa de Plataforma como servicio en distintas categorías: plataforma, datos y app.

## Seguridad de la plataforma {{site.data.keyword.Bluemix_notm}}
{: #platform-security}

{{site.data.keyword.Bluemix_notm}} proporciona seguridad funcional, de infraestructura, operativa y física para la plataforma (a través de {{site.data.keyword.BluSoftlayer}}) para la plataforma principal. Sin embargo, {{site.data.keyword.Bluemix_notm}} local es exclusivo en el sentido de que el cliente proporciona la infraestructura y el centro de datos, a la vez que es propietario de la seguridad física.

El entorno {{site.data.keyword.Bluemix_notm}} en {{site.data.keyword.BluSoftlayer}} cumple con los estándares de seguridad de tecnología de la información (TI) más restrictivos de IBM, que se ajustan o superan los estándares del sector. Estos estándares incluyen lo siguiente:
Red, cifrado de datos y control de acceso
 * ACL de aplicación, permisos y pruebas de penetración
 * Identificación, autenticación y autorización
 * Información y protección de datos
 * Integridad y disponibilidad de servicios
 * Gestión de puntos vulnerables y de arreglos
 * Denegación de servicio y detección de ataques sistemáticos
 * Respuesta ante incidencias de seguridad

![Visión general de la seguridad de la plataforma Bluemix](images/platform_sec.svg)

Figura 1. Visión general de seguridad de la plataforma {{site.data.keyword.Bluemix_notm}}

Con {{site.data.keyword.Bluemix_notm}} local, puede alojar {{site.data.keyword.Bluemix_notm}} detrás del cortafuegos de la empresa y en el centro de datos. Por lo tanto, usted es responsable de determinados aspectos de seguridad. La imagen siguiente detalla las partes de seguridad que son propiedad del cliente y las partes de seguridad que gestiona y mantiene IBM.

![Visión general de la seguridad de la plataforma Bluemix Local](images/security_local_platform.svg)

Figura 2. Visión general de seguridad de la plataforma {{site.data.keyword.Bluemix_notm}} Local

IBM instala, supervisa de forma remota y gestiona {{site.data.keyword.Bluemix_notm}} local en el centro de datos mediante Relay (relé), una funcionalidad de entrega incluida con {{site.data.keyword.Bluemix_notm}} local. El relé se conecta de forma segura con certificados específicos de cada instancia de {{site.data.keyword.Bluemix_notm}} local. Para obtener más información sobre {{site.data.keyword.Bluemix_notm}} local y Relay, consulte [Bluemix local](/docs/local/index.html).

### Seguridad funcional

{{site.data.keyword.Bluemix_notm}} proporciona diversas funciones de seguridad funcional, que incluyen autenticación de usuarios, autorización de accesos, auditoría de operaciones críticas y protección de datos.

<dl>
<dt>Autenticación</dt>
<dd>Los desarrolladores de aplicaciones se autentican ante {{site.data.keyword.Bluemix_notm}} mediante la identidad web de IBM.

Para {{site.data.keyword.Bluemix_notm}} dedicado y local, la autenticación a través LDAP recibe soporte de forma predeterminado. A petición, se puede configurar la autenticación a través de IBM Web Identity en lugar de para {{site.data.keyword.Bluemix_notm}}.
</dd>

<dt>Autorización</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utiliza mecanismos de Cloud Foundry para asegurarse de que cada desarrollador de apps tiene acceso únicamente a las apps e instancias de servicio que ha creado. La autorización sobre los servicios de {{site.data.keyword.Bluemix_notm}} se basa en OAuth. El acceso a los puntos finales internos de la plataforma {{site.data.keyword.Bluemix_notm}} está restringido para los usuarios externos.</dd>

<dt>Auditoría</dt>
<dd>Se crean registros de auditoría sobre todos los intentos correctos o erróneos de autenticación por parte de los desarrolladores de apps. También se crean registros de auditoría sobre el acceso privilegiado a los sistemas Linux que alojan los contenedores donde se ejecutan las apps {{site.data.keyword.Bluemix_notm}}.</dd>

<dt>Protección de los datos</dt>
<dd> Todo el tráfico de {{site.data.keyword.Bluemix_notm}} pasa por IBM WebSphere® DataPower® SOA Appliances, que ofrece funciones de proxy inverso, terminación de SSL y equilibrio de cargas.
Se permiten los siguientes métodos HTTP:
<ul>
<li>DELETE</li>
<li>GET</li>
<li>HEAD</li>
<li>OPTIONS</li>
<li>POST</li>
<li>PUT</li>
<li>TRACE</li>
</ul>
 La inactividad de HTTP supera el tiempo de espera transcurridos 2 minutos.</dd>
<dd>DataPower rellena las siguientes cabeceras:
<dl>
<dt>$wsis</dt>
<dd>Se establece en true si la conexión del lado del cliente es segura (HTTPS); de lo contrario, se establece en false.</dd>
<dt>$wssc</dt>
<dd>Se establece en uno de los siguientes esquemas de conexión de cliente: https, http, ws o wss.</dd>
<dt>$wssn</dt>
<dd>Se establece en el nombre de host que envía el cliente.</dd>
<dt>$wssp</dt>
<dd>Se establece en el puerto del servidor al que se conecta el cliente.</dd>
<dt>x-client-ip</dt>
<dd>Se establece en la dirección IP del cliente.</dd>
<dt>x-forwarded-proto</dt>
<dd>Se establece en uno de los siguientes esquemas de conexión de cliente: https, http, ws o wss.</dd>
</dl>
</dd>

<dt>Prácticas de desarrollo seguro</dt>
<dd> En {{site.data.keyword.Bluemix_notm}} Público y Dedicado, se realizan exploraciones periódicas de vulnerabilidad de seguridad en diversos componentes de {{site.data.keyword.Bluemix_notm}} mediante IBM Security AppScan® Dynamic Analyzer. Se realizan pruebas de modelado de amenazas y penetración a fin de detectar y solucionar cualquier posible vulnerabilidad para todos los tipos de despliegues de {{site.data.keyword.Bluemix_notm}}. Además, los desarrolladores de apps pueden utilizar el servicio AppScan Dynamic Analyzer para proteger sus apps web desplegadas en {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

### Seguridad de la infraestructura

{{site.data.keyword.Bluemix_notm}} se basa en Cloud Foundry para ofrecer una base robusta en la que ejecutar sus apps. Dentro de la arquitectura, se ofrecen diversos componentes que proporcionan funciones de seguridad y aislamiento. Además se implementan procedimientos de gestión de cambios y de copia de seguridad y recuperación para garantizar la integridad y la disponibilidad.

<dl>
<dt>Segregación del entorno</dt>
<dd> En {{site.data.keyword.Bluemix_notm}} público, los entornos de desarrollo y de producción se han separado para mejorar la estabilidad y la seguridad de las apps.</dd>

<dt>Cortafuegos</dt>
<dd> Se han colocado cortafuegos para restringir el acceso a la red {{site.data.keyword.Bluemix_notm}}. En {{site.data.keyword.Bluemix_notm}}
local, el cortafuegos de su empresa segrega el resto de la red desde la instancia de {{site.data.keyword.Bluemix_notm}}.</dd>

<dt>Protección frente a intrusiones</dt>
<dd>{{site.data.keyword.Bluemix_notm}} público y dedicado permiten la protección frente a intrusiones con el fin de descubrir amenazas para que se puedan solucionar. En los cortafuegos se han activado políticas de protección frente a intrusiones.</dd>

<dt>Gestión segura de contenedores de apps</dt>
<dd>Cada app {{site.data.keyword.Bluemix_notm}} está aislada y se ejecuta en su propio contenedor, que tiene límites específicos de recursos de procesador, memoria y disco.</dd>

<dt>Refuerzo de la seguridad del sistema operativo</dt>
<dd>Los administradores de IBM realizan de forma regular operaciones de refuerzo del sistema operativo y de la red mediante herramientas como IBM punto final Manager.</dd>
</dl>

### Seguridad operativa

{{site.data.keyword.Bluemix_notm}} proporciona un sólido entorno de seguridad operativa con los controles siguientes.

<dl>
<dt>Exploración de vulnerabilidades</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utiliza la herramienta de exploración de vulnerabilidades
Tenable Network Security,
Nessus, para detectar cualquier problema en la configuración de la red y del host a fin de solucionar posibles problemas.</dd>

<dt>Gestión de arreglos automáticos</dt>
<dd>Los administradores de {{site.data.keyword.Bluemix_notm}} garantizan que los sistemas operativos se aplican en frecuencias adecuadas. Los arreglos automáticos se activan mediante IBM Endpoint Manager.</dd>

<dt>Análisis y consolidación de registros de auditoría</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utiliza las herramientas IBMSecurity QRadar® para consolidar los registros de Linux a fin de gestionar el acceso con privilegios en sistemas Linux. {{site.data.keyword.Bluemix_notm}} también utiliza la información de seguridad y gestión de sucesos (SIEM) de IBM QRadar para supervisar los intentos correctos y erróneos de inicio de sesión de los desarrolladores de apps.</dd>

<dt>Gestión de accesos de usuario</dt>
<dd>Dentro de {{site.data.keyword.Bluemix_notm}}, se siguen directrices de separación de responsabilidades para asignar a los usuarios privilegios de acceso granulares y para garantizar que los usuarios solo tienen el acceso que necesitan para realizar su trabajo según el principio de privilegio menor.

En los entornos {{site.data.keyword.Bluemix_notm}} dedicado y local, los administradores asignados pueden gestionar roles y permisos para los usuarios de {{site.data.keyword.Bluemix_notm}} en su organización mediante la Consola de administración. Consulte [Gestión de {{site.data.keyword.Bluemix_notm}}](/docs/admin/adminpublic.html#mng) para obtener más detalles.
</dd>
</dl>

### Seguridad física

{{site.data.keyword.Bluemix_notm}} público y dedicado se basan en la topología de red dentro de red de {{site.data.keyword.BluSoftlayer}} para la seguridad de la red física. Esta arquitectura de red dentro de red garantiza que sólo el personal autorizado pueda acceder a los sistemas. En {{site.data.keyword.Bluemix_notm}} local, usted es
el propietario de la seguridad física de la instancia local. El centro de datos está protegido detrás del cortafuegos de la compañía.

En la topología de red dentro de red de {{site.data.keyword.BluSoftlayer}}, la capa de red pública controla el tráfico público a los sitios web alojados o a los recursos en línea. La capa de red privada permite una verdadera gestión fuera de banda a través de un operador autónomo sobre SSL, PPTP o pasarelas IPSec VPN. La capa de red entre centros de datos proporciona conectividad segura y gratuita entre servidores distribuidos en distintas instalaciones de {{site.data.keyword.BluSoftlayer}}.

Cada centro de datos de {{site.data.keyword.BluSoftlayer}} está completamente protegido mediante controles que se ajustan, sin excepción, a los requisitos reconocidos por el sector y a los requisitos de SSAE 16.

## Seguridad de los datos
{: #data-security}

Con {{site.data.keyword.Bluemix_notm}}, proteger sus datos frente a un acceso no autorizado constituye un esfuerzo conjunto entre {{site.data.keyword.Bluemix_notm}} y usted.

Los datos que asociados a una app en ejecución pueden estar en uno de estos tres estados: data-in-transit (datos en tránsito), data-at-rest (datos en reposo) y data-in-use (datos en uso).

<dl>
<dt>Data-in-transit</dt>
<dd>Datos que se están transfiriendo entre nodos de una red.</dd>

<dt>Data-at-rest</dt>
<dd>Datos que están almacenados.</dd>

<dt>Data-in-use</dt>
<dd>Datos que actualmente no están almacenados y sobre los que se está actuando en un punto final.</dd>
</dl>

Hay que tener en cuenta cada tipo de datos al planificar la seguridad de los datos.

La plataforma {{site.data.keyword.Bluemix_notm}} preserva los datos
data-in-transit protegiendo el acceso del usuario final a la app mediante SSL, a través de la red hasta que los datos alcanzan IBM
DataPower Gateway en el límite de la red interna de {{site.data.keyword.Bluemix_notm}}. IBM DataPower Gateway actúa como proxy inverso y ofrece terminación de SSL. Desde ese punto a la aplicación, IPSEC se utiliza para proteger los datos a medida que viajan de IBM DataPower Gateway a la aplicación.

La seguridad de los datos de tipo data-in-use y data-at-rest es responsabilidad del usuario, que es quien desarrolla la app. Puede aprovechar los diversos servicios relacionados con datos disponibles en el Catálogo de {{site.data.keyword.Bluemix_notm}} para ayudarle con este tema.

## Seguridad de las apps de {{site.data.keyword.Bluemix_notm}}
{: #application-security}

Como desarrollador de apps, debe habilitar las configuraciones de seguridad, incluida la protección de los datos de la app, para las apps que se ejecutan en {{site.data.keyword.Bluemix_notm}}.

Puede utilizar las funciones de seguridad que proporcionan diversos servicios de {{site.data.keyword.Bluemix_notm}} para proteger las apps. Todos los servicios de {{site.data.keyword.Bluemix_notm}} que genera IBM siguen las recomendaciones de desarrollo de ingeniería segura de IBM.

**Nota:** Algunos de los servicios que se describen aquí puede que no se apliquen a las instancias dedicadas o locales de {{site.data.keyword.Bluemix_notm}}.

### Servicio SSO

IBM Single Sign On for {{site.data.keyword.Bluemix_notm}} es un servicio de autenticación basado en política que ofrece capacidad de inicio de sesión único de fácil incorporación para
Node.js o Liberty para apps Java™. Para permitir que un desarrollador de apps pueda incluir la capacidad de inicio de sesión único en una app, el administrador crea instancias de servicio y añade orígenes de identidad.

El servicio Single Sign On da soporte a varios orígenes de identidad donde se almacenan las credenciales de los usuarios:

<dl>
<dt>SAML Enterprise</dt>
<dd>Un registro de usuario con intercambio de señales SAML que completa la autenticación.</dd>

<dt>Directorio de nube</dt>
<dd>Un registro de usuario que está alojado en IBM Cloud.</dd>

<dt>Orígenes de identidad social</dt>
<dd> Los registros de usuarios que mantienen Google, Facebook y LinkedIn.</dd>
</dl>

Para obtener más información, consulte [Guía de iniciación a Single Sign On](/docs/services/SingleSignOn/index.html).

### Seguridad de aplicaciones en la nube

Este servicio proporciona un análisis de seguridad para apps web y móviles, y le permite explorar el código fuente en busca
de vulnerabilidad de seguridad. Para obtener más información, consulte [Guía de iniciación para seguridad de aplicaciones en la nube](/docs/services/ApplicationSecurityonCloud/index.html).

### Plug-in IBM UrbanCode para la prueba de seguridad de apps

El plug-in IBM Application Security Testing for {{site.data.keyword.Bluemix_notm}} le permite ejecutar exploraciones de seguridad en la web o en las apps Android alojadas en {{site.data.keyword.Bluemix_notm}}. Este plug-in ha sido desarrollado y recibe soporte de IBM UrbanCode™ Deploy Community en la plataforma IBM Bluemix DevOps Services.

Para obtener más información, vaya a [IBM Application Security Testing for Bluemix ![icono de enlace externo](../icons/launch-glyph.svg)](https://developer.ibm.com/urbancode/plugindoc/ibmucd/ibm-application-security-testing-bluemix/1-0/){: new_window}.

### dashDB

El servicio de dashDB utiliza un servidor LDAP incorporado para la autenticación de usuario. La conexión entre
las apps y la base de datos está protegida mediante certificados SSL. Este servicio utiliza la capacidad de cifrado nativo de DB2® para cifrar de forma automática la base de datos desplegada y las copias de seguridad de la base de datos. La rotación de claves maestras se ejecuta automáticamente cada 90 días.

Para obtener más información, consulte [Guía de iniciación a dashDB](/docs/services/dashDB/index.html).

### Secure Gateway

El servicio Secure Gateway le permite conectar de forma segura apps {{site.data.keyword.Bluemix_notm}} con ubicaciones remotas, tanto locales como en la nube. Proporciona conectividad segura y establece un túnel entre la organización {{site.data.keyword.Bluemix_notm}} y la ubicación remota a la que desea conectarse. Puede configurar y crear una pasarela segura mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} o un paquete de API.

Para obtener más información, consulte [Guía de iniciación a Secure Gateway](/docs/services/SecureGateway/secure_gateway.html).

### Información sobre seguridad y gestión de sucesos

Puede utilizar las herramientas de información de seguridad y gestión de sucesos (SIEM) para analizar las alertas de seguridad en los registros de app. Una de ellas es IBM Security QRadar&reg; SIEM, que proporciona inteligencia y seguridad en entornos de nube. Para obtener información, consulte [IBM QRadar Security Intelligence Platform ![icono de enlace externo](../icons/launch-glyph.svg)](http://www-01.ibm.com/support/knowledgecenter/SS42VS/welcome?lang=en){: new_window}.

## Despliegue de la seguridad de {{site.data.keyword.Bluemix_notm}}
{: #security-deployment}

La arquitectura de despliegue de seguridad de {{site.data.keyword.Bluemix_notm}} incluye distintos flujos de información para los usuarios y desarrolladores de apps para garantizar un acceso seguro.

![Arquitectura de despliegue de seguridad de Bluemix](images/sec_deployment.svg)

Figura 3. Arquitectura de despliegue de seguridad de Bluemix

Para los usuarios de la app de {{site.data.keyword.Bluemix_notm}} **, el **flujo de usuario de la app** es el siguiente:
 1. A través de un cortafuegos, con prevención de intrusiones y seguridad de la red.
 2. A través de IBM DataPower Gateway, con proxy inverso y proxy de terminación de SSL.
 3. A través del direccionador de la red.
 4. Alcanza el tiempo de ejecución de la app en el agente de ejecución de droplet (DEA).

El *desarrollador de* {{site.data.keyword.Bluemix_notm}} sigue dos flujos principales: para inicio de sesión y para desarrollo y despliegue.
 * El **flujo del desarrollador para inicio de sesión** incluye lo siguiente:
    * Para los desarrolladores que han iniciado una sesión en {{site.data.keyword.Bluemix_notm}} público, el flujo es el siguiente:
      1. A través del servicio IBM Single Sign On.
      2. A través de la identidad web de IBM.
    * Para los desarrolladores que han iniciado una sesión en {{site.data.keyword.Bluemix_notm}} dedicado o local, el flujo se realiza a través de LDAP de empresa.
 * El **flujo de desarrollo y despliegue** es el siguiente:
    1. A través de un cortafuegos, con prevención de intrusiones y seguridad de la red. Esto se aplica únicamente a {{site.data.keyword.Bluemix_notm}} dedicado.
    2. A través de IBM DataPower Gateway, con proxy inverso y proxy de terminación de SSL.
    3. A través del direccionador de la red.
    4. A través de autorización mediante el controlador de nube de Cloud Foundry, para garantizar el acceso solo a las apps e instancias de servicio que ha creado el desarrollador.

Para los *administradores* de {{site.data.keyword.Bluemix_notm}} dedicado y {{site.data.keyword.Bluemix_notm}} local, el **flujo del administrador** es el siguiente:
 1. A través de un cortafuegos, con prevención de intrusiones y seguridad de la red.
 2. A través de IBM DataPower Gateway, con proxy inverso y proxy de terminación de SSL.
 3. A través del direccionador de la red.
 4. Va a la página Administración de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

Además de los usuarios suscritos a estos métodos, un equipo de operaciones de seguridad de IBM autorizado realiza diversas tareas de seguridad operativa, como las siguientes:
 * Exploraciones de vulnerabilidad. En {{site.data.keyword.Bluemix_notm}} local, usted es el propietario de la seguridad física y de las exploraciones que se realicen en el cortafuegos.
 * Gestión de accesos de usuario.
 * Refuerzo del sistema operativo mediante la app periódica de arreglos con IBM Endpoint Manager.
 * Gestión de riesgos con protección frente a intrusiones.
 * Supervisión de la seguridad con QRadar.
 * Informes de seguridad disponibles en la página de administración.

## Conformidad de la seguridad
{: #compliance}

{{site.data.keyword.Bluemix}} proporciona una plataforma de nube segura en la que puede confiar. La conformidad de {{site.data.keyword.Bluemix_notm}} proviene de una plataforma y unos servicios que se compilan en los mejores estándares de seguridad del sector, incluidos ISO 27001 e ISO 27002.
{:shortdesc}

![Cláusula de modelo de protección de datos de la EU](images/icon_eumc.png)  Una **Cláusula modelo de la Unión Europea (EU)** es un acuerdo para proteger datos personales que se transfieren desde la EU o el Espacio Económico Europeo (EEA) a un país tercero. La Cláusula modelo de la EU se firma entre el cliente ubicado en la EU o EEA como el exportador de datos y el procesador de datos de IBM ubicado en un país tercero como el importador de datos. La [Cláusula modelo de la EU de SaaS de IBM ![icono de enlace externo](../icons/launch-glyph.svg)](http://www-01.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ST&infotype=SA&htmlfid=KUJ12408USEN&attachment=KUJ12408USEN.PDF){: new_window} contiene los derechos y obligaciones del exportador y del importador de datos, y los derechos de los asuntos de datos. La Cláusula modelo de la EU de SaaS de IBM garantiza que los datos personales, cuando se procesan en un país tercero, estén bajo protección similar a la protección disponible en la EU o la EEA.

Para los clientes que deseen transferir datos que se originan en el Espacio Económico Europeo para un país fuera del EEA, {{site.data.keyword.Bluemix}} ofrece Cláusulas de modelo europeo en el formulario aprobado por la Comisión Europea y las autoridades de protección de datos de la Unión Europea. Las Cláusulas de modelo europeo garantizan a los clientes europeos que {{site.data.keyword.Bluemix_notm}} dé soporte a las protecciones de privacidad de datos necesarias en cada ubicación del mundo.

![Sistemas de información del sector financiero](images/FISC.gif)  Para banca e instituciones relacionadas con las finanzas de Japón, los sistemas informáticos deben tener procedimientos de seguridad en su lugar basados en las directrices de seguridad del FISC (Center for Financial Industry Information Systems). Las directrices de seguridad de FISC las impone FSA (Japan Financial Services Agency), BOJ (Bank of Japan) y FISC.
 

![ISO 27001/2](images/icon_iso27k1.png) {{site.data.keyword.Bluemix_notm}} tiene certificación bajo los **Estándares 27001 y 27002 de ISO (International Organization for Standardization)**, que definen las mejores prácticas para los procesos de gestión de seguridad de información. ISO 27001 es un estándar de seguridad global ampliamente adoptado que describe los requisitos para los sistemas de gestión de seguridad de información. Proporciona un enfoque sistemático para gestionar la información del cliente y de la empresa en función de evaluaciones de riesgo periódicas. El estándar más reciente, ISO/IEC 27001:2013, lo publicó el 25 de septiembre de 2013 la **International Organization of Standardization (Organización Internacional de Normalización) (ISO) y la International Electrotechnical Commission (Comisión Electrotécnica Internacional) (IEC)** conjuntamente con el subcomité de ISO e IEC. El estándar ISO 27001 especifica los requisitos para establecer, implementar y documentar los ISMS (Information Security Management Systems) y los requisitos para implementar los controles de seguridad, de acuerdo con las necesidades de organizaciones individuales. El estándar ISO 27002 explica cada control de seguridad de ISO 27001 en detalle. La familia de estándares ISO 27000 incorpora un proceso de riesgo de escalado y de evaluación de activos, con el objetivo de salvaguardar la confidencialidad, la integridad y la disponibilidad de la información escrita, oral y electrónica.

Para conseguir la certificación ISO 27001:2013, una empresa debe mostrar que tiene un enfoque sistemático y continuado para gestionar riesgos de seguridad de información que afectan a la confidencialidad, integridad y disponibilidad de la información de la empresa y del cliente. Este estándar hace hincapié en la medida y en la evaluación del rendimiento del Information Security Management System (ISMS) de la organización y también incluye controles relacionados con la seguridad de la información que se basan en los requisitos del sistema y otros requisitos.

{{site.data.keyword.Bluemix_notm}} la audita una empresa de seguridad de terceros y cumple todos los requisitos para ISO 27001: [Bluemix ISO 27001:2013 Certificado de registro ![icono de enlace externo](../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/compliance/Bluemix_ISO27K1_WWCert_2016.pdf){: new_window}.

![PCI DSS](images/icon_pci.png)  Los **Payment Card Industry (PCI) Data Security Standards (DSS)** son un estándar de seguridad de información que está diseñado para proteger los datos de la tarjeta de crédito. PCI DSS se aplica a todas las entidades implicadas en el procesamiento de la tarjeta de pago, incluidos los comerciantes, procesadores, emisores y proveedores de servicio. También se aplica al resto de las entidades que almacenan, procesan o transmiten los datos de los titulares de tarjetas o los datos de autenticación confidenciales.

Si almacena o procesa datos de la tarjeta de crédito, la conformidad y la seguridad de red de Payment Card Industry (PCI) será el principal problema para su negocio. Para asegurar estándares coherentes para los comerciantes, el Payment Card Industry Security Standards Council ha establecido estándares de seguridad de datos de PCI. Estas normas incorporan prácticas recomendadas para proteger los datos de titulares de tarjetas, y a menudo requieren la validación de un Asesor de Servicio Calificado (QSA) externo. IBM ayuda a los clientes a satisfacer sus necesidades de conformidad de PCI proporcionando una Certificación de conformidad (Attestation on Compliance) de un QSA independiente. La Certificación de conformidad se puede utilizar junto con el informe SOC 2 y la certificación ISO 27001 para probar que la infraestructura cumpla los controles de PCI.

{{site.data.keyword.Bluemix}} completa un asesoramiento de PCI DSS anual utilizando un Qualified Security Assessor (QSA) aprobado. {{site.data.keyword.Bluemix_notm}} se revisa como conforme en PCI DSS versión 3.1 en el Service Provider Nivel 1, tal como se describe en [Bluemix PCI DSS AOC ![icono de enlace externo](../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/compliance/IBM_Bluemix_PCI.pdf){: new_window}. Para obtener información y asistencia en la conformidad con PCI DSS para el entorno de {{site.data.keyword.Bluemix_notm}}, póngase en contacto con ventas en [Póngase en contacto con nosotros ![icono de enlace externo](../icons/launch-glyph.svg)](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs){: new_window}.

Los informes de ![SSAE16 SOC1/2/3](images/icon_aicpa.png) **SOC (Service Organization Controls)** definen la evaluación de las principales prácticas de control interno relacionadas con la seguridad, la disponibilidad, la integridad del proceso, la confidencialidad y la privacidad en una organización de servicio. Los informes generados mediante la guía del AICPA (American Institute of Certified Public Accountants) incluyen los elementos siguientes: 
  * Supervisión de la organización
  * Programa de gestión del proveedor
  * Procesos de gobierno corporativo interno y de gestión de riesgos
  * Supervisión de la normativa
 
{{site.data.keyword.Bluemix_notm}} proporciona informes SOC 1, SOC 2 y SOC 3. Para obtener más información, póngase en contacto con el equipo de ventas de [{{site.data.keyword.Bluemix_notm}} sales ![icono de enlace externo](../icons/launch-glyph.svg)](mailto:bmxcert1@us.ibm.com){:new_window}. 


![HIPAA](images/icon_hipaa.png) La Ley de Transferencia y Responsabilidad de Seguro Médico (Health Insurance Portability and Accountability Act, HIPAA), decretada por el Congreso de Estados Unidos en 1996, protege la cobertura de los seguros médicos para los empleados tras perder sus trabajos. HIPAA está regulada e impuesta por la Oficina de derechos civiles (Office of Civil Rights) y el Ministerio de Salud Pública y Bienestar Social (Department of Health and Human Services) de Estados Unidos. HIPAA abarca regulaciones desde la ley de 1996, así como requisitos de privacidad de la ley HITECH (Health Information Technology for Economic and Clinical Health) de 2009. {{site.data.keyword.Bluemix_notm}} cumple todos los requisitos para HIPAA del lado del centro de datos o del proveedor de servicios.

Para obtener más información o ayuda para conseguir, certificar y mantener la conformidad con HIPAA para el entorno Bluemix, póngase en contacto con el equipo de ventas de {{site.data.keyword.Bluemix_notm}} [![icono de enlace externo](../icons/launch-glyph.svg)](mailto:cloudplatform_compliance@us.ibm.com){:new_window}.


![ISO 27017](images/icon_ISO27017.png) ISO/IEC 27017:2015 proporciona las directrices para los controles de seguridad de la información aplicables al suministro y uso de los servicios de nube. Además, proporciona unas instrucciones de implementación para proveedores de servicio en la nube y clientes de servicio en la nube. ISO 27017 proporciona unas instrucciones de implementación para controles relevantes que se especifican en ISO/IEC 27002, así como controles e instrucciones adicionales que se relacionan específicamente con los servicios en la nube.

La alineación de {{site.data.keyword.Bluemix_notm}} con ISO 27017:2015 demuestra que IBM tiene un sistema sofisticado de controles específicos de la nube. Además, muestra un compromiso con ser el mejor en IaaS, localmente y en todo el mundo.


![ISO 27018](images/icon_ISO27018.png) ISO 27018:2014 establece objetivos de control comúnmente aceptados, controles y directrices para implementar medidas para proteger información de identificación personal (Personally Identifiable Information, PII). Estas medidas están de acuerdo con los principios de privacidad de ISO 29100 para el entorno informático en la nube público.

En concreto, ISO 27018:2014 especifica directrices que se basan en ISO 27002. Las directrices tienen en cuenta los requisitos de la normativa para la protección de PII, que pueden ser aplicables dentro del contexto de los entornos de riesgo de seguridad de la información de un proveedor de servicios en la nube públicos.


![Cloud Security Alliance – STAR Registrant](images/icon_CSA.png) Cloud Security Alliance es una organización sin ánimo de lucro con una misión para promover el uso de las prácticas recomendadas para proporcionar control de seguridad en la computación en la nube. Uno de los mecanismos que utiliza la Cloud Security Alliance a la hora de cumplir su misión es el STAR (Security, Trust, and Assurance Registry). STAR es un registro gratuito al que se puede acceder de forma pública que documenta los controles de seguridad proporcionados por varias ofertas de computación en la nube.


![Estándares CJIS](images/icon_CJIS.png) Los Servicios de información de la justicia penal (Criminal Justice Information Systems, CJIS) es un servicio de la Oficina Federal de Investigación del Departamento de Justicia de Estados Unidos. Los servicios de CJIS han creado y publicado una Política de seguridad (CJISD-ITS-DOC-08140-5.4). Esta Política de seguridad contiene requisitos de seguridad de información, directrices y acuerdos mínimos que reflejan el compromiso de las agencias de cumplimiento de leyes y de justicia penal para proteger las fuentes, la transmisión, el almacenamiento y la generación de Información de la justicia penal (Criminal Justice Information, CJI).



### Conformidad de plataforma y servicio
En la tabla siguiente se muestran los servicios de {{site.data.keyword.Bluemix_notm}} que son conformes
para cada uno de los estándares.

|Componentes de {{site.data.keyword.Bluemix_notm}}		|FISC		|ISO 27001	|PCI |SOC 2 Tipo 1		|
|:----------------------|:---------:|:---------:|:---------:|:---------:|
|Plataforma {{site.data.keyword.Bluemix_notm}}		|S			|S	|S	|S	|
|{{site.data.keyword.APIM}}			|S	|S |S	|			|
|{{site.data.keyword.autoscaling}}			|S	|S |S	|			|
|{{site.data.keyword.bigicloudst}}			|S |S |	|S |
|{{site.data.keyword.cloudant}}				|S |S |	|S	|
|{{site.data.keyword.dashdbshort}}			|S	|S	|	|S	|
|{{site.data.keyword.datacshort}}			|S	|S	|S	|			|
|{{site.data.keyword.jazzhub_short}}					|S	|S	|	|			|
|{{site.data.keyword.containerlong}}			|S		|S	|	|			|
|{{site.data.keyword.mql}}				|S	|S	|S	|	 		|
|{{site.data.keyword.SecureGateway}}			|S	|S |	|	 		|
|{{site.data.keyword.sescashort}}     |S |S |S	|  |
{: caption="Table 1. Platform and service compliance" caption-side="top"}

# Enlaces relacionados
{: #rellinks}

## Enlaces relacionados
{: #general}

* [Seguridad IBM SaaS ![icono de enlace externo](../icons/launch-glyph.svg)](http://www.ibm.com/cloud-computing/built-on-cloud/saas-security){: new_window}
* [Guía de iniciación a Single Sign On](/docs/services/SingleSignOn/index.html)
