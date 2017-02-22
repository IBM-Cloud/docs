---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion de votre compte {{site.data.keyword.Bluemix_notm}}
{: #mngacct}

Cliquez sur le lien **Compte** pour définir des notifications, afficher l'utilisation de votre compte ou consulter votre facture.
{:shortdesc}

## Inscription à {{site.data.keyword.Bluemix_notm}}
{: #signup}

Vous pouvez vous inscrire à un compte {{site.data.keyword.Bluemix_notm}} en utilisant un IBMid existant, en créant un nouvel IBMid ou en utilisant un ID fédéré. Un ID fédéré est un ID présent dans le domaine d'une société qui a été enregistré auprès d'IBM de sorte que le domaine et les données d'identification de l'utilisateur puissent être utilisés pour accéder aux applications Web IBM.  

Un ID fédéré peut être utilisé pour s'inscrire à {{site.data.keyword.Bluemix_notm}} uniquement si votre société a déjà travaillé avec IBM. L'enregistrement du domaine d'une société auprès d'IBM permet aux utilisateurs de se connecter pour recevoir des produits et des services IBM en utilisant leurs données d'identification d'utilisateur de société existantes. L'authentification est alors gérée par le fournisseur d'identité de votre société. Lorsque vous vous connectez à {{site.data.keyword.Bluemix_notm}} avec un ID fédéré, vous êtes invité à le faire via la page de connexion de votre société. Pour savoir comment demander à enregistrer le domaine de votre société ou de votre organisation auprès d'IBM ou pour obtenir plus d'informations sur cette opération, voir [IBMid Enterprise Federation Adoption Guide ![icône de lien externe](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}. Un sponsor IBM, tel qu'un représentant du client ou un service de conseil, est requis lorsque vous demandez à enregistrer des ID fédérés.

| Méthodes d'inscription | Détails |    
|-----------------|---------|
|IBMid existant | Si vous possédez déjà un IBMid, inscrivez-vous à {{site.data.keyword.Bluemix_notm}} avec les données d'identification existantes que vous utilisez pour recevoir les autres produits et services IBM. Vous devez entrer un numéro de téléphone lorsque vous vous inscrivez. |
|Nouvel IBMid | Si vous ne possédez pas encore d'IBMid, vous pouvez choisir d'en créer un. L'IBMid vous permet d'utiliser un seul et même nom d'utilisateur de connexion pour tous les produits et services IBM que vous utilisez, y compris {{site.data.keyword.Bluemix_notm}}. Vous devez entrer vos informations personnelles, y compris vos nom et prénom, votre numéro de téléphone et votre mot de passe pour les nouvelles données d'identification. Vous pouvez utiliser cet IBMid pour vous connecter lorsque vous utilisez d'autres produits et services IBM.  |
|ID fédéré | Si votre société a demandé à enregistrer auprès d'IBM les données d'identification de l'utilisateur du domaine de votre société, vous pouvez vous inscrire à {{site.data.keyword.Bluemix_notm}} à l'aide des données d'identification dont vous vous servez déjà pour la connexion de votre société. Vous devez entrer un numéro de téléphone lorsque vous vous inscrivez. |
{:caption="Table 1. Sign up methods" caption-side="top"}

## Définition de notifications
{: #notifications}

Cliquez sur **Compte** &gt; **Notifications** pour configurer les notifications générales relatives au compte
et aux dépenses. Les notifications relatives aux dépenses ne sont disponibles que pour les propriétaires de compte {{site.data.keyword.Bluemix_notm}} Abonnement et Paiement à la carte.

Vous pouvez définir des notifications par courrier électronique de plateforme pour les incidents et la maintenance planifiée de {{site.data.keyword.Bluemix_notm}} et vous pouvez définir des notifications relatives aux dépenses qui vous envoient des alertes lorsque vous vous approchez du plafond des dépenses que vous avez spécifié pour compte. Effectuez les tâches ci-après pour définir différents types de notification pour votre compte.

### Définition de notifications de plateforme

Cliquez sur **Compte** &gt; **Notifications** &gt; **Plateforme** pour définir des
notifications par courrier électronique relatives aux incidents {{site.data.keyword.Bluemix_notm}} et à la maintenance planifiée. Vous pouvez sélectionner ou désélectionner chaque option pour activer ou désactiver la notification par courrier électronique.

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### Définition des notifications relatives aux dépenses
{: #spendingnotifications}

Si vous possédez un compte {{site.data.keyword.Bluemix_notm}} de type Abonnement ou Paiement à la carte, vous pouvez configurer des notifications par courrier électronique relatives aux dépenses. Définissez des notifications pour les dépenses totales du compte, pour les dépenses relatives aux contextes
d'exécution, aux conteneurs et aux services, ainsi que pour les dépenses relatives aux services individuels, à l'exception des services de tiers. Vous recevez des
notifications lorsque vous atteignez 80 %, 90 % et 100 % des seuils que vous avez spécifiés pour les dépenses. Vous pouvez éditer chaque notification
relative aux dépenses à tout moment, selon l'évolution de vos besoins.

Procédez comme suit afin de configurer des notifications par courrier électronique pour les limites relatives aux dépenses :

<ol>
<li>Cliquez sur **Compte** &gt; **Notifications** &gt; **Dépenses**.</li>
<li>Entrez une valeur numérique afin de définir un plafond pour les dépenses, en fonction duquel une notification sera déclenchée, pour chaque type de notification :<br />
<ul>
<li>Total lié au compte</li>
<li>Total lié à l'exécution</li>
<li>Total lié aux services</li>
<li>Total lié au conteneur</li>
<li>Dépenses pour un service spécifique</li>
</ul>
</li>
<li>Lorsque vous avez terminé, cliquez sur **Sauvegarder**.</li>
</ol>

**Remarque** : si vous disposez d'un compte d'essai, vous pouvez le mettre à niveau vers un compte d'abonnement ou de type Paiement
à la
carte afin de définir des limites relatives aux dépenses. Pour plus d'informations sur les comptes de type Paiement à la carte et les comptes d'abonnement,
voir
[Facturation](/docs/pricing/index.html#pay-accounts).

## Affichage de l'utilisation
{: #acctusage}

En tant que propriétaire de compte ou responsable de la facturation pour
une organisation, vous pouvez vous servir de la page Tableau de bord de
l'utilisation afin d'afficher les frais en temps réel pour les contextes
d'exécution, les conteneurs, les services et le support que vous utilisez par
mois dans vos organisations. Vous pouvez afficher le nombre de Go/heure utilisés pour le contexte d'exécution, ainsi que la consommation des services dans toutes les
régions, ou sélectionner une région particulière.

Pour ouvrir la page Tableau de bord de l'utilisation, cliquez sur
**Compte** &gt; *nom_de_votre_compte* &gt;
**Tableau de bord de l'utilisation**. Les responsables de la facturation ne peuvent afficher les détails que pour les organisations pour lesquelles ils sont responsables de la
facturation.

Le propriétaire de compte est facturé pour l'utilisation totale occasionnée dans toutes les organisations à la fin de chaque cycle de
facturation. En tant que propriétaire de compte, vous pouvez filtrer le récapitulatif de l'utilisation par région et organisation. Vous pouvez aussi
cliquer sur un mois
particulier afin d'afficher l'utilisation pour ce mois. Sélectionnez
**Toutes les organisations** dans la liste
**Organisation** pour afficher l'utilisation de toutes
les organisations du compte.

## Mise à jour des informations de facturation
{: #account_billing}

En tant que propriétaire de compte, vous pouvez éditer, ajouter ou supprimer des informations de carte de crédit sauvegardées qui sont associées à
votre compte {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Compte** &gt; *nom_de_votre_compte* &gt;
**Facturation**.

Si vous avez un compte SoftLayer lié à votre compte {{site.data.keyword.Bluemix_notm}}, voir
[Facturation de l'utilisation de {{site.data.keyword.Bluemix_notm}} lorsque des comptes sont liés](/docs/admin/softlayerlink.html#bill_usage)
pour plus d'informations sur la manière dont vous êtes facturé.
