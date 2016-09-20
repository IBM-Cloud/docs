---

copyright:
 years: 2015, 2016

---

# Activation des notifications
{: #c_enable_push-notifications}
Dernière mise à jour : 16 août 2016
{: .last-updated}

Vous pouvez activer les applications pour recevoir et envoyer des notifications push à vos périphériques.

Cette section décrit comment configurer vos applications mobiles pour qu'elles reçoivent des notifications push, comment créer des notifications de base, obtenir et initialiser le logiciel SDK ou le plug-in et comment enregistrer votre périphérique pour qu'il reçoive des notifications push. Vous pouvez également activer vos applications mobiles pour la réception de notifications push à l'aide de l'[API REST](t_restapi.html).

Remarque : pour les enregistrements de périphérique avec push, le service {{site.data.keyword.mobilepushshort}} conserve une référence unique aux jetons émis par les fournisseurs de notifications - APNs pour Apple ou GCM pour Google. Les jetons peuvent être invalidés par le fournisseur de service {{site.data.keyword.mobilepushshort}} pour un certain nombre de raisons. 

Cette invalidation peut survenir durant la désinstallation d'une application du périphérique, par exemple. Dans un tel scénario, quand une tentative de distribution d'une notification est effectuée et reçoit une réponse des fournisseurs indiquant que le périphérique est invalidé, le service {{site.data.keyword.mobilepushshort}} retire les enregistrements du périphérique, ce qui aura pour effet d'empêcher d'autres tentatives d'envoi de notifications au périphérique invalidé.
