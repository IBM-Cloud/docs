---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}

# SDKs, amostras, referências de API do {{site.data.keyword.amashort}}
Para incluir SDKs do {{site.data.keyword.amashort}} em seu app, escolha os SDKs que você deseja usar e, em seguida, configure o gerenciador de dependência para enviar os SDKs por pull para seu app.

## Core SDK
{: #coresdk}
O Core SDK inclui APIs para ativar a autenticação customizada, o monitoramento e a criação de log em seu app móvel.

### Android
{: #coresdk-android}
[Repositório Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)

#### Instale o Core SDK com o Gradle
{: #coresdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'core',
    	version: '1.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #coresdk-ios-swift}

[Repositório do Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)

#### Instale o Core SDK com o CocoaPods
{: #coresdk-ios-siwft-cocoapods}

```
use_frameworks!
pod 'BMSCore'
```

### iOS (Objective-C SDK)
{: #coresdk-ios}

[Repositório Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)

#### Instale o Core SDK com o CocoaPods
{: #coresdk-ios-cocoapods}

```Bash
pod 'IMFCore'
```

### Cordova
{: #coresdk-cordova}

[Repositório Git e referência de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instale o Core SDK com o Cordova CLI
{: #coresdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}} Client SDK para autenticação do Facebook
{: #facebooksdk}

### Android
{: #facebooksdk-android}

[Repositório Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-facebookauthentication),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/facebook-api-doc/index.html)

#### Instale o Facebook SDK com o Gradle
{: #facebooksdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'facebookauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #facebooksdk-ios-swift}

[Repositório do Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-facebookauthentication)

#### Instale o Facebook SDK com o CocoaPods
{: #facebooksdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSFacebookAuthentication'
 ```

### iOS (Objective-C SDK)
{: #facebooksdk-ios}

[Repositório Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFFacebookAuthentication_api-doc/html/index.html)

#### Instale o Facebook SDK com o CocoaPods
{: #facebooksdk-ios-cocoapods}

```Bash
pod 'IMFFacebookAuthentication'
```

### Cordova
{: #facebooksdk-cordova}

[Repositório do Github e referência de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instale o Facebook SDK com o Cordova CLI
{: #facebooksdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}} Client SDK para autenticação do Google
{: #googlesdk}

### Android
{: #googlesdk-android}

[Repositório Github](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-security-googleauthentication),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/google-api-doc/index.html)

#### Instale o Google+ SDK com o Gradle
{: #googlesdk-android-gradle}

```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
    	name:'googleauthentication',
    	version: '2.+',
    	ext: 'aar',
    	transitive: true
```

### iOS (Swift SDK)
{: #googlesdk-ios-swift}

[Repositório do Git](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-security-googleauthentication)

#### Instale o Google+ SDK com o CocoaPods
{: #googlesdk-ios-swift-cocoapods}

```
use_frameworks!
pod 'BMSGoogleAuthentication'
```

### iOS (Objective-C SDK)
{: #googlesdk-ios}

[Repositório Git](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk.git),
[Referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFGoogleAuthentication_api-doc/html/index.html)

#### Instale o Google+ SDK com o CocoaPods
{: #googlesdk-ios-cocoapods}

```Bash
pod 'IMFGoogleAuthentication'
```

### Cordova
{: #googlesdk-cordova}

[Repositório Git e referência de API](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

#### Instale o Google+ SDK com o Cordova CLI
{: #googlesdk-cordova-cli}

```Bash
cordova plugin add ibm-mfp-core
```

## {{site.data.keyword.amashort}} Server SDK para servidores Node.js
{: #serversdk}

[Repositório do Git](https://github.com/ibm-bluemix-mobile-services/bms-mca-token-validation-strategy)

#### Instale o Server SDK com o npm
{: #serversdk-npm}

```Bash
npm install -save bms-mca-token-validation-strategy
```

## {{site.data.keyword.amashort}} Server SDK para servidor Liberty for Java&trade;
{: #serverlibertysdk}

[Fazer download de artefatos TAI](https://imf-tai.{DomainName}/public/TAI.zip)

## OAuth SDK Node.js do {{site.data.keyword.amashort}}
{: #serverlibertysdk-github}

[Repositório do Git](https://github.com/ibm-bluemix-mobile-services/bms-mca-oauth-sdk)

#### Instale o OAuth SDK com o npm
{: #oauthsdk}

```Bash
npm install -save bms-mca-oauth-sdk
```

## Amostras de provedor de identidade customizado
{: #customidprovider}

[Repositório Git de amostra simples](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
[Repositório Git de amostra avançada](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

## IMFURLProtocol
{: #IMFURLProtocol}

[referência de API](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFURLProtocol_api-doc/html/index.html)

#### Instale o IMFURLProtocol com o CocoaPods
{: #IMFURLProtocol-cocoapods}

```Bash
pod 'IMFURLProtocol'
```
