---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Canali
{: #v10_dashboard}
Ultimo aggiornamento: 16 marzo 2017
{: .last-updated}

I canali rappresentano un meccanismo incredibilmente potente per il partizionamento e l'isolamento dei dati e forniscono il fondamento primario per
la privacy dei dati.  Per poter effettuare le transazioni, è necessario che ogni rete abbia almeno un canale.  
{:shortdesc}

Puoi suddividere la tua rete in canali, dove ogni canale rappresenta un sottoinsieme di membri
autorizzati a visualizzare i dati per i chaincode istanziati su tale canale; se non sei su un canale non puoi visualizzare
i dati. Ogni canale ha un registro univoco e gli utenti devono essere adeguatamente autenticati per poter effettuare operazioni di lettura/scrittura in questi dati. Inoltre, è possibile implementare degli elenchi di controllo accesso (ACL) per limitare determinati membri e utenti (ad esempio, Membro A limitato alle operazioni di sola lettura).

Immagina di trovarti su una rete con sei membri. Potresti avere un canale di tipo consorzio dove tutti e sei i membri effettuano transazioni
e gestiscono un registro per una risorsa comune.  Tutte le transazioni e lo stato delle risorse coinvolte sono disponibili a
tutti i membri.  Tuttavia, per alcune transazioni bilaterali o multilaterali che richiedono la privacy nella rete in generale,
puoi creare canali separati e quindi occultare questi dati.  

Esistono anche dei metodi per l'interazione da canale a canale nel caso di scenari di business più complessi. Un'applicazione
può essere codificata per la query dei valori di una chiave o una chiave composita sul Canale A e quindi per utilizzare i valori restituiti per la scomposizione
in una transazione sul Canale B. Vedi la [documentazione Hyperledger Fabric](http://hyperledger-fabric.readthedocs.io/en/latest/arch-deep-dive.html) per ulteriori informazioni sui canali, sulle politiche e sulle transazioni tra canali.

La **Figura 2** mostra la schermata iniziale del dashboard con una panoramica di tutti i canali per la tua organizzazione Bluemix:

![Rete blockchain](images/channels.png "Channels")
*Figura 2. Canali*

Da questa schermata puoi creare un canale oppure selezionare un canale specifico per visualizzare dettagli più precisi su registri,
chaincode e appartenenza.  

La **Figura 3** mostra la schermata *Crea un canale*:

![Rete blockchain](images/create_channel.png "Create Channel")
*Figura 3. Crea canale*

Scegli un nome che rifletta l'obiettivo di business del canale e invita una qualsiasi combinazione di membri della tua rete selezionando
il loro **Nome azienda** e facendo clic sul pulsante **Aggiungi membro**.  

La **Figura 4** mostra la panoramica di uno specifico canale.  Sono visualizzate le informazioni di registro come l'altezza del blocco
e la cronologia delle transazioni:

![Rete blockchain](images/channel_overview.png "Channel Overview")
*Figura 4. Panoramica del canale*

La **Figura 5** mostra la cronologia delle transazioni di uno specifico canale.  Sono visualizzate le date/ore per ogni transazione e
l'ID chaincode corrispondente della transazione:

![Rete blockchain](images/channel_transactions.png "Channel Transactions")
*Figura 5. Transazioni del canale*

La **Figura 6** mostra il registro di appartenenza di uno specifico canale.  Sono visualizzati i Nomi azienda e l'e-mail corrispondente
di un amministratore di sistema.

![Rete blockchain](images/channel_members.png "Channel Members")
*Figura 6. Membri del canale*

La **Figura 7** mostra il registro del chaincode di uno specifico canale.  Sono visualizzate le informazioni univoche per ogni chaincode, quali
l'ID chaincode, la versione, gli argomenti di intestazione e i peer.  

![Rete blockchain](images/channel_chaincode.png "Channel Chaincode")
*Figura 7. Chaincode del canale*

Il valore **PEER** è semplicemente il numero di peer sul canale che hanno il contenitore chaincode in esecuzione.  Vedi la sezione
**Chaincode** di seguito per ulteriori informazioni sulla creazione dell'istanza.  
