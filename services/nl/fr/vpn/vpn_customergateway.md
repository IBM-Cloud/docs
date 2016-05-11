---

copyright :

  années : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuration de la passerelle sur votre centre de données ou serveur SoftLayer
{: #vpn_yourdatacenter}
*Dernière mise à jour : 17 mars 2016*

Vous avez besoin d'une passerelle VPN IPSec sur votre centre de données ou serveur SoftLayer pour établir une connexion sécurisée avec le service {{site.data.keyword.vpn_short}}. Les
configurations de passerelles VPN suivantes sont requises sur votre centre de données ou serveur SoftLayer :

* Activez uniquement la traversée NAT (Network Address Translation) sur votre passerelle VPN si votre passerelle VPN est derrière le NAT. 
* Utilisez la même clé pré-partagée que celle utilisée lors de la configuration du service IBM VPN.
* Ajoutez le sous-réseau suivant comme sous-réseau distant :
	* Si vous avez créé des conteneurs uniques dans l'espace IBM Bluemix, ajoutez 172.31.0.0/16.
	* Si vous avez créé des groupes de conteneurs dans l'espace IBM Bluemix, ajoutez 172.30.0.0/16.
	* Si vous avez créé des conteneurs uniques et des groupes de conteneurs dans l'espace IBM Bluemix, ajoutez 172.31.0.0/16 et 172.30.0.0/16.
* Vérifiez que le chiffrement, l'authentification et les paramètres du groupe PFS sont les mêmes sur la passerelle IBM VPN et sur votre passerelle VPN.
