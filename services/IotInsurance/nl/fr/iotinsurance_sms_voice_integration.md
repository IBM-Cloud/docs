---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Activation des SMS et des messages vocaux
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} prend en charge l'intégration avec Twilio pour permettre la messagerie vocale et par SMS. Twilio est une application tierce que vous pouvez installer sur votre tableau de bord {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Conditions préalables
Pour activer la messagerie vocale, vous devez avoir un compte Twilio autorisé et un numéro d'appel téléphonique Twilio. Si vous utilisez un compte Twilio gratuit, vous devez
également autoriser un numéro de téléphone pour recevoir des appels ou des messages. Pour plus d'informations, veuillez vous référer à la
[documentation de Twilio![icône de lien externe](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window}.

## Création et configuration d'une instance Twilio
1. Créez une instance Twilio dans la même organisation {{site.data.keyword.Bluemix_notm}} et dans le même espace dans lequel vous avez installé
{{site.data.keyword.iotinsurance_short}}.
    1. Connectez-vous à [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net).
    2. Sélectionnez l'onglet **Catalogue**.
    3. Localisez la section Mobile du catalogue de service et cliquez sur **Twilio**.

    **Astuce :** cliquez [ici ![icône de lien externe](../../icons/launch-glyph.svg "icône delien externe")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window} pour aller directement à la page de Twilio.

    {: tip}

    4. Sur la page de Twilio, fournissez vos données d'identification et liez l'application comme suit :

      1. Entrez `Twilio-00` comme nom de service. **Important :** vous devez utiliser `Twilio-00` pour vous connecter correctement à {{site.data.keyword.iotinsurance_short}}.

      2. Entrez vos données d'identification Twilio.

      3. Dans le menu **Se connecter à**, sélectionnez votre application iot4i-action-engine pour associer l'instance Twilio
à {{site.data.keyword.iotinsurance_short}}.

      4. Cliquez sur **Créer**.  

    L'application Twilio est installée dans votre environnement. Un message vous invite à reconstituer ou à redémarrer votre application iot4i-action-engine pour permettre la liaison. Vous
pouvez redémarrer maintenant ou attendre d'avoir ajouté la nouvelle variable d'environnement (à l'étape suivante) avant de redémarrer.

2. Créez une variable d'environnement appelée TWILIO_FROM_NUMBER pour le composant iot4i-action-engine.
    1. Sur le tableau de bord Bluemix, ouvrez l'application iot4i-action-engine.
    2. Sélectionnez **Exécution** puis cliquez sur **Variables d'environnement**.
    3. Dans la section **Défini par l'utilisateur**, cliquez sur **Ajouter**.
    4. Dans la colonne Nom, entrez `TWILIO_FROM_NUMBER` puis, dans la colonne Valeur, entrez votre numéro Twilio compatible voix et SMS.
    5. Cliquez sur **Sauvegarder**.

3. Redémarrez l'application Iot4i-action-engine en cliquant sur l'icône Redémarrer située en regard du bouton Routes.

## Ajout des actions SMS et voix à un bouclier

Pour ajouter des fonctions de SMS et de voix à un bouclier, vous devez ajouter les actions suivantes à la définition du bouclier :
  - `send-sms`
  - `phone-call`

Pour afficher un exemple de bouclier contenant une liste d'actions, voir [Créer un exemple
de bouclier ![icône de lien externe](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window}. Dans l'exemple, les actions SMS et voix peuvent être ajoutées à la liste des
actions qui contient les actions `email` et `pushios`.

Pour en savoir plus sur la création des boucliers, voir [Utilisation du kit d'outils de bouclier](iotinsurance_shield_toolkit.html).
