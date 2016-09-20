---

copyright:
  years: 2015, 2016
  
---

{:shortdesc: .shortdesc}

# Initiation à {{site.data.keyword.amashort}}
{: #getting-started}

Le service {{site.data.keyword.amafull}} apporte à votre application mobile les fonctionnalités de sécurité
et de surveillance. Vous pouvez configurer l'authentification de client et les fournisseurs d'identité. Vous pouvez aussi ajouter à votre application une fonction de
surveillance qui active la journalisation client et les statistiques d'utilisation.

Remarque : L'ancien nom du service {{site.data.keyword.amashort}} est Advanced Mobile Access.
{: shortdesc}

1. Configurez un système de back end mobile dans Bluemix et configurez le logiciel SDK dans votre
application mobile. Pour plus d'informations, voir [Initiation](getting-started.html).
1. Sécurisez les ressources côté serveur. Protégez vos ressources de back end mobile qui s'exécutent en contextes d'exécution Node.js ou Liberty for
Java&trade; avec la sécurité OAuth pour les périphériques mobiles. Pour plus d'informations, voir [Protection des ressources](protecting-resources.html).
1. Facultatif : Configurez un fournisseur d'identité pour votre application. Vous ne pouvez configurer qu'un fournisseur d'identité par
application. La configuration d'un fournisseur d'identité permet aux utilisateurs de votre application mobile de se connecter avec leur compte Facebook
ou Google+ existant. Ou bien, vous pouvez définir le mode de connexion des utilisateurs en créant une authentification personnalisée.
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [Authentification personnalisée](custom-auth.html)
1. Configurez la surveillance et la journalisation des applications.  Pour plus d'informations, voir [Surveillance des applis](app-monitoring.html).


># Liens connexes {:class="linklist"}
>## Tutoriels et exemples {:id="samples"}
>* [android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)
>* [ios-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)
>
># Liens connexes {:class="linklist"}
>## Référence d'API{:id="api"}
>* [Référence pour l'API Core (Android)](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
>* [Référence pour l'API Core (iOS) ](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
>
># Liens connexes {:class="linklist"}
>## Logiciel SDK {:id="sdk"}
>* [Logiciel SDK de base (iOS) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)  
>* [bms-clientsdk-android-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)
>* [bms-clientsdk-cordova-plugin-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)
>
>{:elementKind="article" id="rellinks"}
