---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}


# Configuración del SDK de Swift de iOS
{: #getting-started-ios}

Cree las aplicaciones de Swift con el SDK del cliente de {{site.data.keyword.appid_short}}, inicialice el SDK, autentique usuarios y realice solicitudes a recursos protegidos y no protegidos.
{:shortdesc}


## Antes de empezar
{: #before-you-begin}

Necesita la siguiente información:
  * Una instancia de {{site.data.keyword.appid_short_notm}}.
  * Su ID de arrendatario.
    * En el separador **Credenciales de servicio** del panel de control de servicio, pulse **Ver credenciales**. Su ID de arrendatario se muestra en el campo **TenantID**. Este valor se utiliza para inicializar la app.
  * Su región de {{site.data.keyword.Bluemix_notm}}.
  Puede encontrar su región consultando en la IU. El valor se utiliza para inicializar la app.
    <table> <caption> Tabla 1. Regiones de {{site.data.keyword.Bluemix_notm}} y sus correspondientes valores de SDK </caption>
    <tr>
      <th> Región Bluemix </th>
      <th> Valor de SDK </th>
    </tr>
    <tr>
      <td> Sur de EE.UU. </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sídney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Reino Unido </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Un proyecto Xcode (versión 8.1 o superior).
  * CocoaPods (versión 1.1.0 o superior).


## Instalación del SDK del cliente de {{site.data.keyword.appid_short_notm}}
{: #install-appid-sdk}

El SDK del cliente de {{site.data.keyword.appid_short_notm}} se distribuye con CocoaPods, un gestor de dependencias para proyectos de Swift y de Objective-C Cocoa. CocoaPods descarga artefactos, y los pone a disposición de su proyecto.

1. Cree un proyecto de Xcode, o abra uno ya existente.
2. Abra, o cree, el Podfile en el directorio de proyecto.
3. En el destino del proyecto, añada una dependencia para el pod de 'BluemixAppID'. Asegúrese de que el mandato `use_frameworks!` también esté bajo su destino.

  Por ejemplo:

  ```swift
  target '<yourTarget>' do
     use_frameworks!
     pod 'BluemixAppID'
  end
  ```
  {:pre}

4. Para descargar la dependencia de `BluemixAppID`, ejecute el mandato siguiente:

  ```swift
  pod install --repo-update
  ```
  {:pre}

6. Abra el proyecto Xcode y habilite el uso compartido de la cadena de claves. En **Valores de proyecto**, pulse **Prestaciones** > **Uso compartido de la cadena de claves**.
7. En **Valores de proyecto** > **Info** > **Tipos de URL**, añada un Tipo de URL. Rellene los recuadros de texto **Identificador** y **Esquema de URL** con este valor: $(PRODUCT_BUNDLE_IDENTIFIER)


## Inicialización del SDK del cliente de {{site.data.keyword.appid_short_notm}}
{: #initialize-client-sdk}

1. Añada la siguiente importación al archivo `AppDelegate.swift`:

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Inicialice el SDK del cliente pasando los parámetros de tenant ID y de region al método initialize. Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método application:didFinishLaunchingWithOptions: del AppDelegate de la aplicación Swift.

  ```swift
  AppID.sharedInstance.initialize(tenantId: <tenantId>, bluemixRegion: AppID.Region_UK)
  ```
  {:pre}

  * Sustituya "tenantId" por el id de arrendatario para el servicio de la ID de app.
  * Sustituya AppID.REGION_UK por la región de {{site.data.keyword.appid_short_notm}}.

3. Añada el código siguiente al archivo AppDelegate.

  ```swift
  func application(_ application: UIApplication, open url: URL, options :[UIApplicationOpenURLOptionsKey : Any]) -> Bool {
          return AppID.sharedInstance.application(application, open: url, options: options)
      }
  ```
  {:pre}

## Autenticar los usuarios utilizando el widget de inicio de sesión
{: #authenticate-login}

Después de inicializar el SDK del cliente de {{site.data.keyword.appid_short_notm}}, puede autenticar los usuarios ejecutando el widget de inicio de sesión. La configuración predeterminada del widget de inicio de sesión utiliza Facebook, Google, o ambas como opciones de autenticación. Si configura sólo uno de ellos, el widget de inicio de sesión no se iniciará y se redirigirá al usuario a la pantalla de autenticación de IDP configurada.



1. Añada la siguiente importación al archivo en el cual desea utilizar el SDK.

  ```swift
  import BluemixAppID
  ```
  {:pre}

2. Ejecute el siguiente mandato para iniciar el widget.

  ```swift
  class delegate : AuthorizationDelegate {
      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Usuario autenticado
      }

      public func onAuthorizationCanceled() {
          //Autenticación cancelada por el usuario
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Se ha producido una excepción
        }
  }

  AppID.sharedInstance.loginWidget?.launch(delegate: delegate())
  ```
  {:pre}

## Acceso a los atributos de usuario
{: #accessing}

Cuando obtenga una señal de acceso, es posible obtener acceso al punto final de los atributos protegidos del usuario. Esta operación se realiza mediante los siguientes métodos de la API:

  ```swift
  func setAttribute(key: String, value: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func setAttribute(key: String, value: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func getAttributes(completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func getAttributes(accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)

  func deleteAttribute(key: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  func deleteAttribute(key: String, accessTokenString: String, completionHandler: @escaping(Error?, [String:Any]?) -> Void)
  ```
  {:pre}

Cuando no se haya aprobado explícitamente una señal de acceso, {{site.data.keyword.appid_short_notm}} utilizará la última señal recibida.

Por ejemplo, puede invocar este código para establecer un atributo nuevo, o para alterar temporalmente uno existente:

  ```swift
  AppID.sharedInstance.userAttributeManager?.setAttribute("key", "value", completionHandler: { (error, result) in
      if error = nil {
          //Atributos recibidos como un diccionario
      } else {
          // Se ha producido un error
      }
  })
  ```
  {:pre}


### Inicio de sesión anónimo
{: #anonymous notoc}

Con {{site.data.keyword.appid_short_notm}} puede iniciar sesión de forma anónima, consulte [identidad anónima](/docs/services/appid/user-profile.html#anonymous).

  ```swift
  class delegate : AuthorizationDelegate {

      public func onAuthorizationSuccess(accessToken: AccessToken, identityToken: IdentityToken, response:Response?) {
          //Usuario autenticado
      }

      public func onAuthorizationCanceled() {
          //Autenticación cancelada por el usuario
      }

      public func onAuthorizationFailure(error: AuthorizationError) {
          //Se ha producido un error
      }
   }

  AppID.sharedInstance.loginAnonymously( authorizationDelegate: delegate())
  ```
  {:pre}

### Autenticación progresiva
{: #progressive notoc}

Cuando alberga una señal de acceso anónimo, el usuario puede convertirse en un usuario identificado si lo pasa al método loginWidget.launch:

  ```swift
  func launch(accessTokenString: String? , delegate: AuthorizationDelegate)
  ```
  {:pre}

Tras un inicio de sesión anónimo, se producirá la autenticación progresiva, aunque se invoque el widget de inicio de sesión sin pasar una señal de acceso porque el servicio ha utilizado la última señal recibida. Si desea borrar las señales almacenadas, ejecute el siguiente mandato:

  ```swift
  var appIDAuthorizationManager = AppIDAuthorizationManager(appid: AppID.sharedInstance)
  appIDAuthorizationManager.clearAuthorizationData()
  ```
  {:pre}



## Pasos siguientes
{: #next-steps}

{{site.data.keyword.appid_short_notm}} proporciona una configuración predeterminada cuando se configuran inicialmente los proveedores de identidad. Puede utilizar la configuración predeterminada sólo en modalidad de desarrollo. Antes de publicar la aplicación, actualice la configuración predeterminada de [Facebook](/docs/services/appid/identity-providers.html#facebook) y [Google](/docs/services/appid/identity-providers.html#google) a sus propias credenciales.
