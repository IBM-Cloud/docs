---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# A propos de 
{: #about}

Vous pouvez vous servir de {{site.data.keyword.bplong}} pour créer des blocs de construction d'infrastructure. Vous pouvez regrouper des services de cloud {{site.data.keyword.IBM_notm}} pour créer une infrastructure pouvant être déployée et réutilisée.
{:shortdesc}

{{site.data.keyword.bpshort}} utilise Terraform pour simplifier la gestion de l'infrastructure. Par exemple, si vous voulez créer plusieurs copies de votre service, qui utilise un cluster de serveurs d'applications, un équilibreur de charge et un serveur de base de données, vous pouvez écrire un script bash afin d'exécuter des commandes d'utilisation de ces composants. Cependant, il est plus facile, plus rapide et plus méthodique d'utiliser une configuration comportant un module d'exécution qui transforme la configuration en ressources réelles. Avec Terraform, vous pouvez créer de nombreuses ressources simultanément, sous forme de groupe, dans lequel sont établies des dépendances.  

## Raisons d'utiliser {{site.data.keyword.bpshort}}
{: #reasons}

Vous pouvez choisir d'utiliser une infrastructure codifiée dans les scénarios suivants :
{:shortdesc}

| Scénario     | Raisons    |
| :------------- | :------------- |
| Vous voulez recréer et réutiliser votre infrastructure.  | Vous pouvez utiliser {{site.data.keyword.bpshort}} pour gérer l'infrastructure. Avec {{site.data.keyword.bpshort}}, vous pouvez mettre à disposition, modifier et détruire vos ressources à l'aide d'un programme. Lorsque vous codifiez et configurez des ressources, vous pouvez composer une bibliothèque de ressources pouvant être réutilisées indéfiniment afin d'obtenir les mêmes résultats. |
| Vous voulez assurer la transparence concernant la configuration de vos environnements.  | {{site.data.keyword.bpshort}} utilise des configurations du contrôle des sources, ce qui permet la collaboration et la révision et fournit une trace d'audit indiquant comment et quand les modifications ont été apportées. Vous pouvez également visualiser vos modifications s'il est nécessaire de revenir à une configuration précédente.  |
| Vous voulez simplifier l'exécution des modifications environnementales.  | {{site.data.keyword.bpshort}} respecte le modèle déclaratif qui fournit une source unique de données de référence. Lorsque vous planifiez une modification de votre environnement, vous énoncez le résultat souhaité.  |
| Vous utilisez déjà un outil de gestion des configurations mais voulez automatiser davantage la configuration de vos environnements.  | {{site.data.keyword.bpshort}} peut fonctionner avec des outils de gestion des configurations. Les environnements qui sont déployés avec {{site.data.keyword.bpshort}} sont des abstractions de haut niveau pouvant créer des ressources d'infrastructure. Ensuite, vous pouvez utiliser des outils de gestion des configurations pour installer et configurer des logiciels sur les ressources mises à disposition par {{site.data.keyword.bpshort}}.   
  
## Fonctionnement
{: #how}

Vous pouvez déployer des ressources dans vos environnements à l'aide de {{site.data.keyword.bpshort}}.
{:shortdesc}

{{site.data.keyword.bpshort}} utilise Terraform comme outil sous-jacent pour présenter l'infrastructure en tant que code de sorte que vous puissiez définir des ressources de cloud {{site.data.keyword.IBM}} sous forme de code. Les ressources de cloud peuvent constituer différents composants de votre infrastructure, comme des serveurs Bare Metal, des serveurs virtuels, des équilibreurs de charge ou des composants de réseau définis par le logiciel.  

### Configurations pour la définition de ressources
{: #how-define}

Une configuration, ou configuration Terraform, est un fichier qui définit les ressources composant votre infrastructure. Il s'agit d'une architecture pouvant être déployée et qui peut être appliquée à un ou plusieurs environnements. Le diagramme ci-après illustre les composants d'une configuration et la façon dont les éléments sont combinés pour créer un environnement déployable dans {{site.data.keyword.bpshort}}.


![Diagramme de l'architecture {{site.data.keyword.bpshort}}](/images/anatomy_of_a_schematic.png)

Figure 1. Diagramme de l'architecture {{site.data.keyword.bpshort}}

### Contrôle des sources pour l'activation de la collaboration 
{: #how-collaborate}

Les configurations sont stockées dans GitHub pour que les équipes puissent réviser le code et collaborer. Avec GitHub, vous disposez d'une trace d'audit intégrée et pouvez afficher l'historique de validation complet des modifications qui ont été apportées à vos configurations. Vous pouvez sauvegarder les informations d'utilisation dans des fichiers Readme pour que la configuration puisse être partagée et utilisée par plusieurs équipes. 

### Environnements {{site.data.keyword.bpshort}} pour la mise à disposition de ressources 
{: #how-provision}

Vous pouvez utiliser {{site.data.keyword.bpshort}} pour analyser votre code dans GitHub et déployer des ressources dans un environnement. Les environnements peuvent partager des configurations communes. Par exemple, vous pouvez créer un environnement d'assurance qualité temporaire qui ressemble à un environnement de production et le supprimer lorsque vos tests sont terminés. Vous pouvez générer une bibliothèque de configurations d'environnement communes que les utilisateurs sur votre compte {{site.data.keyword.Bluemix_notm}} peuvent étiqueter et rechercher. 
