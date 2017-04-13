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


# High Security Business Network
{: #etn_overview}


Le réseau IBM Blockchain High Security Business Network s'exécute dans un environnement isolé et hautement sécurisé, ce qui le distingue des autres offres hébergées dans le cloud. Le système d'exploitation, la matrice et les noeuds résident tous dans un conteneur IBM Secure Service Container, à condition qu'existent les niveaux de sécurité et d'inviolabilité que les clients de l'entreprise attendent de la technologie z Systems.  IBM Secure Service Container garantit également une optimisation des performances pour la communication d'égal à égal, en termes de disponibilité, d'évolutivité, de chiffrement matériel, de clés de chiffrement infalsifiables, et des machines virtuelles chiffrées de manière sécurisée.  
{:shortdesc}

L'environnement (LinuxONE on z) se compose d'un réseau à quatre homologues qui met en oeuvre le protocole PBFT avec les Services aux membres activés, s'exécutant dans un conteneur d'application.  Ce conteneur d'application protège les logiciels de chaîne de blocs, le code blockchain, ainsi que les données qui s'exécutent au sein du système. Les logiciels de chaîne de blocs au sein de l'amorçage sécurisé peuvent être signés, attestés et chiffrés ; et une fois installés dans le conteneur d'application, ils sont impossibles à reproduire.  Les utilisateurs racine de la plateforme et les administrateurs système ne peuvent ni accéder ni voir le contenu du conteneur sécurisé.  L'environnement LinuxONE sur z assure la conformité FIP, une protection de niveau Evaluation Assurance, un environnement d'exploitation hautement auditable et une optimisation du chiffrement.

Pour plus de détails sur les fonctions de sécurité, consultez la section [IBM Secure Service Container](etn_ssc.html).
