---

copyright:
 years: 2015, 2016

---

# Traitement des incidents
{: #errors}
Dernière mise à jour : 08 novembre 2016
{: .last-updated}

Utilisez cette section pour traiter les incidents courants liés aux notifications de type {{site.data.keyword.mobilepushshort}}.


### Une erreur serveur interne s'est produite. Veuillez contacter l'administrateur. (Code d'erreur interne : PUSHD102E)

####Explication

**Explication** : Cette erreur peut se produire si vous avez créé une instance push avant le mois de novembre 2015.  

####REPONSE DE L'UTILISATEUR

**Action** : Pour résoudre ce problème, supprimez l'instance push et créez-en une nouvelle.

**Remarque** : Lorsque vous supprimez l'instance push, vos balises ne sont pas conservées.


### UnauthorizedRegistration

####Explication

**Explication** : Chrome Web Push ne fonctionne pas avec les clés de Firebase Cloud Messaging (FCM). Si vous ne parvenez pas à recevoir des notifications push Web sur Chrome après avoir migré vers FCM à partir de GCM, c'est parce que le site Web a été configuré pour fonctionner avec le projet GCM et que le nouveau projet est créé dans FCM. Les jetons générés qui identifient le navigateur sont mis en cache par le navigateur Chrome.

**Action **: Vous pouvez résoudre ce problème en supprimant les cookies et en réinitialisant les autorisations du navigateur. Cela demanderait des autorisations pour activer les notifications Push. 

