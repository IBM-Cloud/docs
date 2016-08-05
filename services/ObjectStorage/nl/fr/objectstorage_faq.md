{:new_window: target="_blank"}

# Foire aux questions {: #faq} 

*Dernière mise à jour : 18 juillet 2016*
{: .last-updated}


## Comment les tarifs varient selon le plan que vous choisissez ? {: #plan-price}
La tarification est fonction du plan choisi. Pour plus d'informations sur la tarification, voir la [page relative à la tarification IBM Bluemix](https://console.ng.bluemix.net/pricing/){: new_window} ou utilisez la [calculatrice](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window} pour obtenir des estimations plus détaillées.


## Quels comptes et plans de paiement puis-je utiliser pour {{site.data.keyword.objectstorageshort}} ? {: #account-payment}
Le service {{site.data.keyword.objectstorageshort}} est fourni avec plusieurs options de plan différentes. Dans le cadre de notre édition en disponibilité générale, deux plans sont actuellement proposés, Standard et Gratuit. Le plan Standard est disponible uniquement pour les comptes payants {{site.data.keyword.Bluemix_notm}} (sous la forme Paiement à la carte ou Abonnement) ou pour les utilisateurs internes IBM. Le
plan Standard inclut une franchise de stockage de 5 Go par compte. 

Les comptes d'essai qui sont toujours actifs sont en mesure d'utiliser le plan gratuit qui autorise l'existence d'une instance unique dans une organisation {{site.data.keyword.Bluemix_notm}}. Une fois expiré la période d'essai {{site.data.keyword.Bluemix_notm}}, l'instance de service {{site.data.keyword.objectstorageshort}} associée est désactivée, ce qui signifie qu'il n'est plus possible d'accéder au compte de stockage par la ligne de commande ou l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Après une période de grâce de 30 jours, votre compte {{site.data.keyword.Bluemix_notm}} est purgé et toutes les données supprimées. Pour éviter de perdre des données, il est donc conseillé de procéder à une mise à niveau vers un compte payant {{site.data.keyword.Bluemix_notm}} aussi vite que possible. 
Pour mettre à niveau votre compte, cliquez sur le menu de gestion des utilisateurs, puis sélectionnez l'option
**Compte**, qui fournit des instructions sur le processus de mise à niveau.

## Comment changer de plan ? {: #changeplan}  
Les instances qui ont été créées avec le plan Bêta ou gratuit peuvent être mises à niveau vers le plan Standard. L'organisation associée doit être un
compte payant {{site.data.keyword.Bluemix_notm}}. Les comptes d'essai avec instances {{site.data.keyword.objectstorageshort}} ne peuvent pas
être mis à niveau vers le plan Standard, et les instances du plan Standard ne peuvent pas être rétrogradées vers d'autres plans. Lorsque vous procédez à la
mise à niveau, votre instance de service et vos données client sont transférées vers le nouveau plan.


Pour mettre à niveau votre plan : 
1.	Dans l'interface utilisateur {{site.data.keyword.objectstorageshort}}, cliquez sur **Plan**.
2.	Sélectionnez **Standard** en tant que nouveau plan puis cliquez sur **Sauvegarder**.

Vous pouvez aussi changer votre plan de paiement en utilisant l'interface de ligne de commande. Pour plus d'informations, voir
[Changement de plan](../../pricing/index.html#changing).


## Comment serais-je facturé pour mon utilisation d'{{site.data.keyword.objectstorageshort}} ? {: #charge-bill}

Le service {{site.data.keyword.objectstorageshort}} ne vous facture que pour ce que vous utilisez.  Il n'y a pas de frais minimum, de frais d'installation ou d'engagements pour pouvoir utiliser le service. Les requêtes d'API ou le trafic réseau liés aux données entrantes ne sont pas facturés.

Votre utilisation d'{{site.data.keyword.objectstorageshort}} est facturée en fonction de l'utilisation que vous faites du stockage au
cours du cycle de facturation. Toutes les données objet se trouvant dans des conteneurs ayant été créées sous votre compte d'organisation {{site.data.keyword.Bluemix_notm}} sont prises en compte. 

Les frais pour le transfert de données sortantes s'appliquent dès lors que des données sont lues depuis n'importe quel conteneur d'objets sur le réseau public. La
bande passante sortante publique est facturée dans le cadre de la bande passante consommée au cours du cycle de facturation.


Les composants de mesure pour la tarification d'{{site.data.keyword.objectstorageshort}} sont les suivants :
* Utilisation d'espace de stockage - 0,04 $ par Go/mois
* Transfert de données sortantes publiques - 0,09 $ par Go/mois 

A la fin du cycle de facturation, {{site.data.keyword.Bluemix_notm}} vous facturera automatiquement l'utilisation du service pour la période de facturation en cours. Vous pouvez afficher vos frais pour la période de facturation en cours via la génération de rapports {{site.data.keyword.Bluemix_notm}}.

Le plan de service standard qui est publié pour Londres et Dallas dispose de la même tarification.

## Comment est effectuée la réplication des données dans {{site.data.keyword.objectstorageshort}} ? {: #replication}
Le service {{site.data.keyword.objectstorageshort}} conserve trois copies de vos données, qui sont répliquées sur différents noeuds de
stockage. Pour plus d'informations, consultez le document [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}.

