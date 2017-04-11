---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-22"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuration des certificats
{: #set_up_certificates}

Les certificats sont utilisés pour l'authentification de terminal ou pour remplacer le certificat de serveur {{site.data.keyword.iot_full}} par défaut pour la messagerie MQTT. Tous les terminaux qui ne disposent pas de certificats signés valides se voient refuser l'accès et ne peuvent pas communiquer avec le serveur.

Pour configurer les certificats et l'accès au serveur pour les terminaux, l'opérateur du système enregistre les certificats d'autorité de certification associés et enregistre éventuellement les certificats du serveur de messages dans la plateforme {{site.data.keyword.iot_short_notm}}.

## Exigences du certificat
{: #cert_reqs}

### Certificats d'autorité de certification
Les certificats d'autorité de certification permettent à l'organisation de reconnaître les certificats client sur les terminaux comme dignes de confiance de sorte que les terminaux puissent se connecter au serveur. Un certificat d'autorité de certification peut utiliser une liste de révocation de certificat. Celle-ci doit être accessible au moment où l'autorité de certification est ajoutée à la plateforme, faute de quoi, le certificat d'autorité de certification sera rejeté.

Si vous ajoutez un certificat d'autorité de certification ou que vous remplacez le certificat du serveur de messagerie, tous les terminaux doivent se connecter à l'aide d'un client MQTT prenant en charge SNI (Server Name Indication) afin de permettre au serveur de pouvoir utiliser les autorités de certification appropriées pour authentifier le terminal.

Si vous ajoutez un certificat d'autorité de certification et que vous utilisez un plan de sécurité standard, tous les terminaux se connectent à TLS avec la règle de sécurité de connexion Authentification par certificat client et par jeton. Si vous disposez d'un plan de sécurité gratuit ou avancé, vous pouvez configurer d'autres règles de connexion. Pour plus d'informations sur la configuration des règles de sécurité de connexion, voir [Configuration des règles de sécurité](set_up_policies.html).

### Certificats client ou de terminal
Les certificats client ou de terminal individuels sont conservés sur les terminaux et ne sont pas téléchargés sur la plateforme. Le certificat signataire d'autorité de certification qui est utilisé pour signer tous les certificats de terminal est le seul certificat que vous téléchargez sur la plateforme. Si vous utilisez des certificats serveur autosignés, vous devez télécharger les certificats racine et intermédiaires utilisés pour signer le certificat client (cert.pem).

L'ID de terminal du certificat de terminal individuel que vous signez avec le certificat d'autorité de certification doit être entré comme nom commun (CN) ou SubjectAltName dans le certificat. Le format de la zone *CN* est 'CN=d:devtype:devid'. Le format de la zone SubjectAltName est 'SubjectAltName=email:d:*devtype:devid*', où 'email:d' est constant et '*devtype*' est le type du terminal et '*devid*' est l'ID client du terminal.

## Enregistrement de certificats d'autorité de certification pour l'authentification de terminaux
{: #reg_ca_cert}

1. Connectez-vous à {{site.data.keyword.iot_short_notm}} et accédez à **Paramètres généraux**.
2. Dans la section **Sécurité**, sous **Certificats d'autorité de certification**, cliquez sur **Ajouter un certificat**.
3. Parcourez pour sélectionner un fichier de certificat à télécharger ou faites glisser un fichier dans la fenêtre **Ajout de certificat**. Le fichier ne peut contenir qu'un seul certificat et les dates du certificat doivent être valides. Seuls les certificats au format .pem ou . der sont acceptés. Vous pouvez prévisualiser les informations de certificat dans le fichier sélectionné.
4. Entrez une description du fichier certificat.
5. Confirmez que le fichier correct est sélectionné et cliquez sur **Sauvegarder**. Le certificat sélectionné est répertorié dans le tableau et est actif par défaut.

## Enregistrement des certificats de serveur de messagerie
{: #reg_msg_cert}

Un certificat de serveur par défaut est fourni avec la plateforme. Vous pouvez utiliser le certificat par défaut ou en télécharger un de votre organisation. Si vous n'avez pas encore de certificat à utiliser, vous pouvez créer une demande pour un nouveau certificat. Après avoir reçu le nouveau certificat, vous devez le signer et le retransférer vers la plateforme.

Pour utiliser le certificat par défaut ou un autre certificat qui a déjà été téléchargé, sélectionnez le certificat que vous souhaitez utiliser dans la liste déroulante des **certificats de serveur de messagerie par défaut** dans le tableau, sous les **certificats de serveur de messagerie**.

**Remarque :** Les pages de tableau de bord de la plateforme peuvent établir des connexions internes avec le serveur de messagerie pour extraire des informations sur les terminaux. Lors de la configuration de certificats de serveur autosignés pour une organisation, les utilisateurs de tableau de bord doivent ajouter le certificat de serveur en tant que certificat digne de confiance dans leurs navigateurs pour éviter tout problème de connexion, car, par défaut, les navigateurs ne reconnaissent pas le serveur de messagerie comme serveur digne de confiance.

### Téléchargement d'un certificat à partir de votre organisation
{: #upload_cert}
1. Dans la section **Sécurité** de **Paramètres généraux**, sous **Certificats de serveur de messagerie**, cliquez sur **Ajouter un certificat**.
2. Parcourez pour sélectionner un fichier de certificat à télécharger ou faites glisser un fichier dans la fenêtre **Ajout de certificat**.
3. Parcourez pour sélectionner le fichier de clé privée à télécharger ou faites glisser un fichier dans la fenêtre **Ajout de certificat**.  
4. Entrez la phrase passe de la clé privée si la clé privée a été chiffrée avec une phrase passe.
5. Confirmez que le fichier correct est sélectionné et cliquez sur **Sauvegarder**.
6. Sélectionnez le certificat téléchargé dans la liste déroulante des **Certificats du serveur de messagerie par défaut**. Le certificat sélectionné est répertorié dans le tableau en tant que certificat actif.

### Demande d'un nouveau certificat
{: #request_cert}

Si vous souhaitez utiliser un nouveau certificat de serveur de messagerie, vous pouvez générer une demande de signature de certificat pour demander un nouveau certificat.

 1. Dans la section **Sécurité** de **Paramètres généraux**, sous **Certificats de serveur de messagerie**, cliquez sur **Générer la demande de signature de certificat**.
 2. Entrez les détails de la demande de signature de certificat pour votre serveur, puis cliquez sur **Générer**. La demande de signature de certificat est affichée dans le tableau.
 3. Téléchargez la demande et soumettez-la à une autorité de certification pour signature.
 4. Après avoir obtenu un certificat, revenez à l'entrée de demande de signature de certificat dans le tableau et téléchargez le nouveau certificat. Une fois le certificat téléchargé, la demande de signature de certificat dans le tableau est remplacée par le certificat téléchargé.
