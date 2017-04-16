{:new_window: target="_blank"} 

# Initiation à {{site.data.keyword.blockstorageshort}} (BETA)

{{site.data.keyword.blockstoragefull}} permet d'accéder aux blocs de l'espace de stockage pour les charges de travail comportant de nombreuses transactions et les contextes d'exécution requérant un stockage permanent.

Vous pouvez utiliser IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} pour créer des volumes {{site.data.keyword.blockstorageshort}} pouvant être connectées à des machines virtuelles. Les données de ces volumes sont conservées au-delà du cycle de vie des machines virtuelles. IBM {{site.data.keyword.blockstorageshort}} utilise OpenStack Cinder pour gérer le cycle de vie des volumes.

Les volumes {{site.data.keyword.blockstorageshort}} sont créés via une instance de service {{site.data.keyword.blockstorageshort}}. Vous pouvez les connecter à une machine virtuelle sous une unité donnée fournie par vous, ou bien le système peut sélectionner automatiquement un nom d'unité disponible. La machine virtuelle effectue les opérations d'E-S directement avec l'unité indépendante spécifiée sur le service {{site.data.keyword.blockstorageshort}}.

Vous pouvez également créer des instantanés des volumes au niveau des blocs. Le service {{site.data.keyword.blockstorageshort}} ne permet pas la création d'instantanés lorsque le volume est connecté afin que les instantanés résultant restent cohérents en cas de plantage. 

## Comment créer une instance de service {{site.data.keyword.blockstorageshort}}
Pour créer une instance du service {{site.data.keyword.blockstorageshort}} au sein de votre espace, procédez comme suit :
 
1.	Accédez à l'onglet **Catalogue** de {{site.data.keyword.Bluemix_notm}} et entrez **{{site.data.keyword.blockstorageshort}}** dans la zone de recherche, ou accédez à **Services** et sélectionnez **Stockage**. Cliquez sur le service **{{site.data.keyword.blockstorageshort}}**. 
2.	Entrez un nom d'espace et de service. Sélectionnez le plan et cliquez sur **Créer**.
 	
Le service {{site.data.keyword.blockstorageshort}} est uniquement pris en charge dans les contextes non liés. 

Une instance de service {{site.data.keyword.blockstorageshort}} est créée dans votre espace. Vous pouvez à tout moment ouvrir l'interface utilisateur {{site.data.keyword.blockstorageshort}} afin de gérer les volumes. Pour cela, cliquez sur l'icône de l'instance de service.

## Interface utilisateur {{site.data.keyword.blockstorageshort}}
En haut de la fenêtre, l'interface graphique utilisateur {{site.data.keyword.blockstorageshort}} propose une présentation générale des volumes de stockage, des instantanés et de l'espace de stockage total consommé par les volumes et les instantanés. 

L'en-tête contient la date et l'heure de la dernière actualisation de l'interface utilisateur. Si besoin est, vous pouvez utiliser l'icône d'actualisation (représentant une flèche circulaire) pour procéder manuellement à l'actualisation. 

Utilisez la barre de recherche pour effectuer une recherche de volumes en fonction d'une chaîne donnée. Les tableaux sont filtrés au fur et à mesure que vous saisissez vos termes de recherche, et seuls les volumes correspondant à la chaîne saisie s'affichent.

Deux onglets correspondant aux volumes et aux instantanés sont affichés sous la présentation. L'onglet relatif aux volumes est sélectionné par défaut. Les tableaux qu'il contient présentent des informations détaillées sur les volumes disponibles et connectés. Chaque ligne du tableau détaille les principales propriétés d'un volume. Lorsque vous développez une ligne, d'autres propriétés s'affichent. Les volumes connectés présentent également l'instance de machine virtuelle et l'unité auquel ce volume est connecté. 

L'onglet relatif aux instantanés contient un tableau des instantanés dont les propriétés et le comportement sont similaires. 

Utilisez l'icône Créer affichée au-dessus des tableaux pour créer un volume ou manipuler des volumes existants. Si vous créez des volumes à partir d'un instantané, vous pouvez également utiliser la liste déroulante Actions.


## Actions relatives aux volumes

### Création d'un volume

1.	Cliquez sur **Créer** pour ouvrir la boîte de dialogue **Create Volume**.
2.	Indiquez la taille que vous souhaitez affecter à ce volume. Les nombres décimaux ne sont pas acceptés. La taille est limitée par le quota affecté à votre organisation.
3.	Indiquez un nom. Il n'est utilisé qu'à des fins d'affichage.
4.	Facultatif : Donnez une description plus détaillée du volume. 
5.	Cliquez sur **Créer** pour soumettre les informations et fermer la boîte de dialogue. 

