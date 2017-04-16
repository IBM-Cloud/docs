---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des notifications Rich Media (média enrichi)
{: #interactive-notifications}
Dernière mise à jour : 11 janvier 2017
{: .last-updated}


Vous pouvez activer Rich Media {{site.data.keyword.mobilepushshort}} dans iOS 10 et versions ultérieures. Les notifications Push peuvent être
envoyées avec un contenu audio, vidéo, des GIF et des images. 

Pour configurer votre application pour recevoir des contenus push enrichis dans iOS 10, procédez comme suit :  

1. Dans Xcode, sélectionnez **Fichier** > **Nouveau ** > **Cible** > **Extension de
service de notification**.
2. Sur la méthode `didReceive()` dans `UNNotificationServiceExtension`, ajoutez le code.
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
Pour envoyer un contenu Rich Media {{site.data.keyword.mobilepushshort}} depuis le tableau de bord Push, prenez soin de renseigner les zones
message, titre, sous-titre et attachmentURL.
