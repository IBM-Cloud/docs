---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}

# Gestion des tableaux de bord et des modèles{: #managing-dashboards}

Les données en temps réel de vos périphériques IoT sont affichées dans des tableaux de bord personnalisables. Vous pouvez créer manuellement des tableaux de bord qui affichent des mesures en temps réel, des graphiques et d'autres informations pour un plusieurs périphériques. Les tableaux de bord peuvent également contenir des listes filtrées de périphériques et de liens vers d'autres tableaux de bord.
{: shortdesc}

Outre des tableaux de bord créés manuellement, {{site.data.keyword.iotrtinsights_short}} fournit un tableau de bord d'alertes de périphérique prédéfinies accessible dans **Tableaux de bord > Vue d'ensemble** et crée dynamiquement des tableaux de bord de périphérique basés sur les schémas de message que vous créez. 

## Tableaux de bord {: #dashboards}

Les administrateurs peuvent créer de nouveaux tableaux de bord et modifier des tableaux de bord existants afin d'afficher les données de périphérique qui les intéressent.   
Pour créer un tableau de bord, procédez comme suit :
1.	Accédez à **Tableaux de bord > Parcourir les tableaux de bord**.
2.	Cliquez sur **Ajouter un tableau de bord**.
3.	Affectez un nom au tableau de bord et sélectionnez des attributs, tels que icône et arrière-plan. En outre, indiquez si ce tableau de bord peut être modifié par les opérateurs {{site.data.keyword.iotrtinsights_short}}. 
4.	Cliquez sur l'![icône Créer](images/create.png "icône Créer").
5.	Cliquez sur le nouveau titre de tableau de bord pour ouvrir le tableau de bord vide. 
6.	Pour ajouter des widgets au tableau de bord :  
 1.	Cliquez sur **Ajouter un composant** pour ajouter un widget de tableau de bord initial. 
 2.	Sélectionnez un composant à ajouter, puis choisissez d'autres attributs de composant, et, le cas échéant, sélectionnez des propriétés d'affichage. Par exemple, pour afficher la valeur numérique d'un point de données spécifique pour un périphérique, sélectionnez `Périphérique`, puis choisissez le périphérique à ajouter. Dans l'éditeur de tableau de bord, sous Visualisation, sélectionnez un point de données à afficher. Ensuite, positionnez le widget que vous venez d'ajouter dans la grille du tableau de bord. 
 3.	Cliquez sur l'![icône Créer](images/create.png "icône Créer") pour ajouter le widget au tableau de bord. 
7.	Le tableau de bord est mis à jour avec les widgets que vous venez d'ajouter et affiche les données en temps réel qui sont définies par le point de données sélectionné. 

>**Astuce :** Pour créer un tableau de bord qui répertorie tous vos périphériques, procédez comme suit :  
1. Accédez à **Tableaux de bord > Parcourir le tableaux de bord**, puis cliquez sur **Ajouter un tableau de bord**.
2. Affectez au tableau de bord un nom descriptif, tel que `Tous les périphériques`, puis cliquez sur l'![icône Créer](images/create.png "icône Créer").
3. Dans le panneau des tableaux de bord, cliquez sur le tableau de bord, puis cliquez sur **Ajouter un composant**.
4. Sélectionnez le composant **Conteneur**, puis **Périphériques filtrés** pour créer une liste de vos périphériques. 
5. Cliquez sur l'![icône Créer](images/create.png "icône Créer").  

>Vos périphériques sont répertoriés dans le nouveau tableau de bord. Cliquez sur une icône de périphérique pour ouvrir le tableau de bord correspondant à ce périphérique et afficher les données en temps réel pour ce périphérique.
### Widgets de tableau de bord {: #dashboard-widgets}
Les tableaux de bord sont composés de widgets qui affichent les données en temps réel provenant d'un ou de plusieurs périphériques. Le comportement du widget dépend de son type, du point de données qui s'affiche et de la manière dont le point de données est configuré dans le schéma.  
Par exemple, si vous ajoutez un widget de périphérique pour un point de données 'brut', le widget affiche les données brutes sous forme de chaîne uniquement. 

En revanche, si vous configurez le point de données avec une valeur minimale et une valeur maximale, vous avez la possibilité d'afficher un widget sous forme de jauge. 

