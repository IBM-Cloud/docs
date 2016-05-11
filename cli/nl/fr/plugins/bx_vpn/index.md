---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Plug-in de l'interface de ligne de commande Bluemix pour le réseau privé virtuel

*Dernière mise à jour :* 18 janvier 2016

*Version :* 0.1.5

Vous pouvez utiliser le plug-in de l'interface de ligne de commande Bluemix pour le réseau privé virtuel afin de configurer et de gérer votre
service IBM Virtual Private Network (VPN).
{:shortdesc}

Les informations ci-après répertorient toutes les commandes qui sont prises en charge par le plug-in de l'interface de ligne de commande Bluemix pour
le réseau privé virtuel, ainsi que leurs noms, leurs options, leur syntaxe, les éléments prérequis, leurs descriptions et des exemples.

**Remarque :** la zone *Prérequis* répertorie les actions qui sont requises avant l'utilisation de la commande. Il
peut s'agir d'une ou de plusieurs des actions suivantes :
<dl>
<dt>**Noeud final**</dt>
<dd>Un noeud final d'API doit être défini via `bluemix api` avant l'utilisation de la commande.</dd>
<dt>**Connexion**</dt>
<dd>La connexion avec la commande `bluemix login` est requise avant l'utilisation de cette commande.</dd>
<dt>**Cible**</dt>
<dd>La commande `bluemix target` doit être utilisée pour définir une organisation et un espace avant l'utilisation de cette commande.</dd>
</dl>


## bluemix vpn connection-create
Crée une connexion de réseau privé virtuel.

```
bluemix vpn connection-create NOM_CONNEXION -g NOM_PASSERELLE -k CLE_PRE-PARTAGEE -subnets "SOUS-RESEAU/MASQUE" -cip
ADRESSE_IP_PASSERELLE_CLIENT [-d DESCRIPTION][-peer_id ID_HOMOLOGUE] [-admin_state ETAT_ADMIN][-dpd-action ACTION]
[-gateway_ip ADRESSE_IP][-i ETAT_INITIATEUR] [-dpd-timeout VALEUR][-dpd-interval VALEUR] [-ike
NOM][-ipsec NOM]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_CONNEXION* (requis) : nom de la connexion.

-g *NOM_PASSERELLE* (requis) : nom de la passerelle.

-k *CLE_PRE-PARTAGEE* (requis) : clé pré-partagée.

-subnets "*SOUS-RESEAU*/*MASQUE*" (requis) : adresse de sous-réseau distant au format CIDR.

-cip *ADRESSE_IP_PASSERELLE_CLIENT* (requis) : adresse IP de noeud final distant du tunnel VPN.

-d *DESCRIPTION* (facultatif) : description des paramètres spécifiés.

-peer_id *ID_HOMOLOGUE* (facultatif) : ID de l'homologue distant. Autre noeud final du tunnel VPN.

-admin_state *ETAT_ADMIN* (facultatif) : statut de la connexion de réseau privé virtuel. Les valeurs admises sont `UP`
et `DOWN`.

-dpd-action *ACTION* (facultatif) : action à effectuer lorsque l'homologue est identifié comme non opérationnel. Les valeurs admises sont
`hold`, `clear`, `disabled`, `restart` et `restart-by-peer`. La
valeur par défaut est `hold`.

-gateway_ip *ADRESSE_IP* (facultatif) : adresse IP du noeud final de tunnel VPN local.

-i *ETAT_INITIATEUR* (facultatif) : état de l'initiateur. La valeur par défaut est `bi-directional`.

-dpd-timeout *VALEUR* (facultatif) : valeur de délai en secondes au bout duquel la session est terminée. Plage : 6 à 86400 secondes. La
valeur par défaut est `120` secondes.

-dpd-interval *VALEUR* (facultatif) : intervalle de signal de présence en secondes. Envoyez des messages d'état actif à la fréquence
configurée afin de vérifier l'état opérationnel de l'homologue. Plage : 5 à 86399 secondes. La valeur par défaut est `15` secondes.

-ike *NOM* (facultatif) : nom de la règle IKE (Internet Key Exchange).

-ipsec *NOM* (facultatif) : nom de la règle IPSec (Internet Protocol Security).

**Exemples** :

Créez une connexion de réseau privé virtuel dont le nom est `ma_connexion` :
```
bluemix vpn connection-create ma_connexion -g ma_passerelle -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
Crée une règle IKE (Internet Key Exchange).

