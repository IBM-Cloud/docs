---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Modification de l'application de démarrage sur {{site.data.keyword.Bluemix_short}}
{: #modifying_starter_app}

Vous pouvez modifier l'application de démarrage, puis la redéployer dans {{site.data.keyword.Bluemix_short}} pour afficher les résultats.
{:shortdesc}


Une modification simple consiste à augmenter ou retirer la limite d'événements dans l'application de démarrage pour qu'elle s'exécute plus longtemps.

1. Ouvrez app.js dans un éditeur de texte ou un environnement de développement. 
2. Modifiez la variable eventTarget ou supprimez cette ligne pour retirer entièrement la limite d'événements.
	 <pre><code>var eventTarget = 100;</code></pre>
3. Si vous voulez retirer la limite d'événements, vous devez aussi supprimer l'instruction if suivante :
	 <pre><code>  
	if (eventCount >= eventTarget) {
		    status_step[3] = "Completed";
		    console.log("\nTarget event count has been reached.  Geospatial Analytics service will be stopped.\n");
		    callback(null, null);
		    } 
	</code></pre> 
4. redéployez votre application modifiée sur {{site.data.keyword.Bluemix_short}} à l'aide de la commande cf push.
	 <pre><code>  
	cf push myapp
	</code></pre>
5. Entrez l'adresse URL ou "route" de votre application dans votre navigateur ou lancez votre application depuis le tableau de bord {{site.data.keyword.Bluemix_short}}.
