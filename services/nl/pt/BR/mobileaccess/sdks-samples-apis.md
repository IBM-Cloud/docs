---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# {{site.data.keyword.amashort}} SDKs, amostras e referência de API
Última atualização: 17 de julho de 2016
{: .last-updated}

Para incluir {{site.data.keyword.amashort}} SDKs em seu aplicativo, escolha os SDKs que desejar usar. Em seguida, configure seu
gerenciador de dependência para puxar os SDKs em seu aplicativo.
{:shortdesc}

**Nota:** seções subsequentes fornecem informações adicionais sobre instalar os SDKs.

## Core SDK
{: #coresdk}

O Core SDK inclui as APIs para ativar a autenticação customizada, a criação de log e o monitoramento do seu aplicativo da web.

### Android
{: #coresdk-android}

[Repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Instale o Core SDK com o Gradle
{: #coresdk-android-gradle}

Inclua uma dependência de compilação no arquivo `build.gradle` do aplicativo:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #coresdk-ios-swift}

[Repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security)

#### Instale o Core SDK com o CocoaPods
{: #coresdk-ios-siwft-cocoapods}
Edite o Podfile e inclua a linha a seguir nos destinos necessários e execute:

```
use_frameworks!
pod 'BMSSecurity'
```

### iOS (Objective-C SDK)
{: #coresdk-ios}

Embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix_notm}} Mobile Services, há planos para descontinuá-lo posteriormente este ano em favor do novo Swift SDK (consulte [Configurando o iOS Swift SDK](getting-started-ios-swift-sdk.html)).

[Repositório Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Instale o Core SDK com o CocoaPods
{: #coresdk-ios-cocoapods}

Edite o Podfile e inclua a linha a seguir nos destinos necessários e execute:
```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Repositório GitHub e referência de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instale o Core SDK com o Cordova CLI
{: #coresdk-cordova-cli}

Instale o plug-in do Mobile Client Access Cordova:
```Bash
cordova plugin add ibm-mfp-core
```

## SDK do cliente para autenticação de Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Instale o Facebook SDK com o Gradle
{: #facebooksdk-android-gradle}

Inclua uma dependência de compilação no arquivo `build.gradle` do aplicativo:
```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #facebooksdk-ios-swift}

[Repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Instale o Facebook SDK com o CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

Edite o Perfil e inclua o seguinte nos destinos necessários e execute:
```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Repositório Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

*Nota:* embora o Objective-C SDK permaneça totalmente suportado e ainda considerado o SDK primário para
{{site.data.keyword.Bluemix_notm}} Mobile Services, há planos de descontinuar esse SDK posteriormente neste ano em favor do novo Swift SDK. Para
novos aplicativos, recomendamos altamente o Swift SDK (consulte Configurando o iOS Swift SDK).
#### Instale o Facebook SDK com o CocoaPods
{: #facebooksdk-ios-cocoapods}

Edite o Perfil e inclua a linha a seguir e execute:

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Repositório GitHub e referência de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instale o Facebook SDK com o Cordova CLI
{: #facebooksdk-cordova-cli}

Instale o plug-in Cordova:

```Bash
cordova plugin add ibm-mfp-core
```

## SDK do cliente para autenticação do Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Instale o Google+ SDK com o Gradle
{: #googlesdk-android-gradle}

Inclua uma dependência de compilação no arquivo `build.gradle` do aplicativo:

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #googlesdk-ios-swift}

[Repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Instale o Google+ SDK com o CocoaPods
{: #googlesdk-ios-swift-cocoapods}

Edite o Perfil e inclua o seguinte e execute:

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (Objective-C SDK - descontinuado)
{: #googlesdk-ios}

[Repositório Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Instale o Google+ SDK com o CocoaPods
{: #googlesdk-ios-cocoapods}

Edite o Perfil e inclua a linha a seguir e execute:

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Repositório GitHub e referência de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instale o Google+ SDK com o Cordova CLI
{: #googlesdk-cordova-cli}

Instale o plug-in:

```Bash
cordova plugin add ibm-mfp-core
```

## Server SDK para servidores Node.js
{: #serversdk}

[Repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Instalar o server SDK com o npm
{: #serversdk-npm}

Execute NPM para instalar o SDK:

```Bash
npm install -save bms-mca-token-validation-strategy
```

## Server SDK para servidor Liberty for Java&trade;
{: #serverlibertysdk}

[Fazer download de artefatos TAI](https://imf-tai.{DomainName}/public/TAI.zip)

#### Instale o Liberty SDK
{: #libertysdk}
1. Copie o arquivo `com.ibm.worklight.oauth.tai_1.0.0.jar` no diretório
`$<wlp.user.dir>/extensions/lib`.

**Dica:** `$<wlp.user.dir>` é o diretório do usuário do tempo de execução do Liberty for Java. O nome do diretório padrão é `usr`.

1. Copie o diretório `OAuthTai-1.0.mf` para o diretório `$<wlp.user.dir>/extension/lib/features`.


## Node.js OAuth SDK
{: #serverlibertysdk-github}

[Repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Instale o OAuth SDK com o npm
{: #oauthsdk}

Execute NPM para instalar o SDK:
```Bash
npm install -save bms-mca-oauth-sdk
```

## Amostras do provedor de identidade customizado
{: #customidprovider}

[Repositório GitHub de amostra simples](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)

[Repositório GitHub de amostra avançado](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Instale o IMFURLProtocol com o CocoaPods
{: #IMFURLProtocol-cocoapods}

Edite o Perfil e inclua a linha a seguir e execute:

```Bash
pod 'IMFURLProtocol'
```
