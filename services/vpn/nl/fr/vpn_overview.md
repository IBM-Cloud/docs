---

copyright :

  années : 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# A propos d'{{site.data.keyword.vpn_short}}
{: #vpn_overview}  
*Dernière mise à jour : 17 mars 2016*

Le service {{site.data.keyword.vpn_full}} (VPN) fournit un canal de communication sécurisé entre le centre de données de votre entreprise et vos ressources dans
l'environnement de cloud IBM Bluemix&reg;. La connexion est établie via Internet.
{:shortdesc}

Le service {{site.data.keyword.vpn_short}} offre les fonctions suivantes :  
##Sécurité 
Le service IBM VPN utilise le protocole IPSec (Internet Protocol Security) standard pour authentifier et chiffrer la communication IP entre le centre de données de votre entreprise
et l'environnement de cloud IBM Bluemix. IPSec offre une authentification d'homologue au niveau du réseau, une intégrité des données et une confidentialité des données (chiffrement).

Le service IBM VPN prend en charge les protocoles IPSec et les transformations suivant(e)s :

* Algorithme d'authentification :
	* HMAC-SHA1-96 ; la longueur de la clé partagée est de 160 bits (valeur par défaut)  
* Algorithme de chiffrement :
	* 3DES-CBC ; la longueur de la clé partagée est de 192 bits
	* AES-CBC ; les longueurs de la clé partagée sont de 128 (valeur par défaut), 192 et 256 bits
* Protocoles d'authentification et de chiffrement :
	* Les protocoles AH (Authentication Header) et ESP (Encapsulating Security Payload) sont pris en charge. AH est uniquement utilisé pour l'authentification. ESP est utilisé pour
l'authentification et le chiffrement.
* Echange de clés Diffie-Hellman (DH) IKEv1 groupes 2 (valeur par défaut), 5 et 14

Le service IBM VPN prend en charge le mode tunnel IPSec. Dans ce mode, IPSec protège l'ensemble du paquet IP d'origine. IPSec chiffre le paquet, l'encapsule dans un nouveau paquet
IP et renvoie le nouveau paquet à l'homologue IPSec. 

Le service IBM VPN utilise l'échange de clés Diffie-Hellman et la clé pré-partagée pour sécuriser l'association entre deux homologues. L'authentification échoue si l'une des deux
parties ne fournit pas la clé pré-partagée. 
 
Le service IBM VPN est conforme aux demandes de commentaires (RFC) IETF suivantes :

* RFC 2407, 2408 et 2409 pour IKEv1
* RFC 4301 pour IPv4 security   
* RFC 4302 pour IPv4 Authentication Header  
* RFC 4303 pour IPv4 Encapsulating Security Payload (ESP)  
* RFC 2104 HMAC et RFC 2404 HMAC-SHA-1-96 pour l'authentification  
* RFC 2451 3DES-CBC ; RFC 3602 AES128-CBC, AES192-CBC et AES256-CBC pour le chiffrement
##Simplicité
Vous pouvez créer le service IBM VPN à l'aide d'une interface graphique simple et intuitive. Vous pouvez spécifier l'adresse IP de votre passerelle et les sous-réseaux de votre
centre de données. Vous pouvez utiliser les règles IPSec et IKE par défaut ou personnaliser les règles en fonction de vos besoins.  
##Gestion
Vous pouvez gérer le service IBM VPN à l'aide d'une interface graphique, d'une [interface de ligne de commande](../../cli/plugins/vpn/index.html)
ou à l'aide d'[interfaces API](https://new-console.ng.bluemix.net/apidocs/101).

