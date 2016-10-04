---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# Informazioni su {{site.data.keyword.objectstorageshort}}  {: #about-object-storage} 

*Ultimo aggiornamento: 29 agosto 2016*
{: .last-updated}


IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} utilizza OpenStack Identity (Keystone) per l'autenticazione ed è possibile accedervi direttamente utilizzando le chiamate API OpenStack Object Storage (Swift) v1. È possibile eseguire il bind di IBM {{site.data.keyword.objectstorageshort}} a un'applicazione {{site.data.keyword.Bluemix_notm}} oppure è possibile accedere a esso dall'esterno di un'applicazione {{site.data.keyword.Bluemix_notm}}. 

Per ulteriori informazioni sull'utilizzo di OpenStack Swift e Keystone, consulta il [sito della documentazione di OpenStack](http://docs.openstack.org){: new_window}.

Il diagramma dell'architettura {{site.data.keyword.objectstorageshort}} è il seguente:

![{{site.data.keyword.objectstorageshort architecture diagram }}](images/ObjectStorageArchitectureDiagram.png)

*Figura 1. Diagramma dell'architettura {{site.data.keyword.objectstorageshort}}*

