---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Mode bac à sable et mode production
{: #push-sandboxandproduction-modes}
Dernière mise à jour : 11 janvier 2017
{: .last-updated}

Vous pouvez utiliser {{site.data.keyword.mobilepushshort}} sous l'un des deux modes suivants : bac à sable ou production. Le bac à sable est un environnement de test autonome dans lequel vous pouvez développer et tester l'intégration d'API Push avec le service Push
d'application serveur. 

Configurez les modes bac à sable et production à l'aide du tableau de bord Push. Vous pouvez permuter entre le mode d'opération bac à sable et le mode production du service push à l'aide de l'[API REST Push](https://mobile.{DomainName}/imfpush/){: new_window}. Par défaut, le mode bac à sable est activé. Toutefois, lors du passage d'un mode à l'autre, balises, les appareils et les abonnements ne sont pas partagés.

Lorsque vous êtes prêt à déployer l'application dans un environnement de production, sélectionnez le mode PRODUCTION à l'aide de l'[API REST Push](https://mobile.{DomainName}/imfpush/){: new_window}. 

Pour changer le mode de fonctionnement du service push et passer du mode bac à sable au mode production :

1. Utilisez l'appel d'API REST PUT ApplicationID Settings
2. Dans le corps JSON, vérifiez que le mode a été changé en utilisant l'appel d'API [REST GET ApplicationID Settings](https://mobile.{DomainName}/imfpush/){: new_window}. La réponse attendue est "mode": "PRODUCTION"
```{ 
    "mode": "PRODUCTION"
 }
```
	{: codeblock}
1. Une fois que vous avez changé de mode d'environnement, relancez l'exécution de votre code client de manière à enregistrer votre appareil en mode PRODUCTION.

Pour plus d'informations sur l'API REST, voir [Utilisation des API REST](t_restapi.html).
