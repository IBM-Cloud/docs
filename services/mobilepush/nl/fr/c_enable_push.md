---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des notifications pour les appareils mobiles
{: #c_enable_push-notifications}
Dernière mise à jour : 18 janvier 2017
{: .last-updated}

Vérifiez que vous avez exécuté la procédure [Configuration des données d'identification pour un fournisseur de
notification](t__main_push_config_provider.html).

Cette section décrit comment configurer vos applications - mobiles, Web et applications et extensions Chrome - pour qu'elles reçoivent des notifications push, comment créer des notifications de base, obtenir et initialiser le logiciel SDK ou le plug-in et comment enregistrer votre appareil ou votre navigateur pour qu'il reçoive des notifications push. Vous pouvez également activer vos applications mobiles et de navigateur Web pour la réception de notifications push en utilisant l'[API REST](t_restapi.html).

**Remarque **: Dans le cas d'enregistrement d'un appareil, d'un navigateur, d'applications et d'extensions Chrome, le service
{{site.data.keyword.mobilepushshort}} conserve une référence unique pour les jetons issus des fournisseurs de notification -
des APN pour Apple ou FCM pour Google. Les jetons peuvent être invalidés par le fournisseur de service {{site.data.keyword.mobilepushshort}} pour un certain nombre de raisons. 

Ceci peut survenir, par exemple, lors de la désinstallation d'une application sur l'appareil. Dans un tel scénario, quand une tentative de distribution d'une notification est effectuée et reçoit une réponse des fournisseurs indiquant que l'appareil est invalidé, le service {{site.data.keyword.mobilepushshort}} retire les enregistrements de l'appareil ou du navigateur Web, ce qui aura pour effet d'empêcher d'autres tentatives d'envoi de notifications à l'appareil invalidé.
