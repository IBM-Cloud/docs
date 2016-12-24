---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Annulation de la liaison et de la mise à disposition de votre instance {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

Si vous avez lié {{site.data.keyword.objectstorageshort}} à une application Cloud Foundry et n'avez plus besoin de ce stockage, vous pouvez annuler la liaison et l'accès à votre instance.
{: shortdesc}


## Annulation de la liaison de votre instance
Si vous n'avez plus besoin du stockage {{site.data.keyword.objectstorageshort}} de votre application Cloud Foundry mais que vous souhaitez conserver vos données enregistrées,  vous pouvez annuler la liaison de l'instance de service depuis votre application.

**Attention** : si vous annulez la liaison d'une instance {{site.data.keyword.objectstorageshort}} à partir d'une application {{site.data.keyword.Bluemix_notm}} ou supprimez la clé de service, toutes vos données d'identification pour cette instance sont supprimées et ne peuvent être restaurées. Le compte {{site.data.keyword.objectstorageshort}} n'est pas supprimé tant que la mise à disposition de l'instance {{site.data.keyword.objectstorageshort}} n'est pas annulée. Vous pouvez générer de nouvelles données d'identification de cloud en effectuant une nouvelle liaison ou en créant une nouvelle clé de service.

1. Pour voir les services qui sont liés à votre application, cliquez sur l'onglet relatif aux connexions dans votre application Cloud Foundry.
2. Localisez le service dont vous souhaitez annuler la liaison puis cliquez sur le bouton de menu de la vignette du service.
3. Sélectionnez **Annuler la liaison du service**.
4. Décochez la case associée à l'option relative à la suppression de l'instance de service puis cliquez sur **OK**.
5. Cliquez sur **Reconstituer** pour que vos changements prennent effet.



## Annulation de la mise à disposition de votre instance

Si vous avez une instance d'{{site.data.keyword.objectstorageshort}} dont vous n'avez plus besoin, vous pouvez la supprimer.

**Attention** : quand vous annulez la mise à disposition d'une instance {{site.data.keyword.objectstorageshort}}, le projet de cloud et le compte Swift sont supprimés. Tous les conteneurs et objets de l'instance concernée sont supprimés et ne peuvent être restaurés.

1. Pour voir les services qui sont liés à votre application, cliquez sur l'onglet relatif aux connexions dans votre application Cloud Foundry.
2. Localisez le service dont vous souhaitez annuler la liaison puis cliquez sur le bouton de menu de la vignette du service.
3. Sélectionnez **Supprimer le service**.
4. Cliquez sur **Supprimer** pour confirmer.
5. Cliquez sur **Reconstituer** pour que vos changements prennent effet.
