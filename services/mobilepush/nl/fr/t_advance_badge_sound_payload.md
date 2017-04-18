---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des {{site.data.keyword.mobilepushshort}} avancées
Dernière mise à jour : 23 janvier 2017
{: .last-updated}

Configurez un badge iOS, un son, un contenu JSON supplémentaire, des notifications interactives et la conservation des notifications.

## Configuration d'un son, d'un contenu et d'un badge iOS
{: #badge-sound-payload}

Configurez un badge, un son et un contenu JSON supplémentaire iOS.

1. Dans le tableau de bord {{site.data.keyword.mobilepushshort}}, accédez à l'onglet **Notifications**.
2. Accédez à la section des zones facultatives pour configurer les fonctions {{site.data.keyword.mobilepushshort}}. 
	- **Fichier son** - Entrez une chaîne pour pointer vers le fichier son dans votre application mobile. Dans le contenu, spécifiez le nom de chaîne du fichier son à utiliser.
	- **Badge iOS** - Pour les appareils iOS, numéro à afficher comme badge de l'icône d'application. Si cette propriété manque, le badge n'est pas changé. Pour supprimer le badge, associez cette propriété à la valeur 0.
	
### Android

Ajoutez votre fichier son dans le répertoire `res/raw` de votre application Android. Lors de l'envoi de la notification, ajoutez le nom du fichier son dans la zone son de {{site.data.keyword.mobilepushshort}}.

```
"settings":{
     "gcm" : {
     "sound":"tt.wav",
	  }
 }  
```
    {: codeblock}	
	
### iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	      "sound": "tt.wav",
	  }
}
``` 
	{: codeblock}
		
**Contenu supplémentaire** - Ce contenu peut être représenté par toute paire clé-valeur et doit être un objet JSON que vous voulez envoyer avec la notification de type {{site.data.keyword.mobilepushshort}}.

```
{"clé":"valeur", "clé2":"valeur2"}
```
	{: codeblock}

## Conservation des notifications Android 
{: #hold-notifications-android}

Quand votre application passe en arrière-plan, vous pouvez vouloir que le service {{site.data.keyword.mobilepushshort}} conserve les notifications qui sont envoyées à cette application. Pour conserver des notifications, appelez la méthode hold() dans la méthode onPause() de l'activité qui traite les
notifications de type {{site.data.keyword.mobilepushshort}}.

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}

    
