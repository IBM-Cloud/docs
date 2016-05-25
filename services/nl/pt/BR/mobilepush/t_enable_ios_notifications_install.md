# Inicializando apps Push SDK para iOS
{: #enable-push-ios-notifications-install}

Para um projeto Xcode existente, é possível configurar o SDK do cliente Bluemix
Mobile Services usando a ferramenta de gerenciamento de dependência CocoaPods. Uma alternativa é instalar o SDK manualmente.

**Nota**: Para visualizar o arquivo leia-me de Push do Swift,
acesse https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master

##Instalando o CocoaPods

1. Instale o CocoaPods usando o comando a seguir em seu terminal Mac.
```
$ sudo gem install cocoapods
```
2. Insira o comando a seguir no terminal para inicializar o CocoaPods. Ao emitir
esse comando, certifique-se de executá-lo no diretório em que está o projeto Xcode. O
comando `pod init` cria um título de arquivo.  
```
$ pod init
```
3. No Podfile gerado, inclua as dependências necessárias de SDK. Copie o Podfile a
seguir.

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
3. No Terminal, acesse a pasta do projeto e instale as dependências
com o comando a seguir:
```
$ pod update
```
Esse comando instala suas dependências e cria uma nova área de trabalho Xcode.  **Nota**: assegure-se de sempre abrir a nova área de trabalho do Xcode,
em vez do arquivo de projeto do Xcode original:

	```
	$ open App.xcworkspace
	```
A área de trabalho contém o projeto original e o projeto Pods que contém suas
dependências. Para modificar uma pasta de origem do Bluemix Mobile Services, é possível
localizá-la em seu projeto Pods, em `Pods/yourImportedSourceFolder`,
por exemplo: `Pods/IMFGoogleAuthentication`.

##Usando estruturas importadas e pastas de origem

Referencie o SDK no código.


### Objective-C

Escreva diretivas #import para os cabeçalhos relevantes, por exemplo:

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Nota**: A atualização de seu projeto Pods usando os comandos
CocoaPods `pod install` ou `pod update` poderá
substituir as pastas de origem do Bluemix Mobile Services. Para reter as versões
customizadas dos arquivos originais, assegure-se de que sejam submetidas a backup antes de emitir um destes
comandos.

###Swift

**Pré-requisitos
**

- iOS 8.0 ou superior
- Xcode 7


Escreva diretivas #import para os cabeçalhos relevantes, por exemplo:

```
//swift
import BMSCore
import BMSPush
```


##Configurações de Compilação

Acesse **Xcode > Configurações de compilação > Opções de compilação e
configure Ativar Bitcode** como **Não**.

**Atenção**: Desde o iOS 9, mudanças no recurso App Transport
Security (ATS) podem afetar a maneira de manipular o processo de autenticação. As
postagens do blog a seguir descrevem mais informações sobre as
mudanças:[ATS
e Bitcode no iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) e
[Conecte
seu app iOS 9 ao Bluemix hoje](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)
