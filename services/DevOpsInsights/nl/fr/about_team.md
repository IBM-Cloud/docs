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

# A propos de Team Dynamics

{{site.data.keyword.DRA_full}} Team Dynamics utilise l'analyse du codage social pour identifier le niveau d'interaction entre les membres d'équipe, ce qui permet à l'équipe de mettre un terme à certaines pratiques non productives. 
{:shortdesc}

Après avoir ouvert {{site.data.keyword.DRA_short}} à partir de votre chaîne d'outils, cliquez sur **Team Dynamics**. A partir de là, vous pouvez sélectionner une catégorie d'analyse pour explorer davantage les habitudes et les pratiques de collaboration de votre équipe. Les indications fournies par chaque ensemble de données peuvent varier d'une équipe à l'autre, et vous pouvez examiner de manière plus poussée chaque visualisation afin d'obtenir de l'aide et des conseils.  

## Catégories de données

Les données employées par {{site.data.keyword.DRA_short}} pour remplir ses tableaux de bord sont explorées automatiquement à partir du référentiel de contrôle des sources de votre équipe. Pour obtenir plus d'informations sur la signification des données et sur la manière dont vous pouvez les appliquer dans votre projet, cliquez sur **Information** ou **Conseils** dans n'importe quel graphique.

### Codage social

Le graphique Codage social représente les connexions entre les contributeurs de votre projet de manière visuelle et hautement interactive. Chaque noeud du graphique représente un développeur. La taille d'un noeud est mise à l'échelle de manière logarithmique en fonction des contributions d'un développeur à un projet. Les lignes entre les noeuds indiquent la collaboration ; plus une ligne est épaisse, plus la collaboration entre les développeurs a été intense sur la période sélectionnée. 

Chaque noeud est coloré en bleu et rouge à différents degrés. Le bleu indique le nombre de lignes de code ajoutées par un contributeur en tant que portion du nombre total de lignes modifiées par le contributeur. Le rouge indique le nombre de lignes de code retirées par un contributeur. Un contributeur qui a uniquement ajouté du code serait entièrement bleu, tandis qu'un contributeur ayant ajouté et retiré un nombre égal de lignes serait à moitié bleu et à moitié rouge. 

### Auteurs

La catégorie des auteurs fournit le même nombre de validations, de changements de ligne et de changements de fichier par contributeur du référentiel. Même si le nombre total de lignes codées ne doit pas être utilisé pour déterminer la contribution nette d'un membre d'équipe, cette information peut s'avérer utile pour les chefs d'équipe et les responsables. Un membre d'équipe qui contribue à un nombre excessifs de changements de ligne peut indiquer une surcharge de travail, représenter un goulot d'étranglement dans votre processus ou être significatif d'un style de codage plus prolixe comparé à d'autres membres d'équipe. 
