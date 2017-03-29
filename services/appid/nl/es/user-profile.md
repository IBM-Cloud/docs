---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Perfiles de usuario 
{: #user-profile}

Un perfil de usuario es una entidad que {{site.data.keyword.appid_short}} almacena y mantiene. El perfil contiene los atributos y la identidad de un usuario y puede ser anónimo o bien estar vinculado a una identidad gestionada por un proveedor de identidad.
{:shortdesc}

{{site.data.keyword.appid_short_notm}} proporciona una API para iniciar sesión, ya sea de forma anónima o autenticándose con un IdP OpenId Connect (OIDC), consulte [Configuración de los proveedores de identidad](https://console.stage1.ng.bluemix.net/docs/services/appid/identity-providers.html#setting-up-idp). El punto final de API de atributos de perfil de usuario es un recurso protegido por una señal de acceso generada por {{site.data.keyword.appid_short_notm}} durante el proceso de inicio de sesión y autorización.


## Cómo almacenar, leer y suprimir atributos de usuario
{: #storing-data}

{{site.data.keyword.appid_short_notm}} proporciona una [API REST](http://mobileclientaccess.stage1.mybluemix.net/swagger-ui/#!/Authorization_Server_V3/authorization) para realizar operaciones CRUD en atributos de usuario, así como un SDK para clientes móviles de [Android](https://github.com/ibm-cloud-security/appid-clientsdk-android) y [Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift).


## Identidad OAuth
{: #oauth}

Al llamar a la API de inicio de sesión de OAuth, {{site.data.keyword.appid_short_notm}} utiliza los protocolos OAuth 2.0 y OIDC para autorizar y autenticar al interlocutor con un proveedor de identidad seleccionado. Una vez autenticado, la identidad se asocia con un registro de usuario de {{site.data.keyword.appid_short_notm}}. {{site.data.keyword.appid_short_notm}} devuelve una señal de acceso que se puede utilizar para acceder a los atributos de usuario, y una señal de identidad que contiene la información de identidad proporcionada por el proveedor de identidad. Se puede volver a acceder al mismo registro de usuario y sus atributos desde cualquier cliente que se autentique con esta misma identidad.


## Usuario anónimo
{: #anonymous}

Al iniciar sesión de forma anónima, {{site.data.keyword.appid_short_notm}} crea un registro de usuario ad hoc que se marca como anónimo. {{site.data.keyword.appid_short_notm}} devuelve señales de acceso e identidad anónimas al interlocutor. Al utilizar la señal de acceso anónima, la aplicación de usuario puede crear, leer, actualizar y suprimir atributos, que se almacenan en el registro de usuario. Por ejemplo, un desarrollador puede crear una aplicación en la cual el usuario puede empezar a añadir artículos al carro de la compra inmediatamente, sin tener que iniciar sesión. 


## Usuario identificado
{: #identified}

Un usuario anónimo con una identidad proporcionada por un proveedor de identidad puede convertirse en un usuario identificado. El flujo para pasar de un usuario anónimo a un usuario conocido se describe en los siguientes pasos: 

* El desarrollador pasa la señal de acceso anónimo a la API de inicio de sesión. 
* {{site.data.keyword.appid_short_notm}} autentica al interlocutor con un proveedor de identidad. 
* {{site.data.keyword.appid_short_notm}} encuentra el registro de usuario anónimo definido por la señal de acceso y le asigna la identidad. **Nota**: La identidad se puede asignar al registro anónimo solo si no se había asignado la misma identidad a otro usuario. Si la identidad ya está asociada a otro usuario de {{site.data.keyword.appid_short_notm}}, las señales de acceso e identidad contienen información del registro de ese usuario y proporcionan acceso a sus atributos. El usuario anónimo anterior y sus atributos no serán accesibles a través de la nueva señal de acceso. Hasta que la señal caduque, aún se podrá acceder a la información a través de la señal de acceso anónimo. El desarrollador puede elegir cómo quieren fusionar los atributos anónimos del usuario anónimo y el usuario conocido. 
* Las nuevas señales de acceso e identidad recibidas desde {{site.data.keyword.appid_short_notm}} apuntan al usuario conocido y la señal de identidad contiene la información pública que se recibe del proveedor de identidad. 
* Las señales anónimas se convierten en inválidas para el usuario. 

Los atributos contenidos por este usuario cuando era anónimo serán accesibles con la nueva señal de acceso. Se pueden añadir, cambiar o suprimir nuevas señales. En el futuro, el usuario y sus atributos se resuelven y son accesibles cuando inician sesión con la misma identidad de cualquier cliente. 


## Separación y cifrado de datos
{: #data}

{{site.data.keyword.appid_short_notm}} almacena y cifra atributos de perfil de usuario. Como servicio multiarrendatario, cada arrendatario tiene una clave de cifrado designada y los datos de usuario de cada uno se cifran únicamente con la clave de dicho arrendatario.

{{site.data.keyword.appid_short_notm}} garantiza que la información privada se cifre antes de que se almacene.
