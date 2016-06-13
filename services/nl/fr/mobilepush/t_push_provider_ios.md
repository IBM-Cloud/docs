
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Configuration de données d'identification pour le service Apple Push Notifications (APNs)

{: #create-push-credentials-apns}

Le service Apple Push Notification (APNs) permet au développeur d'applications d'envoyer des notifications distantes depuis l'instance du service
Push dans Bluemix (le fournisseur) à des applications et des périphériques iOS. Les messages sont envoyés à une application cible sur le
périphérique. Obtenez et configurez vos données d'identification APNs. Les certificats APNs sont gérés de façon sécurisée par le service Push Notifications
et utilisés pour la connexion au serveur APNs en tant que fournisseur.

1. Procurez-vous un compte [Apple Developers](https://developer.apple.com/).
2. [Enregistrez un ID d'application](#create-push-credentials-apns-register)
3. [Créez un certificat SSL APNs pour le développement et la distribution
](#create-push-credentials-apns-ssl)
4. [Créez un profil de mise à disposition pour le développement](#create-push-credentials-dev-profile)
5. [Créez un profil de mise à disposition pour la distribution dans un magasin](#create-push-credentials-apns-distribute_profile)
6. [Configurez APNs dans le tableau de bord Push](#create-push-credentials-apns-dashboard)



##Enregistrement d'un ID d'appli
{: #create-push-credentials-apns-register}


L'ID d'application (l'identificateur de bundle) est un identificateur unique identifiant une application spécifique. Chaque application
requiert un ID d'application. Les services tels que Push Notifications sont configurés avec l'ID d'appli.




1. Accédez au portail [Apple Developer](https://developer.apple.com), cliquez sur **Member Center**, puis sélectionnez **Certificates, Identifiers & Profiles**.
2. Accédez à la section **Registering App IDs** dans [Apple Developer Library](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991) et suivez les instructions d'enregistrement de l'ID d'appli.

	**Remarque** : Lorsque vous enregistrez un ID d'appli, sélectionnez les options suivantes :
	* Notifications push

	![Services d'appli](images/appID_appservices_enablepush.jpg)

	* Suffixe d'ID explicite

	![ID explicite](images/appID_bundleID.jpg)
3. Etapes suivantes. Créez un certificat SSL APNs pour le développement et la distribution.

##Créez un certificat SSL APNs pour le développement et la distribution
{: #create-push-credentials-apns-ssl}

Pour pouvoir obtenir un certificat APNs, vous devez générer une demande de signature de certificat et la soumettre à Apple, l'autorité de
certification. La demande de signature de certificat contient des informations qui identifient votre société, ainsi que votre clé publique et votre clé
privée que vous utilisez pour signer vos notifications push Apple. Ensuite, générez le certificat SSL dans le portail des développeurs iOS. Le
certificat, avec sa clé publique et sa clé privée, est stocké dans Keychain Access.

**Avant de commencer**

[Enregistrez un ID d'application](#create-push-credentials-apns-register)

APNs peut être utilisé dans deux modes : bac à sable et production.

* Le mode bac à sable est utilisé au cours du développement et du test.
* Le mode production est utilisé lors de la distribution des applications via l'App Store (ou d'autres mécanismes de distribution d'entreprise).

Vous devez vous procurer des certificats distincts pour vos environnements de développement et de distribution. Les certificats sont
associés à un ID d'application pour l'application qui est le destinataire des notifications distantes. Pour la production, vous pouvez créer jusqu'à deux certificats. Bluemix utilise les certificats afin d'établir une connexion SSL à APNs.

Créez un certificat SSL pour le développement et la distribution.


1. Accédez à [Apple Developer](https://developer.apple.com), cliquez sur **Member Center**, puis sélectionnez **Certificates, Identifiers & Profiles**.
2. Dans la zone **Identifiers**, cliquez sur **App IDs**.
3. Dans la liste des ID d'appli, sélectionnez l'ID d'appli que vous venez de créer, puis sélectionnez **Settings**.
4. Dans la zone **Push Notifications**, créez un certificat SSL de développement, puis un certificat SSL de production.
 
	![Certificats SSL de notification push](images/certificate_createssl.jpg)

	L'écran About Creating a Certificate a Signing Request s'affiche.

	![Ecran Creating a Certificate a Signing Request](images/request.jpg)

5. Sur votre Mac, démarrez l'application **Keychain Access** afin de créer une demande de signature de certificat.
6. Sélectionnez **Keychain Access > Certificate Assistant > Request a Certificate From a Certificate Authority…** ![Keychain Access](images/keychain_request_certificate.jpg)
7. Dans **Certificate Information**, entrez votre adresse électronique qui est associée à votre compte App Developer et un nom usuel. Attribuez un nom significatif qui permet d'identifier s'il s'agit d'un certificat pour le développement (bac à sable) ou pour la distribution
(production), par exemple **certificat_apns_bacàsable** ou
**certificat_apns_production**.

8. Sélectionnez **Saved to disk** pour télécharger le fichier **.certSigningRequest** sur votre bureau, puis
cliquez sur **Continue**.
9. Dans **Save As**, nommez le fichier **.certSigningRequest**, par exemple
**bacàsable.certSigningRequest**, puis cliquez sur **Save**.
10. Cliquez sur **Done**. A présent, vous possédez une demande de signature de certificat.
11. Depuis l'écran **About Creating a Certificate a Signing Request (CSR)**, cliquez sur **Continue**. 12. ![Ecran Certificate a Signing Request](images/request.jpg)
12. Dans l'écran **Generate**, cliquez sur **Choose File...** et sélectionnez le fichier de demande de signature de
certificat que vous avez sauvegardé sur votre bureau. Ensuite, cliquez sur **Generate**.


	![Générer le certificat](images/generate_certificate.jpg)

13. Lorsque votre certificat est prêt, cliquez sur **Done**.
14. Sur l'écran **Push Notifications**, cliquez sur **Download** pour télécharger votre certificat, puis cliquez sur **Done**. ![Téléchargement d'un certificat](images/certificate_download.jpg)
15. Sur votre Mac, accédez à **Keychain Access > My Certificates** et localisez le certificat que vous venez d'installer. Cliquez deux fois sur le certificat pour l'installer dans Keychain Access.
16. Sélectionnez le certificat et la clé privée, puis sélectionnez **Export** pour convertir le certificat au format d'échange d'informations personnelles (format .p12).

	![Exportation de certificat et de clés](images/keychain_export_key.jpg)

17. Dans la zone **Save As**, nommez le certificat de façon à pouvoir l'identifier par la suite (par exemple **certificat_sandbox_apns.p12** ou **production_apns.p12**), puis cliquez sur **Save**.

   	![Exportation de certificat et de clés](images/certificate_p12v2.jpg)

18. Dans la zone **Enter a password**, entrez un mot de passe pour protéger les éléments exportés, puis cliquez sur **OK**. Vous aurez besoin de ce mot de passe pour configurer ultérieurement vos paramètres APNs dans le tableau de bord Push.

	![Exportation de certificat et de clés](images/export_p12.jpg)
19. **Key Access.app** vous invite à exporter votre clé depuis l'écran **Keychain**. Entrez le mot de passe administrateur pour votre Mac pour permettre au système d'exporter ces éléments, puis sélectionnez l'option **Always Allow**. Un certificat .p12 est généré sur votre bureau.


##Création d'un profil de mise à disposition pour le développement
{: #create-push-credentials-dev-profile}

Le profil de mise à disposition est utilisé conjointement avec l'ID d'application pour déterminer quels sont les périphériques qui
peuvent installer et exécuter votre application et quels sont les services auxquels votre application peut accéder. Pour chaque ID d'application, vous créez deux profils de mise à disposition : un pour le développement et un pour la distribution. Xcode utilise le profil de mise à disposition pour le développement afin de déterminer quels sont les développeurs qui sont autorisés à construire
l'application et quels sont les périphériques qui peuvent être testés avec l'application.

**Avant de commencer**

Assurez-vous d'avoir enregistré un ID d'application, de l'avoir activé pour le service Push Notifications, et de
l'avoir configuré pour l'utilisation d'un certificat SSL APNs pour le développement et la production.

Créez un profil de mise à disposition pour le développement.

1. Accédez au portail [Apple Developer](https://developer.apple.com), cliquez sur **Member Center**, puis sélectionnez **Certificates, Identifiers & Profiles**.
2. Accédez au site [Mac Developer Library](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site), faites défiler la page jusqu'à la section **Creating Development Provisioning Profiles** et suivez les instructions de création
d'un profil de développement.

	**Remarque** : Lorsque vous configurez un profil de mise à disposition pour le développement, sélectionnez les options suivantes :
	* **iOS App Development**
	* **For iOS and watchOS apps **



##Création d'un profil de mise à disposition pour la distribution dans un magasin
{: #create-push-credentials-apns-distribute_profile}

Utilisez le profil de mise à disposition dans un magasin afin de soumettre votre application pour la distribution dans l'App Store.

1. Accédez au portail [Apple Developer](https://developer.apple.com), cliquez sur **Member Center**, puis sélectionnez **Certificates, Identifiers & Profiles**.
2. Cliquez deux fois sur le profil de mise à disposition téléchargé afin de l'installer dans Xcode.

##Configuration d'APNs sur le tableau de bord Push Notifications
{: #create-push-credentials-apns-dashboard}

Afin d'utiliser le service Notification push pour envoyer des notifications, téléchargez les certificats SSL requis pour Apple Push Notification service (APNs). Vous
pouvez également utiliser l'API REST pour télécharger un certificat APNs.


**Avant de commencer**


Procurez-vous le certificat SSL APNs pour le développement et la production ainsi que le mot de passe associé à chaque type de certificat. Pour obtenir des informations, voir Création et configuration des données d'identification
Push pour APNs.

Les certificats requis pour APNs sont des certificats
.p12, qui contiennent la clé privée et des certificats SSL nécessaires pour la
construction et la publication de votre application. Vous devez générer les certificats depuis le Member Center du site Web Apple Developer (pour lequel un
compte Apple Developer valide est requis). Des certificats distincts sont requis pour l'environnement de développement (bac à sable) et l'environnement de production
(distribution).

**Remarque** : Une fois le fichier **cer** dans votre accès à la chaîne de certificats, exportez-le sur votre ordinateur pour créer un certificat .p12.

Pour plus d'informations sur APNs, voir
[iOS Developer Library: Local and Push
Notification Programming Guide](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4).

Configuration d'APNs sur le tableau de bord Push

1. Ouvrez votre application de back end dans le tableau de bord Bluemix, puis cliquez sur le service **IBM Push Notifications**
afin d'ouvrir le tableau de bord Push.

	![IBM Push Notifications](images/bluemixdashboard_push.jpg)

	Le tableau de bord Push s'affiche.
	
	![Définition des notifications push](images/wizard.jpg)
1
2. Dans l'onglet **Configuration**, accédez à la section **Apple Push Certificate**, sélectionnez **Bac à sable** (développement) ou **Production** (distribution), puis téléchargez le certificat p.12 dans Bluemix.

	![Définition des notifications push](images/credential_screen.jpg)
3. Dans la zone **Mot de passe**, entrez le mot de passe qui est associé au fichier de certificat **.p12**, puis cliquez sur **Sauvegarde**.
Une fois les certificats téléchargés avec un mot de passe valide, vous pouvez commencer à envoyer des notifications.

