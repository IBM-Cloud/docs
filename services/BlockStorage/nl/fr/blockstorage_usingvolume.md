{:new_window: target="_blank"} 

# Utilisation d'un volume {{site.data.keyword.blockstorageshort}} {: #using-block-storage-volume} 

*Dernière mise à jour : 20 juin 2016*
{: .last-updated}

## Création d'un volume {: #creating-volume} 

1.	Cliquez sur **Créer** pour ouvrir la boîte de dialogue **Create Volume**.
2.	Indiquez la taille que vous souhaitez affecter à ce volume. Les nombres décimaux ne sont pas acceptés. La taille est limitée par le quota affecté à votre organisation.
3.	Indiquez un nom. Il n'est utilisé qu'à des fins d'affichage.
4.	Facultatif : Donnez une description plus détaillée du volume. 
5.	Cliquez sur **Créer** pour soumettre les informations et fermer la boîte de dialogue. 

La création d'un volume peut prendre quelques instants. 

## Suppression d'un volume {: #deleting-volume}

1.	Sélectionnez le volume à supprimer.
2.	Cliquez sur **Supprimer**.
3.	Confirmez la suppression du volume.

Il est impossible de supprimer un volume connecté à une serveur virtuel. Vous devez commencer par le déconnecter.

## Extension d'un volume {: #extending-volume}
Vous pouvez augmenter la taille du volume (jusqu'à dix fois sa taille initiale) à l'aide de l'action **Extend**. Il est impossible de réduire la taille d'un volume.

1.	Sélectionnez le volume à étendre.
2.	Cliquez sur **Extend**.
3.	Sélectionnez la nouvelle taille du volume. Indiquez sa nouvelle taille totale.
4.	Cliquez sur **Extend** pour soumettre les informations et fermer la boîte de dialogue. 

Un volume doit être à l'état **Disponible** pour pouvoir être étendu. 

## Connexion et déconnexion d'un volume avec un serveur virtuel {: #attaching-detaching-volume}
Les volumes sont connectés à des serveurs virtuels et déconnectés de ceux-ci en tant qu'unités dotées d'un nom spécifique. Pour qu'un serveur virtuel puisse conserver des données sur un volume, vous devez connecter ce volume à ce serveur virtuel. 

Pour connecter un volume, procédez comme suit : 

1.	Sélectionnez un volume dans la liste des volumes disponibles.
2.	Cliquez sur **Attach**.
3.	Dans la boîte de dialogue Attach, sélectionnez une instance de serveur virtuel dans la liste déroulante. 
4.	Facultatif : Indiquez l'unité à utiliser pour connecter ce volume. Si vous n'indiquez aucune unité, le système sélectionne automatiquement la première unité disponible sur le serveur virtuel. 
5.	Cliquez sur **Attach** pour soumettre les informations, puis fermez la boîte de dialogue.

Le volume apparaît dans le tableau des volumes connectés parmi les informations relatives à l'instance de serveur virtuel.
Le serveur virtuel peut désormais utiliser cette unité pour conserver des données. 

Pour déconnecter un volume, procédez comme suit : 

1.	Sélectionnez un volume dans la liste des volumes connectés. 
2.	Cliquez sur **Detach**.
3.	Dans la boîte de dialogue, confirmez la déconnexion du volume. 

Une fois le volume déconnecté, il n'est plus disponible pour les opérations d'E-S effectuées dans l'instance de serveur virtuel. Dans l'interface utilisateur du service {{site.data.keyword.blockstorageshort}}, le volume est maintenant disponible pour être connecté à d'autres serveurs virtuels. 
