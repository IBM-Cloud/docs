---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Détails de l'application
{: #manageapps}

Le tableau de bord Applications de la console {{site.data.keyword.Bluemix}} fournit des informations récapitulatives sur les applications que vous avez créées. Ces informations récapitulatives incluent le nom, l'icône, l'URL, le contexte d'exécution, le statut d'exécution, ainsi que les instances de service liées à l'application.
{:shortdesc}

Depuis le tableau de bord Applications, vous pouvez afficher le statut de chaque application. 

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

Pour afficher plus d'informations sur une application, cliquez sur son nom afin d'ouvrir la page Vue d'ensemble de l'application.

Lorsqu'une application est déployée, vous pouvez démarrer, arrêter, redémarrer
ou (dans le cas des applications Web) modifier le nombre d'instances et la quantité de mémoire utilisés par l'application. Actuellement, dans le cas des applications
Web, {{site.data.keyword.Bluemix_notm}} n'ajuste pas automatiquement votre application en fonction de sa charge, et vous
devez donc gérer cet aspect vous-même.

Les applications peuvent être redéployées si une mise à jour est effectuée. Le mécanisme de mise à jour de l'application est identique au mécanisme utilisé pour déployer initialement l'application. {{site.data.keyword.Bluemix_notm}}
arrête toutes les instances en cours d'exécution et les remplace automatiquement par de nouvelles instances.
