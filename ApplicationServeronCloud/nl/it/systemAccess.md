---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Accesso al sistema
{: #system_access}
Questi argomenti comprendono metodi per la creazione e la gestione di un'istanza del servizio, insieme a vari modi per accedere e impostare l'accesso ai tuoi sistemi.
{: shortdesc}

*Ultimo aggiornamento: 08 giugno 2016*
{: .last-updated}

## Utilizzo dell'API REST in WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #restapi_usage}

Le istanze in {{site.data.keyword.Bluemix_notm}} vengono create, sottoposte a provisioning, gestite ed eliminate in uno dei seguenti modi:

* Dal Catalogo e Dashboard del servizio di {{site.data.keyword.Bluemix_notm}} nell'IU {{site.data.keyword.Bluemix_notm}}.
* Dalla creazione di un'applicazione o script che utilizza le API RESTful.

Mediante l'utilizzo delle API REST conformi a Swagger 2.0, i clienti hanno accesso alle stesse funzioni fornite attraverso il portale e il dashboard. Per ulteriori informazioni sulle API REST e sulle risorse supportate, vedi la [Documentazione API REST](https://new-console.{DomainName}/apidocs/212){: new_window} di WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}.

**Nota:** dopo la creazione di un'istanza del servizio, a seconda della dimensione Tee-Shirt creata, il servizio potrebbe non essere immediatamente pronto per l'uso. Si consiglia di eseguire una query nel campo **Stato** del JSON restituito per determinare lo stato corrente dell'istanza del servizio. 

**Nota:** per impostazione predefinita, l'URL BASE API punta a un endpoint nella [Regione Stati Uniti Sud](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api/v1){: new_window}.  Se stai utilizzando la regione Regno Unito o Sydney, assicurati che la tua applicazione utilizzi uno dei seguenti endpoint:

* [Regione Regno Unito](https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api/v1){: new_window}
* [Regione Sydney](https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api/v1){: new_window}


## Dashboard del servizio
{: #service_dashboard}

Dopo che hai creato la tua istanza del servizio, verrai indirizzato al dashboard del servizio. Puoi sempre
tornare al dashboard del servizio facendo clic sull'icona del servizio dal tuo dashboard dell'organizzazione.
Dal dashboard del servizio puoi accedere a:

*  Un link a questa documentazione
*  Un link per scaricare i file di configurazione di OpenVPN richiesti.
*  La possibilità di avviare e arrestare la macchina virtuale. La VM
è inizialmente avviata.
*  Il nome host.
*  L'utente amministratore e la password amministratore.
*  Una chiave SSH privata.
*  L'utente amministratore e la password amministratore di WebSphere®.
*  Gli URL di Admin Center e Admin Console.

**Nota**: a causa di una specifica quantità di risorse I/O, calcolo e memoria, ai clienti vengono addebitate le macchine virtuali accumulate nello stato ARRESTATO a un tasso ridotto del 5%.  I clienti vengono gestiti fino a un numero fisso di istanze ARRESTATE con non più di 10 indirizzi IP o 64 GB di memoria.


## Impostazione di openVPN per le istanze WebSphere Application Server for Bluemix
{: #setup_openvpn}

OpenVPN è richiesto per accedere alla macchina virtuale WebSphere Application Server su Bluemix. Deve essere installato e in esecuzione con privilegi di amministratore.  

### Utilizza le seguenti istruzioni per impostare openVPN in Windows:

1. Dal link [openVPN Windows download](http://swupdate.openvpn.org/community/releases/), scarica
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} for 64-bit o
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window} for 32-bit.
2. Assicurati di selezionare [Esegui come un amministratore Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} e installa openVPN.
3. Scarica i file di configurazione VPN dal link di scaricamento di OpenVPN dell'istanza WebSphere Application Server for Bluemix nel dashboard del servizio. Estrai tutti i quattro file contenuti nel file compresso nella directory **{OpenVPN home}\config**.   Ad esempio:

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. Avvia il programma client openVPN "OpenVPN GUI". Assicurati di selezionare [Esegui come amministratore Windows](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window} per avviare il programma. In caso contrario,
potresti non riuscire a connetterti.

### Utilizza le seguenti istruzioni per impostare openVPN in Linux:
1. Per installare openVPN segui queste [istruzioni ](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}.
  * Se devi scaricare e installare manualmente la gestione pacchetti RPM, passa alla pagina dei [download unix/linux openVPN](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}. Potresti avere bisogno di assistenza dal tuo amministratore Linux.
3. Scarica i file di configurazione VPN dal link di scaricamento di OpenVPN dell'istanza WebSphere Application Server for Bluemix nel dashboard del servizio. Estrai i file nella directory da cui intendi avviare il client
openVPN. Ti serviranno tutti e quattro i file nella stessa directory.
3. Avvia il programma client openVPN.  Apri una finestra di terminale e vai alla directory che contiene i file di configurazione. Esegui il seguente comando come root:

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### Utilizza le seguenti istruzioni per impostare openVPN in Mac:
1. Un metodo consiste nell'installare [Tunnelblick](https://tunnelblick.net/){: new_window}, un prodotto software open source.
2. Estrai i file di configurazione di VPN dal servizio WebSphere. Tunnelblick
ti richiede la password di amministrazione per Mac e aggiunge la configurazione al set di VPN che puoi utilizzare per connetterti.
3. Connettiti alla rete VPN; potrai quindi accedere alla tua macchina virtuale. Dopo il primo accesso, Tunnelblick memorizza in cache la configurazione e puoi connetterti da [Tunnelblick](https://tunnelblick.net/){: new_window}. Puoi
inserire un'icona nella barra dei menu in alto per accedere facilmente.


## Utilizzo di SSH per accedere alle macchine virtuali WebSphere Application Server for Bluemix
{: #using_ssh}

Queste istruzioni presumono che tu stia utilizzando OpenSSH
come tuo client. OpenSSH è di norma disponibile in Linux o in Cygwin in esecuzione su Windows. Può anche essere installato per essere eseguito da un prompt di comandi Windows.

Per verificare l'installazione di OpenSSH, immetti il comando:
  ```
      $ ssh -V
  ```
  {: codeblock}

La tua risposta dovrebbe essere simile a:
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

Utilizza le seguenti istruzioni per impostare l'accesso SSH alle tue macchine virtuali WebSphere Application Server for Bluemix

1. Riesamina il messaggio di avvertenza che compare la prima volta che ti colleghi, "L'autenticità dell'host x.x.x.x non può essere stabilita." Questo
è normale. Quando ti viene richiesto, seleziona yes. La chiave pubblica è ora installata sulla tua VM per l'utente virtuser.
2. Accedi a virtuser utilizzando la chiave privata. Per dei risultati ottimali, utilizza il metodo di autenticazione della chiave privata.
3. Copia il contenuto della chiave privata in un file.
4. Esegui il comando:

  <pre>
    $ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName
  </pre>
  {: codeblock}

5. Acquisisci l'autorità sysadmin completa passando da virtuser a root utilizzando il comando:

  <pre>
    $ sudo su root
  </pre>
  {: codeblock}

6. Se stai riscontrando dei problemi durante l'accesso al sistema con la chiave ssh privata, utilizza la password root che ti è stata fornita. Accedi come root eseguendo il seguente comando e fornisci la password.

 <pre>
    $ ssh root@169.53.246.x
  </pre>
  {: codeblock}

7. Sia che tu acceda al sistema con la chiave ssh privata sia che tu lo faccia
con la password root, cambia immediatamente la password root.
8. Per semplificare i tuoi comandi SSH, crea un file denominato "config" nella directory %HOME%/.ssh. Ad esempio:

  <pre>
   Host VM1
      Hostname 169.53.246.xxx
      User virtuser
      IdentityFile /path/privateKeyFileName
  </pre>
  {: codeblock}

9. Esegui "ssh VM1" per collegarti come virtuser.

## Percorsi di sistema
{: #system_paths}

* I comandi Liberty Profile possono essere immessi da */opt/IBM/WebSphere/Liberty/bin*.
* L'ubicazione del profilo del server Liberty Profile è */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*.
* I comandi WebSphere Application Server tradizionali possono essere immessi da */opt/IBM/WebSphere/AppServer/bin*.
* L'ubicazione del profilo di WebSphere Application Server tradizionale per il server è */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*.

## Utilizzo dei link Admin Center e Admin Console
{: #console_links}

Quando fai clic sul link all'Admin Center o alla Admin Console, potresti ricevere un'avvertenza di *connessione non attendibile*. Il testo esatto
del messaggio varia a seconda del browser; per saltare o eliminare
questa avvertenza, procedi nel seguente modo.

Poiché stai utilizzando dei link forniti da {{site.data.keyword.IBM}}, puoi ignorare senza alcun rischio l'avvertenza e connetterti. Se il tuo browser propone
la memorizzazione di un'eccezione di sicurezza, accettare è il modo più facile per
evitare l'avvertenza in futuro.

Un'altra opzione consiste nell'esportare il certificato del firmatario in entrata
e importarlo quindi nel tuo browser come un certificato root attendibile. Questa opzione richiede che tu crei una voce nel file *hosts* che associ l'indirizzo IP della VM al nome comune del firmatario del certificato. Questo nome è nel seguente formato: wl<pureapplication.ibmcloud.com. Se ora usi il nome host invece dell'indirizzo IP nell'URL, dovresti connetterti
senza alcun problema. Devi quindi accedere all'Admin Center
o alla Admin Console utilizzando il nome host invece dell'indirizzo IP nell'URL.

Infine, i clienti installano spesso dei loro certificati root per le
applicazioni che rendono esterne. Per ulteriori informazioni, vedi [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} o [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} Knowledge Center.

## Porte firewall
{: #firewall_ports}

Potrebbe essere necessario aprire delle porte sul firewall per consentire l'accesso ad applicazioni
e database.
  * Su ciascun nodo WebSphere Application Server for Bluemix, uno script openFirewallPorts.sh è disponibile nella directory WAS_HOME/virtual/bin.
  * Su ciascun host di collettivo Liberty, puoi trovare uno script openFirewallPorts.sh nella directory WAS_HOME/virtual/bin.

Utilizzo:
  ```
      $ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT è il numero di porta
* PROTOCOL è TCP o UDP
* -persist è true o false

Per specificare più porte, separale con una virgola ","

**Nota**: sia sport sia dport della porta aperta vengono aperte nelle sezioni INPUT e OUTPUT del firewall. Devi eseguire questo script come root utilizzando sudo. Puoi anche modificare le tabelle IP direttamente.
