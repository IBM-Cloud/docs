---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Définition de politiques
{: #policies}

Les politiques contrôlent les jalons dans votre pipeline de distribution continue. Si votre code ne satisfait pas, dans un sens ou dans l'autre, une politique appliquée à un jalon particulier, le déploiement est arrêté dans le but d'empêcher la publication de changements risqués.{:shortdesc}

Vous définissez les politiques dans {{site.data.keyword.DRA_short}}. Les politiques sont créées dans l'organisation {{site.data.keyword.Bluemix_notm}} qui contient {{site.data.keyword.DRA_short}}. Toutes les applications qui se trouvent dans la même organisation peuvent utiliser la politique.  

Pour définir une politique :

1. Dans la navigation de gauche, cliquez sur **Paramètres**.

2. Cliquez sur **Politique**.

3. Cliquez sur **Créer une politique**, puis indiquez un nom et une description pour la nouvelle politique.

4. Cliquez sur **Suivant**.

4. Ajoutez au moins une règle à la politique :
  1. Cliquez sur **Ajouter une règle à la politique**.
  2. Sélectionnez le type de règle.
  3. Entrez les détails et les conditions de la règle.
  4. Cliquez sur **Sauvegarder**.

5. Lorsque vous avez terminé l'ajout de règles à la politique, cliquez sur **Terminer**.

## Création de règles
{: #criteria}

Les règles définissent les critères utilisés par vos politiques pour juger du succès ou de l'échec. Vous pouvez créer une politique "Test d'unité et couverture de test" qui contient une règle de test d'unité qui requiert 80 % de réussite au test d'unité et une règle de couverture de test qui requiert 100 % de couverture du code. Si vous ajoutez un jalon qui se réfère à cette règle dans un pipeline, le jalon empêche les générations qui ne satisfont pas les deux règles. 

Vous pouvez exiger la réussite inconditionnelle en marquant les tests comme critiques. Pour créer une règle, sélectionnez une politique, puis cliquez sur **Ajouter une règle à la politique**. 

### Création de règles de test de vérification fonctionnelle
{: #criteria_fvt}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de scénarios de test à réussir pour que la vérification aboutisse.

3. Définissez les scénarios de test critiques.

4. Pour surveiller les régressions de scénario de test, cochez la case **Contrôle pour la régression de scénario de test**.

5. Cliquez sur **Sauvegarder**.


### Création des règles de test d'unité
{: #criteria_ut}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de scénarios de test à réussir pour que la vérification aboutisse.

3. Définissez les scénarios de test critiques.

4. Pour surveiller les régressions de scénario de test, cochez la case **Contrôle pour la régression de scénario de test**.

5. Cliquez sur **Sauvegarder**.


### Création de règles de couverture de code
{: #criteria_codecoverage}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de couverture de code nécessaire pour que la vérification aboutisse.

3. Pour surveiller les régressions de couverture de code, cochez la case **Contrôle pour la régression de scénario de test**.

4. Cliquez sur **Sauvegarder**.

### Création de règles d'examen de sécurité statique
{: #criteria_static}

1. Entrez une description.

2. Indiquez le nombre maximal de problèmes de gravité élevée, moyenne et faible autorisés par la règle. 

3. Cliquez sur **Sauvegarder**.

### Création de règles d'examen de sécurité dynamique
{: #criteria_dynamic}

1. Entrez une description.

2. Indiquez le nombre maximal de problèmes de gravité élevée, moyenne et faible autorisés par la règle. 

3. Cliquez sur **Sauvegarder**.

## Outils et formats des résultats de test

{{site.data.keyword.DRA_short}} prend en charge les types d'indicateur et de format suivants :

* Test de vérification fonctionnelle (Mocha, xUnit)
* Test d'unité (Mocha, xUnit, Karma/Mocha)
* Couverture de code (Istanbul comme format de rapport récapitulatif JSON, Blanket.js)

{{site.data.keyword.DRA_short}} prend également en charge les tests Selenium et Jasmine. Ces tests doivent être inclus dans les outils officiellement pris en charge, tels que xUnit et Mocha. Pour en savoir plus sur l'utilisation conjointe de {{site.data.keyword.deliverypipeline}}, de {{site.data.keyword.DRA_short}} et de Selenium, voir [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Pour les éléments qui disposent de scénarios de test, vous pouvez définir des scénarios de test critiques, c'est-à-dire des tests à réussir indépendamment du pourcentage acceptable. Les noms de test critique doivent correspondre à l'attribut `full title` du scénario de test.    
* Pour les tests Karma/Mocha, les chaînes de description `describe()` et `it()` sont liées ensemble par des espaces.
* Pour les tests xUnit, le nom de package, le nom de classe et le nom de fonction sont liés ensemble par des espaces. Ce cas de figure est illustré par l'exemple suivant : 
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  Cet exemple produit les noms de scénario de test suivants :
```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

Vous pouvez utiliser Sauce Labs avec {{site.data.keyword.DRA_short}} en ajoutant l'intégration d'outil Sauce Labs à votre pipeline. Ensuite, incorporez les variables d'environnement `SAUCE_USERNAME` et `SAUCE_ACCESS_KEY` aux tests Selenium en tant que données d'identification.

Après une exécution, vous pouvez voir les titres complets de tous les tests dans les journaux.  

**Remarques :**
* {{site.data.keyword.DRA_short}} ne prend pas en charge les tests critiques dont le titre complet contient un trait d'union.    
* Si vous modifiez le nom de votre organisation, vous devez recréer les politiques associées au nom précédent. Vous perdrez l'accès à tous les rapports de décision générés avant le changement de nom.

## Affichage de rapports de décision    
{: #DI_decision_reports}

Après l'exécution d'un pipeline, {{site.data.keyword.DRA_short}} commence à collecter et à analyser les résultats de test correspondants pour établir une base de référence. Les données de chaque exécution ultérieure sont collectées et comparées aux résultats précédents. Des jalons de décision utilisent ces données pour déterminer le moment auquel un déploiement doit être arrêté. 

Pour afficher le rapport de décision pour un jalon du pipeline, procédez comme suit :

   1. A l'étape qui contient le jalon à vérifier, cliquez sur **Afficher les journaux et l'historique**.

   2. Dans le travail qui contient le jalon, cliquez sur le nom du jalon. 

   3. Dans la vue du journal, recherchez le message `Check {{site.data.keyword.DRA_short}} report here` et cliquez sur le lien pour ouvrir le rapport.
