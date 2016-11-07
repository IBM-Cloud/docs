---

copyright:
 years: 2015, 2016

---

# Activation des notifications push
{: #c_enable_push-notifications}
Dernière mise à jour : 17 octobre 2016
{: .last-updated}

Vous pouvez activer les applications pour recevoir des notifications push sur vos appareils.

Cette section décrit comment configurer vos applications - mobiles, Web et applications et extensions Chrome - pour qu'elles reçoivent des notifications push, comment créer des notifications de base, obtenir et initialiser le logiciel SDK ou le plug-in et comment enregistrer votre appareil ou votre navigateur pour qu'il reçoive des notifications push. Vous pouvez également activer vos applications mobiles et de navigateur Web pour la réception de notifications push en utilisant l'[API REST](t_restapi.html).

Remarque : pour les enregistrements d'appareil, de navigateur et d'applications et extensions Chrome, le service {{site.data.keyword.mobilepushshort}} conserve une référence unique aux jetons émis par les fournisseurs de notifications - APNs pour Apple ou GCM pour Google. Les jetons peuvent être invalidés par le fournisseur de service {{site.data.keyword.mobilepushshort}} pour un certain nombre de raisons. 

Cette invalidation peut survenir durant la désinstallation d'une application de l'appareil, par exemple. Dans un tel scénario, quand une tentative de distribution d'une notification est effectuée et reçoit une réponse des fournisseurs indiquant que l'appareil est invalidé, le service {{site.data.keyword.mobilepushshort}} retire les enregistrements de l'appareil ou du navigateur Web, ce qui aura pour effet d'empêcher d'autres tentatives d'envoi de notifications à l'appareil invalidé.
