
{:new_window: target="_blank"}


# Connexion de volumes {{site.data.keyword.blockstorageshort}} à un serveur virtuel
{: #attaching-block-storage-volume}

Dernière mise à jour : 13 septembre 2016
{: .last-updated}

Les volumes sont connectés à des serveurs virtuels et déconnectés de ceux-ci en tant qu'unités dotées d'un nom spécifique. Pour qu'un serveur virtuel puisse conserver des données sur un volume, vous devez connecter ce volume à ce serveur virtuel.

Pour connecter un volume, procédez comme suit :

1.  Dans l'interface utilisateur Bluemix, sélectionnez **Console > Stockage**.
2.  Sélectionnez l'instance de stockage par blocs précédemment mise à disposition. 
3.	Sélectionnez un volume dans la liste des volumes disponibles.
4.	Cliquez sur **Connecter**.
5.	Dans la boîte de dialogue Connecter, sélectionnez une instance de serveur virtuel dans la liste déroulante.
6.	Facultatif : Indiquez l'unité à utiliser pour connecter ce volume. 
    
    **Remarque** : Si vous n'indiquez aucune unité, le système sélectionne automatiquement la première unité disponible sur le serveur virtuel. 

7.	Cliquez sur **Connecter** pour soumettre les informations, puis fermez la boîte de dialogue.

Le volume apparaît dans le tableau des volumes connectés parmi les informations relatives à l'instance de serveur virtuel.
Le serveur virtuel peut désormais utiliser cette unité pour conserver des données. 

Etape suivante ?

Une fois le volume créé et connecté à un serveur virtuel, voir [Préparation des volumes](../BlockStorage/blockstorage_preparingvolume.html) afin de le préparer pour utilisation.
