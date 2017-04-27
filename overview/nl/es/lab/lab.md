---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud Identity and Access Management (IAM)
{: #iam_overview}

IBM Cloud IAM proporciona una forma segura de gestionar las identidades de usuarios y servicios y el acceso a los recursos para dichas identidades. Puede ver y gestionar usuarios de la cuenta u organización en función de las opciones de acceso que esté autorizado a gestionar. Puede realizar todas las operaciones para usuarios, incluida la invitación y gestión de usuarios y sus roles asignados, y las cuentas u organizaciones, o ambos, a las que pueden acceder. Como propietario de una cuenta, puede gestionar las opciones de acceso de las que usted y los usuarios son miembros, independientemente del rol, en la cuenta actual.

La gestión de identidades incluye: 
 * Gestión de usuarios 
   * crear, suprimir, actualizar información de usuario
   * Gestión de claves de API
   * creación de señales, renovación e intercambio
   * autenticación de identidades de usuario
 * Gestión de ID de servicio
   * crear, suprimir, actualizar información de usuario
   * Gestión de claves de API
   * creación de señales, renovación e intercambio
   * autenticación de identidades de servicio
   
   
La gestión de accesos incluye: 
 * Gestión de políticas
   * crear, suprimir y actualizar políticas
 * Decisiones sobre el acceso a recursos
 
## Visión general de la identidad
{: #identity}

El servicio Cloud IAM Token es un servicio de autenticación para IBM Cloud que se basa en los estándares abiertos especificados por [OAuth 2.0]( https://tools.ietf.org/html/rfc6749), [JWT](https://tools.ietf.org/html/rfc7519), [JWT Profile](https://tools.ietf.org/html/rfc7523) y [JWKS](https://tools.ietf.org/html/rfc7517).

Uno de los objetivos de Token Service es la autenticación de desarrolladores, operadores y administradores de IBM Cloud Platform. Para esta autenticación, Token Service se conecta al sistema IBMid para autenticar usuarios y, en entornos dedicados y locales, se puede conectar a un sistema de autenticación elegido por el cliente como LDAP.  

Para recuperar una señal IAM, puede utilizar tipos de concesión OAuth 2.0 estándar como, por ejemplo, `password`: 
```
curl
    -u "<clientid>:<clientsecret>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=password&username=<IBMid>&password=<IBMid password>
       [&ims_account=<ims account>][&bss_account=<bss account>]
       [&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

Como extensión de OAuth 2.0, debe proporcionar información sobre la cuenta para que la señal sea específica de la cuenta. También puede crear una lista de los distintos tipos de respuesta para obtener señales `UAA` o `IMS` para interacciones con las API de CloudFoundry o las API de IMS. 

Cloud IAM Token Service le permite crear, actualizar, suprimir y utilizar claves de API para los usuarios. Estas claves de API se pueden crear con llamadas de API o con la consola de Bluemix. Para aprovechar una clave de API, se puede utilizar el siguiente tipo de concesión ampliada: 
```
curl
    -u "<clientid>:<clientsecret>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<apikeyvalue>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

La señal resultante se puede utilizar como una recuperada con una concesión de contraseña o inicio de sesión de IU. 

Como variación, Cloud IAM Token Service le permite iniciar la sesión de forma interactiva con la interfaz de usuario. Esto se implementa con el tipo de autorización de OAuth 2.0 `authorization_code`, que también se conoce como `Dance OAuth`, porque genera varias redirecciones de navegadores web durante la fase de autenticación. 

El otro objetivo de Token Service es la posibilidad de crear ID de servicio y claves de API para los ID de servicio. Un ID de servicio es parecido a un "ID funcional" o a un "ID de aplicación" y se utiliza para autenticar frente a servicios, no para representar a un usuario.

Los usuarios pueden crear ID de servicio y enlazarlos a ámbitos como una cuenta de Bluemix, una organización de CloudFoundry o un espacio de CloudFoundry. Este enlace se realiza para dar al ID de servicio un contenedor en el que residir. Este contenedor también define quién puede actualizar y suprimir los ID de servicio y quién puede crear, actualizar, leer y suprimir claves de API asociadas a dicho ID de servicio. Un ID de servicio NO está relacionado con un usuario.

Para comprender mejor cómo se utilizan los ID de servicio, pruebe la [Aplicación de demostración](https://iam.ng.bluemix.net/demo) que muestra las API.

## Visión general de la gestión de accesos
{: #access_management}

IAM es un sistema de control de accesos basado en atributos (ABAC) con condiciones inspiradas por la publicación [NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf).   

IAM utiliza una combinación de atributos para determinar el acceso a los recursos. Las políticas de IAM tienen reglas que se aplican a los roles, atributos de ID de usuarios y servicios, atributos de recursos y condiciones. Esto permite que un enfoque flexible y potente para definir el acceso para usuarios e ID de servicio.

Por ejemplo, una máquina virtual, VM123, puede tener los atributos siguientes: 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
Cualquier combinación de estos atributos de recurso se puede utilizar para crear una política.

Para ver ejemplos más detallados, consulte los [Ejemplos de política de IAM](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples).

ABAC es otro control de accesos basado en roles (RBAC), en el que se asignan a los usuarios roles predefinidos. Estos roles predefinidos tienen privilegios específicos y los usuarios con un rol tienen todos los privilegios definidos por dicho rol. 
 
Por ejemplo, el rol `Administrador` de máquina virtual. Este rol implica todos privilegios de tipo Administrador sobre cualquier recurso de máquina virtual.  

Una forma sencilla de entender ABAC es la siguiente:

1. Hay Usuarios, Recursos, Contextos y Acciones.
1. Cada instancia de un Usuario, Recurso, Contexto y Acción tiene un identificador exclusivo.
1. Se asignan atributos a cada instancia. Básicamente, esto significa: "Qué es verdadero sobre la instancia desde el punto de vista de la autorización". Ejemplos:
   1. El Usuario es Piscis y nació en los años 60.
   1. El Recurso es la alineación de un equipo de béisbol. 
   1. El Contexto de 9:00 AM a 5:00 PM Hora Este. 
   1. La Acción es "puede actualizar".
1. Se crean políticas para determinar el conjunto de atributos que tendrán permiso para que el Usuario pueda realizar la Acción sobre el Recurso. 
1. Cuando un Usuario realiza una solicitud para realizar una Acción sobre un Recurso, se consultan las políticas para ver si se permite la solicitud. 

En la siguiente imagen se muestra una vista detallada de la secuencia de autorización. 

![Secuencia de autorización](auth_sequence.png)

## Configuración del control de accesos para un servicio
{: #setup_access_mgmt}

Incorporar un servicio en {{site.data.keyword.Bluemix_notm}} implica un conjunto de operaciones distinto del necesario para incorporar un servicio con Cloud IAM. Técnicamente, puede incorporar con {{site.data.keyword.Bluemix_notm}} y con Cloud IAM de forma independiente y en cualquier orden. El equipo de Cloud IAM está trabajando con el equipo de incorporación del servicio {{site.data.keyword.Bluemix_notm}} para que el proceso de incorporación del servicio {{site.data.keyword.Bluemix_notm}} también incluya la incorporación de Cloud IAM. 

Para configurar el control de accesos para el servicio, debe seguir los pasos siguientes como parte del proceso de incorporación: 

### Paso 1: Cree un ID de servicio con esta solicitud http:
```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
```
{: codeblock}

Mandato Curl: 
```  
curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

A continuación se describen con más detalle los valores `Service id` y `Service crn` utilizados en el mandato `curl`: 
  
#### Service id 
  
El nombre del ID de servicio puede coincidir con el nombre de servicio que aparece en crns para el servicio.
  
El ID de servicio debe estar enlazado a una cuenta, organización o espacio. Este enlace determina quién puede gestionar el ID de servicio.  Por ejemplo, el administrador al que está enlazado el ID de servicio puede actualizar o suprimir. La señal de {{site.data.keyword.Bluemix_notm}} debe tener acceso a la cuenta, organización y espacio a los que enlaza el ID. Para enlazar a una cuenta, el crn `boundTo` debe tener el siguiente aspecto:  

`crn:v1:::<service name>::a/<account id>:::` 
  
Para una organización, debe tener el siguiente aspecto:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
Para un espacio, debe tener el siguiente aspecto:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
El valor `boundTo` especificado no tiene ningún efecto sobre los recursos a los que puede acceder el ID de servicio.  
  
Las políticas de acceso de IAM controlan los recursos a los que puede acceder el ID de servicio. Aunque su ID de servicio esté enlazado a una organización de IBM, se pueden crear políticas de IAM que permitir que el ID de servicio pueda acceder a recursos externos a dicha organización. Cuando incorporado con IAM, la primera política de acceso que crea el equipo de IAM permite al ID de servicio crear políticas para cualquier recurso que sea propiedad del servicio.

Consulte [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/) para obtener más información sobre esta API y sobre las API relacionadas. 

#### Service crn

El nombre del servicio del crn `boundTo` debe coincidir con el nombre del servicio que aparece en el crn correspondiente al servicio.
  
Consulte [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) para obtener ayuda sobre cómo rellenar estos campos. 

De la respuesta, guarde metadata->uuid y metadata->crn, que son el ID de servicio y el crn del ID de servicio. 


### Paso 2: Póngase en contacto con AccessControl Squad en [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Se asigna a su ID de servicio el rol de Administrador de políticas para los recursos del servicio.

Utilice este formato: 
```
IAM adopter service info

service id: uuid from step #1
service name: nombre del servicio que aparecerá en los crns del servicio
```
{: codeblock}

### Paso 3: Debe crear una clave de API a partir del ID de servicio. Utilice la siguiente solicitud http: 
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
{: codeblock}

Mandato Curl:  
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo` debe ser el crn del ID de servicio (campo metadata->crn guardado de la respuesta del paso 1). El nombre y la descripción pueden ser cualesquiera. 

De la respuesta, guarde entity->apiKey.

Consulte [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) para ver más información sobre esta API y las API relacionadas. 

### Paso 4: Obtenga una señal de acceso para la clave de API de sus ID de servicio.  

Cuando se haya establecido el permiso, el servicio puede realizar solicitudes PAP y PDP sobre los recursos del servicio. 

Utilice el campo de entidad **apiKey** del paso 3, que es el valor de la clave de API (apikey_value).

  * A continuación, obtenga la señal con el valor de la clave de API (asegúrese de utilizar caracteres de escape):

    Mandato Curl:
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

Utilice el campo **access_token** del resultado, que es la señal de la clave de API (para su ID de servicio). El valor **access_token** tiene que estar codificado en URL si se utiliza en el mandato curl mostrado anteriormente. 


### Paso 5: Registre la lista de posibles acciones de servicio para el nombre de servicio.

  a. Correlacione las acciones de servicio con roles definidos en el sistema IAM. Esta correlación se utilizará más adelante durante el registro del servicio.

  * Para ver una lista de roles definidos en el sistema IAM, realice la siguiente solicitud: 
  
Mandato Curl: 
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**Nota:** Utilice la *versión de crn* de los roles definidos en el sistema IAM de la carga útil de registro del servicio. 

A continuación se muestra un ejemplo de correlación de acciones de servicio con roles. 

  <table>
    <tr>
      <th>Punto final de API</th>
      <th>Acción de servicio</th>
      <th>Roles definidos en el sistema IAM</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrador</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Visor, Editor, Administrador</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrador</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrador</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrador</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrador</td>
    </tr>
  </table>

  b. Utilice la siguiente línea de mandatos para registrar el servicio con `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
{: codeblock}
  
Las acciones se deben definir según lo especificado en el [Formato de acción de servicio](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
Por ejemplo, si se utiliza el formato estándar:

  `<service-name>.<component>.<verb>`
  
  Con la acción `key-protect.keys.decode` del ejemplo anterior 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### Paso 6: Verifique el servicio registrado de acuerdo con los detalles del paso 5.

```
curl -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### Paso 7 (Opcional): Suprima el servicio que ha registrado en el paso 5.

```
curl -X DELETE -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### Paso 8: Configure el servicio para que utilice PEP SDK para comprobar los permisos con PDP. Elija el lenguaje SDK correspondiente.  

  * [PEP SDK para Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK para Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK para Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## Terminología
{: #terminology}

### Terminología de identidades

* ID de IBM - Una identidad proporcionada y mantenida por IBM para acceder a IBM Cloud, aplicaciones, comunidades y soporte de IBM. 
* ID de usuario - Identificación que representa una persona real. 
* ID de servicio - Identificación que representa un usuario técnico, máquina, aplicación o servicios. Se parece a los "ID funcionales" o a los "ID de aplicación", que también representan un usuario técnico, pero que utilizan el tipo de entidad "ID de usuario". 
* OAuth 2.0 - Estándar abierto para autorizar el acceso a aplicaciones y API sin proporcionar credenciales al servicio de destino. OAuth también se utiliza para albergar información de autenticación. 
* OpenID Connect - Estándar abierto instalado sobre OAuth 2.0 cuyo objetivo es ofrecer información sobre el usuario autenticado. 
* Id de cliente - Las aplicaciones que interactúan con puntos finales compatibles con OAuth 2.0 requieren par ID de cliente secreto / secreto para autenticarse. Una aplicación se tiene que registrar con un Token Service para obtener un ID de cliente. 
* Punto final de señal - Lo utiliza el cliente para obtener una o varias señales mediante la presentación de información de identidad, como nombre de usuario o contraseña, concesión de autorización o señal de renovación. 
* Punto final de autorización - Utilizado por el cliente para autenticar un usuario a través de la interfaz de usuario ante el servicio de señal. 
* Señal - Una serie de caracteres opaca o transparente que permite a una aplicación recuperar la autenticación y/o autorización de una identidad. 
* Señal de acceso - Esta señal se utiliza para su envío a las API como información de identidad. Contiene información de identidad y solo es válida durante un breve periodo de tiempo.
* Señal de renovación - Esta señal solo se guarda en el cliente que ha solicitado la autenticación. Se utiliza para obtener una nueva señal de acceso (es decir, para renovar la señal de acceso) si la señal de acceso caduca. Como la señal de renovación es de larga duración, no debe abandonar el sistema del cliente si no es con el objetivo de renovar la propia señal de acceso. 
* Cookie de identidad - Según la lógica de IBM Cloud Token Service, se envía al navegador una cookie que contiene la identidad. No se le volverá a pedir que inicie la sesión mientras esta cookie exista y sea válida. Caduca a las 24 horas, si cierra la sesión de IBM Cloud Token Service o si cierra el navegador. 
* Señal web de JSON - Estándar basado en JSON (RFC 7519) que representa señales de acceso. El contenido de la señal de acceso es transparente (es decir, se puede leer fácilmente). Normalmente se firma una señal basada en JWT para poder verificar el origen de dicha señal. 
* Clave pública - Se puede utilizar para validar una firma de una señal web de JSON. Si se utiliza cifrado asimétrico, la clave pública se puede publicar de forma segura para que la consuman los clientes. 
* Clave privada - Se puede utilizar para crear una firma para una señal web de JSON. Esta clave se debe mantener en secreto; de lo contrario, otros podrían crear señales de acceso válidas. 
* realmid - Identificador para distinguir usuarios de otros registros de usuarios. Los valores que se utilizan actualmente son "IBMid" (ID de IBM) para los usuarios autenticados por el sistema IBMid e "iam" para los ID de servicio autenticados por el servicio de señal. 
* identificador - Identificador que no cambia y que identifica de forma exclusiva un usuario dentro de un registro de usuarios (indicado mediante el parámetro `realmid`). La combinación <realmid>-<identifier> siempre debe dar como resultado un usuario que se pueda identificar de forma exclusiva. En el caso de un ID de IBM, se utiliza el identificador exclusivo de IBM 'IUI'.              
* asunto - El nombre de usuario de la identidad. Suele tener el mismo formato que una dirección de correo electrónico. En el caso de un ID de IBM, es el ID de IBM de la identidad. 
* Reclamaciones personalizadas - Información adicional no estándar contenida en una señal web de JSON.

### Terminología de la gestión de accesos

* (PAP) Punto de administración de políticas - Punto que gestiona las políticas de autorización de acceso. 
* (PDP) Punto de decisión de políticas - Punto que evalúa las solicitudes de acceso según las políticas de autorización antes de emitir decisiones de acceso. 
* (PEP) Punto de aplicación de políticas - Punto que intercepta una solicitud de acceso de usuario a un recurso, realiza una solicitud de decisión al PDP para obtener la decisión de acceso (es decir, el acceso al recurso se aprueba o se rechaza) y actúa en función de la decisión recibida. 
* (PIP) Punto de información de políticas - La entidad del sistema que actúa como origen de valores de atributo (es decir, un recurso, asunto, entorno).
* (PRP) Punto de recuperación de políticas - Punto en el que se guardan las políticas de autorización de acceso de XACML, generalmente una base de datos o el sistema de archivos.
* asunto - El "quien" de un par recurso y autorización de asunto, como por ejemplo un usuario o un grupo. El recurso es el recurso al que puede acceder el asunto. 
* rol - Colección de permisos que se pueden asignar a un usuario, grupo de usuarios, sistema, servicio o aplicación y que les permite realizar determinadas tareas. 
* recurso - Objeto físico o lógico sobre las que se pueden realizar acciones, como por ejemplo una organización, un espacio, una base de datos o una tabla.
* condiciones - Función que se evalúa como verdadera ("True"), falsa ("False") o indeterminada (“Indeterminate”).
* acciones - Una tarea definida por realiza una aplicación sobre un objeto o recurso como resultado de un suceso.
* política - Un conjunto de reglas, un identificador para el algoritmo de combinación de reglas y (opcionalmente) un conjunto de obligaciones o consejos. Puede ser un componente de un conjunto de políticas.

## Roles definido por el sistema
{: #system_defined_roles}

Los roles de IBM Cloud representan una colección de acciones, proporcionadas por servicios habilitados por IAM. 

La agrupación de acciones como roles ofrece flexibilidad para dar soporte a acciones para cualquier servicio o recurso mediante el uso de un conjunto mínimo de roles definidos por el sistema. Por ejemplo, si necesita un `Administrador` para VM, almacenamiento y red, puede utilizar el rol `Administrador` para los tres y cambiar sólo el destino de la política. `Administrador` en VM, `Administrador` en almacenamiento y `Administrador` en red. 

*Lo que IBM Cloud IAM no hace*: Una alternativa que utilizan otros sistemas de gestión de accesos consiste en crear recursos en el rol. Este enfoque genera un nuevo nombre de rol para cada tipo de recurso que se incorpora en el sistema. Por ejemplo, con este enfoque necesitaría un rol `VMAdministrator`, un rol `StorageAdministrator` y un rol un `NetworkAdministrator` para cubrir la administración de para recursos de VM, almacenamiento y red. 


En la tabla siguiente se muestran los roles definidos por el sistema IAM y ejemplos de acciones que se correlacionan con éstos.

|Nombre rol IBM Cloud| Descripción | Acciones de ejemplo|
|:-----------------|:-----------------|:-----------------|
|Visor|acciones que no cambian de estado (es decir, sólo lectura)| <ul><li>enumerar dispositivos</li><li>leer objeto de almacenamiento</li><li>ejecutar consulta</li><li>ejecutar búsqueda</li></ul>|
|Editor|acciones que pueden modificar el estado y crear o suprimir subrecursos|<ul><li>crear vm</li><li>suprimir vm</li><li>conectar almacenamiento
</li><li>reiniciar</li><li>iniciar/detener</li><li>cambiar
el nombre</li></ul>|
|Operador |acciones necesarias para configurar y utilizar recursos|<ul><li>actualizar configuración</li><li>iniciar/detener vm</li><li>ver registros</li><li>hacer copia de seguridad/restaurar</li></ul>|
|Administrador|todas las acciones, incluida la capacidad para gestionar el control de accesos|<ul><li>invitar a usuario</li><li>crear vm</li>actualizar políticas de acceso de usuarios</li><li>enumerar dispositivos</li><li>crear vm</li><li>suprimir vm</li><li>conectar almacenamiento
</li><li>reiniciar</li><li>iniciar/detener</li><li>cambiar
el nombre</li><li>hacer copia de seguridad/restaurar</li></ul>|
|Administrador de facturación|acciones relacionadas con la administración de la facturación|<ul><li>actualizar tarjeta de crédito</li><li>enumerar facturas</li><li>descargar facturas</li></ul>|

La lista más actualizada de roles definidos por el sistema se puede consultar desde el microservicio PAP en: 

Mandato Curl:  

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## Formato de acción de servicio
{: #action_format}

Las acciones debe estar definidas en 1 de estos 2 formatos:
  
* Estándar:

    `<service-name>.<component>.<verb>`
* Punto interceptor de control de acceso:  

    `<METHOD> /<api_route>`
  
### Estándar
La mayoría de los servicios realizan una llamada a IAM PDP directamente y pueden modificar el código fuente para dar soporte al formateo de acción estándar.   
 
 Este formato debe incluir las tres partes y es alfanumérico, sin espacios ni caracteres especiales excepto '-'.

`<service-name>.<component>.<verb>`

Donde 
* service-name - El nombre de servicio definido en el campo service-name de CRN. 
* component - Recurso o subrecurso del servicio. 
* verb - Verbo que define la acción admitida para el componente nombre de servicio.  
  
Por ejemplo: `key-protect.keys.decode` 
* service-name = key-protect
* component = keys
* verb = decode

### Punto interceptor de control de acceso de API REST
{: intercept_point}

En algunos casos, las solicitudes de la API REST se direccionan a través de una pasarela que actúa como Punto interceptor de control de acceso. Se realiza una llamada directamente a IAM PDP desde el punto interceptor antes de llamar al servicio real de la API REST. El servicio que procesa la solicitud de la API REST nunca llama a IAM PDP.

El punto interceptor solo conoce la ruta de la API REST y el punto final al que enviar la solicitud. Consulte [Consideraciones sobre los puntos interceptores de control de acceso](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview) para ver más detalles. 


 Este formato debe incluir ambas partes y da soporte a caracteres seguros para los URL según lo especificado en [RCF 1738](https://www.ietf.org/rfc/rfc1738.txt).
 
 
`<METHOD> /<api_route>`
  
Donde
* METHOD - El método de la API REST.  
* api_route - El URI de la API REST. 

Por ejemplo: `GET /v1/things/thing123`
* METHOD = GET
* api_url = /v1/things/thing123

<!---
# Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To setup access control for your service you must use the following steps.

#### Step 1: Create a service id by making this http request:
  ```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
  ```
Curl command:
  ```  
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
  ```
  
### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value specified has no affect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization.  When on boarding with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createServiceid) for more information on this api and related apis.

###Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help filling in these fields.

From the response, save metadata&ndash>uuid and metadata&ndash>crn, which are your service id and service id crn.


#### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id will be given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```

#### Step 3: You must create an api key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
`boundTo` needs to be the crn of your service id (field metadata&ndash>crn saved from step 1’s response). The name and description can be anything.

From the response, save entity&ndash>apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

#### Step 4: Get an access token for your service id's API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, this is your API key value (apikey_value).

  * Then get the token with the API key value (make sure you use escape characters):

    Curl Command: 
    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
    ```

Use the **access_token** field in the result, this is your api key token(for your service id).


#### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
Curl command:
```
curl -X GET &ndash&ndashheader 'Accept: application/json' &ndash&ndashheader 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  
  [TODO: Also support REST like action format, yet to be approved]: <>

#### Step 6: Configure the service to use the PEP SDK in order to check permissions with the PDP. Pick the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)


<!---
# Identity and Access Management Adopter Guidelines
{: #iam_guidelines}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding. Until that work is complete please use the following onboarding steps.

- Users are identified with their IBMid.
  - Users authenticate with their IBMid and password.
  - Authentication returns a UAA/OAuth token which is used to access services within the IBM Cloud.
  
- Services are identified by their ServiceIDs.
  - Services authenticate with their ServiceID and APIkey.
  - Authentication returns an OAuth token which is used to access other services within the IBM Cloud.
  
- Services grant access to their resources by creating *Access Policies*.
  - *Roles* can be viewed and *Access Policies* can be managed through the 
  *Policy Administration Point (PAP)*.
  - Actions are permitted or denied through the *Policy Enforcement Point (PEP)* and *Policy Decision Point (PDP)*. 
  

## Creating a ServiceID
{: #create_serviceid}

To create a ServiceID you must use one of the following steps:

Make a one-time request for your ServiceID/APIkey.

 * Create a ServiceID with [swagger](https://iam.ng.bluemix.net/docs).
```
POST /serviceids
```
 * Create a ServiceID using `curl`.
```
curl -X POST -H "Authorization: $CF_TOKEN" -H 'Content-Type: application/json' -d '{"name": "IAMdemo", "description": "IAM demo of adopting service", "boundTo": "crn:v1:staging:public:docker-registry:us-south:o/57666a74-e136-4eb0-a085-220345fac266:::"}' 'https://iam.ng.bluemix.net/serviceids’
```
**Note**
The `boundTo` is the {{site.data.keyword.Bluemix_notm}} Org that is owned by you or your admin.

## Creating a ServiceID metadata response
{: #create_serviceid_metadata}

The following is a ServiceID metadata response using `curl`. Your service ID is expressed with a UUID and CRN format.

```
{"metadata":{\
"uuid":"ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"crn":"crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::\
serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"version":"1-4d9b1b10ce893f750a2d7e0d6ee34fd7"},"entity":{"boundTo":"crn:v1:staging:public:docker-registry:\
us-south:o/57666a74-e136-4eb0-a085-220345fac266:::","name":"IAMdemo","descripti\
on":"IAM demo of adopting service"}}
```

## Creating an APIkey for your ServiceID
{: #create_apikey_serviceid}

Create an APIkey
```
POST /apikeys
```

The following is a `curl` example of creating an APIkey
```
curl -X POST -H 'Authorization: $CF_TOKEN' -H 'Content-Type: application/json' -d '{"boundTo": "crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07", "name": "IAMdemo", "description": "IAM deom of adopting service"}' https://iam.ng.bluemix.net/apikeys
```

## Authenticating with an APIkey
{: #auth_apikey}

The following is a `curl` example of authenticating with an APIkey
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H \
"Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-ty\
pe%3Aapikey&apikey=DuE2s….bfRKc=" "https://iam.s\tage1.ng.bluemix.net/oidc/token”
{"access_token":"eyJraWQiOiIyMDE2MTAyNC0wMDowMDowMCIsImFsZyI6IlJTMjU2In0.eyJpZG\
VudGlmaWVyIjoiU2VydmljZUlkLTNlYzBkZDAyLTdhMTAtNDBiZi05MmU3LWI5YTMyOTU0N2MwNyIsI\
nN1YiI6IlNlcnZpY2VJZC0zZWMwZGQwMi03YTEwLTQwYmYtOTJlNy1iOWEzMjk1NDdjMDciLCJzdWJf\
dHlwZSI6IlNlcnZpY2VJZCIsImFjY291bnQiOnsiYnNzIjoiMDY0Zjg3NTZlMzZlODk5MDAyYjliM2M\
wNzZiZTM3OGIifSwibWZhIjp7fSwiaWF0IjoxNDc5Mzk3MTYwLCJleHAiOjE0Nzk0MDA3NjAsImlzcy\
I6Imh0dHBzOi8vaWFtLnN0YWdlMS5uZy5ibHVlbWl4Lm5ldC9vaWRjL3Rva2VuIiwiZ3JhbnRfdHlwZ\
SI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJvcGVuaWQi\
LCJjbGllbnRfaWQiOiJkZWZhdWx0In0.APRVqQmfUwn6K4Kg2sicT_kGpqSGQXr4Vua8Q5p4B0_dfGE\
tbbe10JqHeE4ovud6u8xjclAIcqCcbjIH4RijnUNGReVse49gS6JlXxmiNGA8OVlNGjiL68ygIpYsj-\
crx8kVuTrXAFqx9lhLEBhAzDneldu-gjSz7wrQKqISikcMXPXQkmLDuoT-OGNq8rG4fCiENBiweUrGf\
_Yw9W5NSiWyQGdWmczS70Krc_hx1iXskmt8pz5_0_vPXY6_tG5rY6KPw-bHO1wux91Q7aTZwCmaL0zI\
F2d3cIuFe1XywJ_926MfwWy65MxC3xv7-_rsZMFoprrLtBsuEnshNWUDhg",
"token_type":"Bearer","expires_in":3600,"expiration":1479400760}
```

## Registering your ServiceID with IAM
{: #register_serviceid}

To complete the on boarding process, contact the AccessControl Squad at
[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 

Your service id will be given the role of Administrator of policies for your 
service's resources.

Call the `PAP` and `GET` the existing policies
```
curl -X GET -H 'Authorization:<APIkeyToken>' \
'https://iampap.ng.bluemix.net/acms/v1/scopes/global/service_ids/\
ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07/policies'

Response:
{"policies":[]}  <-- no policies yet
```

## Creating access policies
{: #creating_policies}

Now that you are fully on boarded, you can begin creating access policies 
for resources owned by your service.
-->

# ID de Lab Service y claves de API

interconnect-service1:
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2:
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3:
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4;
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5:
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6:
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7:
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8:
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9:
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10:
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11:
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12:
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13:
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14:
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15:
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16:
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17:
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18:
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19:
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20:
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21:
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22:
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23:
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24:
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25:
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26:
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27:
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28:
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29:
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30:
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31:
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32:
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33:
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34:
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35:
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36:
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37:
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38:
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39:
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40:
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41:
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42:
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43:
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44:
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45:
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46:
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47:
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48:
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49:
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50:
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


