---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Preparación de MQA con una app de iOS (en desuso)
{: #instrumentios}

Para utilizar {{site.data.keyword.mqafull}} con la app de iOS, debe descargar el SDK y prepararlo realizando algunos cambios mediante el entorno de desarrollo de Xcode.
{: shortdesc}

Para poder preparar una app con {{site.data.keyword.mqa}}, debe tener una cuenta de {{site.data.keyword.Bluemix}} y la versión correctamente instalada del entorno de desarrollo para las plataformas de la app que está preparando.

Para preparar {{site.data.keyword.mqa}} para que funcione con la app de Objective-C o Swift, lleve a cabo las siguientes tareas:

1. Añada los permisos necesarios y el SDK descargado al proyecto de iOS.

	1. Cree o abra el proyecto en Xcode.

	2. Añada las siguientes Bibliotecas de dependencia seleccionando `+` en la sección *Infraestructura y bibliotecas enlazados* del separador *General* del proyecto de Xcode:

		* AssetsLibrary.framework
		* AudioToolbox.framework
		* AVFoundation.framework
		* CoreData.framework
		* CoreLocation.framework
		* CoreMedia.framework
		* CoreMotion.framework
		* CoreTelephony.framework
		* CoreText.framework
		* CoreVideo.framework
		* MediaPlayer.framework
		* QuartzCore.framework
		* Security.framework
		* SystemConfiguration.framework

	3. Arrastre el SDK de {{site.data.keyword.mqa}} para la carpeta `Q4M.framework` de iOS al grupo **Infraestructuras** en el árbol del Navegador. En la ventana Elegir opciones, seleccione *Copiar elementos si es necesario*, **Crear grupos**, y consulte el recuadro para ver el nombre de proyecto como el destino.

	4. En la sección Enlaces del separador *Valores de compilación*, defina *Otros distintivos de enlazador* para depuración y publicación en **-ObjC**. Importante: Asegúrese de que el separador *Todos* esté seleccionado para que los Otros distintivos de enlazador se incluyan en la lista.

	5. *Sólo para Objective-C:* Añada la siguiente sentencia de importación a los archivos `AppDelegate.m` y `ViewController.m`:

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *Sólo para Swift:* Añada una cabecera de puente Objective-C para el SDK de {{site.data.keyword.mqa}} para iOS completando los pasos siguientes:

		1. Pulse con el botón derecho del ratón el nodo raíz de proyecto y seleccione **Archivo nuevo**.

		2. En la ventana Elegir plantilla de iOS, pulse la plantilla Archivo de cabecera en la sección Origen.

		3. Nombre al archivo `MyProject-Bridging-Header.h`, donde *MyProject* es el nombre del proyecto de Swift, y seleccione el nombre del proyecto como destino. Por ejemplo, nombre el archivo `MyProject-Bridging-Header.h`.

		4. Pulse **Crear** para guardar el archivo en la raíz del proyecto.

		5. En el archivo nuevo de cabecera de puente, añada la siguiente sentencia de importación para el archivo de cabecera de puente:

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. Con el proyecto seleccionado en
			el Xcode Project Navigator, pulse **Valores de compilación** y busque `Cabecera de puente Objective-C`.

		7. En **Compilador de Swift - General**, establezca el valor de **Cabecera de puente Objective-C** en la vía de acceso de la cabecera de puente. La vía de acceso es relativa a la raíz del proyecto. Por ejemplo, si la MQASampleApp del proyecto se encuentra en `/user/example/MQASampleApp`, la vía de acceso será `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`. Si ha guardado el archivo en la raíz del proyecto, puede utilizar la variable de entorno para establecer la vía de acceso especificando `${SRCROOT}/${PROJECT}-Bridging-Header.h`.

		8. Guarde y cree la app para verificar que la vía de acceso es correcta.

	7. En el archivo `info.plist`, verifique los valores siguientes en la información de proyecto:

		* Versión del paquete: {{site.data.keyword.mqa}} utiliza el valor de este campo para determinar cuándo enviar una nueva notificación de compilación a los probadores. Cuando cargue una nueva compilación en {{site.data.keyword.mqa}}, asegúrese de incrementar este número. La cadena del campo Versión del paquete está restringida a números y al carácter punto (.). Dado que esta restricción es un requisito de Xcode, la mayoría de las aplicaciones siguen esta convención y no necesitan cambios.
		* Cadena de versiones del paquete: Este campo contiene una representación de cadenas del número de versión. La cadena no tiene las mismas restricciones que el campo Versión del paquete.

2. Configure que empiece una sesión nueva con cada inicio de sesión.

    1. Ubique el método `didFinishLaunchingWithOptions` en el archivo `AppDelegate`:

        * Objective-C: archivo `AppDelegate.m`
        * Swift: archivo `AppDelegate.swift`

	2. Inicie la sesión {{site.data.keyword.mqa}}.

		* Objective-C

			1. Inicie la sesión nueva en un método dentro del método `applicationDelegate`, como por ejemplo el método `didFinishLaunchingWithOptions`. Puede encontrar el delegado abriendo la carpeta con el mismo nombre del proyecto en el Project Navigator. Busque el archivo `projectDelegate.m`.

			2. Añada el código siguiente dentro del método `didFinishLaunchingWithOptions` antes de la línea que tiene `return YES;`:

				```
				// Inicia una sesión de control de calidad mediante una
				    clave de marcador de posición y un modo QA
				[MQALogger startNewSessionWithApplicationKey:@"Your_Application_Key"];
				```
				{: codeblock}

			3. Sustituya la variable *Your_Application_Key* por la clave de aplicación de {{site.data.keyword.mqa}}.
               Sugerencia: Puede encontrar la clave de app en el panel web {{site.data.keyword.mqa}} en Configuración de la app.

		* Swift

			1. Ubique el método `didFinishLaunchingWithOptions` en el archivo `AppDelegate.swift`.

			2. Añada el código siguiente dentro del método antes de la línea que dice `return true`, donde *Your_Application_Key* es una clave válida para la app:

				```
				// Establezca la clave de aplicación
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. Defina si desea utilizar la modalidad de preproducción o la modalidad de producción. Para obtener información sobre las diferencias entre la modalidad de preproducción y de producción, consulte [Diferencias entre modalidades de preproducción y de producción ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window} en IBM Knowledge Center.

		* Objective-C

			1. Ubique el método `didFinishLaunchingWithOptions`.

			2. Añada una de las líneas siguientes de código dentro del método didFinishLaunchingWithOptions antes de la línea que tiene `return YES;`:

			Para utilizar la modalidad de preproducción, añada esta línea de código:

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			Para utilizar la modalidad de producción, añada esta línea de código:

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Objective-C complete example**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Punto de sustitución para personalización tras el lanzamiento de la aplicación.
					   if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad) {
					      UISplitViewController *splitViewController = (UISplitViewController*)self.window.rootViewController;
					      UINavigationController *navigationController = [splitViewController.viewControllers lastObject];
					      splitViewController.delegate = (id)navigationController.topViewController;
						}
					     #ifdef Debug
					   [[MQALogger settings] setMode:MQAModeQA];
					   #else
					   [[MQALogger settings] setMode:MQAModeMarket];
					   #endif
					      // Inicia una sesión de control de calidad mediante una clave de marcador de posición
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Permite la creación de informes de bloqueo de la aplicación de control de calidad
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}

        * Swift

			1. En el archivo AppDelegate.swift, busque el método `didFinishLaunchingWithOptions`.

			2. Añada las líneas siguientes al método `didFinishLaunchingWithOptions` antes de la línea que dice `return true`:

				```
				//Establezca la modalidad de SDK Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}

			Un ejemplo del código sería:

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Establezca la modalidad de SDK Market vs QA for Production
				   and Pre-Production
				#if Debug
					MQALogger.settings().mode = MQAMode.QA
				#elseif Release
					MQALogger.settings().mode = MQAMode.Market
				#endif

				// Establezca la clave de aplicación
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")

				// Punto de sustitución para personalización tras
				   el lanzamiento de la aplicación.
				return true
				```
				{: codeblock}

				**Ejemplo completo de Swift**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Punto de sustitución para personalización tras el lanzamiento de la aplicación.
					//Establezca la opción Shake Device en true o false. Si no se ha establecido explícitamente, Shake Device estará habilitado de forma predeterminada.
					MQALogger.settings().reportOnShakeEnabled = true
					//Establezca la modalidad de SDK Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Inicie la sesión de MQA con la clave de app especificada
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Permite que la creación de informes de bloqueo de MQA capture excepciones no capturadas
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}

3. Ejecute la app para asegurarse de que se inicie {{site.data.keyword.mqa}} cuando lo haga la app.

4. Continúe con los pasos de la página [Iniciación a {{site.data.keyword.mqa}}](index.html).

# Enlaces relacionados
{: #rellinks notoc}

## Enlaces relacionados
{: #general notoc}
* [Iniciación a {{site.data.keyword.mqa}}](index.html){:new_window}
