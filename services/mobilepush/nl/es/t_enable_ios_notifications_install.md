# Inicialización de SDK Push para aplicaciones iOS
{: #enable-push-ios-notifications-install}

Para un proyecto Xcode existente, puede configurar el SDK del cliente de Bluemix Mobile Services mediante la herramienta de gestión de dependencias de CocoaPods. Una alternativa es instalar el SDK manualmente.

**Nota**: Para ver el archivo readme Push de Swift, vaya a https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##Instalación de CocoaPods

1. Instale CocoaPods utilizando el siguiente mandato en su terminal Mac.
```
$ sudo gem install cocoapods
```
2. Especifique el mandato siguiente en el terminal para inicializar CocoaPods. Cuando emita este mandato, asegúrese de ejecutarlo en el directorio en el que se encuentra el proyecto de Xcode. El mandato `pod init` creará un título de archivo.  
```
$ pod init
```
3. En el Podfile generado, añada las dependencias de SDK que necesita. Copie el siguiente Podfile.

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. Desde Terminal, vaya a la carpeta del proyecto e instale las dependencias con el mandato siguiente:
```
$ pod update
```
Este mandato instala las dependencias y crea un nuevo espacio de trabajo Xcode.  **Nota**: Asegúrese de abrir siempre el nuevo espacio de trabajo de Xcode, en lugar del archivo de proyecto Xcode original:

	```
	$ open App.xcworkspace
	```
El espacio de trabajo contiene el proyecto original y el proyecto Pods que contiene las dependencias. Si desea modificar una carpeta fuente de Bluemix Mobile Services, puede encontrarla en el proyecto Pods, en `Pods/yourImportedSourceFolder`, por ejemplo: `Pods/IMFGoogleAuthentication`.

##Utilización de infraestructuras importadas y carpetas fuente

Haga referencia al SDK del código.


### Objective-C

Escriba directivas #import para las cabeceras relevantes, por
ejemplo:

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Nota**: La actualización del proyecto Pods utilizando los mandatos CocoaPods `pod install` o `pod update` puede alterar temporalmente las carpetas fuente de Bluemix Mobile Services. Si desea conservar las versiones personalizadas
de los archivos originales, asegúrese de que se les ha hecho la copia de seguridad antes de emitir uno de estos
mandatos.

###Swift

**Requisitos previos**

- iOS 8.0 o superior
- Xcode 7


Escriba directivas #import para las cabeceras relevantes, por
ejemplo:

```
//swift
import BMSCore
import BMSPush
```


##Crear configuración

Vaya a **Xcode > Crear configuración > Opciones de creación y Establecer la habilitación de Bitcode** en **No**.

**Atención**: A partir de iOS 9, los cambios a la característica de App Transport Security (ATS) pueden afectar a la forma de manejar el proceso de autenticación. Las siguientes publicaciones de blog describen más información sobre los cambios:[ATS y Bitcode en iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) y [Conecte la app de iOS 9 a Bluemix ahora mismo](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)
