---



copyright:

  years: 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Changement de plan 
{: #changing}

Vous pouvez changer de plan de service dans {{site.data.keyword.Bluemix_notm}} dans le tableau de bord du service, si le changement de plan est possible pour ce service.

Certains services seulement vous permettent de changer de plan de service. Si le changement de plan est possible pour le service, le tableau de bord
du service affiche l'option **Plan** dans la navigation. Chaque service propose un
ensemble différent d'étapes à suivre si vous changez de plan.

1. Pour changer de plan, dans le tableau de bord du service, cliquez sur **Plan**. En général, vous pouvez mettre à niveau votre plan ou passer à un plan de niveau inférieur.
2. Après avoir changé de plan, vous devez effectuer un certain nombre d'étapes. Celles-ci varient selon le type de changement de plan et le service. Par
exemple, si vous êtes passé à un plan de niveau inférieur, il se peut que vous deviez reconstituer votre application. Ou, si vous avez effectué une mise à niveau de votre plan, il se peut que vous deviez reconstituer votre application et prendre d'autres mesures.<br/><br/>Pour reconstituer votre application, accédez au tableau de bord {{site.data.keyword.Bluemix_notm}} et recherchez l'application à laquelle le service est lié. Dans le menu de l'application, sélectionnez **Redémarrer l'application**.<br/><br/>Les autres actions varient en fonction du service. Reportez-vous au tableau ci-dessous pour prendre connaissance des actions spécifiques à
exécuter.

|Service |	Information|
|--------|-------------|
|Presence Insights 	|Si vous avez choisi un plan léger et que vous dépassez les franchises, un message 403 s'affiche ou est consigné afin d'indiquer que vous ne disposez plus des autorisations, et votre instance de service est désactivée. De plus, les appels API REST POST sont rejetés avec une réponse 403.<br/><br/>Si votre service est désactivé car vous avez dépassé les franchises, vous pouvez procéder à la mise à niveau du plan léger vers un plan payant. Votre service est réactivé dans un délai de 2 heures.<br/><br/>i vous disposez d'un plan payant, vous pouvez passer à un plan inférieur, c'est-à-dire au plan léger, tant que votre utilisation ne dépasse pas la franchise du plan léger pour les événements et l'espace de stockage total.<br/><br/>Lorsque vous mettez à niveau ou réduisez votre plan, vous n'avez pas à reconstituer ou à redémarrer applications.|
{:caption="Tableau 9. Etapes suivantes pour modifier votre plan" caption-side="top"}

##Changement de plan via l'interface de ligne de commande 

Si vous le souhaitez, vous pouvez changer de plan de service via l'interface de ligne de commande.
Pour mettre à jour le plan du service, entrez la commande suivante :
```
cf update-service <nom_service> [-p <nouveau_plan>]
```
