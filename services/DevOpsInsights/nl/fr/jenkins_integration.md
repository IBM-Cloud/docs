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

# Intégration de {{site.data.keyword.DRA_short}} à Jenkins
{: #toolchain_configure_jenkins}

Une fois que vous avez défini les stratégies que {{site.data.keyword.DRA_full}} doit surveiller, l'étape suivante consiste à ajouter {{site.data.keyword.DRA_short}} à une chaîne d'outils, puis de configurer un pipeline de distribution continue.
{:shortdesc}

<!--##Configuring a Jenkins project-->

Vous pouvez intégrer {{site.data.keyword.DRA_short}} dans un projet Jenkins ou dans plusieurs projets Jenkins connexes. Cette intégration vous permet de définir des seuils de qualité et de recevoir des données sur la qualité de génération dans le tableau de bord {{site.data.keyword.DRA_short}}.

## Prérequis    
{: #DI_jenkins_prereqs}

* Vous devez avoir accès à un projet Jenkins local ou au serveur qui exécute un projet Jenkins.

## Installation du plug-in {{site.data.keyword.DRA_short}}
{: #DI_jenkins_install}

Pour installer le plug-in {{site.data.keyword.DRA_short}} dans votre projet Jenkins, procédez comme suit :

  1. [Téléchargez le fichier d'installation du plug-in IBM DevOps Insight (.hpi)](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi) à partir du référentiel GitHub du plug-in.
  2. Dans votre installation Jenkins, cliquez sur **Manage Jenkins**, sélectionnez **Manage Plugins**, puis cliquez sur l'onglet **Advanced**.
  3. Cliquez sur **Choose File** et sélectionnez le fichier d'installation du plug-in DevOps Insight.
  4. Cliquez sur **Upload**.
  5. Redémarrez Jenkins et vérifiez que le plug-in a été installé.

## Intégration de {{site.data.keyword.DRA_short}} à Jenkins    
{: #DI_jenkins_integrate}

Une fois que vous avez installé le plug-in mais avant d'intégrer {{site.data.keyword.DRA_short}} à votre installation Jenkins, accédez au [centre de contrôle](https://control-center.stage1.ng.bluemix.net/) et créez au moins une stratégie.

Pour chaque travail que vous possédez déjà et dans lequel vous voulez utiliser {{site.data.keyword.DRA_short}} :

1. Ajoutez une action post-génération de type **Publish build information to {{site.data.keyword.DRA_short}}**, **Publish deployment information to {{site.data.keyword.DRA_short}}** ou **Publish test result to {{site.data.keyword.DRA_short}}**. Ce type doit correspondre au type de travail (génération, déploiement ou test). Renseignez les zones requises.
  * Dans la zone Credential, sélectionnez votre ID Bluemix et votre mot de passe. Si ces données ne sont pas sauvegardées dans Jenkins, cliquez sur le bouton **Add** et sauvegardez-les.
  * Dans la zone Build Job Name, indiquez le nom de travail de génération défini dans Jenkins. Si la génération s'effectue en même temps que le travail de test, laissez cette zone vide. Si le travail de génération s'effectue hors de Jenkins, cochez la case **Builds are being done outside of Jenkins**, puis indiquez le numéro de version et l'URL de génération.
  * Renseignez la zone Result File Location. Si le test ne génère aucun fichier de résultats, laissez cette zone vide. Le plug-in va télécharger un fichier de résultats par défaut en fonction du statut du travail de test en cours.
3. *Facultatif* : si vous souhaitez que les points de contrôle de stratégie DRA du travail de test contrôlent le travail de déploiement en aval, ajoutez une autre action de post-génération de type **DevOps Risk Analytics Gate** et renseignez les zones requises. Le point de contrôle va empêcher l'exécution du travail en aval si le travail de test ne satisfait pas aux stratégies associées.
4. Cliquez sur **Apply**, puis sur **Save**.

A partir de la page de projet, vous pouvez cliquer sur **Build Now** pour exécuter le projet.

Après l'exécution de la génération, accédez au [centre de contrôle](https://control-center.stage1.ng.bluemix.net/) pour vérifier le statut de génération dans le tableau de bord. Si vous avez configuré des points de contrôle de stratégie, vous pouvez également voir les résultats {{site.data.keyword.DRA_short}} sur la page de statut de la génération en cours.
