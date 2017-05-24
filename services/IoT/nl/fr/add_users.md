---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestion des accès utilisateur
{: #managing-user-access}

Le tableau de bord des membres vous permet de contrôler et gérer les accès à votre organisation {{site.data.keyword.iot_full}}. Vous pouvez ajouter des utilisateurs en les ajoutant, en les invitant<!--, registering--> ou en les important. Vous pouvez également accorder différents niveaux d'accès à vos utilisateurs en affectant des rôles.
{:shortdesc}

## Ajout d'utilisateurs
{: #adding-new-users}

Sur l'onglet **Membres** du tableau de bord, vous pouvez ajouter des membres individuels en utilisant les fonctions<!--Add, Invite, or Register-->  Ajouter ou Inviter. Vous pouvez également <!--add, invite, or register-->ajouter ou inviter plusieurs membres simultanément en utilisant la fonction Importer.

Par défaut, les comptes des membres n'arrivent jamais à expiration. Lorsque vous ajoutez des utilisateurs à votre organisation {{site.data.keyword.iot_short_notm}}, vous pouvez éventuellement définir une date d'expiration pour leur compte.

### Ajout de membres à votre organisation {{site.data.keyword.iot_short_notm}}

Pour ajouter un membre à votre organisation, vous avez besoin de l'IBMid de ce membre. Pour ajouter un membre, vous n'avez pas besoin de la confirmation de celui-ci.

Pour ajouter un membre à votre organisation {{site.data.keyword.iot_short_notm}} :
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Membres**.
2. Cliquez sur **Ajouter des membres** et sélectionnez l'onglet **Ajouter**.
3. Entrez l'IBMid du membre.
4. Sélectionnez un rôle pour le membre.
5. Facultatif : Définissez une date d'expiration pour le membre.
6. Cliquez sur **Ajouter**.

Pour ajouter plusieurs membres en même temps, vous devez télécharger un fichier `.csv` contenant l'IBMid, le rôle et la date d'expiration facultative de chaque membre. Pour plus d'informations, voir [Construction de votre fichier CSV](#constructing-your-csv).
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Membres**.
2. Cliquez sur **Ajouter des membres** et sélectionnez l'onglet **Importer**.
3. Recherchez vos fichiers ou faites glisser le fichier `.csv` dans la fenêtre **Télécharger le fichier CSV**.
4. Sélectionnez un rôle par défaut à utiliser si un rôle indiqué dans le fichier CSV n'est pas reconnu.
5. Mappez les membres de colonne de votre fichier CSV aux entrées d'IBMid, de rôle et, le cas échéant, de date d'expiration correspondantes.
6. Sélectionnez le séparateur de colonne virgule ou point-virgule approprié selon le séparateur utilisé dans votre fichier `.csv`.
7. Cliquez sur **Importer** pour importer les IBMid et créez les membres.


### Invitation de membres dans votre organisation {{site.data.keyword.iot_short_notm}}

Lorsque vous invitez un utilisateur à devenir un membre de votre organisation {{site.data.keyword.iot_short_notm}}, il reçoit un courrier électronique contenant un lien d'invitation. Les liens d'invitation expirent 48 heures après avoir été envoyés. Si un lien d'invitation n'est pas utilisé dans les 48 heures, l'utilisateur doit être de nouveau invité pour recevoir un nouveau lien d'invitation.

**Important :** La fonction Inviter nécessite un service de messagerie configuré. Pour plus d'informations, voir la section Courrier électronique de la rubrique [Intégrations de service externe](reference/extensions/index.html#email).

Pour inviter un membre dans votre organisation {{site.data.keyword.iot_short_notm}} :
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Membres**.
2. Sélectionnez l'onglet **Invitations**.
2. Cliquez sur **Inviter des membres** et sélectionnez l'onglet **Inviter**.
3. Entrez l'adresse électronique du membre.
4. Sélectionnez un rôle pour ce membre.
5. Facultatif : Définissez une date d'expiration pour le membre.
6. Cliquez sur **Inviter un membre**.

Pour inviter plusieurs membres en même temps, vous devez télécharger un fichier `.csv` contenant l'adresse électronique, le rôle et la date d'expiration facultative de chaque membre. Pour plus d'informations, voir [Construction de votre fichier CSV](#constructing-your-csv).
1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, accédez à **Membres**.
2. Sélectionnez l'onglet **Invitations**.
2. Cliquez sur **Inviter des membres** et sélectionnez l'onglet **Importer**.
3. Recherchez vos fichiers ou faites glisser le fichier `.csv` dans la fenêtre **Télécharger le fichier CSV**.
4. Sélectionnez un rôle par défaut à utiliser si un rôle indiqué dans le fichier CSV n'est pas reconnu.
5. Mappez les membres de colonne de votre fichier CSV aux entrées d'adresse électronique, de rôle et, le cas échéant, de date d'expiration correspondantes.
6. Sélectionnez le séparateur de colonne virgule ou point-virgule approprié selon le séparateur utilisé dans votre fichier `.csv`.
7. Cliquez sur **Importer** pour envoyer les invitations.

<!-- ### Registering a member with your {{site.data.keyword.iot_short_notm}} organization

If your organization is using {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, you can add individual members to your organization by registering them, which does not require an IBMid.

To register a member with your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Select the **Invitations** tab.
2. Click **Invite Members** and select **Invite**.
3. Enter the email address of the member.
4. Select a role for this member.
5. Enter the subject, realm name, and issuer.
   **Important:** Ensure that the `Subject`, `Realm Name`, and `Issuer` fields comply with the OpenID Connect recommendations and standards. For more information, see the [OpenID Connect ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://openid.net/connect/){: new_window} website.
6. Optional: Set an expiry date for the member.
7. Click **Register Member**.

To register multiple members simultaneously, you must upload a CSV (`.csv`) file that contains the email address, role, subject, realm name, issuer, and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Register**.
4. Select a default role and ensure that the column numbers on your CSV file match the column numbers in the CSV settings.
5. Ensure the column separator in your CSV file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the CSV file into the **Upload CSV** window. -->

### Construction de votre fichier CSV
{: #constructing-your-csv}

Lorsque vous construisez un fichier CSV pour importer des membres dans votre organisation, prenez soin d'inclure les informations requises pour la méthode que vous utilisez. Utilisez des virgules ou des points-virgule pour séparer les colonnes.  
**Important :** Lorsque vous téléchargez le fichier CSV, sous **Paramètres CSV**, prenez soin de sélectionner le séparateur de colonne approprié.

Exemple de fichier CSV avec une délimitation à l'aide d'une virgule :  
```
user1@sample.com,PD_DEVELOPER_USER,1489505652152
user2@sample.com,PD_OPERATOR_USER,1489505652152
user3@sample.com,PD_ADMIN_USER,1489505652152
```

Où les entrées de colonne suivantes sont utilisées :  
- Colonne 1 : adresse électronique de l'utilisateur.  
Si vous ajoutez des membres, prenez soin d'utiliser l'adresse électronique correspondant à un IBMid valide. Si vous invitez des membres, vous pouvez utiliser n'importe quelle adresse électronique valide.
- Colonne 2 : rôle à affecter à l'utilisateur.  
Entrez l'un des rôles suivants :
 - PD_ADMIN_USER
 - PD_OPERATOR_USER
 - PD_DEVELOPER_USER
 - PD_ANALYST_USER
 - PD_READER_USER  
 Pour plus d'informations sur les rôles utilisateur, voir [Rôles d'utilisateur, d'application et de passerelle](roles_index.html#user_roles).
- Colonne 3: Horodatage Unix (exprimé en millisecondes depuis le 1er janvier 1970, 00:00 UTC) correspondant à la date d'expiration de l'utilisateur.

## Edition d'utilisateurs
{: #editing-users}

Les utilisateurs peuvent être édités pour modifier leur rôle, ajouter, retirer ou modifier une date d'expiration d'accès ou ajouter ou retirer des droits d'accès à l'organisation.

1. Depuis votre tableau de bord {{site.data.keyword.iot_short_notm}}, cliquez sur **Membres** dans la barre de navigation sur la gauche.
2. Cliquez sur l'icône **Editer** en regard de l'utilisateur que vous souhaitez éditer.
3. Apportez les modifications souhaitées à l'utilisateur.
4. Cliquez sur **Sauvegarder**.

## Blocage de l'accès utilisateur
{: #blocking-users}

Il est possible de bloquer l'accès des utilisateurs à l'organisation {{site.data.keyword.iot_short_notm}} tout en conservant l'appartenance de ces utilisateurs à l'organisation.

1. Depuis votre tableau de bord {{site.data.keyword.iot_short_notm}}, cliquez sur **Membres** dans la barre de navigation sur la gauche.
2. Cliquez sur le bouton à bascule en regard de l'utilisateur dont vous souhaitez bloquer l'accès à l'organisation {{site.data.keyword.iot_short_notm}}.


## Retrait d'utilisateurs
{: #removing-users}

Les utilisateurs peuvent être entièrement retirés de l'organisation {{site.data.keyword.iot_short_notm}}. Le retrait d'utilisateurs ne peut pas être annulé, et les utilisateurs doivent être [ajoutés à la plateforme](#adding-new-users) pour restaurer leur accès.

1. Depuis votre tableau de bord {{site.data.keyword.iot_short_notm}}, cliquez sur **Membres** dans la barre de navigation sur la gauche.
2. Cliquez sur l'icône **Supprimer** en regard de l'utilisateur à retirer.
3. Cliquez sur **Supprimer** dans la boîte de dialogue de confirmation.
