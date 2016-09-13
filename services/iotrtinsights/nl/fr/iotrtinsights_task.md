---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Connexion et affichage de vos périphériques
{: #iotrtinsights_task}
*Dernière mise à jour : 11 février 2016*

{{site.data.keyword.iotrtinsights_short}} utilise {{site.data.keyword.iot_short}} pour l'accès aux périphériques et l'extraction de données. Les périphériques que vous connectez à {{site.data.keyword.iot_short}} sont automatiquement connectés à {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

Si vous connectez un nouveau type de périphérique, vous devez également configurer le schéma de message pour le mappage des points de données de périphérique, la définition des unités et la spécification du type de périphérique. Si le type de vos périphériques est déjà configuré, les données de vos périphériques apparaissent automatiquement dans le tableau de bord. 

## Ajout d'un périphérique
{: #iotrtinsights_subtask}

Pour ajouter un périphérique :  
Le processus d'ajout d'un périphérique se déroule en deux étapes. Tout d'abord, vous ajoutez le périphérique à {{site.data.keyword.iot_short}}, puis vous configurez le mode de consommation et d'affichage des données de périphérique par {{site.data.keyword.iotrtinsights_short}}. 
1. Ajoutez des périphériques à votre {{site.data.keyword.iot_short}}.
> **Astuce :** Si vous avez déployé l'application téléphonique Internet of Things (Internet des objets), un périphérique iotphone est déjà ajouté à *iot-phone-iotf-service* {{site.data.keyword.iot_short}} et vous pouvez ignorer cette étape.   

  Pour ajouter des périphériques à votre {{site.data.keyword.iot_short}}, voir la [documentation {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html) et les [recettes de connexion aux périphériques {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF).
2. Configurez votre périphérique dans {{site.data.keyword.iotrtinsights_short}}.  
  1. Connectez-vous à la console {{site.data.keyword.iotrtinsights_short}} en tant qu'utilisateur administrateur.
  9. Accédez à **Périphériques > Parcourir les périphériques** et vérifiez que le périphérique que vous venez d'ajouter figure dans la liste. 
  > **Astuce :** La liste des périphériques est actualisée à partir de votre source de données toutes les minutes. Cliquez sur **Actualiser** pour mettre à jour la liste des périphériques immédiatement.
  3. Accédez à **Périphériques > Gérer les schémas**, puis cliquez sur **Ajouter un schéma de message**.  
  4. Entrez un nom pour le schéma de message, par exemple : `Nouveau schéma de message`.
  5. Cliquez sur **Lier une nouvelle source de données** et sélectionnez la source de données et le type de périphérique correspondant à votre instance et votre périphérique {{site.data.keyword.iot_short}}. Vous pouvez, si vous le souhaitez, entrer un nom d'événement dans le but de collecter des données pour cet événement uniquement ou vous pouvez laisser le caractère générique `+` afin de collecter tous les événements. Vous trouverez davantage d'informations sur la procédure d'identification des types d'événement pour un périphérique [ici](#identify-datapoints "Identification de points de données.").  
  >**Important :** Chaque schéma de message doit comporter une combinaison source de données, type de périphérique et nom d'événement unique. Pour créer plusieurs schémas pour une combinaison source de données et type de périphérique spécifique, spécifiez un nom d'événement unique pour chaque schéma de message au lieu d'utiliser le caractère générique `+` par défaut.    
  6. Ajoutez un ou plusieurs points de données à inclure dans les tableaux de bord de périphériques.
    Vous pouvez sélectionner des points de données à partir d'un périphérique connecté ou ajouter manuellement des points de données. Les points de données disponibles sont définis dans le contenu des messages qui sont envoyés par un périphérique. Pour toute information sur le format de contenu {{site.data.keyword.iot_short}}, voir la rubrique [Message Payload](https://docs.internetofthings.ibmcloud.com/messaging/payload.html "Message Payload.") dans la documentation {{site.data.keyword.iot_short}}.    
    > **Astuce :** Vous pouvez créer manuellement des points de données virtuels qui modifient ou combinent des points de données existants de type Entier ou Flottant. Par exemple, si le point de données de périphérique temp renvoie une valeur de température exprimée en Fahrenheit alors que vous souhaitez utiliser des Celsius, vous pouvez créer un point de données virtuel *temp_c* à l'aide la fonction suivante : *temp_c=(temp-32)/1.8*. Vous pouvez ensuite utiliser le point de données *temp_c* virtuel à la place du point de données *temp* en temps réel dans vos conditions de règle. Dans les tableaux de bord, les points de données virtuels sont identifiés par un soulignement en pointillé.    

  <dl>
  <dt>Effectuez une sélection parmi les périphériques connectés</dt>
  <dd>
  <ol>
    <li>Cliquez sur **Sélectionner parmi les périphériques connectés**.</li>  
    <li>Dans la boîte de dialogue d'ajout de points de données, sélectionnez un ou plusieurs points de données à ajouter, puis cliquez sur **OK**.</li>   
    <li>Les points de données sélectionnés sont ajoutés avec la description définie au nom du point de données. Cliquez sur le point de données dans la liste pour l'éditer, puis ajoutez des attributs supplémentaires, tels que le type de capteur, le type de données et le nombre de positions décimales. </li>
  </ol>
  </dd>
  <dt>Ajoutez manuellement</dt>
  <p><b>Astuce :</b> Pour créer une [structure de point de données imbriquée](schemas.html), commencez par ajouter un point de données de type Parent. Dans la table des points de données, vous pouvez ensuite cliquer sur l'![icône Ajouter un enfant](images/add_child.png "Ajouter un enfant") pour ajouter un ou plusieurs points de données enfant. </p>
  <dd>
  <ol>
    <li>Cliquez sur **Ajouter manuellement**.</li>
    <li>Sélectionnez **Point de données en temps réel** ou **Point de données virtuel**.</br></li>
    <li>Définissez les informations de point de données suivantes :
    <ul>  
     <li> Point de données - Identificateur de point de données que vous avez [localisé dans le tableau de bord {{site.data.keyword.iot_short}}](#identify-datapoints "Identifier des points de données."). Par exemple :  
   `id`, `ts`, `lat`  </li>
     <li>Description - Brève description du point de données. Cette description est utilisée lors de l'affichage des points de données dans les tableaux de bord. </li>
     <li>Fonction de point de données virtuel - Ajoutez un ou plusieurs composants pour définir une fonction valide. Vous pouvez utiliser des points de données, des valeurs numériques et des opérateurs mathématiques, tels que +, -, \*, /, ( et ) pour construire votre fonction. </li>
     <li>Type de données - Type de données du point de données :  
   `Chaîne`, `Entier`, `Flottant` ou `Parent`.</li>
     <li>Type de capteur - Vous pouvez, si vous le souhaitez, sélectionner la façon dont vous souhaitez interpréter le point de données dans les tableaux de bord. Selon la combinaison de type de données et de type de capteur, des options de visualisation supplémentaires peuvent être disponibles pour vos widgets de tableau de bord. Pour plus d'informations sur les types de capteur et les options de visualisation, voir [Widgets de tableau de bord](dashboards.html#dashboard-widget "Widgets de tableau de bord").</li>
     <li>Icône de point de données - Vous pouvez, si vous le souhaitez, sélectionner une icône destinée à représenter le point de données dans les widgets de tableau de bord. </li>
     <li>Valeur min./max. (facultatif) - Types Entier et Flottant uniquement : Si une valeur maximale et une valeur minimale sont entrées, les données de périphérique peuvent être affichées en tant que jauge dans les tableaux de bord. </li>
     <li>Unité de données (facultatif) : Unité de données du point de données. Par exemple :  
     `C`, `Mph`  </li>
     <li> Positions décimales (facultatif) - Type Flottant uniquement : nombre de positions décimales à inclure dans les données d'unité. </li>
    </ul>
    </li>
  </ol>
  </dd>
  </dl>
   8. Cliquez sur **OK** pour créer le schéma de message. 
   9. Accédez à **Périphériques > Parcourir les périphériques** et cliquez sur le périphérique que vous venez d'ajouter pour vérifier que les données de périphérique en temps réel sont affichées et que les points de données sont correctement mappés. 

## Identification des points de données et des événements dans le tableau de bord {{site.data.keyword.iot_short}}
{: #identify-datapoints}
   Les points de données et les types d'événement d'un périphérique sont consultables dans le tableau de bord {{site.data.keyword.iot_short}}. 
   >**Astuce :** Si vous utilisez l'application téléphonique Internet of Things (Internet des objets) comme périphérique IoT, vous pouvez utiliser l'événement sensorData et les points de données suivants pour configurer le schéma de message :
   >- d.id - ID périphérique
   >- d.ts - Horodatage
   >- d.lat - Latitude
   >- d.lng - Longitude
   >- d.ax - Accélération X
   >- d.ay - Accélération Y
   >- d.az - Accélération Z
   >- d.oa - Mouvement alpha
   >- d.ob - Mouvement bêta
   >- d.og - Mouvement gamma
   >Où d.*point_données* indique que le point de données est imbriqué sous un point de données d de type Parent dans le contenu de message .

   1. A partir du tableau de bord Bluemix, cliquez sur la vignette Internet of Things (Internet des objets).   
   >**Remarque :** Si vous utilisez l'application téléphonique Internet of Things (Internet des objets), cliquez sur la vignette *iot-phone-iotf-service*.   
   2. Cliquez sur **Lancer le tableau de bord** pour ouvrir le tableau de bord {{site.data.keyword.iot_short}}. 
   3. Accédez à la page **Périphériques**. 
   4. Cliquez sur le périphérique pour ouvrir la page de détails de périphérique.
Faites défiler l'écran vers le bas jusqu'à la section **Informations sur le capteur** pour voir la liste des événements et points de données disponibles pour le périphérique. Ces informations sont requises lorsque vous configurez le périphérique dans {{site.data.keyword.iotrtinsights_short}}.
