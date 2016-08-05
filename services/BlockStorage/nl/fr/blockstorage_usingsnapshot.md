{:new_window: target="_blank"} 


# Utilisation d'un instantané {{site.data.keyword.blockstorageshort}} {: #using-block-storage-snapshot} 

*Dernière mise à jour : 20 juin 2016*
{: .last-updated}

## Création d'un instantané{: #creating-snapshot} 

1.	Sélectionnez l'onglet **Volumes** pour obtenir la liste des volumes.
2.	Sélectionnez le volume dont vous souhaitez créer un instantané dans la colonne des volumes non connectés. Assurez-vous que le volume que vous avez sélectionné n'est connecté à aucune machine. Le volume sélectionné est mis en évidence. 
3.	Cliquez sur **Actions** et sélectionnez **Create Snapshot** dans la liste déroulante.
4.	Donnez un nom à l'instantané et cliquez sur **Créer**.

**Remarque :** Il est impossible de supprimer un volume tant qu'il existe des instantanés associés à celui-ci. 

## Création d'un volume à partir d'un instantané{: #creating-volume-from-snapshot}

1.	Sélectionnez l'onglet **Instantanés** pour obtenir la liste des instantanés.
2.	Sélectionnez l'instantané à partir duquel vous souhaitez créer un volume. L'instantané sélectionné est mis en évidence.
3.	Cliquez sur **Actions** et sélectionnez **Create Volume** dans la liste déroulante.
4.	Donnez un nom au nouveau volume et, éventuellement, indiquez une nouvelle taille, puis cliquez sur **Créer**. 

**Remarque :** La taille du nouveau volume doit être égale ou supérieure à la taille de l'instantané. 

## Suppression d'un instantané {: #deleting-snapshot}

1.	Sélectionnez l'onglet **Instantanés** pour obtenir la liste des instantanés.
2.	Sélectionnez l'instantané à supprimer. L'instantané sélectionné est mis en évidence.
3.	Cliquez sur **Actions** et sélectionnez **Supprimer**. 



