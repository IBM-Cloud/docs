{:new_window: target="_blank"} 

# Initiation à {{site.data.keyword.blockstorageshort}} (Bêta)

*Dernière mise à jour : 15 juillet 2016*
{: .last-updated}

{{site.data.keyword.blockstoragefull}} permet d'accéder aux blocs de l'espace de stockage pour les charges de travail comportant de nombreuses transactions et les contextes d'exécution requérant un stockage permanent.

Vous pouvez utiliser IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} pour créer des volumes {{site.data.keyword.blockstorageshort}} pouvant être connectés à des serveurs virtuels. Les données de ces volumes sont conservées au-delà du cycle de vie des serveurs virtuels. IBM {{site.data.keyword.blockstorageshort}} utilise OpenStack Cinder pour gérer le cycle de vie des volumes.

Les volumes {{site.data.keyword.blockstorageshort}} sont créés via une instance de service {{site.data.keyword.blockstorageshort}}. Vous pouvez les connecter à un serveur virtuel sous une unité donnée fournie par vous, ou bien le système peut sélectionner automatiquement un nom d'unité disponible. Le serveur virtuel effectue les opérations d'E-S directement avec l'unité spécifiée indépendamment du service {{site.data.keyword.blockstorageshort}}. 

Vous pouvez également créer des instantanés des volumes au niveau des blocs. Le service {{site.data.keyword.blockstorageshort}} ne permet pas la création d'instantanés lorsque le volume est connecté afin que les instantanés résultant restent cohérents en cas de plantage. 


## Comment créer une instance de service {{site.data.keyword.blockstorageshort}}
Pour créer une instance du service {{site.data.keyword.blockstorageshort}} au sein de votre espace, procédez comme suit :
 
1.	Accédez à l'onglet **Catalogue** de {{site.data.keyword.Bluemix_notm}} et entrez **{{site.data.keyword.blockstorageshort}}** dans la zone de recherche, ou accédez à **Services** et sélectionnez **Stockage**. Cliquez sur le service **{{site.data.keyword.blockstorageshort}}**. 
2.	Entrez un nom d'espace et de service. Sélectionnez le plan et cliquez sur **Créer**.
 	
Le service {{site.data.keyword.blockstorageshort}} est uniquement pris en charge dans les contextes non liés. 

Une instance de service {{site.data.keyword.blockstorageshort}} est créée dans votre espace. Vous pouvez à tout moment ouvrir l'interface utilisateur {{site.data.keyword.blockstorageshort}} afin de gérer les volumes. Pour cela, cliquez sur l'icône de l'instance de service.



## Utilisation de l'interface utilisateur de {{site.data.keyword.blockstorageshort}} {: #using-block-storage-ui}
En haut de la fenêtre, l'interface graphique utilisateur {{site.data.keyword.blockstorageshort}} propose une présentation générale des volumes de stockage, des instantanés et de l'espace de stockage total consommé par les volumes et les instantanés. 

L'en-tête contient la date et l'heure de la dernière actualisation de l'interface utilisateur. Si besoin est, vous pouvez utiliser l'icône d'actualisation (représentant une flèche circulaire) pour procéder manuellement à l'actualisation. 

Utilisez la barre de recherche pour effectuer une recherche de volumes en fonction d'une chaîne donnée. Les tableaux sont filtrés au fur et à mesure que vous saisissez vos termes de recherche, et seuls les volumes correspondant à la chaîne saisie s'affichent.

Deux onglets correspondant aux volumes et aux instantanés sont affichés sous la présentation. L'onglet relatif aux volumes est sélectionné par défaut. Les tableaux qu'il contient présentent des informations détaillées sur les volumes disponibles et connectés. Chaque ligne du tableau détaille les principales propriétés d'un volume. Lorsque vous développez une ligne, d'autres propriétés s'affichent. Les volumes connectés présentent également l'instance de serveur virtuel et l'unité auquel ce volume est connecté. 

L'onglet relatif aux instantanés contient un tableau des instantanés dont les propriétés et le comportement sont similaires. 

Utilisez l'icône Créer affichée au-dessus des tableaux pour créer un volume ou manipuler des volumes existants. Si vous créez des volumes à partir d'un instantané, vous pouvez également utiliser la liste déroulante Actions.




## Connexion d'un volume à un serveur virtuel{: #attaching-detaching-volume}
Les volumes sont connectés à des serveurs virtuels et déconnectés de ceux-ci en tant qu'unités dotées d'un nom spécifique. Pour qu'un serveur virtuel puisse conserver des données sur un volume, vous devez connecter ce volume à ce serveur virtuel. 

Pour connecter un volume, procédez comme suit : 

1.	Sélectionnez un volume dans la liste des volumes disponibles.
2.	Cliquez sur **Attach**.
3.	Dans la boîte de dialogue Attach, sélectionnez une instance de serveur virtuel dans la liste déroulante. 
4.	Facultatif : Indiquez l'unité à utiliser pour connecter ce volume. Si vous n'indiquez aucune unité, le système sélectionne automatiquement la première unité disponible sur le serveur virtuel. 
5.	Cliquez sur **Attach** pour soumettre les informations, puis fermez la boîte de dialogue.

Le volume apparaît dans le tableau des volumes connectés parmi les informations relatives à l'instance de serveur virtuel.
Le serveur virtuel peut désormais utiliser cette unité pour conserver des données. 


# Liens connexes
{: #rellinks}

## Informations de référence sur l'API
{: #api}
* [API OpenStack Block Storage (Cinder) version 2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

