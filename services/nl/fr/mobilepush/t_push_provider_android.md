
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Configuration de données d'identification pour Google Cloud Messaging (GCM)
{: #create-push-enable-gcm}

Obtenez vos données d'identification Google Cloud Messaging (GCM), puis configurez le service Push Notifications dans le tableau de bord Push.

##Obtention de votre ID d'émetteur et de la clé d'API

La clé d'API est stockée de façon sécurisée et utilisée par le service Push Notifications pour la connexion au serveur GCM. L'ID d'émetteur (numéro de projet) est utilisé par le logiciel SDK Android côté client. Pour plus d'informations sur l'ID émetteur, voir [Google Cloud Message](https://developers.google.com/cloud-messaging/gcm#arch).

1. Créez un compte de développement Google à l'aide de la [console des développeurs Google](https://console.developers.google.com/start){: new_window}. Pour plus d'informations sur Google Cloud Messaging (GCM), voir [Creating a Google API Project](https://developers.google.com/console/help/new/){: new_window}.

2. Dans la console des développeurs Google, créez un projet, par exemple "hello world".

	![Créez un projet](images/gcm_createproject.jpg)

3. Dans la zone **Project name**, entrez le nom de votre projet, puis cliquez sur le bouton **Create**.
4. Cliquez sur **Home** pour afficher le numéro du projet. Documentez votre numéro de projet.

	![Numéro de projet GCM](images/gcm_projectnumber.jpg)

	**Remarque** : Lorsque vous créez votre projet, un numéro de projet (ID d'émetteur) est créé. Utilisez-le pour configurer le service Push Notifications dans le tableau de bord Push.

5. Cliquez sur **APIs & Auth** et, dans la section **Mobile APIs**, cliquez sur **Cloud Messaging for Android**.

	![API](images/gcm_mobileapi.jpg)

6. Cliquez sur **APIs**, puis cliquez sur le bouton **Enable API** pour créer votre clé d'API pour votre projet.

	![Activation d'API](images/gcm_enable_api.jpg)

7. Accédez à l'écran **APIs & Auths -> Credentials**. Cliquez sur **Add Credentials**, puis cliquez sur **API Key**.

	![Données d'identification d'API](images/api_credentials.jpg)

8. Cliquez sur l'option **Server Key** pour générer une clé d'API GCM que vous utiliserez dans le tableau de bord Push de Bluemix.
9. Dans la zone **Name**, entrez le nom de la clé d'API de serveur.

	![Clé de serveur GCM](images/gcm_serverkey.jpg)

10. Cliquez sur le bouton **Create**. 
La clé d'API est affichée.

	![Clé d'API GCM](images/gcm_apikey.jpg)

11. Copiez votre clé d'API GCM, puis cliquez sur le bouton **OK**. Vous aurez besoin du numéro de projet (ID d'émetteur) et de la clé d'API pour configurer vos données d'identification dans l'écran Configuration du tableau de bord Push Notifications de Bluemix. 
12. Etapes suivantes. Configuration du service Push Notifications pour Android.

##Configuration du service Push Notifications pour Android

**Avant de commencer**

Obtenez une clé d'API GCM et un ID d'émetteur (numéro de projet). 

1. Ouvrez votre application de back end dans le tableau de bord Bluemix, puis cliquez sur IBM Push Notifications pour ouvrir le tableau de bord du service Push Notifications.
 
	![Tableau de bord Push](images/bluemixdashboard_push.jpg)

	Le tableau de bord Push s'affiche.
	
	![Configuration de Push](images/setup_push_main.jpg)

2. Cliquez sur le bouton **Setup Push** pour configurer les données d'identification GCM.
1. Sur l'onglet **Configuration**, accédez à la section **Google Cloud Messaging** et configurez l'ID d'émetteur (numéro de projet CGM) et la clé d'API.

4. Cliquez sur le bouton **Save**. 
5. Etapes suivantes. [Activation des notifications pour Android](c_enable_push.html).
