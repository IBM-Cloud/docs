---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}
# Configuration d'un badge, d'un son, d'un contenu et d'un badge iOS

{: #badge-sound-payload}

Configurez un badge iOS, un son et un contenu JSON supplémentaire.


1. Dans le tableau de bord Push Notifications, accédez à l'onglet **Notifications**.
2. Accédez à la section des **zones facultatives** pour configurer les fonctions de notification push ci-après. Badge ios, son et contenu supplémentaire. 

	a. **iOS Badge** - Pour les périphériques iOS, numéro à afficher pour le badge de l'icône d'application. Si cette propriété manque, le badge n'est pas changé. Pour supprimer le badge, associez cette propriété à la valeur 0.

	b. **Fichier son** - Entrez une chaîne qui désigne le fichier son dans votre application mobile. Dans le contenu, spécifiez le nom de
chaîne du fichier son à utiliser.


	Android

	```
	"settings": {
	     "gcm" : {
	     "sound":"tt.wav",
	  }
	 }  
	```

	iOS

	```
	"settings": {
	     "apns" : {
	      "badge": 10,
	      "sound": "tt.wav",
	  }
	}
	``` 		
**Contenu supplémentaire** - Ce contenu peut être représenté par n'importe quelle paire clé-valeur et doit être un objet JSON que
vous voulez envoyer avec la notification push.

	```
	{"clé":"valeur", "clé2":"valeur2"}
	```
