---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Filtros y cabeceras de autorización
{: #auth}

El SDK del servidor de {{site.data.keyword.appid_short}} proporciona estrategias para proteger dos tipos de recursos: API y aplicaciones web.
{:shortdesc}


## Filtros de autorización
{: #auth-filter}

La estrategia de protección de API devuelve una respuesta HTTP 401 con una lista de ámbitos para obtener la autorización para un cliente no autenticado. La estrategia de protección de aplicaciones web devuelve una redirección HTTP 302. La redirección envía a un cliente no autenticado a la página de inicio de sesión que aloja el servicio {{site.data.keyword.appid_short_notm}}, o bien directamente a la página de inicio de sesión de un proveedor de identidad, en función de su configuración.



### Estrategia de API
{: #api}

La estrategia de API espera que las solicitudes contengan una cabecera de autorización con una señal de acceso válida. La respuesta también puede incluir una señal de identidad, pero no es obligatorio; consulte [Señales de acceso e identidad](/docs/services/appid/access-identity.html#access-and-identity).

Si una señal no es válida o ha caducado, la estrategia de API devuelve un error HTTP 401 que contiene la siguiente información: Www-Authenticate=Bearer scope="{scope}" error="{error}". El componente `error` es opcional.

Si la solicitud devuelve una señal válida, el control se pasa al siguiente middleware y la propiedad `appIdAuthorizationContext` se inyecta en el objeto de solicitud. Esta propiedad contiene señales de acceso e identidad originales, así como información de carga útil descodificada como objetos JSON simples.


### Estrategia de app web
{: #web}

Cuando la estrategia de app web detecta intentos no autenticados de acceso a un recurso protegido, automáticamente redirige el navegador de un usuario a la página de autenticación. Tras la correcta autenticación, el usuario vuelve al URL de devolución de llamada de la aplicación web. El servicio utiliza la clase de estrategia de app web para obtener señales de acceso e identidad. Después de obtener estas señales, la clase de estrategia de app web las almacena en una sesión HTTP bajo `WebAppStrategy.AUTH_CONTEXT`. Depende del usuario decidir si desea almacenar las señales de acceso e identidad en la base de datos de la aplicación.

## Cabecera de autorización
{: #auth-header}

La cabecera de autorización de la solicitud entrante consta de tres partes, que están separadas por espacios en blanco: Bearer, señal de acceso y señal de ID. La señal de acceso es un componente obligatorio mientras que la señal de ID es opcional. La estructura de cabecera esperada es: Authorization=Bearer {access_token} [{id_token}]
