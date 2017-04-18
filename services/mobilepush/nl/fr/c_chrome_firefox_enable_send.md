---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Envoi de notifications de base aux navigateurs Web
{: #web_notifications}
Dernière mise à jour : 11 janvier 2017
{: .last-updated}

Une fois que vous avez développé vos applications, vous pouvez envoyer une notification push. 

1. Sélectionnez **Envoyer des notifications** et rédigez un message en choisissant **Notifications Web** comme option **Envoyer à**. 
2. Entrez le message qui doit être distribué dans la zone **Message**.
3. Vous pouvez choisir de fournir des paramètres facultatifs :
  - **Titre de la notification** : il s'agit du texte qui s'affichera comme en-tête de l'alerte du message.
  - **URL de l'icône de notification** : si votre message doit être distribué avec une icône de notification d'application, fournissez dans cette zone le lien à l'icône.
  - **Time to live** : avise le serveur de la validité des messages.
4. Pour les notifications Web envoyées au navigateur Safari, certaines informations supplémentaires sont requises :
  - **Action** : libellé du bouton d'action.
  - **URL Arguments** : arguments d'URL à utiliser avec cette notification. Doivent être soumis sous forme de tableau JSON. 
 
L'image suivante montre l'option Notifications Web du tableau de bord.

  ![Ecran Notifications](images/DashboardWebpush.jpg)


## Etapes suivantes
  {: #next_steps_tags}

Une fois que vous avez configuré les notifications de base, vous pouvez choisir de configurer des notifications basées sur des balises et des options
avancées.

Ajoutez ces fonctions de service {{site.data.keyword.mobilepushshort}} à votre application. Pour utiliser des notifications basées sur les balises, voir [Notifications basées sur les balises](c_tag_basednotifications.html). Pour utiliser des options de notification avancées, voir [Activation des notifications push avancées](t_advance_badge_sound_payload.html).



