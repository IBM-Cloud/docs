---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Envoi de notifications de base aux Applications et extensions Google Chrome 
{: #web_extensions_notifications}
Dernière mise à jour : 11 janvier 2017
{: .last-updated}

Une fois que vous avez développé vos applications, vous pouvez envoyer une notification push. 

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant **Notifications Web** comme option **Envoyer à**. 
2. Entrez le message qui doit être distribué dans la zone **Message**.
3. Vous pouvez choisir de fournir des paramètres facultatifs :
  - **Titre de la notification** : il s'agit du texte qui s'affichera comme en-tête de l'alerte du message.
  - **URL de l'icône de notification** : si votre message doit être distribué avec une icône de notification d'application, fournissez dans cette zone le lien à l'icône.
  - **Touche de réduction** : des touches de réduction sont attachées aux notifications. Si plusieurs notifications arrivent séquentiellement avec la même touche de réduction quand l'appareil est hors ligne, elles sont réduites. Quand un appareil passe en ligne, il reçoit des notifications du serveur FCM/GCM et n'affiche que la dernière notification portant la même touche de réduction. Si aucune touche de réduction n'est définie, les nouveaux et les anciens messages sont stockés pour une distribution future.
  - **Durée de vie** : cette valeur est définie en secondes. Si ce paramètre n'est pas spécifié, le serveur FCM/GCM stocke le message pendant quatre semaines et tente de le distribuer. La validité expire après quatre semaines. La plage des valeurs possibles va de 0 à 2419200 secondes.
  - ****Retarder si inactif : en définissant cette valeur à `true`, vous demandez au serveur FCM/GCM de ne pas distribuer de notification si le serveur est inactif. Définissez cette valeur à `false` pour garantir la distribution de la notification même si l'appareil est en veille.
  - **Contenu supplémentaire** : spécifie les valeurs de contenu personnalisées pour vos notifications.

L'image suivante montre l'option Applications et extensions Google Chrome du tableau de bord.

  ![Ecran Notifications](images/push_chrome_extns.jpg)
  
## Etapes suivantes
  {: #next_steps_tags}

Une fois que vous avez configuré les notifications de base, vous pouvez choisir de configurer des notifications basées sur des balises et des options
avancées.

Ajoutez ces fonctions de service {{site.data.keyword.mobilepushshort}} à votre application. Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html). Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).