La création d'un volume peut prendre quelques instants. 

### Suppression d'un volume

1.	Sélectionnez le volume à supprimer.
2.	Cliquez sur **Supprimer**.
3.	Confirmez la suppression du volume.

Il est impossible de supprimer un volume connecté à une machine virtuelle. Vous devez commencer par le déconnecter.

### Extension d'un volume
Vous pouvez augmenter la taille d'un volume à l'aide de l'action **Extend**. Il est impossible de réduire la taille d'un volume.

1.	Sélectionnez le volume à étendre.
2.	Cliquez sur **Extend**.
3.	Sélectionnez la nouvelle taille du volume. Indiquez sa nouvelle taille totale.
4.	Cliquez sur **Extend** pour soumettre les informations et fermer la boîte de dialogue. 

Un volume doit être à l'état **Disponible** pour pouvoir être étendu. 

### Connexion et déconnexion d'un volume
Les volumes sont connectés à des machines virtuelles et déconnectés de celles-ci en tant qu'unités dotées d'un nom spécifique. Pour qu'une machine virtuelle puisse conserver des données sur un volume, vous devez connecter ce volume à cette machine.

Pour connecter un volume, procédez comme suit : 

1.	Sélectionnez un volume dans la liste des volumes disponibles.
2.	Cliquez sur **Attach**.
3.	Dans la boîte de dialogue Attach, sélectionnez une instance de machine virtuelle dans la liste déroulante. 
4.	Facultatif : Indiquez l'unité à utiliser pour connecter ce volume. Si vous n'indiquez aucune unité, le système sélectionne automatiquement la première unité disponible sur la machine virtuelle.
5.	Cliquez sur **Attach** pour soumettre les informations, puis fermez la boîte de dialogue.

Le volume apparaît dans le tableau des volumes connectés parmi les informations relatives à l'instance de machine virtuelle. 
La machine virtuelle peut désormais utiliser cette unité pour conserver des données. 

Pour déconnecter un volume, procédez comme suit : 

1.	Sélectionnez un volume dans la liste des volumes connectés. 
2.	Cliquez sur **Detach**.
3.	Dans la boîte de dialogue, confirmez la déconnexion du volume. 

Une fois le volume déconnecté, il n'est plus disponible pour les opérations d'E-S effectuées dans l'instance de machine virtuelle. Dans l'interface utilisateur du service {{site.data.keyword.blockstorageshort}}, ce volume est disponible en vue d'une éventuelle connexion à d'autres machines virtuelles.

## Actions relatives aux instantanés

### Création d'un instantané

1.	Sélectionnez l'onglet **Volumes** pour obtenir la liste des volumes.
2.	Sélectionnez le volume dont vous souhaitez créer un instantané dans la colonne des volumes non connectés. Assurez-vous que le volume que vous avez sélectionné n'est connecté à aucune machine. Le volume sélectionné est mis en évidence. 
3.	Cliquez sur **Actions** et sélectionnez **Create Snapshot** dans la liste déroulante.
4.	Donnez un nom à l'instantané et cliquez sur **Créer**.

**Remarque :** Il est impossible de supprimer un volume tant qu'il existe des instantanés associés à celui-ci. 

### Création d'un volume à partir d'un instantané

1.	Sélectionnez l'onglet **Instantanés** pour obtenir la liste des instantanés.
2.	Sélectionnez l'instantané à partir duquel vous souhaitez créer un volume. L'instantané sélectionné est mis en évidence.
3.	Cliquez sur **Actions** et sélectionnez **Create Volume** dans la liste déroulante.
4.	Donnez un nom au nouveau volume et, éventuellement, indiquez une nouvelle taille, puis cliquez sur **Créer**. 

**Remarque :** La taille du nouveau volume doit être égale ou supérieure à la taille de l'instantané. 

### Suppression d'un instantané

1.	Sélectionnez l'onglet **Instantanés** pour obtenir la liste des instantanés.
2.	Sélectionnez l'instantané à supprimer. L'instantané sélectionné est mis en évidence.
3.	Cliquez sur **Actions** et sélectionnez **Supprimer**. 



># Liens connexes {:class="linklist"}
>## Informations de référence sur l'API {:id="api"}
>* [API OpenStack Block Storage (Cinder) version 2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}
>
>{:elementKind="article" id="rellinks"}
