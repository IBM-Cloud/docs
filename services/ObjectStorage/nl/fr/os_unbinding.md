---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Annulation de la liaison et de la mise à disposition de votre instance {{site.data.keyword.objectstorageshort}}{: #deprovisioning-object-storage}

*Dernière mise à jour : 19 octobre 2016*
{: .last-updated}


### Annulation de la liaison de votre instance
Si vous n'avez plus besoin du stockage {{site.data.keyword.objectstorageshort}} de votre application Cloud Foundry mais que vous souhaitez conserver vos données enregistrées, vous pouvez annuler la liaison de votre instance de service depuis votre application.

**Attention** : si vous annulez la liaison d'une instance {{site.data.keyword.objectstorageshort}} à partir d'une application {{site.data.keyword.Bluemix_notm}} ou supprimez la clé de service, toutes vos données d'identification pour cette instance sont supprimées et ne peuvent être restaurées.

1. Ouvrez les détails de votre application dans la console {{site.data.keyword.Bluemix_notm}}.
2. Sélectionnez votre instance {{site.data.keyword.objectstorageshort}} et cliquez sur **Annuler la liaison du service**.
3. Cliquez sur **RETIRER**.
4. Cliquez sur **RECONSTITUER**.



### Annulation de la mise à disposition de votre instance

Si vous avez une instance non liée d'{{site.data.keyword.objectstorageshort}} dont vous n'avez plus besoin, vous pouvez la supprimer.

**Attention** : quand vous annulez la mise à disposition d'une instance {{site.data.keyword.objectstorageshort}}, le projet de cloud est supprimé. Tous les conteneurs et objets de l'instance concernée sont supprimés et ne peuvent être restaurés.

1. Ouvrez les détails de votre application dans la console {{site.data.keyword.Bluemix_notm}}.
2. Sélectionnez votre instance {{site.data.keyword.objectstorageshort}} et cliquez sur **Supprimer**.
3. Cliquez sur **RECONSTITUER**.
