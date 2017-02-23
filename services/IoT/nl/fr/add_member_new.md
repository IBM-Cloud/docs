---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestion des accès utilisateur
Dernière mise à jour : 16 septembre 2016
{: .last-updated}

Le tableau de bord d'accès vous permet de contrôler et gérer les accès à votre organisation {{site.data.keyword.iot_full}}. Vous pouvez ajouter des utilisateurs en les ajoutant, en les invitant, en les enregistrant ou en les important. Vous pouvez également accorder différents niveaux d'accès à vos utilisateurs en affectant des rôles.
{:shortdesc}

## Accès utilisateur

Sur l'onglet **Accès** du tableau de bord, vous pouvez ajouter des membres individuels en utilisant les fonctions Ajouter, Inviter ou Enregistrer. Vous pouvez également ajouter, inviter ou enregistrer plusieurs membres en même temps à l'aide de la fonction d'importation.

Par défaut, les comptes des membres n'arrivent jamais à expiration. Lorsque vous ajoutez des utilisateurs à votre organisation {{site.data.keyword.iot_short_notm}}, vous pouvez éventuellement définir une date d'expiration pour leur compte.

### Ajout de membres à votre organisation {{site.data.keyword.iot_short_notm}}

Pour ajouter un membre à votre organisation, vous avez besoin de l'IBMid de ce membre. Pour ajouter un membre, vous n'avez pas besoin de la confirmation de celui-ci.

Pour ajouter un membre à votre organisation {{site.data.keyword.iot_short_notm}} :
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Accès**.
2. Cliquez sur **Ajouter un membre** et sélectionnez **Ajouter**.
3. Entrez l'IBMid du membre.
4. Sélectionnez un rôle pour le membre.
5. Facultatif : Définissez une date d'expiration pour le membre.
6. Cliquez sur **Ajouter un membre**.

Pour ajouter plusieurs membres en même temps, vous devez télécharger un fichier `.csv` contenant l'IBMid, le rôle et la date d'expiration facultative de chaque membre.
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Accès**.
2. Cliquez sur **Ajouter un membre** et sélectionnez **Importer**.
3. Cliquez sur **Ajouter en nombre**.
4. Sélectionnez un rôle par défaut et vérifiez que les numéros de colonne dans votre fichier `.csv` correspondent aux numéros de colonne définis dans les paramètres CSV.
5. Assurez-vous que le séparateur de colonnes dans votre fichier `.csv` correspond au séparateur de colonnes défini dans les paramètres CSV.
6. Cliquez sur **Parcourir** ou faites glisser le fichier `.csv` dans la fenêtre **Télécharger le fichier CSV**.

### Invitation de membres dans votre organisation {{site.data.keyword.iot_short_notm}}

Lorsque vous invitez un utilisateur à devenir un membre de votre organisation {{site.data.keyword.iot_short_notm}}, il reçoit un courrier électronique contenant un lien d'invitation. Les liens d'invitation expirent 48 heures après avoir été envoyés. Si un lien d'invitation n'est pas utilisé dans les 48 heures, l'utilisateur doit être de nouveau invité pour recevoir un nouveau lien d'invitation.

Pour inviter un membre dans votre organisation {{site.data.keyword.iot_short_notm}} :
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Accès**.
2. Cliquez sur **Ajouter un membre** et sélectionnez **Inviter**.
3. Entrez l'adresse électronique du membre.
4. Sélectionnez un rôle pour ce membre.
5. Facultatif : Définissez une date d'expiration pour le membre.
6. Cliquez sur **Inviter un membre**.

Pour inviter plusieurs membres en même temps, vous devez télécharger un fichier `.csv` contenant l'adresse électronique, le rôle et la date d'expiration facultative de chaque membre.
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Accès**.
2. Cliquez sur **Ajouter un membre** et sélectionnez **Importer**.
3. Cliquez sur **Inviter en nombre**.
4. Sélectionnez un rôle par défaut et vérifiez que les numéros de colonne dans votre fichier `.csv` correspondent aux numéros de colonne définis dans les paramètres CSV.
5. Assurez-vous que le séparateur de colonnes dans votre fichier `.csv` correspond au séparateur de colonnes défini dans les paramètres CSV.
6. Cliquez sur **Parcourir** ou faites glisser le fichier `.csv` dans la fenêtre **Télécharger le fichier CSV**.

### Enregistrement d'un membre dans votre organisation {{site.data.keyword.iot_short_notm}}

Si votre organisation n'utilise pas la fonction {{site.data.keyword.ssoshort}} de {{site.data.keyword.Bluemix_notm}}, vous pouvez ajouter des membres individuels à votre organisation en les enregistrant ; cette opération ne requiert pas d'IBMid.

Pour enregistrer un membre auprès de votre organisation {{site.data.keyword.iot_short_notm}} :
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Accès**.
2. Cliquez sur **Ajouter un membre** et sélectionnez **Inviter**.
3. Entrez l'adresse électronique du membre.
4. Sélectionnez un rôle pour ce membre.
5. Entrez l'objet, le nom de domaine et l'émetteur.
   **Important :** Assurez-vous que les zones `Objet`, `Nom de domaine` et `Emetteur` sont conformes aux recommandations et aux normes d'OpenID Connect. Pour plus d'informations, voir le site Web [OpenID Connect ![](../../icons/launch-glyph.svg "")](http://openid.net/connect/ ""){: new_window}. 
6. Facultatif : Définissez une date d'expiration pour le membre.
7. Cliquez sur **Enregistrer un membre**.

Pour enregistrer plusieurs membres en même temps, vous devez télécharger un fichier CSV (`.csv`) contenant l'adresse électronique, le rôle, l'objet, le nom de domaine, l'émetteur et la date d'expiration facultative de chaque membre.
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Accès**.
2. Cliquez sur **Ajouter un membre** et sélectionnez **Importer**.
3. Cliquez sur **Enregistrer en nombre**.
4. Sélectionnez un rôle par défaut et vérifiez que les numéros de colonne dans votre fichier CSV correspondent aux numéros de colonne définis dans les paramètres CSV.
5. Assurez-vous que le séparateur de colonnes dans votre fichier CSV correspond au séparateur de colonnes défini dans les paramètres CSV.
6. Cliquez sur **Parcourir** ou faites glisser le fichier CSV dans la fenêtre **Télécharger le fichier CSV**.

### Construction de votre fichier CSV

Lorsque vous construisez un fichier CSV pour importer des membres dans votre organisation, prenez soin d'inclure les informations requises pour la méthode que vous utilisez. Utilisez des virgules ou des points-virgule pour séparer les colonnes. Lorsque vous téléchargez le fichier CSV, sous **Paramètres CSV**, prenez soin de sélectionner le séparateur de colonnes approprié.
