{:new_window: target="_blank"} 


# Utilisation d'un instantané {{site.data.keyword.blockstorageshort}} {: #using-block-storage-snapshot} 
Dernière mise à jour : 7 septembre 2016
{: .last-updated}

Pour utiliser des instantanés, procédez comme suit :

## Création d'un instantané {: #creating-snapshot} 

1.  Dans l'interface utilisateur Bluemix, sélectionnez **Console > Stockage**.
2.  Sélectionnez l'instance de stockage par blocs précédemment mise à disposition. 
3.	Cliquez sur l'onglet Gérer. 
4.	Sur la page Gérer, cliquez sur l'onglet **Volumes** pour obtenir une liste de volumes. 
5.	Sélectionnez le volume dont vous souhaitez créer un instantané dans la colonne des volumes non connectés. Assurez-vous que le volume que vous avez sélectionné n'est connecté à aucune machine. Le volume sélectionné est mis en évidence. 
6.	Dans le menu déroulant Actions, cliquez sur **Créer un instantané**.
7.	Donnez un nom à l'instantané et cliquez sur **Créer**.

**Remarque : ** 

* Il est impossible de supprimer un volume tant qu'il existe des instantanés associés à celui-ci. 
* La taille de l'instantané est automatiquement définie pour être égale à celle du volume d'origine. 

## Création d'un volume à partir d'un instantané {: #creating-volume-from-snapshot}

1.  Dans l'interface utilisateur Bluemix, sélectionnez **Console > Stockage**.
2.  Sélectionnez l'instance de stockage par blocs précédemment mise à disposition. 
3.	Cliquez sur l'onglet Gérer. 
4.	Sur la page Gérer, cliquez sur l'onglet **Instantanés** pour obtenir une liste d'instantanés. 
5.	Sélectionnez l'instantané à partir duquel vous souhaitez créer un volume. L'instantané sélectionné est mis en évidence.
6.	Dans le menu déroulant Actions, cliquez sur **Créer un volume**.
7.	Donnez un nom au nouveau volume et, éventuellement, indiquez une nouvelle taille, puis cliquez sur **Créer**. 

**Remarque :** La taille du nouveau volume doit être égale ou supérieure à la taille de l'instantané. 

## Suppression d'un instantané {: #deleting-snapshot}

1.  Dans l'interface utilisateur Bluemix, sélectionnez **Console > Stockage**.
2.  Sélectionnez l'instance de stockage par blocs précédemment mise à disposition. 
3.	Cliquez sur l'onglet Gérer. 
4.	Sur la page Gérer, cliquez sur l'onglet **Instantanés** pour obtenir une liste d'instantanés. 
5.	Sélectionnez l'instantané à supprimer. L'instantané sélectionné est mis en évidence.
6.	Dans le menu déroulant Actions, cliquez sur **Supprimer**. 



