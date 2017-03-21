---

copyright:
  years: 2015, 2017
lastupdated: "2015-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestion des applications
{: #manageapps}

Vous pouvez utiliser le tableau de bord de l'interface utilisateur {{site.data.keyword.Bluemix}} pour afficher et gérer vos applications
et vos services, ainsi que pour surveiller
l'utilisation des ressources à l'aide des jauges de quotas.
{:shortdesc}

La section des applications du tableau de bord fournit des informations récapitulatives sur les applications que vous avez créées. Ces informations récapitulatives incluent le nom, l'icône, l'URL, le contexte d'exécution et le statut d'exécution de l'application, ainsi
que les instances de service liées à l'application. Des couleurs différentes sont utilisées pour indiquer le statut d'exécution de chaque application.

**Arrêté ou Inconnu (gris)**

  Votre application est arrêtée ou le statut est Inconnu. L'icône grise indique que l'application est arrêtée ou que le statut est inconnu.

**En cours d'exécution (vert)**

  Votre application est en cours d'exécution. L'icône verte indique que l'application est démarrée et que toutes les instances sont en cours d'exécution.

*Nombre* ** en cours d'exécution (jaune)**

  L'application est démarrée mais toutes les instances ne sont pas en cours d'exécution. L'icône jaune indique que moins de 100% des instances sont
en cours d'exécution. Le nombre d'instances en cours d'exécution et le nombre
d'instances ayant échoué sont affichés.

**Pas en cours d'exécution (rouge)**

  Votre application n'est pas en cours d'exécution. L'icône rouge indique que l'application est démarrée mais qu'aucune instance n'est en cours d'exécution.

Le catalogue {{site.data.keyword.Bluemix_notm}} permet de visualiser les services et les modules de démarrage disponibles. Vous pouvez sélectionner un module de démarrage pour créer une application, lier un service et gérer l'application. Une fois qu'un service est lié à une application, vous pouvez gérer les instances de service
existantes qui sont liées à l'application en cours, et créer des instances de service pour l'application. Vous pouvez également annuler la liaison de l'instance de service à l'application,
supprimer l'instance de service de l'application, ou sélectionner un plan de service
différent.

Pour afficher plus d'informations sur une application, cliquez sur sa vignette afin d'ouvrir la page Vue d'ensemble de l'application.

**Remarque :** vous ne pouvez examiner les ressources que d'une seule organisation à la fois. Si vous êtes membre de plusieurs
organisations, vous pouvez passer d'une organisation à une autre en cliquant sur l'icône **Changer l'organisation** en regard de
l'organisation en cours affichée dans l'en-tête du tableau de bord.

Lorsqu'une application est déployée, vous pouvez démarrer, arrêter, redémarrer
ou (dans le cas des applications Web) modifier le nombre d'instances et la quantité de mémoire utilisés par l'application. Actuellement, dans le cas des applications
Web, {{site.data.keyword.Bluemix_notm}} n'ajuste pas automatiquement votre application en fonction de sa charge, et vous
devez donc gérer cet aspect vous-même.

Les applications peuvent être redéployées si une mise à jour est effectuée. Le mécanisme de mise à
jour de l'application est identique au mécanisme utilisé pour déployer initialement l'application. {{site.data.keyword.Bluemix_notm}}
arrête toutes les instances en cours d'exécution et les remplace automatiquement par de nouvelles instances.
