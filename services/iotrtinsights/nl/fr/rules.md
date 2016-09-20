---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}

# Création de règles et réponse aux alertes{: #rules}

Utilisez des règles d'analyse pour configurer des alertes et des notifications pour vos périphériques. Par exemple, vous pouvez créer une règle qui ajoute une alerte au tableau de bord de périphérique et envoie un courrier électronique à un administrateur si le capteur de température du périphérique enregistre une température anormalement élevée.
{: shortdesc}

Vous pouvez utiliser des règles comprenant des conditions qui comparent des points de données ou des paramètres de contexte, tels que des mappages d'actifs avec des valeurs statiques, d'autres points de données ou des paramètres de contexte. 

>**Remarque :** Lorsque vous utilisez une instance de forfait gratuit d'{{site.data.keyword.iotrtinsights_short}}, toutes les règles sont automatiquement désactivées au bout d'une heure. Vous pouvez les réactiver manuellement. Si vous souhaitez que les règles s'appliquent en continu, vous pouvez opter pour un forfait payant.

Pour créer une règle pour un périphérique :
1. Dans la console {{site.data.keyword.iotrtinsights_short}}, accédez à **Analyse > Règles**.
2. Cliquez sur **Ajouter une règle**, attribuez un nom à la règle, indiquez une description et sélectionnez un schéma de message pour la règle, puis cliquez sur **Suivant**.  
3. Cliquez sur **OK** pour créer la nouvelle règle. 
3. **Facultatif :** Sélectionnez une priorité d'alerte pour la règle.
La priorité est utilisée pour classifier les alertes qui s'affichent dans le panneau des alertes. La priorité par défaut est Low (faible).
3. Pour configurer la logique de règle, ajoutez une ou plusieurs conditions IF qui sont utilisées en tant que déclencheurs pour la règle. Vous pouvez ajouter des conditions sur des lignes parallèles afin de les appliquer en tant que conditions OR ou vous pouvez ajouter des conditions dans des colonnes séquentielles afin de les appliquer en tant que conditions AND.
**Astuce :** Pour obtenir un aperçu des valeurs typiques renvoyées par vos périphériques, accédez à **Périphériques > Parcourir les périphériques** et cliquez sur votre périphérique pour voir les données en temps réel affichées.
**Important :** Pour déclencher une condition qui compare deux points de données ou pour déclencher au moins deux conditions de point de données combinées de manière séquentielle, vous devez inclure les données de déclenchement dans le même message. S les données sont reçues dans plusieurs messages, la condition ou les conditions séquentielles ne se déclenchent pas.   
> **Exemples :**   
Une règle simple peut déclencher une alerte si une valeur de paramètre est supérieure à une valeur spécifiée.  
Par exemple : Condition = `ax>5`  
Une règle plus complexe peut déclencher une alerte si une valeur de paramètre pour un périphérique mappé à un actif spécifique est supérieure à une valeur donnée.   
Par exemple : Condition = `ax>5 AND asset.assetnum==5001`   
Pour obtenir des instructions détaillées, voir [Exemple : Création d'une règle complexe à l'aide de conditions de schéma de message et de paramètre de contexte](#complex "Exemple : Création d'une règle complexe à l'aide de conditions de schéma de message et de paramètre de contexte").  
4. Configurez les exigences de déclenchement conditionnel pour votre règle.
Pour contrôler le nombre d'alertes qui sont déclenchées pour une règle pendant une période donnée, vous pouvez configurer des exigences de déclenchement conditionnel pour votre règle. **Important :** Le déclenchement conditionnel agit sur n'importe quelle condition dans la règle. Par exemple, si 5 conditions parallèles différentes (OR) sont définies pour une règle, chaque condition qui est remplie est décomptée du nombre de déclenchements conditionnels.
Pour définir un déclenchement conditionnel pour une règle :
 1. Dans l'éditeur de règles, cliquez sur le lien **Déclencher chaque fois que les conditions sont remplies** pour ouvrir la boîte de dialogue de condition. 
 2. Sélectionnez et configurez le déclencheur conditionnel que vous souhaitez utiliser avec la règle.
 <ul>
 <li>Déclencher chaque fois que les conditions sont remplies</li>
 <li>Déclencher si des conditions sont remplies N fois en M *unité de temps*</li>
 </ul>  
 Pour obtenir une description plus détaillée des déclencheurs conditionnels, voir  [Déclenchement conditionnel](#conditional "Vue d'ensemble du déclenchement conditionnel").
5. Créez ou sélectionnez une ou plusieurs actions qui se déclenchent si les conditions de règle sont remplies.
Pour plus d'informations sur les actions, voir [Créer des actions](actions.html#shared "Créer des actions").   
 > Par exemple, une action peut être envoyée par courrier électronique. Pour plus d'informations sur les différents types d'action, voir [Types d'action](actions.html "Types d'action").
6. Lorsque la règle vous convient, cliquez sur **Sauvegarder**.
7. Sur la page Règles, cliquez sur l'![icône Configurer](images/gear.png "icône Configurer") et sélectionnez **Activer** pour activer la règle. 

Votre règle est active. Si les conditions de la règle sont remplies, une alerte est ajoutée au tableau de bord **Tableaux de bord > Vue d'ensemble** et toute action associée à la règle est exécutée. 

## Déclenchement conditionnel {: #conditional}

Pour contrôler le nombre d'alertes qui sont déclenchées pour une règle pendant une période donnée, vous pouvez configurer des exigences de déclenchement conditionnel pour votre règle. 

Selon la fréquence de message et les conditions de règle, une règle peut se déclencher de nombreuses fois dès lors qu'une condition de déclenchement est remplie. Par exemple, si la condition est `temp >= 90` et que la température augmente et se stabilise à 91, la règle se déclenche à chaque message entrant. Selon la fréquence des messages de périphérique et les actions associées à la règle, votre boîte de réception de messagerie électronique peut se remplir rapidement ou un flux Twitter peut être inondé de messages qui n'apportent rien de plus que le premier message. 

**Important :** Le déclenchement conditionnel agit sur n'importe quelle condition dans la règle. Par exemple, si 5 conditions parallèles différentes (OR) sont définies pour une règle, chaque condition qui est remplie est décomptée du nombre de déclenchements conditionnels.


Condition | Description
------------- | -------------
Déclencher chaque fois que les conditions sont remplies | La règle est déclenchée chaque fois que les conditions qui lui sont associées sont remplies.
Déclencher si des conditions sont remplies N fois en M *jours/heures/minutes/personnalisé* | La règle est déclenchée lorsque les conditions ont été remplies N fois au cours de l'intervalle de temps sélectionné, puis elle n'est pas redéclenchée tant que le délai configuré n'est pas dépassé. </br>Exemple : Exigence de déclenchement conditionnel =`Déclencher une fois si les conditions sont remplies 4 fois en 30 minutes`. Le périphérique envoie un nouveau message toutes les cinq minutes. A midi, la température dépasse 90 degrés et remplit ainsi la condition. Le compteur associé au déclenchement conditionnel est démarré mais la règle n'est pas encore déclenchée. Au bout de 15 minutes et la réception de plus de trois messages indiquant `temp > 90`, la règle est déclenchée. Ensuite, la règle n'est pas déclenchée au cours des 15 minutes suivantes, quelle que soit la température.

## Exemple : Création d'une règle complexe à l'aide de conditions de schéma de message et de paramètre de contexte{: #complex}
Pour créer une règle plus complexe qui génère une alerte dans le tableau de bord d'alertes lorsque le paramètre des ax dépasse la valeur 5 pour n'importe quel périphérique IoT Phone qui est mappé au numéro d'actif 5001 , procédez comme suit : 
1. Accédez à **Périphériques > Gérer les mappages d'actifs** et mappez au moins un périphérique IoT Phone à un actif portant le numéro d'actif 5001.
Pour obtenir des instructions détaillées, voir [Gestion des actifs](assets.html "Gestion des actifs").
2. Accédez à **Analyse**, puis cliquez sur **Ajouter une règle**.
3. Attribuez à la règle un nom descriptif et une description et indiquez le type de périphérique pour lequel la règle s'applique en sélectionnant le schéma de message que vous avez créé pour votre type de périphérique IoT Phone. 
4. Cliquez sur **OK** pour créer la nouvelle règle. 
<!-- 5. Click ![Add icon.](images/rules_plus.png "Add icon") to add an initial condition. -->
6. Cliquez sur la vignette de la nouvelle condition et éditez la condition initiale. 
 1. Sélectionnez **Point de données** comme opérande à comparer. 
 2. Sélectionnez le point de données **ax**. 
 3. Sélectionnez l'opérateur **>** de sorte que la condition soit remplie si la valeur de la première opérande est supérieure à celle de la seconde opérande. 
 3. Sélectionnez **Valeur statique** comme opérande de comparaison cible. 
 4. Entrez `5` comme valeur à laquelle comparer le point de données ax. 
 5.  Cliquez sur **OK** pour ajouter la condition. 
5. Pour ajouter la condition AND, cliquez sur l'![icône Ajouter](images/rules_plus.png "icône Ajouter") située à droite de la première condition.
6. Cliquez sur la vignette de la nouvelle condition et éditez la condition. 
  1. Sélectionnez **context** comme opérande à comparer.
  2. Dans le menu de paramètre de contexte, cliquez sur le triangle figurant devant le schéma de contexte **assets** pour développer la liste de paramètres de contexte asset. 
  3. Sélectionnez le paramètre de schéma de contexte **ASSETNUM**. 
  3. Sélectionnez l'opérateur **==** de sorte que la condition soit remplie si les valeurs de la première opérande et de la seconde opérande sont égales. 
  3. Sélectionnez **Valeur statique** comme opérande de comparaison cible. 
  4. Entrez `5001` comme valeur à laquelle comparer le paramètre de schéma de contexte **ASSETNUM**. 
  5.  Cliquez sur **OK** pour créer la condition. 
7. Utilisez le déclenchement conditionnel par défaut, `Déclencher chaque fois que les conditions sont remplies`. 
7. Créez ou sélectionnez une ou plusieurs actions.
7. Sauvegardez la nouvelle règle.
7. Sur la page Règles, dans la vignette de la nouvelle règle, cliquez sur l'![icône Configurer](images/gear.png "icône Configurer") et sélectionnez **Activer** pour activer la règle. 

## Exemple : Création de règles basées sur des actifs{: #asset_rules}

Après avoir mappé vos périphériques à des actifs, vous pouvez créer des règles qui utilisent les informations détaillées relatives aux actifs. Le mappage de périphériques à des actifs et la création de règles qui intègrent à la fois les points de données et les informations sur les actifs représentent un puissant outil. 

Dans les exemples ci-après, nous utilisons des actifs pour effectuer le suivi des téléphones portables de l'entreprise. Deux actifs ont été créés et mappés à des téléphones portables. L'actif 5001 est mappé à des téléphones pour lesquels PURCHASEPRICE < 100 et l'actif 5002 est mappé à des téléphones pour lesquels PURCHASEPRICE >=100. La condition de déclenchement des données de périphérique pour chaque exemple est `d.ax>5`, ce qui, dans cet exemple simplifié, correspond à une accélération brutale du téléphone, par exemple, si l'utilisateur le fait tomber. 

Vous pouvez maintenant configurer deux règles simples afin de signaler qu'un téléphone mappé à l'actif 5001 est tombé. Il est tout aussi simple de configurer une règle afin de signaler qu'un téléphone non mappé à 5001 est tombé. Il peut s'agir de n'importe quel téléphone mappé à 5002 ou de n'importe quel téléphone qui n'est pas mappé à aucun actif. 

Exemple | Règle
------------- | -------------
Déclencher la règle uniquement si le périphérique fait partie de l'actif 5001 | IF `d.ax>5` AND `asset.assetnum==5001` THEN ...
Déclencher la règle uniquement si le périphérique NE fait PAS partie de l'actif 5001 | IF `d.ax>5` AND `asset.assetnum!=5001` THEN ...

Vous pouvez également configurer des règles qui se déclenchent pour des téléphones auxquelles une valeur PURCHASEPRICE spécifique est associée.   

Exemple | Règle
------------- | -------------
Déclencher la règle uniquement si le téléphone coûte moins de 100 | IF `d.ax>5` AND `asset.purchaseprice<100` THEN ...
Déclencher la règle uniquement si le téléphone coûte plus de 100 | IF `d.ax>5` AND `asset.purchaseprice>=100` THEN ...

Enfin, vous pouvez associer ces règles pour un comportement plus complexe. 

Exemple | Règle
------------- | -------------
Déclencher la règle uniquement si le téléphone fait partie de l'actif 5001 (coûts inférieurs à 100) mais coûte plus de 75 | IF `d.ax>5` AND `asset.assetnum==5001` AND  `asset.purchaseprice>75` THEN ...
Déclencher la règle uniquement si le téléphone fait partie de l'actif 5002 (coûts supérieurs à 100) mais coûte moins de 200 | IF `d.ax>5` AND `asset.assetnum==5002` AND  `asset.purchaseprice<200` THEN ...
