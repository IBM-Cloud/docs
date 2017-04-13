---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Risorse
{: #dashboard_resources}
Ultimo aggiornamento: 16 marzo 2017
{: .last-updated}

Questa schermata contiene importanti dettagli di rete e informazioni sullo stato in tempo reale per i tuoi componenti blockchain.  Questi
componenti includono i tuoi peer, CA e nodo di ordinamento.  Ogni componente ha quattro intestazioni
distinte - **Nome**, **URL**, **Stato** e **Azioni**.
{:shortdesc}

La **Figura 1** mostra la schermata iniziale del dashboard che visualizza i tuoi componenti di rete:

![Rete blockchain](images/myresources.png "My Resources")
*Figura 1. Le mie risorse*

#### Nome

L'intestazione "Nome" visualizza il nome formale a livello di sistema per il tuo componente.  I nostri componenti sono
denominati `order01`, `peer01` e `ca01`.  

#### URL

L'intestazione "URL" visualizza l'endpoint API per ogni componente.  Questi endpoint sono necessari per
indirizzare specifici componenti di rete da un'applicazione lato client e le loro definizioni si trovano solitamente
in un file di configurazione di tipo JSON che accompagna l'applicazione.  Se stai personalizzando un'applicazione
che richiede l'approvazione da peer che non fanno parte della tua organizzazione, dovrai recuperare questi
indirizzi IP dagli amministratori appropriati in un'operazione fuori banda.  I client devono riuscire a connettersi a
un qualsiasi peer da cui necessitano di una risposta.

#### Stato

L'intestazione "Stato" visualizza lo stato della rete corrente di ogni componente (ad esempio, In esecuzione o Arrestato).

#### Azioni

L'intestazione "Azioni" fornisce i pulsanti per avviare o arrestare i tuoi componenti.  Contiene anche una casella
a discesa che si collega ai log dei componenti. I log espongono le chiamate di procedura remota che si verificano
tra i vari componenti di rete e sono utili per il debug e la risoluzione dei problemi.  Fai una prova
arrestando un peer e tentando di indirizzarlo con una transazione: vedrai degli errori di connettività gRPC.  Adesso riavvia il peer e tenta di nuovo la transazione: vedrai che la connessione ha esito positivo.  Puoi anche
lasciare inattivo il peer per un periodi di tempo prolungato mentre il tuo canale prosegue con la transazione.  Quando il peer
verrà di nuovo riattivato, noterai una sincronizzazione del registro attraverso il protocollo gossip.  Una volta che
il peer avrà completamente sincronizzato il registro, potrai eseguire le normali chiamate e query.  

#### Credenziali del servizio

Nella parte superiore destra di questa schermata noterai una scheda Credenziali del servizio.  Fai clic su questa scheda per esporre
un file JSON contenente le informazioni di rete di basso livello per ciascuno dei tuoi componenti
(ad esempio, enrollID/enrollSecret per il tuo CA).  Queste sono tutte le informazioni di configurazione di cui avrai bisogno
per un'applicazione.  Nota, tuttavia, che questo file contiene solo il tuo IP peer.  Se hai bisogno di indirizzare
ulteriori peer, dovrai ottenere questi endpoint.   
