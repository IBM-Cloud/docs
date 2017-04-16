{:new_window: target="_blank"}


# A propos de {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Dernière mise à jour : 7 septembre 2016
{: .last-updated}

Le service IBM {{site.data.keyword.blockstorageshort}} vous permet de connecter un stockage permanent à un serveur virtuel. Pour utiliser le stockage, vous connectez les volumes de stockage par blocs à vos serveurs virtuels. Les données contenues dans les volumes de stockage par blocs sont conservées au-delà du cycle de vie de votre serveur virtuel. Cela signifie que vous pouvez déconnecter les volumes d'une instance de serveur et les reconnecter à une autre instance de serveur, sans modifier vos données. {{site.data.keyword.blockstorageshort}} utilise OpenStack Cinder pour gérer le cycle de vie des volumes. 

Vous accédez au stockage sur une unité par bloc que vous pouvez partitionner, formater et sur laquelle vous pouvez effectuer des montages, par exemple, /dev/vdb. Les données sont conservées tant que vous ne les supprimez pas.  

## Volumes 
{: #using-volumes-concept}

Les volumes {{site.data.keyword.blockstorageshort}} sont créés via une instance de service {{site.data.keyword.blockstorageshort}}. Vous pouvez les connecter à un serveur virtuel en procédant comme suit :
  

* Spécifiez un périphérique que vous fournissez. 
* Indiquez que le système sélectionne automatiquement un nom de périphérique disponible. 

Le serveur virtuel effectue les opérations d'E-S directement avec le périphérique spécifié, indépendamment du service {{site.data.keyword.blockstorageshort}}.

## Instantanés 
{: #using-snapshots-concept}

Vous pouvez également créer des instantanés des volumes au niveau des blocs. Un instantané capture des données sur le volume de stockage par blocs à un point de cohérence spécifique. Vous pouvez utiliser des instantanés pour effectuer des sauvegardes incrémentielles de vos données. Cela dit, les instantanés existent sur le même stockage que le volume d'origine. Par conséquent, les instantanés ne constituent par une stratégie de reprise après incident suffisante.

**Remarque** : Vous ne pouvez pas créer d'instantanés lorsqu'un volume est connecté à une instance de serveur.  

Lorsque vous créez volume à partir d'un instantané, un nouveau volume est créé avec un état identique à celui du volume d'origine au moment de la prise de l'instantané.  

Les conséquences de la création d'un volume à partir d'un instantané sont les suivantes :

* Les volumes existants ne sont pas retirés. 
* Les données créées, modifiées ou supprimées après l'instantané concerné ne sont pas incluses dans le nouveau volume.

Etape suivante ?

Créez un volume. Pour plus d'informations, voir [Création de volumes](../BlockStorage/blockstorage_creatingvolume.html).
