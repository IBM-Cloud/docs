{:new_window: target="_blank"}


# About {{site.data.keyword.blockstorageshort}}
{: #about-block-storage}

Last updated: 01 August 2016
{: .last-updated}

## Volumes 
{: #using-volumes-concept}

You can use IBM {{site.data.keyword.blockstorageshort}} to create volumes and attach them to virtual servers. By default, IBM {{site.data.keyword.virtualmachinesshort}} do not have persistent storage, and revert to the default image when they are restarted. {{site.data.keyword.blockstorageshort}} provides persistent storage for your virtual server. The data in block storage volumes persists beyond the lifecycle of your virtual server. {{site.data.keyword.blockstorageshort}} uses OpenStack Cinder to manage the volume lifecycle.

{{site.data.keyword.blockstorageshort}} volumes are created through a {{site.data.keyword.blockstorageshort}} service instance. You can attach the volumes to a virtual server in the following ways:
  

* Specify a particular device that you provide. 
* Specify that the system automatically selects an available device name. 

The virtual server performs its I/O operations directly with the specified device, independent of the {{site.data.keyword.blockstorageshort}} service.

## Snapshots 
{: #using-snapshots-concept}

You can also create block-level snapshots of volumes. You can't create snapshots while the volume is attached, so the resulting snapshots will be crash-consistent. 

What's next?

Create a volume. For more information, see [Creating volumes](../BlockStorage/blockstorage_creatingvolume.html).
