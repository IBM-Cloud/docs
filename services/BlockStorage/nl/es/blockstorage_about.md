{:new_window: target="_blank"}


# Acerca de {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Última actualización: 1 de agosto de 2016
{: .last-updated}

## Volúmenes 
{: #using-volumes-concept}

Puede utilizar IBM {{site.data.keyword.blockstorageshort}} para crear volúmenes y adjuntarlos a los servidores virtuales. De manera predeterminada, las {{site.data.keyword.virtualmachinesshort}} de IBM no disponen de almacén persistente y revierten a la imagen predeterminada cuando se reinician. {{site.data.keyword.blockstorageshort}} proporciona almacenamiento persistente para su servidor virtual. Los datos en los volúmenes de almacenamiento en bloque persisten más allá del ciclo de vida de su servidor virtual. {{site.data.keyword.blockstorageshort}} utiliza OpenStack Cinder para gestionar el ciclo de vida del volumen. 

Los volúmenes de {{site.data.keyword.blockstorageshort}} se crean a través de una instancia de servicio de {{site.data.keyword.blockstorageshort}}. Puede adjuntar los volúmenes a un servidor virtual de las siguientes maneras:
  

* Especifique un dispositivo concreto que proporcione usted.  
* Especifique que el sistema seleccione automáticamente un nombre de dispositivo disponible.  

El servidor virtual realiza sus operaciones de E/S directamente con el dispositivo especificado, independientemente del servicio {{site.data.keyword.blockstorageshort}}. 

## Instantáneas 
{: #using-snapshots-concept}

También puede crear instantáneas de volúmenes a nivel de bloque. Puede crear instantáneas mientras el volumen esté adjunto, de modo que las instantáneas resultantes serán coherentes a bloqueo.  

Qué hacer a continuación

Cree un volumen. Para más información, consulte [Creación de volúmenes](../BlockStorage/blockstorage_creatingvolume.html).
