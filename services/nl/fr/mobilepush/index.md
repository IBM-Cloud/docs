---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Initiation à {{site.data.keyword.mobilepushshort}}

{: #gettingstartedtemplate}


{:shortdesc}

Le service Push Notifications met à disposition une plateforme unifiée pour l'envoi et la gestion de
notifications push mobiles ciblées pour les plateformes iOS et Android. Il gère le mappage des utilisateurs de votre application aux périphériques et à
la plateforme de périphérique, ainsi que la répartition des notifications push sur ces périphériques. Avec ce service, vous pouvez envoyer des
notifications push de diffusion, des notifications push unicast (en fonction de l'ID de périphérique), mais également des notifications push basées sur les balises (ou les rubriques) aux utilisateurs de vos applications mobiles. Vous pouvez également utiliser un logiciel SDK et des [API REST](https://mobile.{DomainName}/imfpushrestapidocs/) pour développer davantage vos applications client.

Cette section explique comment configurer des notifications push de base. Lorsque vous utilisez une notification de base, les
notifications sont diffusées au lieu d'être envoyées à un ensemble spécifique d'utilisateurs abonnés à des balises.

1. [Configurez les données d'identification pour un fournisseur de notification](t__main_push_config_provider.html)
2. [Configurez l'application mobile pour qu'elle reçoive des notifications](c_enable_push.html)
3. [Envoyez des notifications de base](t_send_push_notifications.html)

# Liens connexes
{: #rellinks}

* [Présentation](c_overview_push.md){: new_window}

## Tutoriels et exemples {:id="samples"}
{: #samples}
* [Modèle d'application Android helloPush](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/){: new_window}
- [Modèle d'application Cordova](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-hellopush){: new_window}
* [Modèle d'application iOS helloPush](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellopush/){: new_window}

## Logiciel SDK
{: #sdk}
* [Logiciel SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [Logiciel SDK Cordova](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [Logiciel SDK iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}

## Référence d'API
{: #api}
* [Référence d'API Push (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [Référence d'API IMFPush (iOS)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [Référence d'API REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
