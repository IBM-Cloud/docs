{:new_window: target="_blank"}


# Acerca de {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Última actualización: 7 de septiembre de 2016
{: .last-updated}

El servicio {{site.data.keyword.blockstorageshort}} de IBM
le permite adjuntar almacén persistente al servidor virtual.
Para utilizar el almacenamiento, adjunte los volúmenes en bloque a
sus servidores virtuales. Los datos en los volúmenes de almacenamiento en bloque persisten más allá del ciclo de vida de su servidor virtual. Esto
implica que puede desconectar los volúmenes de la instancia del
servidor y reacoplarlos a otra instancia de servidor, sin sufrir
cambios en los datos. {{site.data.keyword.blockstorageshort}} utiliza OpenStack Cinder para gestionar el ciclo de vida del volumen. 

El almacenamiento se accede con un dispositivo de bloque que
puede particionar, formatear y montar, como /dev/vdb. Los datos
persisten hasta que se suprimen. 

## Volúmenes 
{: #using-volumes-concept}

Los volúmenes de {{site.data.keyword.blockstorageshort}} se crean a través de una instancia de servicio de {{site.data.keyword.blockstorageshort}}. Puede adjuntar los volúmenes a un servidor virtual de las siguientes maneras:
  

* Especifique un dispositivo concreto que proporcione usted. 
* Especifique que el sistema seleccione automáticamente un nombre de dispositivo disponible. 

El servidor virtual realiza sus operaciones de E/S directamente con el dispositivo especificado, independientemente del servicio {{site.data.keyword.blockstorageshort}}.

## Instantáneas 
{: #using-snapshots-concept}

También puede crear instantáneas de volúmenes a nivel de bloque. Una
instantánea captura los datos en el volumen de almacenamiento en
bloques en un punto específico del tiempo. Puede utilizar
instantáneas para realizar copia de seguridad incremental de sus
datos. Es decir, las instantáneas existen en el mismo
almacenamiento que el volumen original. Por ello, las
instantáneas no son una estrategia de recuperación tras
desastre suficiente.

**Nota**: No puede crear instantáneas
mientras haya un volumen adjunto a una instancia de servidor. 

Cuando crea un volumen desde una instantánea, se crea un
volumen nuevo que ya existe en el mismo estado en el que estaba el
volumen original en el momento en que tomó la instantánea. 

La creación de un volumen desde una instantánea tiene el
siguiente impacto:

* Los volúmenes existente no se eliminan.
* Los datos que se crean, modifican o se eliminan después
de que se tome una instantánea relevante, no se incluyen en el nuevo
volumen.

Qué hacer a continuación

Cree un volumen. Para más información, consulte [Creación de volúmenes](../BlockStorage/blockstorage_creatingvolume.html).
