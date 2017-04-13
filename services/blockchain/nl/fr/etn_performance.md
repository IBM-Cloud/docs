---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Performance vérifiée
{: #etn_performance}


Les comportements suivants ont été testés et vérifiés par IBM. Les résultats ont été obtenus dans un environnement High Security (sauf indication contraire) :
{:shortdesc}

### Performances/Contrainte

Ces tests ont été effectués en vue d'obtenir le nombre de TPS (transactions par seconde) des appels et requêtes au cours d'intervalles de test de courte durée (10 minutes) et de longue durée (60 minutes) avec les services PBFT / Sécurité & Confidentialité activés.  Les performances peuvent varier selon l'environnement, le type d'application, les paramètres de configuration/sécurité, la taille des lots de transaction et d'autres facteurs.  (**Remarque :** ces mesures ont été obtenues dans un réseau distribué à service partagé.)

- code blockchain example02
- niveau de consignation : error
- nombre d'unités d'exécution : 100
- taille de lot : 1000
- durée : 10 minutes et 60 minutes.
- types de transaction : invoke a->b, invoke b->a, puis repeat & query a, query b, puis repeat

| Type transaction | Nbre homologues | Nbre menaces | Durée exécution (min) | Transactions par seconde |
| ---------- |:-------:|:-----:|:------:|:------:|
| invokes   |  4  | 100 | 10 | 72  |
| invokes   |  4  | 100 | 60 | 66  |
| queries   |  4  | 100 | 10 | 252 |
| queries   |  4  | 100 | 60 | 248 |

### Résistance/Consensus

Ces tests ont été effectués pour garantir la stabilité et la résistance de PBFT en cas de défaillances de noeuds Byzantine.  Les tests incluaient :

- L'arrêt de 1 noeud et la poursuite de l'envoi de transactions deploy, invoke et query.  Le réseau continue à fonctionner. Exécution sur chaque noeud du réseau.
- L'arrêt de 2 noeuds, le réseau s'arrête en l'absence de consensus.
- Le redémarrage de l'un des noeuds arrêtés au cours du test précédent.  Le réseau reprend et le noeud qui a redémarré se synchronise avec d'autres homologues de validation. Pour plus de détails sur les étapes de test PBFT, consultez la rubrique [Tests du consensus et de la disponibilité](etn_pbft.html).

Passez à la rubrique [Tests
complémentaires](etn_next.html) pour effectuer des tests supplémentaires et
des fonctionnalités vérifiés.  
