---

copyright:
  years: 2016
lastupdated: "2016-10-10"
---
{:screen: .screen}
{:shortdesc: .shortdesc}

# Habilitación de la autenticación de Facebook para apps de iOS (SDK de Swift)
{: #facebook-auth-ios}


Para utilizar Facebook como proveedor de identidad en las aplicaciones de {{site.data.keyword.amafull}} iOS, añada y configure la plataforma iOS para la aplicación de Facebook.
{:shortdesc}

## Antes de empezar
{: #facebook-auth-ios-before}
 Debe tener lo siguiente:
* Un proyecto de iOS configurado para funcionar con CocoaPods.  Para obtener información, consulte **Instalar CocoaPods** en [Configuración del SDK de Swift para iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).  
   **Nota:** no es necesario que instale el SDK de cliente {{site.data.keyword.amashort}} principal antes de proceder.
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* Una aplicación de Facebook en el sitio [Facebook for Developers](https://developers.facebook.com). 


**Importante:** no es necesario instalar de forma independiente el SDK de SDK (`com.facebook.FacebookSdk`). El SDK de Facebook instala automáticamente mediante el pod {{site.data.keyword.amashort}} `BMSFacebookAuthentication`. Puede omitir el paso **Añadir el SDK de Facebook a su proyecto Xcode** cuando añada o configure su aplicación en el sitio web de Facebook para desarrolladores.

**Nota:** Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.Bluemix_notm}} Mobile Services, está previsto dejar de mantener este SDK a finales del año en favor del nuevo SDK de Swift.
## Configuración de la aplicación de Facebook para la plataforma iOS
{: #facebook-auth-ios-config}
En el sitio Facebook for Developers:

1. Inicie la sesión en su cuenta en [Facebook for Developers](https://developers.facebook.com).

1. Asegúrese de que la plataforma iOS se haya añadido a su app. Al añadir o configurar la plataforma iOS, se ofrecen más detalles sobre los pasos siguientes.

1. Especifique *bundleId* de la aplicación de iOS. Para encontrar *bundleId* de la aplicación de iOS, busque el **Identificador de paquete** en el archivo `info.plist` o el separador **General** del proyecto Xcode.

  **Sugerencia**: habilite el sufijo de esquema URL o el inicio de sesión único si tiene pensado utilizar estas características.

1. Pulse **Save Settings**.

## Configuración de {{site.data.keyword.amashort}} para la autenticación de Facebook
{: #facebook-auth-ios-configmca}

Después de configurar el ID de la aplicación de Facebook y la aplicación de Facebook para dar servicio a clientes de iOS, puede habilitar la autenticación de Facebook en {{site.data.keyword.amashort}}.

1. Abra el servicio en el panel de control de {{site.data.keyword.Bluemix}}. 

1. Pulse **Opciones móviles** y anote los valores correspondientes a **Ruta** (*applicationRoute*) y **GUID de app / TenantId** (*tenantId*). Necesitará estos valores cuando inicialice el SDK, y cuando envíe solicitudes a la aplicación de fondo.

1. Pulse el icono de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.

1. Pulse el botón **Configurar** en el panel **Facebook**.

1. Especifique el ID de aplicación de Facebook y haga clic en **Guardar**.

## Configuración del SDK del cliente de {{site.data.keyword.amashort}} para iOS
{: #facebook-auth-ios-sdk}

### Instalación de CocoaPods
{: #install-cocoapods}

1. Abra Terminal y ejecute el mandato **pod --version**. Si CocoaPods está instalado, se muestra el número de versión. Puede omitir la sección siguiente para instalar el SDK.

1. Si CocoaPods no está instalado, ejecute:

```
sudo gem install cocoapods
```

Para obtener más información, consulte el [sitio web de CocoaPods](https://cocoapods.org/).

### Instalación del SDK de Swift de cliente de {{site.data.keyword.amashort}} con CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Si no tiene `Podfile` en su proyecto iOS, ejecute `pod init` para crear el archivo.

1. Edite el `Podfile` y añada las líneas siguientes:

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'
	```
   **Nota:** si tiene la línea `pod 'BMSSecurity'` en el archivo del pod, debe eliminarla. El pod `BMSFacebookAuthentication` instala todas las infraestructuras necesarias.

   **Consejo:** puede añadir `use_frameworks!` al destino de Xcode en lugar de especificarlo en el archivo Podfile.

1. Guarde `Podfile` y ejecute el mandato `pod install` desde la línea de mandatos. CocoaPods instala las dependencias. Se mostrarán el progreso y los componentes que se han añadido.

 **Importante**: ahora debe abrir el proyecto utilizando el archivo `xcworkspace` que ha generado CocoaPods. El nombre suele ser `{nombre-proyecto}.xcworkspace`.  

1. Ejecute `open {nombre-proyecto}.xcworkspace` desde una línea de mandatos para abrir su espacio de trabajo de iOS.

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

   Actualice las propiedades `CFBundleURLSchemes` y `FacebookappID` con el ID de aplicación de Facebook. Actualice  `FacebookDisplayName` con el nombre de la aplicación de Facebook.

   **Importante**: asegúrese de no sustituir las propiedades existentes del archivo `info.plist`. Si hay propiedades solapadas, tendrá que fusionarlas manualmente. Para obtener más información, consulte [Configure Xcode Project](https://developers.facebook.com/docs/ios/getting-started/) y [Preparing Your Apps for iOS9](https://developers.facebook.com/docs/ios/ios9).

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
2. Inicialice el SDK del cliente.

 ```Swift
	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>

	func application(_ application: UIApplication, 
	    didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
   			 mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	//el regionName debería ser una de los siguientes: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, o BMSClient.Region.sydney
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager
	
		FacebookAuthenticationManager.sharedInstance.register()
	}

 ```
 
 En el código:
 
 * Sustituya `<applicationBluemixRegion>` por la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}. Para ver la región de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Avatar** ![icono de Avatar](images/face.jpg "icono de Avatar") en la barra de menús para abrir el widget **Cuenta y soporte**. El valor de región que aparece debería ser uno de los siguientes: **EE.UU. sur**, **Reino Unido** o **Sídney**, y se corresponde con los valores necesarios en el código: `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom`, o `BMSClient.Region.sydney`.
 * Sustituya el `tenantId` por el valor **GUID de app / TenantId** que ha guardado desde las **Opciones móviles** (consulte [Configuración de Mobile Client Access para la autenticación de Facebook](#facebook-auth-ios-configmca)).

1. Notifique la activación de la app al SDK de Facebook y registre el manejador de autenticación de Facebook añadiendo el código siguiente al método `application:didFinishLaunchingWithOptions` en el delegado de la app. Añada este código justo después de inicializar la instancia de BMSClient y registrar Facebook como el gestor de autenticación.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. Copie el archivo `FacebookAuthenticationManager.swift` de los archivos fuente de pod `BMSFacebookAuthentication` en el directorio del proyecto.

1. Añada el código siguiente al delegado de la app.

 ```Swift
  
	func application(_ application: UIApplication, open url: URL,
                     sourceApplication: String?, annotation: Any) -> Bool {
        
        return FacebookAuthenticationManager.sharedInstance.onOpenURL(application: application, 
		url: url, sourceApplication: sourceApplication, annotation: annotation)
        
    }
 ```

## Prueba de autenticación
{: #facebook-auth-ios-testing}

Después de inicializar el SDK del cliente y de registrar el gestor de autenticación de Facebook, puede empezar a realizar solicitudes a la aplicación de programa de fondo móvil.

### Antes de empezar
{: #facebook-auth-ios-testing-before}

Debe utilizar el contenedor modelo de {{site.data.keyword.mobilefirstbp}} y debe disponer de un recurso que esté protegido por {{site.data.keyword.amashort}} en el punto final `/protected`. Si tiene que configurar un punto final `/protected`, consulte [Protección de recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

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


 Si invoca este código después de que el usuario haya iniciado sesión en Facebook, y el usuario intenta iniciar sesión de nuevo, se le solicitará que autorice a {{site.data.keyword.amashort}} para utilizar Facebook para llevar a cabo la autenticación.

 Para cambiar de usuario, debe invocar este código y el usuario debe finalizar su sesión en Facebook desde su navegador.

 Es opcional pasar `callBack` a la función de cierre de sesión. También puede pasar `nil`.
