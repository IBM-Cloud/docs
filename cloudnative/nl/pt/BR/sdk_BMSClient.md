---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Inicializando BMSClient
{: #sdk_BMSClient}

O `BMSCore` fornece a infraestrutura HTTP que os outros SDKs do cliente de serviços móveis do {{site.data.keyword.Bluemix}} usam para se comunicarem com os seus serviços do {{site.data.keyword.Bluemix_notm}} correspondentes.


## Inicializando seu aplicativo Android
{: #init-BMSClient-android}

É possível fazer download e importar o
pacote `BMSCore` em seu projeto Android Studio ou usar o Gradle.

1. Importe o Client SDK incluindo a instrução `import` a seguir no início do seu arquivo de projeto:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. Inicialize o SDK `BMSClient` em seu aplicativo Android incluindo o código de
inicialização no método `onCreate` da atividade principal ou em um local que funcione melhor
para seu projeto.

  ```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
  ```
  {: codeblock}

  Deve-se inicializar o `BMSClient` com o parâmetro **bluemixRegion**. No inicializador, o valor **bluemixRegion** especifica qual implementação do {{site.data.keyword.Bluemix_notm}} está sendo usada, por exemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.


## Inicializando seu aplicativo iOS
{: #init-BMSClient-ios}

É possível usar o [CocoaPods](https://cocoapods.org){: new_window} ou o [Carthage](https://github.com/Carthage/Carthage){: new_window} para obter o pacote `BMSCore`.

1. Para instalar o `BMSCore` usando o
CocoaPods, inclua as linhas a seguir em seu Podfile. Se seu projeto
ainda não tiver um Podfile, use o comando `pod init`.

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  Em seguida, execute o comando `pod install`
e abra o arquivo `.xcworkspace` gerado. Para
atualizar para uma liberação mais recente do
`BMSCore`, use `pod update BMSCore`.

  Para obter mais informações sobre como usar o CocoaPods, veja os [Guias do CocoaPods ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://guides.cocoapods.org/using/index.html){: new_window}.

2. Para instalar o `BMSCore` usando o Carthage, siga estas [instruções ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/Carthage/Carthage#getting-started){: new_window}.

  1. Inclua a linha a seguir em seu Cartfile:

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. Execute o comando `carthage update`.

  3. Após a conclusão da construção, inclua `BMSCore.framework` no projeto seguindo a [Etapa 3 ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/Carthage/Carthage#getting-started) nas instruções do Carthage.

      Para aplicativos que são construídos com o Swift 2.3, use o comando `carthage update --toolchain com.apple.dt.toolchain.Swift_2_3`. Caso contrário, use o comando `carthage update`.

3. Importe o módulo.

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. Inicialize a classe `BMSClient`, usando o código a seguir.

  Coloque o código de inicialização no método `application(_:didFinishLaunchingWithOptions:)` de seu delegado do aplicativo ou em um local que funcione melhor para seu projeto.

  ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
  ```
  {: codeblock}

  Deve-se inicializar o `BMSClient` com o
parâmetro **bluemixRegion**. No inicializador, o valor **bluemixRegion** especifica qual implementação {{site.data.keyword.Bluemix_notm}} você está usando, por exemplo, `BMSClient.Region.usSouth`,
`BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`.


## Inicializando seu aplicativo Cordova
{: #init-BMSClient-cordova}

1. Inclua o plug-in do Cordova executando o comando a seguir no diretório-raiz de seu aplicativo Cordova:

  ```
  cordova plugin add bms-core
  ```
  {: codeblock}

2. Inicialize a classe `BMSClient` em seu aplicativo Cordova incluindo o código de inicialização no arquivo JavaScript principal ou em um local que funcione melhor para seu projeto.

  ```
  BMSClient.initialize(BMSClient.REGION_US_SOUTH);
  ```
  {: codeblock}
	
  Deve-se inicializar o `BMSClient` com o
parâmetro **bluemixRegion**. No inicializador, o valor **bluemixRegion** especifica qual implementação do {{site.data.keyword.Bluemix_notm}} está sendo usada, por exemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.


# Links relacionados
{: #rellinks notoc}

## Links relacionados
{: #general notoc}

* [SDK Android BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [SDK iOS BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Plug-in do Cordova BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
