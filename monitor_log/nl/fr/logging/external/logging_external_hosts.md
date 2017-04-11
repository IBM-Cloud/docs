---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Configuration d'hôtes de journaux externes
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} conserve une quantité limitée d'informations de journal en mémoire. Lorsque des informations sont journalisées, les anciennes informations sont remplacées par les informations plus récentes. Pour conserver toutes les informations de journal, vous pouvez sauvegarder vos journaux sur un hôte de journaux externe, par exemple dans un service de gestion des journaux tiers ou sur un autre hôte.
{:shortdesc}

Pour transférer les journaux de votre application et du système vers un hôte de journaux externe, procédez comme suit :

  1. Déterminez le noeud final de journalisation.

	 Vous pouvez envoyer des journaux à un regroupeur de journaux tiers, comme Papertrail, Splunk ou Sumologic. Vous pouvez aussi envoyer des journaux à un hôte syslog, un hôte syslog chiffré avec TLS (Transport Layer Security) ou un noeud final HTTPS POST. Les méthodes d'obtention de noeuds finaux de journalisation varient selon l'hôte de journaux.

  2. Créez une instance de service fournie par l'utilisateur.

	 Utilisez la commande `cf create-user-provided-service` (ou sa version courte `cups`) pour créer une instance de
service fournie par l'utilisateur :
	 ```
	 cf create-user-provided-service <nom_service> -l <noeud_final_journalisation>
	 ```
	 &lt;nom_service&gt;

	 Nom de l'instance de service fournie par l'utilisateur.

	 &lt;noeud_final_journalisation&gt;

	 Noeud final de journalisation auquel {{site.data.keyword.Bluemix_notm}} envoie des journaux. Reportez-vous au tableau suivant pour remplacer *noeud_final_journalisation* par la valeur appropriée :

	 <table>
	 <caption>Tableau 1. Valeurs de noeud final de journalisation</caption>
     <thead>
     <tr>
     <th>Noeud final de journalisation</th>
     <th>Commande</th>
	 <th>Remarques</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>hôte syslog</td>
     <td>`cf cups my-logs -l syslog://HOTE:PORT`</td>
	 <td>Par exemple, pour activer la journalisation dans Papertrail, entrez `cf cups my-logs -l syslog://<url_papertrail>`. Remplacez `<url_papertrail>` par l'adresse URL de votre noeud final de journalisation pour Papertrail.</td>
     </tr>
	 <tr>
     <td>hôte syslog-tls</td>
     <td>`cf cups my-logs -l syslog-tls://HOTE:PORT`</td>
	 <td>Le certificat doit être considéré comme digne de confiance par une autorité de certification. N'utilisez pas de certificat autosigné.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOTE:PORT`</td>
	 <td>Ce noeud final doit se trouver sur l'Internet public et {{site.data.keyword.Bluemix_notm}} doit pouvoir y accéder.</td>
     </tr>
     </tbody>
     </table>
  3. Liez l'instance de service à votre application.

	 Utilisez la commande suivante pour lier l'instance de service à votre application :

	 ```
	 cf bind-service <nom_app> <nom_service>
	 ```
	 &lt;nom_app&gt;

	 Nom de votre application.

	 &lt;nom_service&gt;

	 Nom de l'instance de service fournie par l'utilisateur.

  4. Reconstituez l'application. Entrez `cf restage nom_app` pour que les modifications soient appliquées.

