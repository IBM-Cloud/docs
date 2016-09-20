{:new_window: target="_blank"}


# A propos de {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Dernière mise à jour : 1 août 2016
{: .last-updated}

## Volumes 
{: #using-volumes-concept}

Vous pouvez utiliser IBM {{site.data.keyword.blockstorageshort}} pour créer des volumes et les connecter à des serveurs virtuels. Par défaut, les {{site.data.keyword.virtualmachinesshort}} IBM ne possèdent pas de stockage permanent et l'image par défaut est restaurée lorsqu'ils sont redémarrés. {{site.data.keyword.blockstorageshort}} fournit du stockage permanent pour votre serveur virtuel. Les données contenues dans les volumes de stockage par blocs sont conservées au-delà du cycle de vie de votre serveur virtuel. {{site.data.keyword.blockstorageshort}} utilise OpenStack Cinder pour gérer le cycle de vie des volumes. 

Les volumes {{site.data.keyword.blockstorageshort}} sont créés via une instance de service {{site.data.keyword.blockstorageshort}}. Vous pouvez les connecter à un serveur virtuel en procédant comme suit : 
  

* Spécifiez un périphérique que vous fournissez.  
* Indiquez que le système sélectionne automatiquement un nom de périphérique disponible.  

Le serveur virtuel effectue les opérations d'E-S directement avec le périphérique spécifié, indépendamment du service {{site.data.keyword.blockstorageshort}}. 

## Instantanés 
{: #using-snapshots-concept}

Vous pouvez également créer des instantanés des volumes au niveau des blocs. Vous ne pouvez pas créer d'instantanés tant que le volume est connecté, par conséquent, les instantanés obtenus restent cohérents en cas de panne.  

Etape suivante ?

Créez un volume. Pour plus d'informations, voir [Création de volumes](../BlockStorage/blockstorage_creatingvolume.html).
