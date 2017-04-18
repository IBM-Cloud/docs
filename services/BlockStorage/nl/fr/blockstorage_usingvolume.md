{:new_window: target="_blank"} 

# Utilisation d'un volume {{site.data.keyword.blockstorageshort}} 
{: #using-block-storage-volume} 
Dernière mise à jour : 7 septembre 2016
{: .last-updated}

Pour utiliser des volumes, procédez comme suit :

## Suppression d'un volume {: #deleting-volume}

1.  Dans l'interface utilisateur Bluemix, sélectionnez **Console > Stockage**.
2.  Sélectionnez l'instance de stockage par blocs précédemment mise à disposition. 
3.	Sélectionnez le volume à supprimer.
4.	Dans le menu déroulant Actions, cliquez sur **Supprimer**.
5.	Confirmez la suppression du volume.

Il est impossible de supprimer un volume connecté à une serveur virtuel. Vous devez commencer par le déconnecter. Lorsqu'il est supprimé, un volume devient inaccessible pour une utilisation ultérieure et les données qu'il contient son perdues. De plus, vous ne pouvez pas supprimer des volumes auxquels des instantanés sont associés. 

## Extension d'un volume {: #extending-volume}
Vous pouvez augmenter la taille du volume (jusqu'à dix fois sa taille initiale) à l'aide de l'action **Extend**. Il est impossible de réduire la taille d'un volume.

1.  Dans l'interface utilisateur Bluemix, sélectionnez **Console > Stockage**.
2.  Sélectionnez l'instance de stockage par blocs précédemment mise à disposition. 
3.	Sélectionnez le volume à étendre.
4.	Dans le menu déroulant Actions, cliquez sur **Etendre**.
5.	Sélectionnez la nouvelle taille du volume. Indiquez sa nouvelle taille totale.
6.	Cliquez sur **Extend** pour soumettre les informations et fermer la boîte de dialogue. 

Un volume doit être à l'état **Disponible** pour pouvoir être étendu. Une fois que vous avez étendu le volume, vous devez prévenir le système de fichiers (par exemple, ext4) que le disque a été étendu en redimensionnant le système de fichiers.  

## Connexion et déconnexion d'un volume avec un serveur virtuel {: #attaching-detaching-volume}
Les volumes sont connectés à des serveurs virtuels et déconnectés de ceux-ci en tant qu'unités dotées d'un nom spécifique. Pour qu'un serveur virtuel puisse conserver des données sur un volume, vous devez connecter ce volume à ce serveur virtuel.

Pour connecter un volume, procédez comme suit : 

1.  Dans l'interface utilisateur Bluemix, sélectionnez **Console > Stockage**.
2.  Sélectionnez l'instance de stockage par blocs précédemment mise à disposition. 
3.	Sélectionnez un volume dans la liste des volumes disponibles.
4.	Dans le menu déroulant Actions, cliquez sur **Connecter**.
5.	Dans la boîte de dialogue Connecter, sélectionnez une instance de serveur virtuel dans la liste déroulante. 
6.	Facultatif : Indiquez l'unité à utiliser pour connecter ce volume. Si vous n'indiquez aucune unité, le système sélectionne automatiquement la première unité disponible sur le serveur virtuel.
7.	Cliquez sur **Connecter** pour soumettre les informations, puis fermez la boîte de dialogue.

Le volume apparaît dans le tableau des volumes connectés parmi les informations relatives à l'instance de serveur virtuel. 
Le serveur virtuel peut désormais utiliser cette unité pour conserver des données. 

Si vous êtes prêt à déconnecter un volume, vous devez préparer le serveur virtuel à cette opération. Par exemple, arrêter les applications qui utilisent le système de fichiers. De plus, démontez l'unité de l'instance de serveur virtuel. 

Pour déconnecter un volume, procédez comme suit : 

1.  Dans l'interface utilisateur Bluemix, sélectionnez **Console > Stockage**.
2.  Sélectionnez l'instance de stockage par blocs précédemment mise à disposition. 
3.	Sélectionnez un volume dans la liste des volumes connectés. 
4.	Dans le menu déroulant Actions, cliquez sur **Déconnecter**.
5.	Dans la boîte de dialogue, confirmez la déconnexion du volume. 

Une fois le volume déconnecté, il n'est plus disponible pour les opérations d'E-S effectuées dans l'instance de serveur virtuel. Dans l'interface utilisateur du service {{site.data.keyword.blockstorageshort}}, le volume est maintenant disponible pour être connecté à d'autres serveurs virtuels.
