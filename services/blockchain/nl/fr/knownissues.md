---

copyright:
  years: 2017
lastupdated: "2017-03-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Problèmes connus de HSBN
{: #etn_overview}



Les problèmes de plan HSBN suivants ont été signalés :

1. Lors de l'utilisation de High Security Business
Network, qui utilise Hyperledger Fabric v0.6.1, il est
conseillé de réinitialiser régulièrement le réseau s'il y a environ
une cinquantaine
de déploiements de code blockchain.  Cette réinitialisation
permet de supprimer le code blockchain et les données qui ont
été collectées.  Le code blockchain plus ancien peut ainsi
éventuellement être remplacé par des améliorations effectuées au
cours d'une phase du développement itératif.  Si vous êtes en phase
de post-développement, le nombre de déploiements de code
blockchain doit être surveillé afin d'affecter la capacité au
code blockchain le plus important.
2. Erreurs sporadiques "503 Service Unavailable" et "502 Bad Gateway"
reçues lors de l'exécution d'une interrogation d'état du réseau et
des homologues.
3. Des messages "Server.Serve failed to complete
security
handshake" peuvent figurer dans les journaux de vp1. Il ne s'agit
pas d'une erreur fatale et elle n'est pas liée aux opérations réseau.
4. La zone **Données d'identification pour le
service** peut ne pas se remplir automatiquement ; dans ce
cas, générez ces données d'identification du service comme suit :

 a) Depuis le tableau de bord de votre service, cliquez sur
l'onglet **Données d'identification pour le service** :

  ![HSBN Données d'identification pour le service](images/hsbn.png "HSBN Données d'identification pour le service")

 b) Sous l'onglet **Données d'identification pour le service**,
cliquez sur le bouton **Nouvelles données d'identification**:

  ![HSBN Nouvelles données d'identification](images/hsbn1.png "HSBN Nouvelles données d'identification")

c) Une nouvelle fenêtre intitulée
**Ajouter des données d'identification** s'affiche
; cliquez sur le bouton **Ajouter** au bas de
la fenêtre :

  ![HSBN Ajouter des données d'identification](images/hsbn2.png "HSBN Ajouter des données d'identification")

 d) A présent, votre écran doit être similaire à
l'exemple suivant. Un clic sur **Afficher les données
d'identification** permet d'afficher un contenu
JSON contenant les données d'identification de service pour
votre instance HSBN.  

  ![HSBN Données d'identification générées](images/hsbn3.png "Données d'identification générées")


## Obtention d'aide

Pour obtenir du support et de l'aide sur votre réseau IBM Blockchain on Bluemix, voir [Obtention de support](ibmblockchain_support.html).
