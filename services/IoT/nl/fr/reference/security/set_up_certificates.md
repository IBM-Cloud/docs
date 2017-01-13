---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuration des certificats
{: #set_up_certificates.md}
Dernière mise à jour : 15 novembre 2016
{: .last-updated}

Avec le module complémentaire Gestion des risques et de la sécurité, les certificats sont utilisés pour l'authentification de terminal ou pour remplacer le certificat de serveur IBM Watson IoT Platform par défaut pour la messagerie MQTT. Tous les terminaux qui ne disposent pas de certificats signés valides se voient refuser l'accès et ne peuvent pas communiquer avec le serveur.

Pour configurer les certificats et l'accès au serveur pour les terminaux, l'opérateur du système enregistre les certificats d'autorité de certification associés (AC) et enregistre éventuellement les certificats du serveur de messages dans la plateforme Watson IoT.

## Exigences du certificat

L'ID de terminal doit être entré comme nom commun (CN) ou SubjectAltName dans le certificat que vous enregistrez. Pour la zone *CN*, le format est CN=d:devtype:devid. Pour la zone SubjectAltName, le format est : SubjectAltName=d:devtype:devid où devtype est le type de terminal et devid est l'ID client du terminal.

L'utilisation d'une liste de révocation de certificats pour indiquer quels terminaux ne sont plus autorisés à se connecter n'est pas prise en charge dans la version bêta.

Si vous ajoutez un certificat d'autorité de certification ou que vous remplacez le certificat du serveur de messagerie, tous les terminaux doivent se connecter à l'aide d'un client MQTT prenant en charge SNI (Server Name Indication). Avec l'architecture en multilocation, SNI indique au serveur MQTT quels certificats doivent être utilisés pour chaque connexion organisation/locataire.

##Enregistrement de certificats d'autorité de certification (AC) pour l'authentification de terminaux

1. Connectez-vous à Watson IoT Platform et accédez à **Paramètres généraux**.
2. Dans la section **Gestion des risques**, sous **Certificats d'autorité de certification**, cliquez sur **Ajouter un certificat**.
3. Parcourez pour sélectionner un fichier de certificat à télécharger ou faites glisser un fichier dans la fenêtre **Ajout de certificat**. Le fichier ne peut contenir qu'un seul certificat et les dates du certificat doivent être valides. Les fichiers qui ont des extensions .pem, .cer, .cert ou .crt sont acceptés. Vous pouvez prévisualiser les informations de certificat dans le fichier sélectionné.
4. Entrez une description du fichier de certificat.
5. Confirmez que le fichier correct est sélectionné et cliquez sur **Sauvegarder**. Le certificat sélectionné est répertorié dans le tableau et est actif par défaut.

## Enregistrement des certificats du serveur de messagerie

Les certificats de serveur par défaut sont fournis avec la plateforme. Vous pouvez utiliser l'un des certificats par défaut ou en télécharger un de votre organisation. Si vous n'avez pas encore de certificat à utiliser, vous pouvez créer une demande pour un nouveau certificat. Après avoir reçu le nouveau certificat, vous devez le signer et le retransférer vers la plateforme.

Pour utiliser l'un des certificats par défaut ou un autre certificat qui a déjà été téléchargé, sélectionnez le certificat que vous souhaitez utiliser dans la liste déroulante des **certificats du serveur de messagerie par défaut** dans le tableau, sous les **certificats de serveur de messagerie**.

### <a name="upload"> </a> Téléchargement d'un certificat de votre organisation

1. Dans la section **Gestion des risques** des **Paramètres généraux**, sous **Certificats de serveur de messagerie**, cliquez sur **Ajouter un certificat**.
2. Parcourez pour sélectionner un fichier de certificat à télécharger ou faites glisser un fichier dans la fenêtre **Ajout de certificat**. 
3. Parcourez pour sélectionner le fichier de clé privée à télécharger ou faites glisser un fichier dans la fenêtre **Ajout de certificat**.   
4. Entrez la phrase passe de la clé privée si la clé privée a été chiffrée avec une phrase passe.
5. Confirmez que le fichier correct est sélectionné et cliquez sur **Sauvegarder**. 
6. Sélectionnez le certificat téléchargé dans la liste déroulante des **Certificats du serveur de messagerie par défaut**. Le certificat sélectionné est répertorié dans le tableau en tant que certificat actif.


### Demande d'un nouveau certificat

 Si vous souhaitez utiliser un nouveau certificat de serveur de messagerie, vous pouvez générer une demande de signature de certificat (CSR) pour demander un nouveau certificat.

 1. Dans la section **Gestion des risques** des **Paramètres généraux**, sous **Certificats de serveur de messagerie**, cliquez sur **Générer la demande de signature de certificat**.
 2. Entrez les détails pour solliciter une demande de signature de certificat (CSR) pour votre serveur, puis cliquez sur **Générer**. La demande de signature de certificat est affichée dans le tableau.
 3. Téléchargez la demande et soumettez-la à une autorité de certification pour signature.
 4. Après avoir obtenu un certificat, vous pouvez le télécharger en effectuant les étapes de la section Téléchargement d'un certificat de votre organisation. Une fois le certificat téléchargé, la demande de signature de certificat dans le tableau est remplacée par le certificat téléchargé.
