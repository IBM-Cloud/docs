---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Maintenance et mises à jour
{: #maintupdates_mf}

{{site.data.keyword.mobilefoundation_short}} fournit un serveur {{site.data.keyword.mfserver_short_notm}}<!-- on {{site.data.keyword.containerlong}} as a container group-->. Les mises à jour du serveur {{site.data.keyword.mobilefoundation_short}} sont notifiées aux utilisateurs. Vous pouvez choisir de mettre à jour le serveur {{site.data.keyword.mobilefoundation_short}} quand cela vous arrange.
{:shortdesc}

## Stratégie de maintenance
{: #maintupdate_strategy_mf}

Quand {{site.data.keyword.mobilefoundation_short}} est mis à jour, l'utilisateur est averti de la disponibilité de cette mise à jour.  Une notification apparaît dans le tableau de bord de l'instance de service. L'utilisateur peut choisir d'appliquer la mise à jour dans {{site.data.keyword.mobilefoundation_short}} lors d'une fenêtre de maintenance dont il décide de la date d'exécution.

La mise à jour du service {{site.data.keyword.mobilefoundation_short}} sera mise à disposition quand l'un des composants suivants est mis à jour.

* {{site.data.keyword.mfserver_short_notm}}.
* Version Liberty sous-jacente
* Version Java Developer Kit sous-jacente


## Application des mises à jour
{: #apply_update_mf}

La mise à jour dans {{site.data.keyword.mobilefoundation_short}} peut être appliquée en cliquant sur la commande de recréation.

Lors de l'application de la mise à jour, la version du serveur, comme affichée dans {{site.data.keyword.mfp_oc_short_notm}}, sera modifiée pour indiquer la version de mise à jour du serveur.

### Remarque :
{: #note notoc}

* Les utilisateurs ne seront pas en mesure d'appliquer leurs propres correctifs et mises à jour à leur instance de service {{site.data.keyword.mobilefoundation_short}}.
* Voir les rubriques relatives à la [recréation du serveur dans le plan Developer](c_using_mfs_p1.html#recreate_mobilefoundation_p1) et la [recréation du serveur dans le plan Professional 1 Application](c_using_mfs_p2.html#recreate_mobilefoundation_p2) pour comprendre la différence de comportement entre les plans lorsque vous cliquez sur la commande de recréation.
