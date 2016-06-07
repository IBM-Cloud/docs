---

copyright:
  2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administration d'{{site.data.keyword.iotdriverinsights_short}}
{: #1stanchor}
*Dernière mise à jour : 6 mai 2016*


L'administration d'{{site.data.keyword.iotdriverinsights_full}} inclut l'affichage d'informations relatives au locataire et à la réinitialisation de son mot de passe, à la configuration des paramètres pour le service et à la gestion des données stockées dans le service.
{:shortdesc}

Vous pouvez effectuer des tâches d'administration en utilisant la console d'administration {{site.data.keyword.iotdriverinsights_full}}.

Pour accéder à la console d'administration :

1. Accédez à la vue **Gérer** de votre instance de service.
2. Cliquez sur **Lancer**. La console d'administration s'ouvre, dans une nouvelle fenêtre.
3. Renseignez les zones *Nom d'utilisateur* et *Mot de passe* présentées dans la vue **Gérer** puis cliquez sur **SE CONNECTER**.

## Affichages des informations relatives au locataire
{: #viewtenantinfo}

Après connexion à la console d'administration, la vue relative aux informations du locataire s'affiche.

## Réinitialisation du mot de passe du locataire
{: #resettenantpassword}

Dans la vue relative aux informations du locataire, 

1. Cliquez sur **REINITIALISER**.
2. Dans la boîte de dialogue de confirmation, cliquez sur **OK**.
Le nouveau mot de passe s'affiche dans la vue relative aux informations du locataire.

## Configuration des paramètres pour le service
{: #configureparameters}

Cliquez sur **Paramètres** dans le panneau de navigation. La vue **Paramètres** et les paramètres s'affichent.

Vous pouvez éditer les paramètres pour modifier les résultats d'analyse.

Le tableau ci-dessous décrit le fonctionnement des paramètres :

|Catégorie|Nom du paramètre|Description|Valeur par défaut|
|:-------:|:--------:|:--------|:-------:|
|Limitation de vitesse (km/h)|\-|Limitation de vitesse pour chaque type de route. Si la vitesse du véhicule dépasse cette valeur sur une route de chaque type, le service identifie ceci comme un excès de vitesse.|\-|
|Limitation de vitesse (km/h)|Autoroute|Limitation de vitesse pour Autoroute|130|
|Limitation de vitesse (km/h)|Périphérique|Limitation de vitesse pour Périphérique|70|
|Limitation de vitesse (km/h)|Axe urbain principal|Limitation de vitesse pour Axe urbain principal|50|
|Limitation de vitesse (km/h)|Axe urbain|Limitation de vitesse pour Axe urbain|30|
|Limitation de vitesse (km/h)|Autres|Limitation de vitesse pour Autres types de voie|30|
|Limitation de vitesse (km/h)|Inconnu|Limitation de vitesse pour Inconnu|130|
|Virage|Vitesse angulaire (min \- max, deg/s)|Valeur normale de vitesse angulaire dans un virage. La valeur minimale est utilisée en tant que seuil pour identifier un segment de virage. La valeur minimale sert à détecter un comportement de virage serré.|10 \- 25|
|Virage|Vitesse moyenne (km/h)|Vitesse normale lors d'un virage. Cette valeur est utilisée pour identifier les comportements dans un segment de virage conjointement avec les valeurs Vitesse angulaire.|60|
|Fatigue au volant|Temps de conduite sans pause|Si un véhicule est conduit de façon continue pendant une durée supérieure à la valeur spécifiée ici, le service identifie ce comportement comme "Fatigue au volant".|10800|

Le tableau suivant décrit les paramètres de contexte :

|Catégorie|Nom du paramètre|Description|Valeur par défaut|
|:-------:|:--------:|:--------|:-------:|
|Fuseau horaire de l'analyse|\-|Fuseau horaire appliqué pour l'analyse |+00:00|
|Plage horaire|\-|Cette valeur définit le type de plage de temps.|\-|
|Plage horaire|Horaires de jour|Plage de temps des horaires journaliers|1030 \- 1730|
|Plage horaire|Horaires de nuit|Plage de temps des horaires de nuit|2030 \- 0700|
|Plage horaire|Heures de pointe - matinée|Plage de temps des heures de pointe en matinée|0700 \- 1030|
|Plage horaire|Heures de pointe - soirée|Plage de temps des heures de pointe en soirée|1730 \- 2030|
|Type de route|\-|Ces valeurs sont utilisées pour faire correspondre la valeur de type de route de l'utilisateur dans les entrées de données aux classifications de type de route uniques et spécifiques à {{site.data.keyword.iotdriverinsights_short}}. Si vous ne disposez pas de valeur Type de route, vous pouvez extraire cette valeur en utilisant l'API REST `getLinkInformation`. qui est fournie par **{{site.data.keyword.iotmapinsights_short}}**. La valeur de type de route est stockée dans **propriétés > type**, dans la réponse. [Exemple JSON](#sampleJson) représente la position de `type` dans la réponse.|\-|
|Type de route|Autoroute|Correspondance entre les valeurs Type de route et Autoroute|1|
|Type de route|Périphérique|Correspondance entre les valeurs Type de route et Périphérique|2|
|Type de route|Axe urbain principal|Correspondance entre les valeurs Type de route et Axe urbain principal|3|
|Type de route|Axe urbain|Correspondance entre les valeurs Type de route et Axe urbain|4|
|Type de route|Autres|Correspondance entre les valeurs Type de route et Autres|5|
|Seuil de vitesse (basse \- haute, km/h)|\-|Cette valeur définit la plage de vitesse moyenne pour chaque type de route.|\-|
|Seuil de vitesse (basse \- haute, km/h)|Autoroute|Plage de vitesse moyenne pour Autoroute|55 \- 85|
|Seuil de vitesse (basse \- haute, km/h)|Périphérique|Plage de vitesse moyenne pour Périphérique|35 \- 65|
|Seuil de vitesse (basse \- haute, km/h)|Axe urbain principal|Plage de vitesse moyenne pour Axe urbain principal|20 \- 40|
|Seuil de vitesse (basse \- haute, km/h)|Axe urbain|Plage de vitesse moyenne pour Axe urbain|15 \- 35|
|Seuil de vitesse (basse \- haute, km/h)|Autres|Plage de vitesse moyenne pour Autres|10 \- 20|
|Seuil de vitesse (basse \- haute, km/h)|Inconnu|Plage de vitesse moyenne pour Inconnu|20 \- 60|


Pour appliquer des changements aux paramètres :

1. Cliquez sur **SAUVEGARDER**. 
2. Dans la boîte de dialogue de confirmation, cliquez sur **OK**.

Les nouveaux paramètres sont appliqués et deviennent effectifs pour le travail soumis suivant.

### Réponse JSON exemple de l'API REST "getLinkInformation"
{: #sampleJson}

```
{
	"links": [{
		"internal_link_id": "32088220365736308",
		"external_link_id": "3846419005",
		...
		"properties": {
			"type": "5",
			...
		},
		...
	}]
}
```
{: screen}


## Gestion des données stockées dans le service
{: #managedata}

- Cliquez sur **Gestion des données** dans le panneau de navigation. Vous pouvez afficher la vue **Gestion des données** ainsi que les données de détection de véhicule et de résultats d'analyse.
- Vous pouvez supprimer des données en cliquant sur **SUPPRIMER** dans un enregistrement.
