---

Copyright :
  Années : 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Initiation à {{site.data.keyword.graphfull}}
{: #gettingstartedtemplate}
Dernière mise à jour : 27 Juillet 2016
{: .last-updated}

{{site.data.keyword.graphfull}} est un service de base de données graphique entièrement géré, accessible via une interface d'API HTTP basée sur REST.
Utilisez-le pour générer vos applications Web et mobiles qui requièrent des fonctions de base de données graphique.
{:shortdesc}

{{site.data.keyword.graphfull}} est basé sur la pile [Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade;, pour générer des applications graphiques à performances élevées utilisant une API compatible v3.
La pile vous offre plus de souplesse et des fonctions basées sur un environnement familier.
A l'aide du tableau de bord {{site.data.keyword.Bluemix}}, vous pouvez facilement intégrer le service {{site.data.keyword.graphfull}} à vos applications {{site.data.keyword.Bluemix_short}}.

Vous pouvez utiliser {{site.data.keyword.graphfull}} de deux manières :

*	A l'aide des commandes d'API simplifiées {{site.data.keyword.graphfull}}
*	A l'aide du langage d'interrogation Apache TinkerPop v3 (Gremlin)

Les fonctions {{site.data.keyword.graphfull}} sont disponibles sous la forme d'une API en utilisant des noeuds finaux HTTP REST.
Ces noeuds finaux permettent à vos applications de se connecter et d'utiliser facilement le service {{site.data.keyword.graphfull}}, en utilisant HTTP pour effectuer des demandes d'API et obtenir des résultats.
Utilisez les fonctions HTTP fournies par votre langage de programmation d'application pour accéder aux noeuds finaux.
Vous pouvez également utiliser une interface de commande ou un script `curl`.
La documentation de référence sur l'API décrit les différentes fonctions fournies par le service {{site.data.keyword.graphfull}} et propose des exemples d'utilisation.


Votre application peut également utiliser le langage d'interrogation Apache TinkerPop, appelé Gremlin, pour les tâches utilisant le service {{site.data.keyword.graphfull}}.
Incluez la demande Gremlin dans un document JSON, puis transmettez le document au noeud final de service `/gremlin`.
Des exemples d'utilisation de Gremlin avec {{site.data.keyword.graphfull}} sont fournis dans la documentation complète.

Procédez comme indiqué ci-dessous pour commencer à utiliser le service {{site.data.keyword.graphfull}} :

1.	[Créez une instance](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance) du service {{site.data.keyword.graphfull}}.
2.	Enregistrez les trois valeurs essentielles générées lors de la création d'une instance. Elles sont disponibles à partir de l'onglet `Données d'identification pour le service` après avoir cliqué sur la vignette du service.
	*	Noeud final IBM Graph : `apiURL`.
	*	Nom d'utilisateur de l'instance du service `username`.
	*	Mot de passe de l'instance du service `password`.
3.	Utilisez ces trois valeurs essentielles dans vos applications ou scripts pour les tâches {{site.data.keyword.graphfull}}. Des exemples sont fournis dans la documentation complète.

# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}

* [Exemples](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## Référence des API
{: #api}

* [API REST pour IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [Utilisation de Gremlin avec IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## Liens connexes
{: #general}

* [Documentation complète](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Dépassement de pile](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
