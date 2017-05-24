---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.iot_short_notm}} Starter
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

Commencez à utiliser {{site.data.keyword.iot_full}} en vous faisant la main avec
le projet GitHub d'application {{site.data.keyword.iot_short_notm}} Starter. Avec le projet d'application Starter (ou application de démarrage), vous pouvez rapidement simuler
un terminal, créer des cartes, générer des données et commencer à analyser et afficher des données dans le
tableau de bord {{site.data.keyword.iot_short_notm}}.   
{:shortdesc}

## Présentation
{: #overview}  

L'application Starter déploie et connecte automatiquement ces services :

<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>Service web IoT qui inclut la gestion des passerelle, la gestion des terminaux et l'accès aux applications.
{{site.data.keyword.iot_short_notm}} vous permet de collecter des données
de terminaux connectés et d'exécuter des analyses sur les données temps
réel de votre organisation.
</dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>Environnement d'exécution dans lequel fonctionne Node-RED. </br>Pour plus d'informations, consultez
la
[documentation de {{site.data.keyword.sdk4nodefull}}](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html) Starter.
</dd>
<dd>Node-RED est un outil qui permet de relier des terminaux matériels, des API et des services en ligne de façon inédite et intéressante.
Vous pouvez utiliser Node-RED pour créer un thermostat simulé qui envoie des données simulées à votre service {{site.data.keyword.iot_short_notm}}. Vous pouvez créer des cartes pour afficher des données temps réel dans le tableau de bord de {{site.data.keyword.iot_short_notm}}. </br>
Pour plus d'informations, consultez la [documentation Node-RED](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>Base de données dans laquelle Node-RED stocke les métadonnées.
</dd>
</dl>

## Avant de commencer
{: #byb}  

- Comptes nécessaires  
Il vous faut avant tout un [compte IBM Bluemix](https://bluemix.net/registration).

- Naviguer dans l'application  
Pour vous déplacer plus facilement de tâche en tâche dans le processus qui suit,
ouvrez le tableau de bord {{site.data.keyword.Bluemix_notm}},
le tableau de bord {{site.data.keyword.iot_short_notm}} et l'application Node-RED chacun dans un onglet de navigateur à part.

<dl>
<dt>*Tableau de bord {{site.data.keyword.Bluemix_notm}}*</dt>
<dd>Permet de consulter l'état de votre déploiement, de lire la documentation et de lancer les tableaux de bord. </dd>
<dt>*Tableau de bord {{site.data.keyword.iot_short_notm}}*</dt>
<dd>Permet de définir des types de terminaux, d'enregistrer des terminaux, de surveiller les données en provenance
de capteurs, de créer des cartes de visualisation de données et de voir des visualisations de données temps réel ("live"). </dd>
<dt>*Node-RED*</dt>
<dd>Permet de configurer et d'exécuter le flux du simulateur de terminaux et de travailler avec d'autres flux pour traiter les données
de {{site.data.keyword.iot_short_notm}}.</dd>
</dl>

## Etape 1 : Déployez l'application {{site.data.keyword.iot_short_notm}} Starter
{: #deployStarter}

Effectuez les étapes suivantes pour déployer l'application exemple Starter : 

1. Déployez l'application Starter.
 1. Cliquez sur
<a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a> pour
créer une nouvelle chaîne d'outils de distribution continue dans Bluemix (via le service Continuous Delivery)  
 **Astuce :** Si vous préférez déployer à partir de la ligne de commande,
[procurez-vous l'application {{site.data.keyword.iot_short_notm}} Starter](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter) (vous la trouverez dans
l'organisation IBM Watson IoT du site GitHub).
 2. Lorsque vous y êtes invité, connectez-vous à IBM Bluemix.
 3. Si nécessaire, sélectionnez l'organisation Bluemix où vous voulez déployer l'application Starter.
 4. Conservez le nom Toolchain ou changez-le selon nécessité.
Il est utilisé comme nom d'application par défaut et comme racine de l'URL de votre application : `<nom-app>.mybluemix.net`
 5. Cliquez sur **Créer**.  
**Astuce :** Cliquez sur la vignette **Delivery Pipeline** pour suivre la progression de votre premier déploiement.

 6. Une fois le déploiement achevé, cliquez sur **Afficher l'application** pour ouvrir votre nouvelle
application Node-RED dans un nouvel onglet.

2. Localisez les services de l'application Starter.
 1. Dans le menu Bluemix, sélectionnez **Tableau de bord**.
 2. Localisez les services suivants sous *Tous les services* :
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. Localisez la chaîne d'outils sous *Toutes les applis* :
    - default-toolchain-{id}}


## Etape 2 : Définissez un terminal simulé dans {{site.data.keyword.iot_short_notm}}
{: #definingsimdev}

Effectuez les étapes suivantes pour simuler un scénario mettant en jeu un terminal de type thermostat, combinant la surveillance
de température et d'humidité, ainsi que le lieu ou se trouve ce terminal (une pièce d'habitation, telle qu'un living room). 

1.	Lancez le tableau de bord {{site.data.keyword.iot_short_notm}}.
  1. Dans le tableau de bord Bluemix, sous *Tous les services*, cliquez sur le nom
de votre instance {{site.data.keyword.iot_short_notm}}.
**Astuce :** Le nom d'instance inclut généralement `iotp-starter`.
  2. Cliquez sur **Lancer** pour ouvrir le tableau de bord {{site.data.keyword.iot_short_notm}} dans un nouvel onglet du navigateur.    
La page `Tous les tableaux` est affichée par défaut.
2. Créez un type de terminal. 
  1.	Dans le menu principal, sélectionnez **Terminaux**, puis cliquez sur **Ajouter un terminal**.
  2.	Dans la page Ajouter un terminal, cliquez sur **Créer un type de terminal**.
  3.	Dans la page Créer un type de terminal, cliquez sur **Créer un type de terminal**.
  4. Entrez un nom unique (par exemple, `Thermostat`) pour votre type de terminal, puis cliquez sur
**Suivant**.
  5. Optionnel : la définition d'un modèle et de métadonnées sur les deux pages
suivantes est optionnelle. Vous pouvez sans risque omettre cette partie en cliquant sur
le bouton **Suivant** de chaque page.

  6.	Cliquez sur **Créer** pour ajouter le type de terminal.
3.	Ajoutez un terminal qui utilise le type de terminal que vous venez de créer. 
  1. Sur la page Ajouter un terminal, le type de terminal que vous venez de créer figure dans la
liste des types de terminaux.
Cliquez sur **Suivant** pour ajouter un terminal qui utilise ce type de terminal.
  2. Entrez un ID de terminal unique (par exemple, `LivingRoomThermo1`).
  3. Optionnel : la fourniture de données descriptives sur la page Ajouter un terminal ainsi que l'entrée de métadonnées de terminal sur la page suivante
sont des étapes optionnelles. Vous pouvez les omettre en cliquant sur le bouton **Suivant** de chaque page.

  4. Sur la page Sécurité, cliquez sur **Suivant** pour générer un jeton d'authentification pour votre terminal.

  5. Sur la page Récapitulatif, vérifiez que les informations sont correctes, puis cliquez sur **Ajouter** pour ajouter
le terminal.
Cliquez sur **Retour**
pour revenir à une page précédente.

4.	Prenez note des informations affichées sur la page Données d'identification du terminal.    
Vous aurez besoin des informations suivantes pour configurer le simulateur et afficher les données :

 - ID d'organisation
 - Type de terminal
 - ID de terminal
 - Méthode d'authentification
 - Jeton d'authentification

## Etape 3 : Configurez et exécutez le simulateur de terminaux Node-RED.   
{: #confignodered}  
Configurez le simulateur de terminaux Node-RED pour qu'il envoie à
{{site.data.keyword.iot_short_notm}} des messages MQTT combinant informations de
température et d'humidité.

1. Lancez l'éditeur de flux Node-RED.
  1. Dans le tableau de bord Bluemix, sous *Toutes les applis*, cliquez sur le nom
de votre chaîne d'outils.
  
**Astuce :** Le nom de la chaîne d'outils inclut généralement `default-toolchain...`.
  2. Dans le tableau de bord de la chaîne d'outils, ouvrez votre instance
Node-RED en cliquant sur **Routes** et en sélectionnant le lien de la route.   
  2. Cliquez sur **Go to your Node-RED flow editor** pour ouvrir l'éditeur.
2. Déployez votre terminal.
  1. Dans le flux du simulateur de terminaux, double-cliquez sur le noeud bleu **Envoyer à IBM IoT Platform**.
  2. Vérifiez que l'authentification est réglée sur **Service Bluemix**.
  3. Entrez le **type de terminal** et l'**ID de terminal** de votre terminal et cliquez sur **Terminé**.
  4. Déployez le terminal en cliquant sur **Déployer**.
3. Configurez le flux du moniteur de température Node-RED.
  1. Dans le flux du simulateur de terminaux, double-cliquez sur le noeud bleu **IBM IoT App In**.
  2. Dans Authentification, sélectionnez **Service Bluemix**.
  3.	Sélectionnez **Tout** pour Type de terminal, ID de terminal, Evénement et Format.
  4.	Cliquez sur **Terminé**.
  5.  Déployez votre moniteur en cliquant sur **Déployer**.
4. Validez la connexion du terminal.
  1.	Ouvrez le tableau de bord {{site.data.keyword.iot_short_notm}}.  
**Astuce :** Si le tableau de bord {{site.data.keyword.iot_short_notm}} n'est pas déjà ouvert
dans un autre onglet, retournez à votre tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur le nom
de votre instance {{site.data.keyword.iot_short_notm}}, puis sur **Lancer le tableau de bord**.
  2. Dans le menu principal, sélectionnez **Terminaux**.
  3. Cliquez sur le nom du terminal que vous avez ajouté.    
L'état de connexion de votre terminal est affiché. 
  4.	Dans votre éditeur de flux Node-RED, double-cliquez sur le noeud d'**envoi de données**,
réglez la valeur de répétition sur **Intervalle** et fixez l'intervalle de répétition à `3` secondes. 
  5. Cliquez sur **Terminé**.
  6. Déployez vos changements en cliquant sur **Déployer**.  
La charge utile contient des points de données tels que ceux de l'exemple suivant : 
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. Optionnel : ouvrez l'onglet Déboguer pour vérifier que des messages sont créés à intervalles réguliers. 
    1. Dans le menu situé dans la section d'en-tête, sélectionnez **Afficher**.
    2. Sélectionnez **Show Sidebar** (afficher la barre latérale).
    3. Cliquez sur l'onglet Déboguer pour voir les messages.

  8. Dans la page d'informations sur le terminal {{site.data.keyword.iot_short_notm}}, vérifiez que
des points de données émis par le terminal apparaissent bien dans la section Informations du capteur.



## Etape 4 : Créez des cartes dans {{site.data.keyword.iot_short_notm}} pour afficher les données temps réel  
{: #createcards}  
Créez un tableau et des cartes pour afficher les données de terminaux dans le tableau de bord de {{site.data.keyword.iot_short_notm}}.
Pour plus d'informations sur les tableaux et les cartes,
consultez [Visualisation des données en temps réel à l'aide de tableaux et de cartes](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

1. Créez un tableau
  1. Ouvrez le tableau de bord {{site.data.keyword.iot_short_notm}}.  
  **Astuce :** Si le tableau de bord {{site.data.keyword.iot_short_notm}} n'est pas déjà ouvert
dans un autre onglet, retournez à votre tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur le nom
de votre instance {{site.data.keyword.iot_short_notm}}, puis sur **Lancer le tableau de bord**.  
  2. Créez un tableau pour y placer les cartes de vos terminaux simulés.
    1. Si la page Tous les tableaux n'est pas déjà affichée,
sélectionnez **Tableaux** dans le menu principal du
tableau de bord {{site.data.keyword.iot_short_notm}}, puis cliquez sur **Créer un nouveau tableau**.
    2. Entrez un nom pour le tableau (par exemple, `Environnement habitation`) et cliquez sur **Suivant**.
    3. Sur la page suivante, cliquez sur **Soumettre**.  
  3. Cliquez sur le tableau que vous venez de créer pour l'ouvrir.

2. Créez une carte pour y afficher la température.
  1. Cliquez sur **Ajouter une nouvelle carte** et, dans la section Terminaux,
sélectionnez le type de carte **Graphique à courbes**.

  2. Sélectionnez votre terminal dans la liste des terminaux, puis cliquez sur **Suivant**.
  3. Cliquez sur **Connecter un nouveau fichier**.
  4. Dans la page Créer une carte Valeur, sélectionnez ou entrez les valeurs suivantes,
puis cliquez sur **Suivant**.
    - Événement : Mise à jour
    - Propriété : temp
    - Nom : Température
    - Type : Variable flottante
    - Unité : °C
    - Précision : 2
    - Min : 0
    - Max : 50
  5. Dans la page Aperçu de la carte, sélectionnez **L** pour la taille du graphique à courbes,
puis cliquez sur **Suivant**.
  6. Dans la page Informations sur la carte, changez le nom de la carte pour **Température** et cliquez sur **Soumettre**.   
La carte Température apparaît sur le tableau de bord. Elle inclut une courbe indiquant la température en temps réel. 
3. Créez une carte pour y afficher l'humidité.
  1. Cliquez sur **Ajouter une nouvelle carte** et, dans la section Terminaux,
sélectionnez le type de carte **Jauge**.

  2. Sélectionnez votre terminal dans la liste, puis cliquez sur **Suivant**.
  3. Cliquez sur **Connecter un nouveau fichier**.
  4. Dans la page Créer une carte Valeur, sélectionnez ou entrez les valeurs suivantes, puis cliquez sur **Suivant**.
  Événement : Mise à jour
     - Propriété : humidity
     - Nom : Humidité
     - Type : Variable flottante
     - Unité : %
     - Précision : 1
     - Min : 10
     - Max : 95
  5. Dans la page Aperçu de la carte, sélectionnez **M** pour la taille de la jauge,
puis cliquez sur **Suivant**.
  6. Dans la page Informations sur la carte, changez le nom de la carte pour **Humidité** et cliquez sur **Soumettre**.   
La carte Humidité apparaît sur le tableau de bord. Elle inclut un cadran (jauge) indiquant le taux d'humidité en temps réel.   

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## Etapes suivantes  
{: #whats-next}  
A présent que votre terminal simulé envoie des données à {{site.data.keyword.iot_short_notm}}, vous pouvez continuer d'effectuer des itérations sur votre projet IoT. 
 - Observez vos cartes afficher les données générées par le flux Node-RED.   
Node-Red continue à envoyer des données jusqu'à ce que vous l'arrêtiez. Pour mettre fin au flux de données simulées, effectuez les étapes suivantes : 
    1.	Dans votre éditeur de flux Node-RED, double-cliquez sur le noeud gris d'**envoi de données**,
réglez la valeur de répétition sur **Intervalle** et fixez l'intervalle de répétition à **3** secondes. 
    2. Cliquez sur **Terminé**.
    3. Déployez vos changements en cliquant sur **Déployer**.

 - Connectez un terminal physique.  
[Faites des recherches dans nos recettes IoT](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) pour
découvrir comment connecter un terminal physique tel qu'un Raspberry Pi et lui faire envoyer des données à {{site.data.keyword.iot_short_notm}}.

 - Explorez les options de visualisation.  
[Déployez une application exemple Node.js pour visualiser les données d'un terminal](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html).

 -	Protégez l'éditeur de flux Node-RED par un mot de passe.    
Par défaut, l'éditeur est ouvert et tout utilisateur peut accéder aux flux et les modifier. Pour le protéger par un mot de passe, procédez comme suit :
    1.	Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur le nom de votre application Starter pour ouvrir les pages correspondantes. 
    2. Cliquez sur **Exécution** pour afficher la page du même nom. 
    3. Cliquez sur **Variables d'environnement** pour afficher la page du même nom.
    4. Dans la section **Défini par l'utilisateur**, cliquez sur **Ajouter**, puis entrez les
variables définies par l'utilisateur suivantes : 
         -	NODE_RED_PASSWORD - nom d'utilisateur pour sécuriser l'éditeur
         -	NODE_RED_PASSWORD - mot de passe pour sécuriser l'éditeur
    3.	Cliquez sur **Sauvegarder**.
