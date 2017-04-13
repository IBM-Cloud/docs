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


# Problemi noti HSBN
{: #etn_overview}



Sono stati segnalati i seguenti problemi relativi al piano HSBN:

1. Quando si utilizza High Security Business Network, che utilizza Hyperledger Fabric v0.6.1, è suggerita la reimpostazione della rete periodicamente durante una fase di sviluppo se sono presenti grossomodo più di cinquanta distribuzioni chaincode.  La reimpostazione della rete rimuove il chaincode distribuito e i dati che sono stati raccolti.  Ciò fornisce una possibilità di rimuovere i vecchi chaincode che sono stati sostituiti da miglioramenti effettuati durante una fase di distribuzione interattiva.  Se non sei nella fase di post-sviluppo, il numero di distribuzioni di chaincode dovrebbe essere monitorato per lasciare la capacità per il chaincode più importante.
2. Vengono ricevuti degli errori "503 Service Unavailable" e "502 Bad Gateway" sporadici durante l'esecuzione di una query di stato della rete e dei peer.
3. Una sicurezza potenziale per i messaggi "Server.Serve failed to complete security handshake" nei log per vp1. Questo è un errore non irreversibile e non correlato all'operazione di rete.
4. Le **Credenziali del servizio** potrebbero non popolarsi automaticamente; in questo caso, genera le credenziali nel seguente modo:

 a) Dal tuo dashboard del servizio, fai clic sulla scheda **Service Credentials**:

  ![Credenziali di servizio HSBN](images/hsbn.png "Credenziali di servizio HSBN")

 b) Dalla scheda **Service Credentials**, fai clic sul pulsante per **New Credential**:

  ![Nuova credenziale HSBN](images/hsbn1.png "Nuova credenziale HSBN")

c) Viene visualizzata una nuova finestra denominata **Add New Credential**; fai clic sul pulsante **Add** in fondo a questa finestra:

  ![Aggiungi nuova credenziale HSBN](images/hsbn2.png "Aggiungi nuova credenziale HSBN")

 d) Ora la tua schermata dovrebbe essere simile al seguente esempio. Facendo clic su **View Credentials** visualizzerai un payload JSON contenente le credenziali del servizio per la tua istanza HSBN.  

  ![Credenziali generate HSBN](images/hsbn3.png "Credenziali generate")


## Come ottenere supporto

Per ottenere supporto e assistenza con la rete IBM Blockchain su Bluemix, vedi [Getting support](ibmblockchain_support.html).