Vous pouvez également affecter un type de capteur au point de données afin d'activer un type spécial de widget de visualisation et mieux illustrer le type de données de capteur affiché. Par exemple, vous pouvez sélectionner le type de capteur `Lumière activée/désactivée` afin d'activer le widget de visualisation `Indicateur de lumière brut (activée/désactivée)`. 

Vous avez également la possibilité d'inclure plusieurs widgets pour un même point de données dans un tableau de bord donné afin d'afficher la valeur numérique brute et l'humidité côte à côte.![Plusieurs widgets pour le même point de données](images/widgets.svg "Plusieurs widgets pour le même point de données").  
*Trois options de visualisation pour le même point de données*.


Widget | Type et visualisation
------------- | -------------
Périphérique | Données - Valeur en temps réel des points de données pour le périphérique. Si le point de données est configuré pour inclure une valeur minimale et une valeur maximale, les options de visualisation incluent l'affichage du point de données en tant que jauge. De plus, si le point de données est configuré avec un type de capteur, d'autres options de visualisation sont disponibles.
Graphique | Graphique - Valeurs de tracé en temps réel des points de données pour un ou plusieurs périphériques.
Tableau de bord | Lien vers un tableau de bord ou un modèle.
Texte | Zone de texte - Texte formaté.
Conteneur | Types de widgets conteneur :<ul><li>Tous les tableaux de bord - Liste liée répertoriant tous les tableaux de bord.</li><li>Périphériques filtrés - Liste de tous les périphériques ou liste filtrée par nom ou emplacement. </li><li>Périphériques filtrés avec des alertes - Liste de tous les périphériques avec des alertes ou liste filtrée par nom ou emplacement. </li><li>Alertes pour les périphériques - Liste d'alertes pour un périphérique qui est sélectionné dans une liste de périphériques filtrée avec un conteneur d'alertes. </li></ul>
Spécial | Types de widgets spéciaux :<ul><li>Mappe – Mappe qui permet de localiser le périphérique sélectionné. </li><li>Autres informations sur le périphérique - Informations supplémentaires sur le périphérique sélectionné. </li></ul>

Le tableau suivant récapitule les options de visualisation disponibles pour les widgets de périphérique si le point de données sélectionné est configuré avec un attribut de type de capteur dans le schéma de message.

Type de capteur de point de données | Options de visualisation | Détails | Type de données prises en charge
------------- | ------------- | -------------
Pas de sélection | Valeur brute | - | Chaîne/Entier/Flottant
Lumière activée/désactivée | Indicateur de lumière brut (activée/désactivée) | 0=désactivée | Entier
Commutateur activé/désactivé | Indicateur de commutateur brut (activé/désactivé) | 0=désactivé | Entier
Capteur de température | Jauge de température générique | Non applicable | Entier/Flottant
Contrôle de température | Jauge de température générique | Non applicable | Entier/Flottant
Capteur de pression | Jauge de pression brute | Non applicable | Entier/Flottant
Niveaux de batterie | Widget de batterie brut (bas/élevé) | 0=correct | Entier
Luminosité | Indicateur de luminosité (foncée/claire) | 0=foncée | Entier
Fenêtre ouverte/fermée | Etat de fenêtre brut (ouverte/fermée) | 0=fermée | Entier
Porte ouverte/fermée | Etat de porte brut (ouverte/fermée) | 0=fermée | Entier
Capteur d'hygrométrie | Etat d'hygrométrie (sec/mouillé) | 0=sec | Entier
Consommation électrique | Jauge d'alimentation brute | Non applicable | Entier/Flottant
Compteur énergétique | Valeur brute | Non applicable | Entier/Flottant
Pourcentage | Pourcentage brut (0-100) | Non applicable | Entier/Flottant
Tension | Jauge de tension brute | Non applicable | Entier/Flottant
Courant | Jauge de courant brute | Non applicable | Entier/Flottant
Longitude | Emplacement de périphérique sur Spécial > Widget de mappe (le widget de latitude est également requis) | **Important :** Le type de capteur Longitude défini dans le schéma de message doit être affecté au point de données utilisé pour la valeur de longitude.  | Latitude flottante | Emplacement de périphérique sur Spécial > Widget de mappe (le widget de longitude est également requis) | **Important :** Le type de capteur Latitude défini dans le schéma de message doit être affecté au point de données utilisé pour la valeur de latitude.  | Flottant  


