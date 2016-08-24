---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administration d'{{site.data.keyword.iot4auto_short}}
{: #1stanchor}
Dernière mise à jour : 29 juillet 2016
{: .last-updated}

Administrez votre instance de service {{site.data.keyword.iot4auto_full}} en utilisant la console d'administration du tableau de bord {{site.data.keyword.Bluemix_notm}}. Depuis la console d'administration, vous pouvez configurer les paramètres pour {{site.data.keyword.iot4auto_short}} et gérer les données qui sont stockées dans le service. Vous pouvez aussi afficher les informations relatives au titulaire et réinitialiser le mot de passe du titulaire.

{:shortdesc}

## Démarrage de la console d'administration
{: #start_admin_console}

Pour accéder à la console d'administration pour le service {{site.data.keyword.iot4auto_short}} :

1. Sur le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur la vignette du service {{site.data.keyword.iot4auto_short}}.
2. Sélectionnez la vue **Gérer** de votre instance de service.
Prenez note des données d'identification de nom d'utilisateur et de mot de passe, car vous en aurez besoin plus tard. Pour accéder à la console d'administration, votre ID IBM est requis, qui peut différer de vos données d'identification {{site.data.keyword.Bluemix_notm}}.
3. Cliquez sur **Lancer** et, quand vous y êtes invité, entrez vos données d'identification d'ID IBM.
4. Cliquez sur **SE CONNECTER**. La fenêtre de la **console d'administration** s'ouvre.

## Gestion des informations  relatives au titulaire
{: #view_tenant_info}

Pour afficher les informations relatives au titulaire, cliquez sur la commande correspondante.

### Réinitialisation du mot de passe du locataire
{: #reset_tenant_password}

Pour réinitialiser le mot de passe du titulaire :

1. Dans la fenêtre relative aux informations de titulaire, cliquez sur **REINITIALISER**.
2. Dans la boîte de dialogue, cliquez sur **OK**.
Un nouveau mot de passe est généré et s'affiche dans la vue relative aux informations du titulaire.  
**Important :** prenez soin de mettre à jour le mot de passe dans toutes vos applications qui accèdent à l'API {{site.data.keyword.iot4auto_short}}.

## Configuration des paramètres de service
{: #configure_parameters}

Les paramètres de service contrôlent comment les données de trajets sont analysées. Pour modifier les paramètres de service :

1. Ouvrez la vue relative aux paramètres et ajustez les paramètres de service suivants :
  - Cliquez sur l'onglet **Comportement** et mettez à jour les [paramètres de type de conduite](#behavior_parameters) pour les faire correspondre à vos besoins.
  - Cliquez sur l'onglet **Contexte** et mettez à jour les [paramètres de mappage de contexte](#context_parameters) pour les faire correspondre à vos besoins.
2. Cliquez sur **SAUVEGARDER**.
3. Cliquez sur **OK**.

Les valeurs des paramètres mis à jour sont appliqués au prochain travail qui est soumis.

### Paramètres de types de conduite
{: #behavior_parameters}


Les tableaux suivants décrivent les paramètres de types de conduite pour les catégories que vous pouvez configurer sur l'onglet **Comportement**.

#### Paramètres de limitation de vitesse

Vous pouvez spécifier la limite de vitesse en km/h pour chaque type de route. Si la vitesse dépasse la valeur que vous avez spécifiée comme limite maximale pour le type de route, un excès de vitesse est détecté.

|Nom du paramètre|Description|Valeur par défaut (km/h)|
|:--------|:--------|:-------|
|Autoroute|Limite de vitesse pour une autoroute|130|
|Périphérique|Limite de vitesse pour un périphérique|70|
|Axe urbain principal|Limite de vitesse pour un axe urbain principal|50|
|Axe urbain|Limite de vitesse pour un axe urbain|30|
|Autres|Limite de vitesse pour les autres types de route|30|
|Inconnu|Limite de vitesse pour les routes de type inconnu|130|
*Tableau 1. Paramètres de configuration des limitations de vitesse*
#### Paramètres relatifs aux virages

|Nom du paramètre|Description|Valeur par défaut|
|:--------|:--------|:-------|
|Vitesse angulaire (min \- max, deg/s)|Valeur de vitesse angulaire normale d'un virage. La valeur minimale est utilisée en tant que seuil pour identifier le segment de virage. La valeur maximale sert à détecter un comportement de virage serré.|10 \- 25|
|Vitesse moyenne (km/h)|Vitesse normale lors d'un virage. Cette valeur est utilisée pour identifier les comportements dans un segment de virage qui dispose de valeurs de vitesse angulaire.|60|
*Tableau 2. Paramètres de configuration relatifs aux virages*
#### Paramètres de fatigue au volant

|Nom du paramètre|Description|Valeur par défaut|
|:--------|:--------|:-------|
|Temps de conduite sans pause|Durée maximale de conduite sans pause qui est autorisée.|10800|
*Tableau 3. Paramètres de configuration relatifs à la détection de la fatigue au volant*
### Paramètres de mappage de contexte
{: #context_parameters}

Les tableaux suivants décrivent les paramètres de mappage de contexte pour les catégories que vous pouvez configurer sur l'onglet **Contexte**.

#### Paramètres de fuseau horaire et de plage horaire

Spécifiez le fuseau horaire et les heures pour chaque période.

|Nom du paramètre|Description|Valeur par défaut|
|:--------|:--------|:-------|
|Fuseau horaire de l'analyse|Fuseau horaire appliqué pour l'analyse. |+00:00|
|Horaires de jour|Plage de temps des horaires journaliers.|1030 \- 1730|
|Horaires de nuit|Plage de temps des horaires de nuit.|2030 \- 0700|
|Heures de pointe - matinée|Plage de temps des heures de pointe en matinée.|0700 \- 1030|
|Heures de pointe - soirée|Plage de temps des heures de pointe en soirée.|1730 \- 2030|
*Tableau 4. Paramètres de configuration des plages et fuseaux horaires*

#### Types de route

Les paramètres de types de route sont utilisés pour faire correspondre les valeurs de types de route aux classifications de types de route {{site.data.keyword.iot4auto_short}}. Si vous ne disposez pas de valeur type de route, vous pouvez extraire cette valeur en utilisant l'API REST `getLinkInformation`, qui est fournie par le service {{site.data.keyword.iotmapinsights_short}}.

La valeur de type de route est retournée et stockée dans la section des propriétés de la réponse JSON `getLinkInformation` et est définie en tant que `type`, comme décrit dans [Réponse JSON exemple pour `getLinkInformation`](#sampleJson).


|Nom du paramètre|Description|Valeur par défaut|
|:--------|:--------|:-------|
|Autoroute|Valeur Type de route qui est mappée à Autoroute.|1|
|Périphérique|Valeur Type de route qui est mappée à Périphérique.|2|
|Axe urbain principal|Valeur Type de route qui est mappée à Axe urbain principal.|3|
|Axe urbain|Valeur Type de route qui est mappée à Axe urbain.|4|
|Autres|Valeur Type de route qui est mappée à Autres.|5|
*Tableau 5. Paramètres de configuration des types de route*

#### Seuil de vitesse

Les paramètres de seuil de vitesse définissent la plage de vitesse moyenne pour chaque type de route en km/h. La plage de vitesse moyenne est la plage située entre la valeur la plus basse et la valeur la plus haute qui est spécifiée.

|Nom du paramètre|Description|Valeur par défaut|
|:--------|:--------|:-------|
|Autoroute|Plage de vitesse moyenne pour le type de route Autoroute.|55 \- 85|
|Périphérique|Plage de vitesse moyenne pour le type de route Périphérique.|35 \- 65|
|Axe urbain principal|Plage de vitesse moyenne pour le type de route Axe urbain principal.|20 \- 40|
|Axe urbain|Plage de vitesse moyenne pour le type de route Axe urbain.|15 \- 35|
|Autres|Plage de vitesse moyenne pour le type de route Autres.|10 \- 20|
|Inconnu|Plage de vitesse moyenne pour le type de route Inconnu.|20 \- 60|
*Tableau 6. Paramètres de configuration des seuils de vitesse*


### Réponse JSON exemple pour `getLinkInformation`
{: #sampleJson}

L'exemple de code suivant fournit un exemple d'une réponse JSON pour la commande d'API REST `getLinkInformation` :

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

## Suppression des données qui sont stockées dans le service
{: #managedata}

Les données de détection de véhicules, les données de contexte et les résultats d'analyse sont stockés dans le service jusqu'à ce qu'ils soient supprimés.

Pour supprimer les données qui sont stockées dans le service :

1. Pour afficher les données de détection de véhicule et les résultats d'analyse, cliquez sur **Gestion des données**.
2. Sélectionnez un enregistrement puis cliquez sur **SUPPRIMER**.
