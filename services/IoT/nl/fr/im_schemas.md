---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Création de schémas de type de terminal
{: #iotrtinsights_task}

Pour utiliser les fonctions {{site.data.keyword.iot_short}}, telles que des règles et des actions, vous devez créer un schéma pour mapper des propriétés de terminal à des noms de propriété conviviaux, définir les unités de données pour les propriétés et spécifier un type de message à utiliser avec le schéma.
{: shortdesc}

**Important :** Des schémas sont requis pour utiliser des règles et des actions. Pour plus d'informations, voir [Cloud Analytics](cloud_analytics.html#rules).

**Important :** Les fonctions d'analyse sont fusionnées à partir du service {{site.data.keyword.iotrtinsights_full}}. Si votre organisation {{site.data.keyword.iot_short_notm}} est utilisée comme source de données pour une instance {{site.data.keyword.iotrtinsights_short}} existante, Cloud and Edge Analytics n'est pas activé tant que les instances {{site.data.keyword.iotrtinsights_short}} existantes n'ont pas été migrées. Continuez d'utiliser le tableau de bord {{site.data.keyword.iotrtinsights_short}} pour vos besoins en analyse tant que la migration n'est pas terminée. Pour plus d'informations, voir le [blogue IBM Watson IoT Platform![](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} sur IBM developerWorks et vos tableaux de bord de l'instance {{site.data.keyword.iotrtinsights_short}} existante.   

## Ajout d'un schéma de terminal
{: #add_schema}

Pour ajouter un schéma :  
1. Accédez à **Terminaux > Gérer les schémas**, puis cliquez sur **Ajouter un schéma**.  
2. Sélectionnez un type de terminal à associer à ce schéma de message. **Important :** Un seul schéma peut être défini pour un type de terminal.

3. Ajoutez une ou plusieurs propriétés.  
    Vous pouvez sélectionner des propriétés à partir d'un terminal connecté, créer des propriétés virtuelles qui modifient ou combinent des propriétés existantes, ou ajouter manuellement des propriétés.  

    **Astuce : ** Les propriétés disponibles sont définies dans le contenu des messages qui sont envoyés par un terminal. Pour plus d'informations sur le format de contenu {{site.data.keyword.iot_short}} payload format, voir la rubrique [Contenu de message](reference/mqtt/index.html#message-payloadl "Contenu de message.").   
  <dl>
  <dt>Ajouter manuellement une propriété</dt>
  <p><b>Astuce :</b> Pour créer une structure de propriété imbriquée, commencez par ajouter une propriété dont le type de données est Parent. Dans la table des propriétés, vous pouvez ensuite cliquer sur l'icône ![Ajouter un enfant](images/add_child.png "Ajouter un enfant") pour ajouter une ou plusieurs propriétés enfant.</p>
  <dd>
  <ol>
    <li>Sélectionnez l'onglet **Manuel**.</li>
    <li>Définissez les détails de propriété suivants :
    <ul>  
      <li>Nom - Nom descriptif pour la propriété qui est utilisée dans les tableaux de bord, les menus et les assistants {{site.data.keyword.iot_short}}.</li>
      <li>Type de données - Type des données de la propriété :  
   `Chaîne`, `Entier`, `Flottant` ou `Parent`.</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>Propriété - Identificateur de propriété, par exemple :  
 `temp` ou `vitesse`  </br> Pour savoir comment identifier les propriétés à partir des messages de terminal, voir [Identification des propriétés pour vos terminaux](#identify-datapoints "Identifier les propriétés.").</li>
  <li>Unité de données - Facultatif. Unité de données de la propriété. Par exemple :  
     `C` ou `Mph`  </li>
     <li> Positions décimales (facultatif) - Type Flottant uniquement : nombre de positions décimales à inclure dans les données d'unité.</li>
    </ul>
    </li>
    <li>Cliquez sur **Terminer** pour créer la propriété.</li>
  </ol>
  </dd>
  <dt>Créer une propriété virtuelle</dt>
  <dd> Par exemple, si la propriété de terminal temp renvoie une valeur de température exprimée en Fahrenheit alors que vous souhaitez utiliser des Celsius, vous pouvez créer une propriété virtuelle *temp_c* avec la fonction suivante : *temp_c=(temp-32)/1.8*. Vous pouvez ensuite utiliser la propriété virtuelle *temp_c* à la place de la propriété en temps réel *temp* dans vos conditions de règle.  
  Pour créer une propriété virtuelle :
  <ol>
    <li>Sélectionnez l'onglet **Propriété virtuelle**.</li>  
    <li>Définissez les détails de propriété suivants :
    <ul>
    <li>Nom - Nom descriptif pour la propriété qui est utilisée dans les tableaux de bord, les menus et les assistants {{site.data.keyword.iot_short}}.</li>
    <li>Type de données - Type des données de la propriété :  
 `Flottant` ou `Entier`.</li>
 <li>Propriété - Identificateur de la propriété virtuelle. Par exemple :  
`temp_virt`</li>
    <li>Calcul - Ajoutez un ou plusieurs composants afin de définir une fonction valide. Vous pouvez utiliser des propriétés, des valeurs numériques et des opérateurs mathématiques, tels que +, -, \*, /, ( et ).  
    Cliquez sur **Avancé** pour obtenir un ensemble de formules à utiliser avec une série de points de données sur des terminaux Edge. Pour plus d'informations sur les formules avancées, voir [Calculs avancés pour les propriétés virtuelles Edge](im_vir_calculations.html).  
    **Important :** Les conditions de règle qui comparent des propriétés virtuelles en fonction de formules avancées ne sont pas prises en charge. </li>
    <li>Unité de données - Facultatif. Unité de données de la propriété. Par exemple : `C` ou `Mph`</li>
    <li> Positions décimales (facultatif) - Type Flottant uniquement : nombre de positions décimales à inclure dans les données d'unité.</li>
   </ul>
   </li>
   <li>Cliquez sur **Terminer** pour créer la propriété.</li>
  </ol>
  </dd>
  <dt>Sélectionner les propriétés à partir d'un terminal connecté</dt>
  <dd>
  <ol>
    <li>Sélectionnez l'onglet **A partir de terminaux connectés**.</li>  
    <li>Sélectionnez une ou plusieurs propriétés à ajouter au schéma. Ces propriétés peuvent ensuite être éditées pour définir des attributs, par exemple, un nom et une unité de données.  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>Cliquez sur **OK** pour créer les propriétés.</li>
  </ol>
  </dd>
    <dd>Les propriétés sélectionnées sont ajoutées et le nom de la propriété est affecté à la description. Cliquez sur la propriété dans la liste pour l'éditer, puis ajoutez des attributs supplémentaires, tels que le type de capteur, le type de données et le nombre de positions décimales.</dd>
  </dl>
8. Cliquez sur **Terminer** pour créer le schéma de message.

## Identification de propriétés pour vos terminaux
{: #identify-datapoints}
   Les propriétés d'un terminal sont consultables dans le tableau de bord {{site.data.keyword.iot_short}}.

1. Dans le tableau de bord {{site.data.keyword.iot_short}}, accédez à **Terminaux**.
2. Cliquez sur un terminal pour ouvrir une page affichant des détails sur le terminal.
3. Faites défiler l'écran vers le bas jusqu'à la section **Informations sur le capteur** pour voir la liste des propriétés disponibles pour un terminal connecté.
