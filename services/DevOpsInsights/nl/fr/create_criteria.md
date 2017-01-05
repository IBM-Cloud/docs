---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Définition de stratégies
{: #criteria}

Avec {{site.data.keyword.DRA_short}}, vous pouvez facilement définir des stratégies pour votre application. Pour commencer, procédez comme suit :
{:shortdesc}

1. Dans le menu latéral, cliquez sur **Policy**.

2. Cliquez sur **Create Policy (+)**, puis entrez un nom et une description pour la nouvelle stratégie.

3. Cliquez sur **Suivant**.

4. Ajoutez au moins une règle à la stratégie :
  1. Cliquez sur **Create Rule (+)**.
  2. Sélectionnez le type de règle.
  3. Entrez les détails et les conditions de la règle.
  4. Cliquez sur **Save**.

5. Lorsque vous avez terminé l'ajout de règles à la stratégie, cliquez sur **Complete**.

Les stratégies sont créées dans l'organisation {{site.data.keyword.Bluemix_notm}} à laquelle {{site.data.keyword.DRA_short}} a été ajouté. Toutes les applications qui font partie de la même organisation peuvent utiliser la stratégie.

{{site.data.keyword.DRA_short}} prend en charge les types d'indicateurs et les formats suivants :

* Test de vérification fonctionnelle (Mocha, JUnit)
* Test unitaire (Mocha, JUnit, Karma/Mocha)
* Couverture de code (Istanbul comme format de rapport récapitulatif JSON, Blanket.js)

{{site.data.keyword.DRA_short}} prend également en charge les tests Selenium et Jasmine. Ces tests doivent être inclus dans les outils officiellement pris en charge tels que JUnit, xUnit et Mocha. Pour en savoir plus sur l'utilisation conjointe de {{site.data.keyword.deliverypipeline}}, de {{site.data.keyword.DRA_short}} et de Selenium, voir [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Pour les éléments qui disposent de scénarios de test, vous pouvez définir des scénarios de test critiques, c'est-à-dire des tests à réussir
indépendamment du pourcentage acceptable. Les noms de scénario de test critique doivent correspondre à l'attribut `full title` du scénario de test :    
* Pour les tests Karma/Mocha, les chaînes de description `describe()` et `it()` sont liées par des espaces
* Pour les tests JUnit, le nom de package, le nom de classe et le nom de fonction sont liés par des espaces    

Vous pouvez utiliser Sauce Labs avec {{site.data.keyword.DRA_short}} en ajoutant l'intégration de Sauce Labs à votre pipeline. Ensuite, incorporez les variables
d'environnement `SAUCE_USERNAME` et `SAUCE_ACCESS_KEY` aux tests Selenium en tant que données d'identification.

Après une exécution, vous pouvez voir les titres complets de tous les tests dans les journaux.  

Remarques :
* {{site.data.keyword.DRA_short}} ne prend pas en charge les tests critiques dont le titre complet contient un trait d'union.    
* Si vous modifiez le nom de votre organisation, vous devez recréer les stratégies associées au nom précédent. Vous perdrez l'accès aux
rapports de décision générés avant le changement de nom.

## Création de règles de test de vérification fonctionnelle
{: #criteria_fvt}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de scénarios de test à réussir pour que la vérification aboutisse.

3. Définissez les scénarios de test critiques.

4. Pour surveiller les régressions de scénario de test, cochez la case **Monitor for test case regression**.

5. Cliquez sur **Save**.


## Création de règles de test unitaire
{: #criteria_ut}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de scénarios de test à réussir pour que la vérification aboutisse.

3. Définissez les scénarios de test critiques.

4. Pour surveiller les régressions de scénario de test, cochez la case **Monitor for test case regression**.

5. Cliquez sur **Save**.


## Création de règles de couverture de code
{: #criteria_codecoverage}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de couverture de code nécessaire pour que la vérification aboutisse.

3. Pour surveiller les régressions de couverture de code, cochez la case **Monitor for test case regression**.

4. Cliquez sur **Save**.