## Présentation des tableaux de bord par défaut
{{site.data.keyword.iotrtinsights_short}} fournit deux tableaux de bord prédéfinis : un tableau de bord d'alertes et un tableau de bord de périphérique. 

Les tableaux ci-après décrivent les widgets et la présentation des tableaux de bord prédéfinis.
### Tableau de bord d'alertes (Tableaux de bord > Vue d'ensemble)
Ce tableau de bord est inclus dans le produit et fournit une liste de périphériques pour lesquels il existe des alertes ouvertes. Vous pouvez sélectionner un périphérique pour afficher les détails sur les alertes, et vous pouvez cliquer sur l'icône de périphérique pour ouvrir un tableau de bord correspondant à ce périphérique et afficher les données en temps réel relatives à ce périphérique.

<table>
<thead>
<tr>
<th colspan="3">Tableau de bord d'alertes</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Conteneur : Périphériques avec des alertes</td>
<td style="width:30%">Conteneur : Alertes pour les périphériques</td>
<td style="width:30%">Spécial : Autres informations sur le périphérique</td>
</tr>
<tr>
<td style="width:30%"></td>
<td style="width:30%"></td>
<td style="width:30%">Spécial : Mappe</td>
</tr>
</tbody>
</table>

*Présentation du tableau de bord d'alertes*

### Tableaux de bord de périphérique
Lorsque vous cliquez sur une icône de périphérique dans une liste de périphériques, un tableau de bord correspondant à périphérique s'ouvre. Lorsqu'un point de données est ajouté au schéma de message, il est également ajouté en tant que widget dans le modèle de périphérique, ce qui crée le tableau de bord de périphérique de façon dynamique. Les administrateurs peuvent ajouter ou retirer manuellement des widgets.

<table>
<thead>
<tr>
<th colspan="3">Tableau de bord de périphérique</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Périphérique : Point de données 1</td>
<td style="width:30%">Périphérique : Point de données 2</td>
<td style="width:30%">Périphérique : Point de données 3</td>
</tr>
<tr>
<td style="width:30%">Périphérique : Point de données N</td>
<td style="width:30%"></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Présentation du tableau de bord de périphérique prédéfini*

### Exemple de tableau de bord : Liste de tous les périphériques
Le tableau de bord ci-après comprend la liste de tous les périphériques et fournit des informations sur un périphérique lorsque vous le sélectionnez dans la liste. 

<table>
<thead>
<tr>
<th colspan="3">Tableau de bord Liste de tous les périphériques</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Conteneur : Périphériques filtrés (aucun paramètre filtre défini)</td>
<td style="width:30%">Spécial : Autres informations sur le périphérique</td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Présentation du tableau de bord Liste de tous les périphériques*

## Modèles {: #templates}
Les modèles contrôle la présentation des tableaux de bord prédéfinis pour un type de périphérique donné. Les administrateurs peuvent modifier ces modèles prédéfinis en fonction de vos besoins. Par exemple, un modèle prédéfini inclut uniquement les points de données génériques. Vous pouvez ajouter des graphiques et d'autres composants selon vos besoins. 

Par exemple, un utilisateur peut accéder à un tableau de bord de périphérique prédéfini pour voir des données de périphérique de base, puis suivre un lien vers un modèle créé manuellement susceptible de contenir un jeu complet de graphiques en temps réel. Vous créez un modèle en procédant à peu près de la même manière que pour créer un tableau de bord.   

Pour modifier un modèle prédéfini :
1.	Accédez à **Tableaux de bord > Gérer les modèles**.
2.	Dans le panneau Gérer les modèles, recherchez la vignette du modèle, puis cliquez sur l'![icône Configurer](images/gear.png "icône Configurer")** > Modifier la présentation** pour ouvrir le modèle à éditer.   
3.	Ajoutez des widgets au modèle. 
 1.	Cliquez sur **Ajouter un composant de modèle** pour ajouter un widget de modèle initial.
 2.	Sélectionnez un composant à ajouter, puis choisissez d'autres attributs de composant, et, le cas échéant, sélectionnez des propriétés d'affichage.   
 3.	Cliquez sur l'![icône Créer](images/create.png "icône Créer") pour ajouter le widget au modèle. 
