---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Developer Insights (Expérimental)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} Developer Insights fournit une méthode globale permettant d'explorer les risques de développement de votre projet. Vous pouvez identifier les fichiers présentant une prédisposition élevée aux erreurs et obtenir une vue de conformité du projet par rapport aux pratiques DevOps. {:shortdesc}

Après avoir ouvert {{site.data.keyword.DRA_short}} à partir de votre chaîne d'outils, cliquez sur **Developer Insights**. A partir de là, vous pouvez sélectionner une catégorie d'analyse pour explorer davantage le codebase de votre projet. Les indications fournies par chaque ensemble de données peuvent varier d'une équipe à l'autre, et vous pouvez examiner de manière plus poussée chaque visualisation afin d'obtenir de l'aide et des conseils. 

## Catégories de données
Les données employées par {{site.data.keyword.DRA_short}} pour remplir ses tableaux de bord sont explorées automatiquement à partir du référentiel de contrôle des sources de votre équipe. Pour obtenir plus d'informations sur la signification des données et sur la manière dont vous pouvez les appliquer dans votre projet, cliquez sur **Information** ou **Conseils** dans n'importe quel graphique.

### Meilleures pratiques du développeur

Developer Insights fournit de nombreux graphiques mesurant l'état de votre projet par rapport aux bonnes pratiques DevOps et du développeur. Utilisez cette catégorie pour obtenir une vue de niveau supérieur quant à la maturité, la santé et l'efficience de votre projet.  

### Prédisposition aux erreurs

La *prédisposition aux erreurs* est la probabilité qu'un fichier ou une validation génère des défauts en fonction de tendances historiques, de l'expérience du valideur, de la fréquence des changements, de la pondération des changements et d'autres facteurs. 

Vous pouvez rechercher cette catégorie lors d'une révision du code ou lors de l'amélioration du processus de révision du code. Les fichiers à risque méritent davantage de vigilance que les fichiers relativement sûrs. A l'inverse, les validations et les fichiers sûrs peuvent servir d'exemples à votre équipe dans le cadre de l'amélioration de votre mode de travail. 

### Problèmes

La catégorie des problèmes affiche tous les problèmes faisant l'objet d'un suivi de la part de votre équipe à un endroit. Les problèmes sont automatiquement groupés, dans la durée, par type, par priorité et par étiquette.  

La signification de ces regroupements de problèmes peut varier d'une équipe à une autre. Une équipe peut souhaiter savoir si la plupart des éléments étiquetés pour une édition particulière sont fermés, tandis qu'une autre peut ne pas étiqueter les éditions et travailler à la place en fonction des priorités des problèmes ouverts.   

### Validations

Les validations indiquent le travail fourni par les membres de votre équipe dans le cadre de la contribution au codebase. Examinez vos données de validation pour identifier les points sur lesquels l'effort se concentre dans le temps et comprendre comment vous pouvez mieux équilibrer les charges de travail des membres de votre équipe. 

### Fichiers

Cette catégorie indique les fichiers les plus actifs de votre projet. Qu'il s'agisse du nombre de changements de ligne, de validations, d'auteurs ou de défauts, ces données indiquent l'endroit où votre équipe est la plus active.  

Il convient généralement d'essayer de réduire le nombre de contacts qui modifient un fichier, ainsi que la fréquence de changement de ce fichier. Cet objectif peut s'avérer impossible avec certains fichiers, comme les fichiers de configuration communs. Toutefois, le fait que de nombreux développeurs effectuent simultanément de nombreux changements dans le même fichier peut constituer une véritable source de problèmes.  

**Remarque** : DevOps Insights ignore les fichiers dotés des extensions suivantes :

* .bin
* .cdr
* .jpeg
* .jpg
* .json
* .markdown
* .md
* .png
* .pyc
* .svg
* .text
* .yaml
* .yml

