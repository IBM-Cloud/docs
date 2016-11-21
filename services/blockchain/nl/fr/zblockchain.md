---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Blockchain sur z
{: #zblockchain}
Dernière mise à jour : 8 juillet 2016
{: .last-updated}



Vous pouvez utiliser le service Blockchain dans l'offre dédiée Bluemix avec z/OS pour créer des actifs privés et sécurisés, qui peuvent ensuite être échangés de manière rapide et sécurisée sur des réseaux privés.  *(Infos supplémentaires dans une brève description)*
{:shortdesc}


* Ce contenu mérite-t-il de lui consacrer une section spécifique ?  Ou bien le laissons-nous dans une rubrique imbriquée sous la rubrique "A propos de" ?
* En attente d'informations concernant les notions suivantes : PBFT, Sécurité, Performance, Support.


## PBFT
{: #PBFT}

Le protocole PBFT (Practical Byzantine Fault Tolerance) est un protocole de consensus fondateur qui peut être connecté et configuré en fonction de chaque déploiement. Le package `obcpbft` est une implémentation du protocole de consensus [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT") originel, lequel permet d'atteindre un consensus entre les valideurs, même si un seuil de valideurs agit en mode *Byzantine*, c'est-à-dire, de façon malveillante, ou en cas de défaillance imprévisible. Dans la configuration par défaut, PBFT et Sieve sont conçus pour une exécution sur au moins *3t+1* valideurs (répliques), avec une tolérance de *t* répliques potentiellement défaillantes (y compris, répliques malveillantes ou de type *Byzantine*). Pour en savoir plus sur les fonctions PBFT de base, consultez la section relative à la [spécification de protocole](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) du projet Hyperledger de Linux Foundation. 

Voir un [![aperçu](http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)](http://www.youtube.com/watch?v=EKa5Gh9whgU)

*(Il faut indiquer une raison pratique pour laquelle les utilisateurs doivent connaître PBFT. Quel rôle PBFT joue-t-il dans le support de la chaîne de blocs sur z et quelle est sa relation avec ce support.)*


### Cas de défaillance pris en charge
{: #failure}

*Quels sont les cas de défaillance pris ou non en charge.*

*(Barry Mosakowski/Raleigh/IBM ou Tuan Dang/Raleigh/IBM peuvent fournir davantage de détails.)*

### Disponibilité de l'offre dédiée avec z/OS
{: #Availability}

*Disponibilité et attentes autour de la disponibilité basée sur les tests PBFT.*

*(Plus de détails sont nécessaires.)*

### Vérification des fonctionnalités de base de PBFT
{: #Test PBFT}

*(Données de Gari. Besoin de plus d'infos de Jason au sujet de l'exécution des étapes de tests, avec captures d'écran.)*

Pour vérifier les fonctionnalités de base de PBFT, procédez comme suit :

1. Soumettez des transactions sur un ou plusieurs homologues du réseau.
2. Vérifiez qu'au moins *2f+1* (3 dans ce cas) homologues ont le même état. *(Comment vérifier cela ? Besoin des détails d'un scénario de test.)*

  *Exemple d'utilisation de l'API REST*
3. Sur le tableau de bord, cliquez sur le bouton permettant d'arrêter l'homologue 4. *(Utilisez la fonctionnalité "stop peer" (arrêt d'homologue) du tableau de bord pour arrêter l'homologue 4. Un scénario de test est nécessaire pour décrire l'opération détaillée.)*
4. Vérifiez que le réseau poursuit le traitement. *(Comment vérifier cela ?)*
5. Sur le tableau de bord, cliquez sur le bouton permettant d'arrêter l'homologue 3.
6. Vérifiez que le réseau arrête le traitement.
7. Sur le tableau de bord, cliquez sur le bouton permettant de redémarrer l'homologue 3.

Si l'homologue 3 rattrape son retard et que le réseau poursuit le traitement, vous pouvez utiliser les fonctions PBFT de base.

**Remarques :**
* Après le redémarrage de l'homologue 3, vous devez observer un délai avant de soumettre de nouvelles transactions à l'homologue 3.

* Les transactions, qui sont envoyées aux homologues actifs lorsque le réseau arrête le traitement, sont mises en tampon et soumises sur le réseau lorsque ce dernier reprend le traitement.

## Environnement pour la chaîne de blocs sur z
{: #z environment}

Pour utiliser le service Blockchain dans l'offre dédiée Bluemix avec z/OS, assurez-vous que votre environnement respecte les conditions suivantes :

* Quatre réseaux homologues exécutent PBFT avec des Services aux membres. Pour en savoir plus sur les Services aux membres, consultez la section relative à la [spécification de protocole](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) du projet Hyperledger de Linux Foundation. 
* Un réseau isolé qui ne comporte pas d'ordinateurs ou de mémoire partagés.
* Des homologues isolés au sein du réseau.
* Un système qui est protégé des administrateurs système du cloud.

Le moniteur de chaîne de blocs fournit une vue d'ensemble de votre environnement de chaîne de blocs et extrait des données détaillées concernant votre réseau. Pour en savoir plus sur votre environnement de chaîne de blocs et comment le surveiller, consultez les sections [Managing chaincode with the blockchain monitor](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) et [Sample apps and tutorials for blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).

## Sécurité

*Ce document ne comporte pas des informations sur la sécurité ?*

## Performances

*Ce document ne comporte pas des informations sur les performances ?*

## Support client

Si vous rencontrez des problèmes lors de l'utilisation du service Blockchain dans l'offre dédiée Bluemix avec z/OS, suivez le processus de traitement des incidents IBM Bluemix. Pour plus de détails à ce sujet, voir [Traitement des incidents](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html).
