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


L'IBM Blockchain High Security Business Network viene eseguito in un ambiente isolato e altamente protetto, distinguendolo dalle altre offerte ospitate sul cloud. Il sistema operativo, il fabric e i nodi si trovano tutti in un IBM Secure Service Container, fornendo i livelli di sicurezza e impenetrabilità che i clienti aziendali si aspettano dalla tecnologia z Systems.  L'IBM Secure Service Container offre anche un'ottimizzazione delle prestazioni per le comunicazioni peer-to-peer, la disponibilità, la scalabilità, la crittografia hardware, le criptochiavi a prova di manomissione e le macchine virtuali crittografate in modo sicuro.  
{:shortdesc}

L'ambiente (LinuxONE su z) consiste in una rete a quattro peer che implementa PBFT con Membership Services abilitato, in esecuzione in un contenitore applicazioni.  Il contenitore applicazioni protegge il software blockchain, il chaincode e i dati in esecuzione nel sistema. Il software blockchain nell'avvio protetto può essere firmato, confermato e crittografato e, dopo essere stato installato nel contenitore applicazioni, è resistente alle manomissioni.  Gli utenti root della piattaforma e gli amministratori di sistema non possono accedere o visualizzare il contenuto dei contenitori protetti.  LinuxONE su z fornisce la conformità FIPS, un'elevata protezione del livello di garanzia della valutazione, un ambiente operativo altamente controllabile e un'ottimizzazione della crittografia.

Consulta la sezione [IBM Secure Service Container](etn_ssc.html) per ulteriori dettagli sulle funzioni di sicurezza.
