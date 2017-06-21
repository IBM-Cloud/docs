---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Création de politiques et de règles
{: #policies_and_rules}

Les politiques sont des ensembles de règles qui contrôlent les jalons de votre pipeline de distribution. Si votre code ne satisfait pas, dans un sens ou dans l'autre, une politique appliquée à un jalon particulier, le déploiement est arrêté dans le but d'empêcher la publication de changements risqués.

Vous définissez les politiques dans {{site.data.keyword.DRA_short}}. Les politiques sont créées dans l'organisation {{site.data.keyword.Bluemix_notm}} qui contient {{site.data.keyword.DRA_short}}. Toutes les applications qui se trouvent dans la même organisation peuvent utiliser la politique. 

## Création de politiques
{: #create_policies}

Pour créer une politique :

1. Dans le menu de navigation de {{site.data.keyword.DRA_short}}, cliquez sur **Paramètres**.

2. Cliquez sur **Politiques**.

3. Cliquez sur **Créer une politique**, puis indiquez un nom et une description pour la nouvelle politique.

4. Cliquez sur **Suivant**.

4. Ajoutez au moins une règle à la politique :
  1. Cliquez sur **Ajouter une règle à la politique**.
  2. Sélectionnez le type de règle.
  3. Entrez les détails et les conditions de la règle.
  4. Cliquez sur **Sauvegarder**.

5. Lorsque vous avez terminé l'ajout de règles à la politique, cliquez sur **Terminer**.

## Création de règles
{: #creating_rules}

Les règles définissent les critères utilisés par vos politiques pour juger du succès ou de l'échec. Vous pouvez créer une politique "Test d'unité et couverture de test" qui contient une règle de test d'unité qui requiert 80 % de réussite au test d'unité et une règle de couverture de test qui requiert 100 % de couverture du code. Si vous ajoutez un jalon qui se réfère à cette règle dans un pipeline, le jalon empêche les générations qui ne satisfont pas les deux règles. 

Vous pouvez exiger la réussite inconditionnelle en marquant les tests comme critiques. Pour créer une règle, sélectionnez une politique, puis cliquez sur **Ajouter une règle à la politique**. 

### Création de règles de test de vérification fonctionnelle
{: #criteria_fvt}

1. Entrez une description et sélectionnez un format.

2. Indiquez le pourcentage de scénarios de test à réussir pour que la vérification aboutisse.

3. Définissez les scénarios de test critiques.

4. Pour surveiller les régressions de scénario de test, cochez la case **Contrôle pour la régression de scénario de test**.

5. Cliquez sur **Sauvegarder**.


### Création de règles de test d'unité
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

Vous pouvez intégrer {{site.data.keyword.DRA_short}} à IBM Application Security on Cloud pour exécuter des examens de code statique et d'application dynamique. Pour plus d'informations sur Application Security on Cloud,voir la [documentation officielle](/docs/services/ApplicationSecurityonCloud/index.html).

1. Entrez une description.

2. Indiquez le nombre maximal de problèmes de gravité élevée, moyenne et faible autorisés par la règle. 

3. Cliquez sur **Sauvegarder**.

### Création de règles d'examen de sécurité dynamique
{: #criteria_dynamic}

Vous pouvez intégrer {{site.data.keyword.DRA_short}} à {{site.data.keyword.appseccloudfull}} pour exécuter des examens d'application dynamiques. Pour plus d'informations sur Application Security on Cloud,voir la [documentation officielle](/docs/services/ApplicationSecurityonCloud/index.html).

1. Entrez une description.

2. Indiquez le nombre maximal de problèmes de gravité élevée, moyenne et faible autorisés par la règle. 

3. Cliquez sur **Sauvegarder**.