4.	Editez les widgets existants.
 1.	Survolez un widget de modèle, puis cliquez sur l'![icône Configurer](images/gear.png "icône Configurer").
 2.	Modifiez le composant et ses attributs, puis repositionnez le widget selon vos besoins.
 3.	Cliquez sur l'![icône Créer](images/create.png "icône Créer") pour mettre à jour le widget.  

Le modèle est mis à jour avec vos modifications.

<!-- Administrators can also manually add templates for specific device types. These templates can then be linked to from the predefined templates.  -->

<!-- To create a template:
1.	Go to **Dashboards > Manage templates**.
2.	Click **Add new template**.
3.	Give the template a name, select a device type and attributes such as icon and background.
4.	Click ![Create icon.](images/create.png "Create icon").
5.	The empty template opens.
6.	Add widgets to the template.  
For a list of widgets, see below.
 1.	Click **Add new component** to add an initial template widget.
 2.	Select a component to add, then select further component attributes and, if needed, select display properties.
 For example, ... Then position the newly added widget in the dashboard grid.
 3.	Click ![Create icon.](images/create.png "Create icon") to add the widget to the template.
7.	The template updates with the newly added widgets.

### Template widgets
Widget | Type and visualization
------------- | -------------
Device | Data - Real-time value of data points for the device. For a description of the available widget options, see [Dashboard widgets](#dashboard-widgets "Dashboard widgets") above.
Chart | Graph - Plot real-time values of data points for one or more devices.
Dashboard | Link to a dashboard or a template.
Text | Text box - Formatted text
Container | Types of containers:<ul><li>All dashboards – A linked list of all dashboards</li><li>Filtered devices – A list of all devices, or filtered by name or location</li><li>Filtered devices with alerts – A list of all devices with alerts, or filtered by name or location</li><li>Alerts for device – A list of alerts for a device that is selected in a Filtered devices with alerts container</li></ul>
Special | Types of special:<ul><li>Map – A map that locates the selected device</li><li>Additional device information – More information about the selected device</li></ul>

### Template example: Selected set of graphs
One way of using device templates is to expand on the predefined device template by creating specialized templates for a device type, and then linking these from the predefined template by using a Dashboard widget.

<table>
<thead>
<tr>
<th colspan="3">Descriptive graphs template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: ID</td>
<td style="width:30%">Graph: One data point</td>
<td style="width:30%">Graph: Another data point</td>
</tr>
<tr>
<td style="width:30%">Special: Additional device information</td>
<td style="width:30%">Text: Short description of how to <br>interpret the device data in the graphs.</td>
<td></td>
</tr>
</tbody>
</table>

*Descriptive graphs template*

Link to this template from a predefined device template:

<table>
<thead>
<tr>
<th colspan="3">Predefined device dashboard layout with link to template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: Datapoint 1</td>
<td style="width:30%">Device: Datapoint 2</td>
<td style="width:30%">Device: Datapoint 3</td>
</tr>
<tr>
<td style="width:30%">Device: Datapoint N</td>
<td style="width:30%"><b>Dashboard: Descriptive graphs template</b></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Predefined device dashboard layout with link to template* -->


## Réinitialisation des tableaux de bord et des modèles prédéfinis{: #resetting-dashboards}
Si vous modifiez un modèle prédéfini, il n'est plus mis à jour de manière dynamique à partir des mises à jour de schéma de message, et vous devez réinitialiser le tableau de bord ou le modèle pour restaurer la présentation et les widgets d'origine. Pour réinitialiser les tableaux de bord et les modèles prédéfinis :
1.	Accédez à **Tableaux de bord > Gérer les modèles** ou à **Tableaux de bord > Parcourir les tableaux de Bord**.
2.	Localisez la vignette de modèle ou de tableau de bord prédéfini et cliquez sur l'**![icône Configurer](images/gear.png "icône Configurer") > Réinitialiser la présentation** pour supprimer, puis recréer le modèle.   

Le modèle ou tableau de bord est recréé avec le widget par défaut défini. 