```
bluemix vpn ike-create NOM_REGLE -g NOM_PASSERELLE [-d DESCRIPTION][-pfs GROUPE] [-e
ALGORITHME_CHIFFREMENT][-lv VALEUR_DUREE_VIE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_REGLE* (requis) : nom de la règle IKE (Internet Key Exchange).

-g *NOM_PASSERELLE* (requis) : nom de la passerelle.

-d *DESCRIPTION* (facultatif) : description des paramètres spécifiés.

-pfs *GROUPE* (facultatif) : identificateur de groupe Diffie-Hellman (DH). Les valeurs admises sont `Group2`,
`Group5` et `Group14`. La valeur par défaut est `Group2`.

-e *ALGORITHME_CHIFFREMENT* (facultatif) : algorithme de chiffrement. Les valeurs admises sont `aes-128`,
`aes-192`, `aes-256` et `3des`. La valeur par défaut est `aes-128`.

-lv *VALEUR_DUREE_VIE* (facultatif) : valeur de durée de vie de l'association de sécurité IKE (Internet Key Exchange). Plage : 60 à
86400 secondes. La valeur par défaut est `86400` secondes.

**Exemples** :

Créez une règle IKE (Internet Key Exchange) dont le nom est `mon_ike` :
```
bluemix vpn ike-create mon_ike -g ma_passerelle
```


## bluemix vpn ipsec-create
Crée une règle IPSec (Internet Protocol Security).

```
bluemix vpn ipsec-create NOM_REGLE -g NOM_PASSERELLE [-d DESCRIPTION][-pfs GROUPE] [-e
ALGORITHME_CHIFFREMENT][-lv VALEUR_DUREE_VIE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_REGLE* (requis) : nom de la règle IPSec (Internet Protocol Security).

-g *NOM_PASSERELLE* (requis) : nom de la passerelle.

-d *DESCRIPTION* (facultatif) : description des paramètres spécifiés.

-pfs *GROUPE* (facultatif) : identificateur de groupe Diffie-Hellman (DH). Les valeurs admises sont `Group2`,
`Group5` et `Group14`. La valeur par défaut est `Group2`.

-e *ALGORITHME_CHIFFREMENT* (facultatif) : algorithme de chiffrement. Les valeurs admises sont `aes-128`,
`aes-192`, `aes-256` et `3des`. La valeur par défaut est `aes-128`.

-lv *VALEUR_DUREE_VIE* (facultatif) : valeur de durée de vie de l'association de sécurité. Plage : 60 à 86400 secondes. La valeur par
défaut est `3600` secondes.

**Exemples** :

Créez une règle IPSec (Internet Protocol Security) dont le nom est `ma_règle` :
```
bluemix vpn ipsec-create ma_règle -g ma_passerelle
```


## bluemix vpn gateway-create
Crée une passerelle de réseau privé virtuel.

```
bluemix vpn gateway-create NOM_PASSERELLE -t TYPE [-gateway_ip ADRESSE_IP][-subnets ADRESSE_SOUS-RESEAU]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_PASSERELLE* (requis) : nom de la passerelle.

-t *TYPE* (requis) : conteneurs pour lesquels activer le service. Les valeurs admises sont `allSingleContainers`,
`allContainerGroups` et `allContainers`. Aucune valeur par défaut ; vous devez spécifier un type.

-gateway_ip *ADRESSE_IP* (facultatif) : adresse IP de la passerelle.

-subnets *ADRESSE_SOUS-RESEAU* (facultatif) : adresse de sous-réseau au format CIDR.

**Exemples** :

Créez une passerelle dont le nom est `ma_passerelle` et le type `allContainerGroups` :
```
bluemix vpn gateway-create ma_passerelle -t allContainerGroups
```


## bluemix vpn connections
Affiche des informations sur toutes les connexions en cours.

```
bluemix vpn connections
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix vpn ikes
Affiche des informations sur les connexions IKE (Internet Key Exchange) en cours.

```
bluemix vpn ikes
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix vpn ipsecs
Affiche des informations sur les connexions IPSec (Internet Protocol Security) en cours.

```
bluemix vpn ipsecs
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix vpn gateways
Affiche des informations sur les passerelles en cours.

```
bluemix vpn gateways
```

**Prérequis** : Noeud final, Connexion, Cible


## bluemix vpn connection
Affiche toutes les informations sur une connexion particulière.

```
bluemix vpn connection NOM_CONNEXION
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_CONNEXION* (requis) : nom de la connexion à afficher.


## bluemix vpn ike
Affiche des informations sur une connexion IKE (Internet Key Exchange).

```
bluemix vpn ike NOM_REGLE
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_REGLE* (requis) : nom de la règle IKE (Internet Key Exchange) à afficher.


## bluemix vpn ipsec
Affiche des informations sur une connexion IPSec (Internet Protocol Security).

```
bluemix vpn ipsec NOM_REGLE
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_REGLE* (requis) : nom de la règle IPSec (Internet Protocol Security) à afficher.


## bluemix vpn gateway
Affiche les informations de connexion d'une passerelle.

```
bluemix vpn gateway NOM_PASSERELLE
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_PASSERELLE* (requis) : nom de la passerelle à afficher.


## bluemix vpn connection-delete
Supprime une connexion existante.

```
bluemix vpn connection-delete NOM_CONNEXION
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_CONNEXION* (requis) : nom de la connexion à supprimer.


## bluemix vpn ike-delete
Supprime une règle IKE (Internet Key Exchange) existante.

```
bluemix vpn ike-delete NOM_REGLE
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_REGLE* (requis) : nom de la règle IKE (Internet Key Exchange) à supprimer.


## bluemix vpn ipsec-delete
Supprime une règle IPSec (Internet Protocol Security) existante.

```
bluemix vpn ipsec-delete NOM_REGLE
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_REGLE* (requis) : nom de la règle IPSec (Internet Protocol Security) à supprimer.


## bluemix vpn gateway-delete
Supprime une passerelle existante.

```
bluemix vpn gateway-delete NOM_PASSERELLE
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_PASSERELLE* (requis) : nom de la passerelle à supprimer.


## bluemix vpn connection-update
Met à jour une connexion de réseau privé virtuel existante.

```
bluemix vpn connection-update NOM_CONNEXION [-g NOM_PASSERELLE][-k CLE_PRE-PARTAGEE]
[-subnets
"SOUS-RESEAU/MASQUE"][-cip ADRESSE_IP_PASSERELLE_CLIENT] [-d DESCRIPTION][-peer_id ID_HOMOLOGUE] [-admin_state ETAT_ADMIN][-dpd-action ACTION]
[-gateway_ip ADRESSE_IP][-i ETAT_INITIATEUR] [-dpd-timeout VALEUR][-dpd-interval VALEUR] [-ike
NOM][-ipsec NOM]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_CONNEXION* (requis) : nom de la connexion.

-g *NOM_PASSERELLE* (facultatif) : nom de la passerelle.

-k *CLE_PRE-PARTAGEE* (facultatif) : clé pré-partagée.

-subnets "*SOUS-RESEAU*/*MASQUE*" (facultatif) : adresse de sous-réseau au format CIDR.

-cip *ADRESSE_IP_PASSERELLE_CLIENT* (facultatif) : adresse IP de noeud final distant du tunnel VPN.

-d *DESCRIPTION* (facultatif) : description des paramètres spécifiés.

-peer_id *ID_HOMOLOGUE* (facultatif) : ID de l'homologue distant. Autre noeud final du tunnel VPN.

-admin_state *ETAT_ADMIN* (facultatif) : statut de la connexion de réseau privé virtuel. Les valeurs admises sont `UP`
et `DOWN`.

-dpd-action *ACTION* (facultatif) : action à effectuer lorsque l'homologue est identifié comme mort. Les valeurs admises sont
`hold`, `clear`, `disabled`, `restart` et `restart-by-peer`.

-gateway_ip *ADRESSE_IP* (facultatif) : adresse IP du noeud final de tunnel VPN local.

-i *ETAT_INITIATEUR* (facultatif) : état de l'initiateur.

-dpd-timeout *VALEUR* (facultatif) : valeur de délai en secondes au bout duquel la session est terminée. Plage : 6 à 86400 secondes.

-dpd-interval *VALEUR* (facultatif) : intervalle de signal de présence en secondes. Envoyez des messages d'état actif à la fréquence
configurée afin de vérifier l'état opérationnel de l'homologue. Plage : 5 à 86399 secondes.

-ike *NOM* (facultatif) : nom de la règle IKE (Internet Key Exchange).

-ipsec *NOM* (facultatif) : nom de la règle IPSec (Internet Protocol Security).


## bluemix vpn ike-update
Met à jour une règle IKE (Internet Key Exchange).

```
bluemix vpn ike-update NOM_REGLE [-g NOM_PASSERELLE][-d DESCRIPTION] [-pfs
GROUPE][-e ALGORITHME_CHIFFREMENT] [-lv VALEUR_DUREE_VIE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_REGLE* (requis) : nom de la règle IKE (Internet Key Exchange).

-g *NOM_PASSERELLE* (facultatif) : nom de la passerelle.

-d *DESCRIPTION* (facultatif) : description des paramètres spécifiés.

-pfs *GROUPE* (facultatif) : identificateur de groupe Diffie-Hellman (DH). Les valeurs admises sont `Group2`,
`Group5` et `Group14`.

-e *ALGORITHME_CHIFFREMENT* (facultatif) : algorithme de chiffrement. Les valeurs admises sont `aes-128`,
`aes-192`, `aes-256` et `3des`.

-lv *VALEUR_DUREE_VIE* (facultatif) : valeur de durée de vie de l'association de sécurité IKE (Internet Key Exchange). Plage : 60 à
86400 secondes.


## bluemix vpn ipsec-update
Met à jour une règle IPSec (Internet Protocol Security).

```
bluemix vpn ipsec-update NOM_REGLE [-g NOM_PASSERELLE][-d DESCRIPTION] [-pfs
GROUPE][-e ALGORITHME_CHIFFREMENT] [-lv VALEUR_DUREE_VIE]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_REGLE* (requis) : nom de la règle IPSec (Internet Protocol Security).

-g *NOM_PASSERELLE* (facultatif) : nom de la passerelle.

-d *DESCRIPTION* (facultatif) : description des paramètres spécifiés.

-pfs *GROUPE* (facultatif) : identificateur de groupe Diffie-Hellman (DH). Les valeurs admises sont `Group2`,
`Group5` et `Group14`.

-e *ALGORITHME_CHIFFREMENT* (facultatif) : algorithme de chiffrement. Les valeurs admises sont `aes-128`,
`aes-192`, `aes-256` et `3des`.

-lv *VALEUR_DUREE_VIE* (facultatif) : valeur de durée de vie de l'association de sécurité. Plage : 60 à 86400 secondes.


## bluemix vpn gateway-update
Met à jour une passerelle de réseau privé virtuel existante.

```
bluemix vpn gateway-update NOM_PASSERELLE [-t TYPE][-gateway_ip ADRESSE_IP] [-subnets ADRESSE_SOUS-RESEAU]
```

**Prérequis** : Noeud final, Connexion, Cible

**Options de commande** :

*NOM_PASSERELLE* (requis) : nom de la passerelle.

-t *TYPE* (facultatif) : conteneurs pour lesquels activer le service. Les valeurs admises sont `allSingleContainers`,
`allContainerGroups` et `allContainers`.

-gateway_ip *ADRESSE_IP* (facultatif) : adresse IP de la passerelle.

-subnets *ADRESSE_SOUS-RESEAU* (facultatif) : adresse de sous-réseau au format CIDR.
