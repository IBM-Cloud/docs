---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Interface de ligne de commande d'IBM VPN
*Dernière mise à jour : 03 mai 2016*

Vous pouvez utiliser l'interface de ligne de commande pour configurer et gérer votre service IBM® Virtual Private Network (VPN). L'interface de ligne de commande d'IBM VPN est un
plug-in qui est utilisé avec le plug-in de l'interface de ligne de commande de Cloud Foundry. Le plug-in est disponible pour les systèmes d'exploitation Windows, MAC et Linux. Assurez-vous d'utiliser celui qui vous correspond.

Avant de commencer, installez l'interface de ligne de commande de Cloud Foundry. Pour plus de détails, voir
[Interface de ligne de commande de Cloud Foundry](https://console.{DomainName}/docs/cli/downloads.html). 

##Installation du plug-in de l'interface de ligne de commande d'IBM VPN
**Remarque :** Si une version précédente du plug-in de l'interface de ligne de commande d'IBM VPN est installée, vous devez d'abord la désinstaller. Utilisez la
commande : 

```
cf uninstall-plugin vpn
```  

**Installation locale**

1. Téléchargez le plug-in IBM VPN correspondant à votre plateforme du [référentiel de plug-in de l'interface de ligne de commande IBM
Bluemix](http://plugins.ng.bluemix.net).
2. Installez le plug-in IBM VPN à l'aide de la commande suivante :
**Remarque :** Accédez à l'emplacement du plug-in VPN ou spécifiez le chemin d'accès à l'emplacement du plug-in.  

	**Pour les systèmes d'exploitation MS Windows :**

	```
	cf install-plugin vpn_windows64.exe
	```  

	**Pour les systèmes d'exploitation Apple MAC :**

	```
	cf install-plugin vpn_mac_os_amd64
	```  

	**Pour les systèmes d'exploitation Linux :**

	```
	cf install-plugin vpn_linuxamd64
	```  


**Installation depuis le référentiel Bluemix**  

1. Ajoutez le référentiel Bluemix aux référentiels de l'interface de ligne de commande de Cloud Foundry. Utilisez la commande suivante :

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. Exécutez la commande suivante :  

	```
	cf install-plugin vpn -r bluemix
	```
##Liste des commandes du service IBM VPN

### cf vpn-create connection

Crée une connexion VPN.

```
cf vpn-create connection <connection name> -g <gateway name> -k <preshared key> -subnets ["<subnet/mask>"] -cip <customer gateway IP address> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### Paramètres
{: #p1}

**connection name :**
Nom de la connexion.

**gateway name :** Nom de la passerelle.

**-k :**
Clé pré-partagée.

**subnet/mask :**
Adresse de sous-réseau distante au format CIDR. 

**customer gateway IP address :**
Adresse IP du noeud final distant du tunnel VPN. 

##### Paramètres facultatifs :
{: #op1}

**-d :** Description des paramètres spécifiés.

**-peer_id :** ID de l'homologue distant. Autre noeud final du tunnel VPN.

**-admin_state :** Etat de la connexion VPN. Valeurs : UP ou DOWN.

**-dpd-action :** Action à effectuer lorsque l'homologue est identifié comme non opérationnel. Valeurs : hold ; clear ; disabled ; restart ; restart-by-peer. Valeur par défaut : hold

**-gateway_ip :** Adresse IP du noeud final du tunnel VPN local. 

**-i :** Etat de l'initiateur. Valeur par défaut : bi-directional.

**-dpd-timeout :** Valeur du délai d'attente (en secondes) au bout duquel la session est terminée.  Plage : 6 à 86400 secondes. Valeur par défaut : 120 secondes. La
valeur du délai d'attente de l'intervalle de signal de présence doit être supérieure à la valeur de l'intervalle de signal de présence.

**-dpd-interval :** Intervalle de signal de présence, en secondes. Envoyez des messages d'état actif à la fréquence
configurée afin de vérifier l'état opérationnel de l'homologue. Plage : 5 à 86399 secondes. Valeur par défaut : 15 secondes

**-ike :** Nom de la règle IKE.

**-ipsec :** Nom de la règle IPSec.


### cf vpn-create ike

Crée une règle IKE (Internet Key Exchange).

```
cf vpn-create ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Paramètres
{: #p2}

**policy name :**
Nom de la règle IKE.

**gateway name :** Nom de la passerelle. 

##### Paramètres facultatifs :
{: #op2}

**-d :** Description des paramètres spécifiés.

**-pfs :** Identificateur de groupe Diffie-Hellman (DH). Valeurs : Group2 ; Group5 ; Group14. Valeur par défaut : Group2 

**-e :** Algorithme de chiffrement. Valeurs : aes-128 ; aes-192 ; aes-256 ; 3des. Valeur par défaut : aes-128

**-lv :** Valeur de durée de vie de l'association de sécurité IKE. Plage : 60 à 86400 secondes. Valeur par défaut : 86400 secondes


### cf vpn-create ipsec

Crée une règle IPSec (Internet Protocol Security).

```
cf vpn-create ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Paramètres
{: #p3}

**policy name :**
Nom de la règle IPSec. 

**gateway name :** Nom de la passerelle. 

##### Paramètres facultatifs :
{: #op3}

**-d :** Description des paramètres spécifiés.

**-pfs :** Identificateur de groupe Diffie-Hellman (DH). Valeurs : Group2 ; Group5 ; Group14. Valeur par défaut : Group2  

**-e :** Algorithme de chiffrement. Valeurs : aes-128 ; aes-192 ; aes-256 ; 3des. Valeur par défaut : aes-128

**-lv:** Valeur de durée de vie de l'association de sécurité. Plage : 60 à 86400 secondes. Valeur par défaut : 3600 secondes

### cf vpn-create gateway

Crée une passerelle VPN.

```
cf vpn-create gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### Paramètres
{: #p4}

**gateway name :** Nom de la passerelle.

**-t :** Conteneurs pour lesquels vous souhaitez activer le service. Valeurs : allSingleContainers ; allContainerGroups ; allContainers. Valeur par défaut : aucune
valeur par défaut. Vous devez spécifier un type. 

#####Paramètres facultatifs :
{: #op4}

**-gateway_ip :** Adresse IP de la passerelle. 

**-subnets :** Adresse de sous-réseau au format CIDR. 

### cf vpn-show gateways

Affiche des informations sur les passerelles actuelles.

```
cf vpn-show gateways
```
### cf vpn-show ikes

Affiche des informations sur les connexions IKE (Internet Key Exchange) en cours.

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

Affiche des informations sur les connexions IPSec (Internet Protocol Security) en cours.

```
cf vpn-show ipsecs
```
### cf vpn-show connections

Affiche des informations sur toutes les connexions en cours.

```
cf vpn-show connections
```
### cf vpn-show ike

Affiche des informations sur une connexion IKE (Internet Key Exchange).

```
cf vpn-show ike <policy name>
```
### cf vpn-show ipsec

Affiche des informations sur une connexion IPSec (Internet Protocol Security).

```
cf vpn-show ipsec <policy name>
```
### cf vpn-show gateway

Affiche les informations de connexion d'une passerelle.

```
cf vpn-show gateway <gateway name>
```
### cf vpn-show connection

Affiche toutes les informations sur une connexion particulière.

```
cf vpn-show connection <connection name>
```
### cf vpn-delete

Supprime une connexion, une règle ou une passerelle existante.

```
cf vpn-delete ike <policy name>
```

```
cf vpn-delete ipsec <policy name>
```

```
cf vpn-delete connection <connection name>
```

```
cf vpn-delete gateway <gateway name>
```


### cf vpn-update connection

Met à jour une connexion VPN.

```
cf vpn-update connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### Paramètres
{: #p5}

**connection name :**
Nom de la connexion.


##### Paramètres facultatifs :
{: #op5}

**gateway name :** Nom de la passerelle.

**customer gateway IP address :**
Adresse IP du noeud final distant du tunnel VPN. 

**subnet/mask :**
Adresse de sous-réseau au format CIDR. 

**-k :**
Clé pré-partagée.

**-d :** Description des paramètres spécifiés.

**-peer_id :** ID de l'homologue distant. Autre noeud final du tunnel VPN.

**-admin_state :** Etat de la connexion VPN. Valeurs : UP ou DOWN.

**-dpd-action :** Action à effectuer lorsque l'homologue est identifié comme non opérationnel. Valeurs : hold ; clear ; disabled ; restart ; restart-by-peer. Valeur par défaut : hold

**-gateway_ip :** Adresse IP du noeud final du tunnel VPN local. 

**-i :** Etat de l'initiateur. Valeur par défaut : bi-directional.

**-dpd-timeout :** Valeur de délai d'attente (en secondes) au bout duquel la session est terminée. Plage : 6 à 86400 secondes. Valeur par défaut : 120
secondes

**-dpd-interval :** Intervalle de signal de présence, en secondes. Envoyez des messages d'état actif à la fréquence
configurée afin de vérifier l'état opérationnel de l'homologue. Plage : 5 à 86399 secondes. Valeur par défaut : 15 secondes

**-ike :** Nom de la règle IKE.

**-ipsec :** Nom de la règle IPSec.


### cf vpn-update ike

Met à jour une règle IKE (Internet Key Exchange).

```
cf vpn-update ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Paramètres
{: #p6}

**policy name :**
Nom de la règle IKE. 

##### Paramètres facultatifs :
{: #op6}

**gateway name :** Nom de la passerelle. 

**-d :** Description des paramètres spécifiés.

**-pfs :** Identificateur de groupe Diffie-Hellman (DH). Valeurs : Group2 ; Group5 ; Group14. Valeur par défaut : Group2 

**-e :** Algorithme de chiffrement. Valeurs : aes-128 ; aes-192 ; aes-256 ; 3des. Valeur par défaut : aes-128

**-lv :** Valeur de durée de vie de l'association de sécurité IKE. Plage : 60 à 86400 secondes. Valeur par défaut : 86400 secondes


### cf vpn-update ipsec

Met à jour une règle IPSec (Internet Protocol Security).

```
cf vpn-update ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Paramètres
{: #p7}

**policy name :**
Nom de la règle IPSec.


##### Paramètres facultatifs :
{: #op7}

**gateway name :** Nom de la passerelle.

**-d :** Description des paramètres spécifiés.

**-pfs :** Identificateur de groupe Diffie-Hellman (DH). Valeurs : Group2 ; Group5 ; Group14. Valeur par défaut : Group2 

**-e :** Algorithme de chiffrement. Valeurs : aes-128 ; aes-192 ; aes-256 ; 3des. Valeur par défaut : aes-128

**-lv:** Valeur de durée de vie de l'association de sécurité. Plage : 60 à 86400 secondes. Valeur par défaut : 3600 secondes

### cf vpn-update gateway

Met à jour une passerelle VPN.

```
cf vpn-update gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### Paramètres
{: #p8}

**gateway name :** Nom de la passerelle.

#####Paramètres facultatifs :
{: #op8}

**-t :** Conteneurs pour lesquels vous souhaitez activer le service. Valeurs : allSingleContainers ; allContainerGroups ; allContainers. Valeur par défaut : aucune
valeur par défaut. Vous devez spécifier un type.

**-gateway_ip :** Adresse IP de la passerelle. 

**-subnets :** Adresse de sous-réseau au format CIDR. 

# Liens associés
## Informations générales  
{: #general}  
* [Service IBM VPN](../../../services/vpn/index.html)
* [Interface de ligne de commande de Cloud Foundry](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
