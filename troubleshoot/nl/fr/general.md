{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# Problèmes d'ordre général liés aux services
{: #general}

*Dernière mise à jour : 9 décembre 2015*

Des problèmes liés aux services {{site.data.keyword.Bluemix}} peuvent survenir :
par exemple, une erreur de dépassement de délai d'attente de la passerelle peut se produire lorsque vous supprimez une instance de service. Toutefois, dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{:shortdesc}

## Un message d'erreur de dépassement du délai d'attente de la passerelle s'affiche lorsque vous supprimez une instance de service
{: #ts_service_broker}

Il se peut que vous receviez un message d'erreur lorsque vous tentez de supprimer une instance de service qui a déjà été supprimée du contrôleur de cloud.
{:shortdesc}


Lorsque vous tentez de supprimer une instance de service, le message d'erreur suivant du courtier de services, qui indique le dépassement du
délai d'attente de la passerelle, s'affiche : ```Gateway timeout```.
{: tsSymptoms}


Ce problème se produit lorsque l'instance de service a déjà été supprimée du contrôleur de cloud.
{: tsCauses}


Pour résoudre le problème, créez une instance de service portant ce nom de service et liez-la à vos applications. Vous pourrez ensuite supprimer l'instance de service et les applications utilisant ce service.   
{: tsResolve}


