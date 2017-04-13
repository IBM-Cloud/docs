---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Tests du consensus et de la disponibilité
{: #etn_pbft}

Le plan Starter Developer et le plan High Security Business Network vous permettent de tester le protocole de consensus Practical Byzantine Fault Tolerance (PBFT) sur un réseau de blockchain à quatre noeuds. Les rubriques ci-après fournissent des détails sur le consensus en général, et sur PBFT en particulier. Dès que vous êtes prêt à démarrer les tests, des scénarios de test PBFT sont fournis.  
{:shortdesc}  

## Qu'est-ce que le consensus ?

Le consensus est une méthode qui permet de valider le classement des demandes, ou transactions (deploy et invoke), sur un réseau de blockchain. Le classement correct des transactions est essentiel, car de nombreuses transactions dépendent d'une ou de plusieurs transactions préalables (les comptes de débit dépendent souvent de crédits préalables, par exemple).

Sur un réseau de blockchain, aucune autorité centralisée ne détermine le classement des transactions ; en revanche, nombre de noeuds de validations (ou homologues) implémentent le protocole de consensus réseau. Le consensus garantit qu'un quorum de noeuds conviennent de l'ordre (ou classement) dans lequel les transactions sont ajoutées dans le registre partagé. En résolvant toutes les différences dans l'ordre (ou classement) proposé, le consensus garantit que tous les noeuds du réseau de blockchain opèrent dans un registre identique. En
d'autres termes, le consensus garantit* l'intégrité et la cohérence
de toutes les transactions du réseau de blockchain.

* Cette garantie dépend de variables, notamment le protocole de consensus spécifique implémenté et le nombre de noeuds dans le réseau de blockchain. Les deux plans Blockchain sur Bluemix mettent en oeuvre le protocole de consensus PBFT.  

<br>
## Qu'est-ce que le protocole PBFT ?

Le protocole PBFT (Practical Byzantine Fault Tolerance) est une version du protocole de consensus. La fonction d'un protocole de consensus est de maintenir le classement des transactions sur un réseau de blockchain, malgré les menaces qui pèsent sur ce classement. L'une de ces menaces peut être la défaillance simultanée arbitraire (type de défaillance de noeud Byzantine) de plusieurs noeuds réseau. Avec le protocole PBFT, un réseau de blockchain de (N) noeuds peut supporter un nombre (f) de noeuds Byzantine, où f = (N-1)/3. En d'autres termes, PBFT garantit qu'au moins 2\*f + 1 noeuds parviennent à un consensus sur le classement des transactions avant de les ajouter dans le registre partagé. Une règle dérive de ces formules, selon laquelle un réseau PBFT garantit la cohérence et l'intégrité des données malgré des défaillances Byzantine sur moins d'un tiers de tous les noeuds réseau.  

<br>
## PBFT et votre réseau de blockchain

La règle PBFT 2\*f + 1 a les implications suivantes pour le plan Starter Developer et le plan High Security Business Network :

1. Le réseau peut tolérer au maximum un noeud Byzantine. Chaque réseau contient N=4 noeuds, de sorte que l'application de la formule pour le nombre maximum de noeuds Byzantine tolérés donne le résultat : f=(4-1)/3=1. S'il existe au moins deux noeuds Byzantine (f>1), un réseau PBFT à 4 noeuds ne peut pas garantir la cohérence ou l'intégrité du registre entre tous les noeuds. (Par comparaison, la tolérance de deux noeuds Byzantine nécessiterait f=(7-1)/3=2, ou au minimum un réseau de blockchain PBFT 7 noeuds.)
2. Si moins de 2\*f + 1 noeuds sont connectés, le réseau cesse les ajouts dans le registre, car PBFT ne peut pas garantir la cohérence de données ou l'intégrité entre les noeuds. Le réseau ne reprendra les ajouts dans le registre que lorsqu'au moins 2\*f + 1 noeuds seront connectés (trois ou quatre noeuds, dans le cas présent).
3. Etant donné que seul un minimum de 2\*f + 1 noeuds doivent parvenir à un consensus avant de passer au bloc de transactions suivant, le registre peut temporairement prendre du retard sur les éventuels noeuds additionnels (au-delà de 2\*f + 1). Ce retard de synchronisation du registre partagé entre tous les noeuds est une limitation inévitable sur tous les réseaux PFBT.
<br>

## Scénarios de test de consensus
Les scénarios de test de consensus suivants ont été certifiés par IBM comme répondant aux normes de disponibilité réseau pour PBFT :

1. [Tests de PBFT sans aucun noeud Byzantine](pbft_test1.html). Le processus de consensus exécute les transactions et les ajoute dans le registre.
2. [Simulation d'un noeud Byzantine](pbft_test2.html) par l'arrêt d'un noeud et poursuite de l'envoi de transactions deploy (déploiement), invoke (appel) et query (requête). Le processus de consensus PBFT exécute les transactions et les ajoute dans le registre. Ce test a été répété pour chaque noeud dans un environnement à quatre noeuds.
3. [Simulation de deux noeuds Byzantine](pbft_test3.html) par l'arrêt de deux noeuds et poursuite de l'envoi de transactions deploy (déploiement), invoke (appel) et query (requête). En raison de l'échec de l'obtention d'un consensus PBFT, les transactions ne sont pas exécutées ou ajoutées dans le registre.
4. [Redémarrage d'un noeud qui a été arrêté](pbft_test4.html) dans le scénario de test précédent (3). Le processus de consensus PBFT reprend l'exécution des transactions et les ajouts dans le registre. Le noeud qui a été redémarré synchronise son registre avec le registre partagé.  

Attention : Passez en revue les remarques suivantes avec de démarrer vos tests de consensus :

- Tous les scénarios de test de consensus utilisent l'API REST pour interagir avec les homologues réseau.
- HTTP/2 est le protocole de communication ; les scénarios de test utilisent les URL homologues. Exemple : 'VP0–api.dev.blockchain.ibm.com:80'. Les valeurs symboliques ***VP0, VP1, VP2 et VP3*** sont utilisées en tant qu'espaces réservés pour les URL d'homologue littérales.
-  Pour la connexion à un homologue, utilisez les données d'identification qui ont été fournies lors du déploiement de votre service Bluemix. Pour les scénarios de test, **test\_user1** et **test\_user1\_enrollSecret** sont utilisés comme valeurs de *enrollID* et *enrollSecret*, respectivement.
-  Simulez des plantages de noeud par l'arrêt et le démarrage manuels des homologues à l'aide des boutons **Actions** sur la console réseau. La Figure 1 ci-dessous illustre **Actions** sous l'onglet **Network** :

![](images/stopstartpeer.png "Démarrage et arrêt des homologues")
*Figure 1. Démarrage et arrêt des homologues*

- Les scénarios de test utilisent
**chaincode_example02**, par défaut, de l'adresse
https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go/chaincode_example02. Toutefois, vous pouvez utiliser votre propre code blockchain, ou l'un
des exemples de code blockchain à l'adresse :
https://github.com/hyperledger/fabric/tree/v0.6/examples/chaincode/go.
- Les demandes sont regroupées par lot dans une transaction à des fins de traitement. Toutefois, vous pouvez garantir un traitement immédiat en vous basant sur la valeur de délai de traitement par lots ; si vous patientez au moins deux secondes avant de soumettre la demande suivante, la transaction sera traitée immédiatement.
