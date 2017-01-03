---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuration des données d'identification pour le navigateur Web Safari
{: #configure-credential-for-safari}
Dernière mise à jour : 6 décembre 2016
{: .last-updated}

Le service IBM {{site.data.keyword.mobilepushshort}} étend désormais les capacités d'envoi de notifications à votre navigateur Safari. Notez que la version prise en charge est Safari 10.0.

## Génération d'un certificat
  {: #certificate-generation}

Assurez-vous que vous disposez d'un compte Développeur Apple. Vous devez enregistrer un ID push du site web et générer un certificat afin de configurer votre navigateur Safari pour la réception des notifications. Les étapes suivantes vous aideront à démarrer.

1. Dans le centre des membres développeurs Apple, cliquez sur **Certificates, ID & Profiles**. 
2. Cliquez sur **Identifiers**, puis sur **Website Push IDs**.
3. Choisissez de créer une nouvelle entrée en sélectionnant l'icône plus.
  ![Tableau de bord Push](images/safari_1.jpg)

4. Dans le panneau Register Website Push ID, indiquez une description et un identificateur d'ID Push de site Web appropriés. Il est recommandé d'utiliser un format de nom de domaine inverse, en commençant par 'web'. Par exemple : web.com.example.dailyweatherreports.
5. Enregistrez l'ID Push de site Web. Vous disposez à présent de votre ID Push de site Web 
6. Sélectionnez **Editer** pour créer un certificat à utiliser pour l'ID Push de site Web.
7. Dans la fenêtre Certificate Assistant de Certificate Information, indiquez votre ID de courrier électronique et un nom usuel. N'indiquez pas l'adresse de courrier électronique de l'autorité de certification.
8. Cliquez sur **Save to disk** et sélectionnez **Continue**.
9. Choisissez d'enregistrer le certificat dans un dossier approprié.
10. Sélectionnez la demande `.certSigningRequest` créée sur le disque à l'invite par l'assistant de générer le certificat. Prenez soin de télécharger le certificat push de site Web créé au format `.cer`.
11. Ouvrez le certificat dans l'outil KeyChain Access. Cliquez sur le bouton droit de la souris et exportez-le en tant que certificat p12. Notez le mot de passe fourni lors de la génération du certificat p12.


## Configuration pour notifications
  {: #configuration-notification}
 
Après avoir généré le certificat, vous devez configurer le service pour envoyer des notifications à Safari. 

Procédez comme suit :

1. Dans le tableau de bord du service Push Notifications, **cliquez sur Configurer**. 
2. Sélectionnez l'onglet Web. 
3. Dans la section Safari Push, mettez à jour le formulaire avec les informations requises. 
	- **Nom du site web **: nom que vous avez indiqué dans le centre de notification.
	- **ID push du site web **: mettez à jour cette zone avec la chaîne de domaine inverse pour votre ID push de site Web. Par exemple, web.com.example.www.
	- **URL du site Web **: indiquez l'URL du site Web à abonner pour les notifications push. Par exemple, https://www.example.com.
	- **Domaines autorisés **: ce paramètre est facultatif. Il s'agit de la liste des sites Web qui réclament une permission de l'utilisateur. Vérifiez que les URL sont des valeurs séparées par des virgules. Notez que la valeur de l'URL de site Web sera utilisée si cette liste n'est pas fournie. 
	- **Chaîne de format de l'URL **: URL à résoudre lors d'un clic sur la notification. Par exemple, ["https://www.example.com"]. L'URL doit utiliser le schéma http ou https.
	- **Certificat push web Safari **: téléchargez le certificat .p12 et fournissez le mot de passe.
4. Cliquez sur **Sauvegarder**.	

![Tableau de bord Push](images/push_configure_safari.jpg)	

Vous avez effectué la configuration pour envoyer des notifications push au navigateur Safari.

	
