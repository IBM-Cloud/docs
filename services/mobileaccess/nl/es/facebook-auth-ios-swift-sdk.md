---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Habilitación de la autenticación de Facebook para apps de iOS (SDK de Swift)
{: #facebook-auth-ios}

Para utilizar Facebook como proveedor de identidad en las aplicaciones de {{site.data.keyword.amafull}} iOS, añada y configure la plataforma iOS para la aplicación de Facebook.
{: shortdesc}

## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:

* Una instancia de un servicio de {{site.data.keyword.amafull}} y una aplicación {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* El URL de la aplicación de programa de fondo (**Ruta de app**). Necesitará estos valores para enviar solicitudes a los puntos finales protegidos de la aplicación de programa de fondo.
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su {{site.data.keyword.Bluemix_notm}} **Región**. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de región que aparece debe ser uno de los siguientes: `EE.UU. Sur`, `Reino Unido` o `Sidney` y debe corresponder con los valores de SDK necesarios para Swift SDK: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` o `BMSClient.Region.sydney`. Necesitará este valor para inicializar el cliente {{site.data.keyword.amashort}}.
* Un proyecto de iOS configurado para funcionar con CocoaPods.  Para obtener información, consulte **Instalar CocoaPods** en [Configuración del SDK de Swift para iOS](getting-started-ios-swift-sdk.html).  
     
   **Nota:** no es necesario que instale el SDK de cliente {{site.data.keyword.amashort}} principal antes de proceder.
* Una aplicación de Facebook en el sitio web de [Facebook for Developers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developers.facebook.com "Icono de enlace externo"){: new_window}.

**Importante:** no es necesario instalar de forma independiente el SDK de SDK (`com.facebook.FacebookSdk`). El SDK de Facebook instala automáticamente mediante el pod {{site.data.keyword.amashort}} `BMSFacebookAuthentication`. Puede omitir el paso **Añadir el SDK de Facebook a su proyecto Xcode** cuando añada o configure su aplicación en el sitio web de Facebook para desarrolladores.

## Configuración de la aplicación de Facebook para la plataforma iOS
{: #facebook-auth-ios-config}

En el sitio Facebook for Developers:

1. Inicie sesión en su cuenta en [Facebook for Developers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developers.facebook.com "Icono de enlace externo"){: new_window}.

1. Asegúrese de que la plataforma iOS se haya añadido a la app. Cuando añada o configure la plataforma iOS, deberá especificar el valor de **bundleId** de la aplicación iOS. Para encontrar **bundleId** de la aplicación de iOS, busque el **Identificador de paquete** en el archivo `info.plist` o el separador **General** del proyecto Xcode.

  **Sugerencia**: habilite el sufijo de esquema URL o el inicio de sesión único si tiene pensado utilizar estas características.

1. Pulse **Save Settings**.

## Configuración de {{site.data.keyword.amashort}} para la autenticación de Facebook
{: #facebook-auth-ios-configmca}

Después de configurar el ID de la aplicación de Facebook y la aplicación de Facebook para dar servicio a clientes de iOS, puede habilitar la autenticación de Facebook en el servicio de {{site.data.keyword.amashort}}.

1. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}.
1. En el separador **Gestionar**, active **Autorización**.
1. Expanda la sección **Facebook**.
1. Añada el **ID de aplicación de Facebook** y pulse **Guardar**.

## Configuración del SDK del cliente de {{site.data.keyword.amashort}} para iOS
{: #facebook-auth-ios-sdk}

### Instalación de CocoaPods
{: #install-cocoapods}

1. Abra Terminal y ejecute el mandato **pod --version**. Si CocoaPods está instalado, se muestra el número de versión. Puede omitir la sección siguiente para instalar el SDK.

1. Si CocoaPods no está instalado, ejecute:

   ```
   sudo gem install cocoapods
   ```
   {: codeblock}

Para obtener más información, consulte el [sitio web de CocoaPods ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cocoapods.org/ "Icono de enlace externo"){: new_window}.

### Instalación del SDK de Swift de cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Si no tiene `Podfile` en su proyecto iOS, ejecute `pod init` para crear el archivo.

1. Edite el `Podfile` y añada las líneas siguientes:

   ```
   use_frameworks!
   pod 'BMSFacebookAuthentication'
   ```
   {: codeblock}

   **Nota:** si tiene la línea `pod 'BMSSecurity'` en el archivo del pod, debe eliminarla. El pod `BMSFacebookAuthentication` instala todas las infraestructuras necesarias.

   **Consejo:** puede añadir `use_frameworks!` al destino de Xcode en lugar de especificarlo en el archivo Podfile.

1. Guarde `Podfile` y ejecute el mandato `pod install` desde la línea de mandatos. CocoaPods instala las dependencias. Se mostrarán el progreso y los componentes que se han añadido.

   **Importante**: ahora debe abrir el proyecto utilizando el archivo `xcworkspace` que ha generado CocoaPods. El nombre suele ser `{nombre-proyecto}.xcworkspace`.  

1. Ejecute `open {nombre-proyecto}.xcworkspace` desde una línea de mandatos para abrir su espacio de trabajo de iOS.

### Habilitación de Keychain Sharing para iOS
{: #enable_keychain}

Habilite `Keychain Sharing`. Vaya al separador `Capacidades` y `active` `Keychain Sharing` en el proyecto Xcode.

### Configuración del proyecto de iOS para la autenticación de Facebook
{: #facebook-auth-ios-configproject}

1. Busque el `info.plist` archivo, que normalmente se encuentra bajo `archivos de soporte` carpeta en el proyecto Xcode.

1. Para configurar la integración con Facebook añada las propiedades siguientes al archivo `info.plist`:

   ![imagen](images/ios-facebook-infoplist-settings.png)

   Actualice las propiedades de esquema URL y FacebookAppID con el ID de aplicación de Facebook.

   También puede actualizar el archivo `info.plist` si pulsa con el botón de derecho en el mismo, selecciona **Abrir como > Código fuente** y añade el XML siguiente:

   ```XML
   <key>CFBundleURLTypes</key>
   <array>
      <dict>
         <key>CFBundleURLSchemes</key>
         <array>
            <string>fb{your-facebook-application-id}</string>
         </array>
      </dict>
   </array>
   <key>FacebookAppID</key>
   <string>{your-facebook-application-id}</string>
   <key>FacebookDisplayName</key>
   <string>{your-faceebook-application-name}</string>
   <key>LSApplicationQueriesSchemes</key>
   <array>
      <string>fbauth</string>
      <string>fbauth2</string>
   </array>
   <key>NSAppTransportSecurity</key>
   <dict>
      <key>NSExceptionDomains</key>
      <dict>
         <key>facebook.com</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>                
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>fbcdn.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
         <key>akamaihd.net</key>
         <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
         </dict>
      </dict>
   </dict>
   ```
   {: codeblock}

   Actualice las propiedades `CFBundleURLSchemes` y `FacebookappID` con el ID de aplicación de Facebook. Actualice  `FacebookDisplayName` con el nombre de la aplicación de Facebook.

   **Importante**: asegúrese de no sustituir las propiedades existentes del archivo `info.plist`. Si hay propiedades solapadas, tendrá que fusionarlas manualmente. Para obtener más información, consulte [Configurar proyecto de Xcode ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developers.facebook.com/docs/ios/getting-started/ "Icono de enlace externo"){: new_window} y [Preparación de las apps para iOS9 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developers.facebook.com/docs/ios/ios9 "Icono de enlace externo"){: new_window}.

## Inicialización del SDK de Swift de cliente de {{site.data.keyword.amashort}}
{: #facebook-auth-ios-initalize-swift}

Inicialice el SDK del cliente pasando `tenantId`.

Un lugar habitual, pero no obligatorio, donde poner el código de inicialización es en el método `application:didFinishLaunchingWithOptions` del delegado de la aplicación.

1. Para importar la infraestructura necesaria a la clase en la que desea utilizar el SDK del cliente de {{site.data.keyword.amashort}}, añada las cabeceras siguientes:

   ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
   ```
   {: codeblock}

1. Inicialice el SDK del cliente.

   ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

   func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
      let mcaAuthManager = MCAAuthorizationManager.sharedInstance
      mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
      //the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
      BMSClient.sharedInstance.authorizationManager = mcaAuthManager
      FacebookAuthenticationManager.sharedInstance.register()
   }
   ```
   {: codeblock}

   En el código:

   * Sustituya `<applicationBluemixRegion>` por la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}.
   * Sustituya `tenantId` por el valor de **TenantId/App GUID**.

   Para obtener más información sobre estos valores, consulte [Antes de comenzar](#before-you-begin).

1. Notifique la activación de la app al SDK de Facebook y registre el manejador de autenticación de Facebook añadiendo el código siguiente al método `application:didFinishLaunchingWithOptions` en el delegado de la app. Añada este código justo después de inicializar la instancia de BMSClient y registrar Facebook como el gestor de autenticación.

   ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
   ```
   {: codeblock}

1. Copie el archivo `FacebookAuthenticationManager.swift` de los archivos fuente de pod `BMSFacebookAuthentication` en el directorio del proyecto.

1. Añada el código siguiente al delegado de la app.

   ```Swift
   func application(_ app: UIApplication,
      open url: URL,
      options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool{
         return FacebookAuthenticationManager.sharedInstance.onOpenURL(app, open: url, options: options)
      }
   ```
   {: codeblock}

## Prueba de autenticación
{: #facebook-auth-ios-testing}

Después de inicializar el SDK del cliente y de registrar el gestor de autenticación de Facebook, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

### Antes de empezar
{: #facebook-auth-ios-testing-before}

Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](protecting-resources.html).

1. Intente enviar una solicitud al punto final protegido de la aplicación de programa de fondo móvil recién creada en su navegador. Abra el siguiente URL: `{applicationRoute}/protected`, sustituyendo la `{applicationRoute}` por el valor recuperado desde **Opciones móviles** (consulte [Configuración de Mobile Client Access para la autenticación de Facebook](#facebook-auth-ios-configmca)).
Por ejemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>El punto final `/protected` de una aplicación de programa de fondo móvil que se ha creado con el contenedor modelo de MobileFirst Services Starter está protegido con {{site.data.keyword.amashort}}. Se devuelve un mensaje `Unauthorized` en el navegador. Este mensaje se devuelve porque solo se puede acceder a este punto final con aplicaciones móviles instrumentadas con el SDK del cliente de {{site.data.keyword.amashort}}.

1. Utilice la aplicación de iOS para realizar una solicitud al mismo punto final.

   ```Swift
	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

   let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
  if error == nil {
         print ("response:\(response?.responseText), no error")
  } else {
         print ("error: \(error)")
  }
   }
	request.send(completionHandler: callBack)
   ```
   {: codeblock}

1. Ejecute la aplicación. Aparece una pantalla de inicio de sesión de Facebook.

   ![imagen](images/ios-facebook-login.png)

   Esta pantalla puede ser ligeramente diferente si no ha iniciado una sesión en Facebook.

1. Pulse **Aceptar** para autorizar que {{site.data.keyword.amashort}} utilice su identidad de usuario de Facebook para fines de autenticación.

1. 	Cuando la solicitud se realiza correctamente, se muestra la salida siguiente en la consola de Xcode:

   ```
   response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
   ```
   {: screen}

1. También puede añadir la funcionalidad de finalización de sesión añadiendo este código:

   ```
   FacebookAuthenticationManager.sharedInstance.logout(callBack)
   ```
   {: codeblock}

   Si invoca este código después de que el usuario haya iniciado sesión en Facebook, y el usuario intenta iniciar sesión de nuevo, se le solicitará que autorice a {{site.data.keyword.amashort}} para utilizar Facebook para llevar a cabo la autenticación.

   Para cambiar de usuario, debe invocar este código y el usuario debe finalizar su sesión en Facebook desde su navegador.

   Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
