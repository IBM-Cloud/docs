---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administration de l'analyse des modèles de trajectoire
{: #tp_iotdriverinsights_admin}

Dernière mise à jour : 22 juillet 2016
{: .last-updated}

Pour administrer le service d'analyse des modèles de trajectoire, utilisez la console d'administration du tableau de bord {{site.data.keyword.Bluemix_notm}}. Depuis la console d'administration, vous pouvez configurer les paramètres pour l'analyse des modèles de trajectoire et gérer les données qui sont stockées dans le service. Vous pouvez aussi afficher les informations relatives au titulaire et réinitialiser le mot de passe du titulaire.

{:shortdesc}

## Démarrage de la console d'administration
{: #start-admin-console}

Pour accéder à la console d'administration pour le service d'analyse des modèles de trajectoire d'{{site.data.keyword.iotdriverinsights_full}} :

1. Sur le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur la vignette du service {{site.data.keyword.iotdriverinsights_short}}.
2. Sélectionnez la vue **Gérer** de votre instance de service.
Prenez note des données d'identification de nom d'utilisateur et de mot de passe, car vous en aurez besoin plus tard. Pour accéder à la console d'administration, votre ID IBM est requis, qui peut différer de vos données d'identification {{site.data.keyword.Bluemix_notm}}.
3. Cliquez sur **Lancer** et, quand vous y êtes invité, entrez vos données d'identification d'ID IBM.
4. Cliquez sur **SE CONNECTER**. La fenêtre de la **console d'administration** s'ouvre.


## Gestion des informations  relatives au titulaire
{: #viewtenantinfo}

Pour afficher les informations relatives au titulaire, cliquez sur la commande correspondante.

### Réinitialisation du mot de passe du locataire
{: #resettenantpassword}

Pour réinitialiser le mot de passe du titulaire :

1. Depuis la fenêtre relative aux informations du titulaire, cliquez sur **REINITIALISER**.
2. Dans la boîte de dialogue de confirmation, cliquez sur **OK**.
Un nouveau mot de passe est généré et s'affiche dans la vue relative aux informations du titulaire.  
**Important :** prenez soin de mettre à jour le mot de passe dans toutes vos applications qui accèdent à l'API {{site.data.keyword.iotdriverinsights_short}}.

## Configuration des paramètres de service
{: #configureparameters}

Les paramètres de service contrôlent comment les données de trajets sont analysées. Pour modifier les paramètres du service d'analyse des modèles de trajectoire :

1. Ouvrez la vue **Paramètres**.
2. Cliquez sur l'onglet relatif aux paramètres du modèle de trajectoire et mettez à jour les [paramètres d'analyse de ce modèle](#tp_parameters) pour les faire correspondre à vos besoins.
3. Cliquez sur **SAUVEGARDER**.
4. Cliquez sur **OK**.

Les valeurs des paramètres mis à jour sont appliqués au prochain travail qui est soumis.

### Paramètres de seuil de prise en charge

Le tableau suivant décrit les paramètres de seuil de prise en charge que vous pouvez configurer sur l'onglet relatif aux paramètres du modèle de trajectoire.

|Nom du paramètre|Description|Valeur par défaut|
|:--------|:--------|:-------|
|Prise en charge d'un nombre de trajets minimal pour un modèle O/D|Nombre de trajets absolu minimal pris en charge qui est requis pour un modèle O/D (Origine/Destination)|4 (doit être supérieur à zéro)|
|Prise en charge d'un nombre de trajets minimal pour une route|Nombre de trajets absolu minimal pris en charge qui est requis pour un modèle de route|2 (doit être supérieur à zéro)|

## Gestion des données de résultats
{: #managedata}

Les données de résultats qui sont générées par les analyses du service d'analyse des modèles de trajectoire sont stockées dans le système jusqu'à ce que vous les supprimiez.

Pour supprimer les données de résultats :

1. Cliquez sur la commande de gestion des données puis sur celles des résultats du modèle de trajectoire. Les données de résultats s'affichent.
2. Sélectionnez un enregistrement puis cliquez sur **SUPPRIMER**.
