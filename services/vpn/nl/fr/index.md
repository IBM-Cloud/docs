---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Initiation à {{site.data.keyword.vpn_short}}
{: #vpn}  
*Dernière mise à jour : 09 mai 2016*

Le service {{site.data.keyword.vpn_full}} for Bluemix&reg; est disponible pour accéder aux conteneurs IBM (conteneurs Docker) en toute sécurité au sein de l'environnement cloud IBM Bluemix. Vous pouvez utiliser l'environnement cloud IBM Bluemix comme une extension de votre centre de données d'entreprise. Vous pouvez également établir une connexion avec les serveurs SoftLayer à l'aide du service IBM VPN.
{:shortdesc}

Avant de commencer, veillez à disposer d'un conteneur IBM Docker prêt à être utilisé. Voir [IBM Containers for Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html) pour plus de détails sur la création et la gestion des conteneurs IBM.  

Pour commencer, sélectionnez la vignette de l'instance de service **Virtual Private Network** dans le tableau de bord Bluemix. Procédez comme suit :

1. Configurez la passerelle {{site.data.keyword.vpn_short}} en sélectionnant **CREATE GATEWAY**. Une passerelle par défaut est créée. Si nécessaire, éditez la configuration de la passerelle comme indiqué dans les étapes suivantes.  
{: #gateway}  

  1. Sélectionnez **EDIT**.  
  2. Spécifiez le nom de la passerelle.  
  3. Sélectionnez le conteneur et le groupe de conteneurs  avec lesquels vous souhaitez utiliser le service VPN. **Remarque :** Les sous-réseaux privés du conteneur et du groupe de conteneurs sont présélectionnés pour que vous puissiez y accéder via la connexion VPN.
  4. Sélectionnez **SAVE**.  

 Vous pouvez utiliser les règles IKE et IPSec ou configurer des règles personnalisées. Si vous souhaitez utiliser les règles par défaut, passez à l'étape 4.

2. Configurez la règle IKE en sélectionnant l'onglet **IKE & IPSec Policies**.
  1. Sélectionnez **ADD NEW**.  
  2. Spécifiez les détails suivants :
	* **Name** : Nom de la règle IKE
	* **Authorization Algorithm** : sha1 ; ne peut pas être changé.  
	* **Encryption Algorithm** : Sélectionnez un algorithme de chiffrement dans la liste déroulante. Valeurs : aes-128 (valeur par défaut), aes-192, aes-256, 3des
	* **Key Lifetime** : Valeur de la durée de vie (en secondes) de l'association de sécurité IKE. Plage : 60-86400. Valeur par défaut : 86400
	* **PFS** : Identificateur de groupe Diffie-Hellman (DH). Valeurs : Group2, Group5, Group14. Valeur par défaut : Group2
	* **Negotiation Mode** : Main ; ne peut pas être changé
	* **Version** : IKEV1 ; ne peut pas être changé
  3. Sélectionnez **SAVE**.

3. Configurez la règle IPSec :
  1. Sélectionnez **ADD NEW**.  
  2. Spécifiez les détails suivants :
  	* **Name** : Nom de la règle IPSec  
  	* **Authorization Algorithm** : sha1 ; ne peut pas être changé.  
  	* **Encryption Algorithm** : Sélectionnez un algorithme de chiffrement dans la liste déroulante. Valeurs : aes-128 (valeur par défaut), aes-192, aes-256, 3des
  	* **Key Lifetime** : Valeur de la durée de vie (en secondes) de l'association de sécurité. Plage : 60-86400. Valeur par défaut : 3600
  	* **PFS** : Identificateur de groupe Diffie-Hellman (DH). Valeurs : Group2, Group5, Group14. Valeur par défaut : Group2
  	* **Transform Protocol** : ESP ; ne peut pas être changé
  	* **Encapsulation Mode** : Tunnel ; ne peut pas être changé
  3. Sélectionnez **SAVE**.  

4. Fournissez les détails pour établir la connexion entre votre centre de données, ou la passerelle VPN du serveur SoftLayer, et la passerelle IBM VPN.  
{: #site}  

  1. Sélectionnez l'onglet **Gateway Appliance**.
  2. Sélectionnez **Create Connection** dans la section **Site Connections**.
  3. Spécifiez les détails de connexion pour le site suivants :  
  	* **Name** : Nom de la connexion  
  	* **Description** : Description de la connexion (facultatif)  
  	* **Preshared Key String** : Clé pré-partagée (valeur confidentielle) à utiliser pour l'authentification
  	* **Admin State** : Statut de la connexion VPN. Sélectionnez une valeur dans la liste déroulante : UP ou DOWN. Valeur par défaut : UP  
  	* **Customer Gateway IP** : Adresse IP de noeud final distant du tunnel VPN  
  	* **Customer Subnet** : Adresse de sous-réseau distant au format CIDR. Sélectionnez le signe plus pour ajouter un autre sous-réseau.
  4. (Facultatif) Configurez les paramètres avancés suivants :  
  	* **IKE Policy** : Sélectionnez la règle IKE.  
  	* **Keep Alive Interval** : Intervalle de signal de présence, en secondes. Envoyez des messages d'état actif à la fréquence configurée afin de vérifier l'état opérationnel de l'homologue. Valeur par défaut : 15. Plage : 5-86399
  	* **Action on dead peer** : Action à effectuer lorsque l'homologue est identifié comme non opérationnel.  
    	Valeurs : 
  		* hold (valeur par défaut) : L'association de sécurité est suspendue 
  		* clear : L'association de sécurité est supprimée
  		* disabled : L'association de sécurité est désactivée
  		* restart : L'association de sécurité est renégociée
  		* restart-by-peer : Toutes les associations de sécurité avec l'homologue identifié comme non opérationnel sont renégociées  
  	* **IPSec Policy** : Sélectionnez la règle IPSec.
  	* **Keep Alive Timeout** : Valeur de délai d'attente (en secondes) au bout duquel la session est terminée. Valeur par défaut : 120. Plage : 6-86400. La valeur du délai d'attente de l'intervalle de signal de présence doit être supérieure à la valeur de l'intervalle de signal de présence.
  5. Sélectionnez **SAVE**.

  **Remarque :** Lorsque la connexion est en cours d'établissement, le statut de la connexion s'affiche comme étant ***pending create***. Lorsque vous voyez ce statut, actualisez l'écran plusieurs fois jusqu'à ce que la connexion soit active.

**Important :** Si vous utilisez une application Web, vous devez lier l'application Web au conteneur Docker que vous utilisez. Cette liaison est obligatoire pour que le trafic s'écoule via le tunnel VPN IPSec.

**Important :** Le service IBM VPN fonctionne actuellement en mode répondeur. Pour initier la connexion VPN, un paquet de données doit être envoyé de la passerelle IBM VPN de votre centre de données sur site ou du serveur SoftLayer. Une fois la connexion VPN établie, le trafic peut s'écouler dans l'une ou l'autre des directions entre les noeuds finaux de la connexion VPN.

 
# rellinks
## samples 
{: #samples}  
* [Exemple de configuration de la passerelle strongSwan sur site](vpn_onpremises.html#strongswan){: new_window}
* [Exemple de configuration de la passerelle Vyatta sur site](vpn_onpremises.html#vyatta){: new_window}
* [Exemple de configuration GaaS SoftLayer sur site](vpn_onpremises.html#gaas){: new_window}
* [Exemple de configuration ASA Cisco sur site](vpn_onpremises.html#cisco){: new_window}

## api  
{: #api}  
* [API IBM VPN RESTful](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## Informations générales  
{: #general}  
* [Interface de ligne de commande IBM VPN](../../cli/plugins/vpn/index.html){: new_window}
* [FAQ - IBM VPN](vpn_faq.html#vpn_faq){: new_window}
* [Fiche des prix IBM Bluemix](https://console.{DomainName}/pricing/){: new_window}
* [Prérequis IBM Bluemix](https://developer.ibm.com/bluemix/support/#prereqs)
