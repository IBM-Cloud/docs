---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Foire aux questions {: #faq}

Cette foire aux questions fournit des réponses aux questions courantes sur le service {{site.data.keyword.objectstorageshort}}.
{: shortdesc}


## Quels comptes et plans de paiement puis-je utiliser pour {{site.data.keyword.objectstorageshort}} ? {: #account-payment}

Le service {{site.data.keyword.objectstorageshort}} offre deux options de plan, Gratuit et Standard. La [tarification](https://www.ibm.com/cloud-computing/bluemix/pricing/) est fonction du plan choisi.

<table>
<caption> Tableau 1. Comparaison du plan gratuit et du plan standard </caption>
  <tr>
    <th> Plan gratuit </th>
    <th> Plan standard </th>
  </tr>
  <tr>
    <td> N'autorise l'existence que d'une seule instance de service à la fois dans une organisation {{site.data.keyword.Bluemix_notm}} </td>
    <td> Nombre illimité d'instances de service </td>
  </tr>
  <tr>
    <td> Disponible pour tout le monde </td>
    <td> Disponible uniquement pour les comptes {{site.data.keyword.Bluemix_notm}} payants et les utilisateurs IBM internes </td>
  </tr>
  <tr>
    <td> Gratuit </td>
    <td> Paiement à la carte ou sur abonnement </td>
  </tr>
  <tr>
    <td> Inclut une limite d'utilisation de stockage préalable de 5 Go </td>
    <td> Stockage illimité </td>
  </tr>
</table>

**Attention** : les utilisateurs d'un compte d'essai {{site.data.keyword.Bluemix_notm}} peuvent se servir du plan gratuit. Une fois expiré la période d'essai, l'instance de service {{site.data.keyword.objectstorageshort}} associée est désactivée, ce qui signifie qu'il n'est plus possible d'accéder au compte de stockage. Après 30 jours, votre compte {{site.data.keyword.Bluemix_notm}} est purgé et toutes les données sont supprimées. Pour éviter de perdre des données, procédez à une mise à niveau vers un [compte {{site.data.keyword.Bluemix_notm}} payant ](/docs/admin/account.html) dès que possible.

## Comment changer de plan ? {: #changeplan}  
Les instances qui ont été créées avec le plan Bêta ou gratuit peuvent être mises à niveau vers le plan Standard. L'organisation associée doit être un
compte payant {{site.data.keyword.Bluemix_notm}}. Les comptes d'essai avec instances Object Storage ne peuvent pas
être mis à niveau vers le plan Standard, et les instances du plan Standard ne peuvent pas être rétrogradées vers d'autres plans. Lorsque vous procédez à la
mise à niveau, votre instance de service et vos données client sont transférées vers le nouveau plan.

Pour effectuer une mise à niveau :
1.	Dans l'interface utilisateur {{site.data.keyword.objectstorageshort}}, cliquez sur **Plan**.
2.	Sélectionnez **Standard** en tant que nouveau plan puis cliquez sur **Sauvegarder**.

Vous pouvez aussi [changer votre plan de paiement](/docs/pricing/index.html#changing) en utilisant l'interface de ligne de commande.

## Comment serais-je facturé pour mon utilisation d'{{site.data.keyword.objectstorageshort}} ? {: #charge-bill}

Le service {{site.data.keyword.objectstorageshort}} ne vous facture que pour ce que vous utilisez.  Aucun engagement ou frais n'est demandé pour commencer à utiliser le service. Vous n'êtes pas facturé pour les demandes d'API ou le trafic réseau lié aux données entrantes.

{{site.data.keyword.objectstorageshort}} est facturé en fonction de l'utilisation que vous faites du stockage au
cours du cycle de facturation. Toutes les données objet incluses dans des conteneurs créés au sein de votre organisation {{site.data.keyword.Bluemix_notm}} sont incluses.

Les frais pour le transfert de données sortantes s'appliquent dès lors que des données sont lues depuis l'un de vos conteneurs d'objets sur le réseau public. Toute la bande passante qui est consommée dans le cycle de facturation est facturée en tant que bande passante sortante publique.

A la fin du cycle de facturation, {{site.data.keyword.Bluemix_notm}} vous facture automatiquement l'utilisation du service pour cette période de facturation. Vous pouvez afficher vos frais pour la période de facturation en cours via la génération de rapports {{site.data.keyword.Bluemix_notm}}.

## Est-ce que ma région {{site.data.keyword.Bluemix_notm}} et ma région de stockage sont identiques ? {: #region}

Le service {{site.data.keyword.objectstorageshort}} prend en charge les régions de stockage Dallas et Londres. Ces régions de stockage sont indépendantes de la région {{site.data.keyword.Bluemix_notm}} (Sud des Etats-Unis ou Royaume-Uni, par exemple) dans laquelle l'instance de service {{site.data.keyword.objectstorageshort}} est créée. Si vous créez une instance dans la région {{site.data.keyword.Bluemix_notm}} Sud des Etats-Unis, vous pouvez lire et écrire des données dans l'une des deux régions de stockage, Dallas ou Londres. La valeur par défaut de la région de stockage repose sur votre région {{site.data.keyword.Bluemix_notm}}. Vous pouvez changer de région en choisissant une autre région dans la liste déroulante de l'interface utilisateur.
