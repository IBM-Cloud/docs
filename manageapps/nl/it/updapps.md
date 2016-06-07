---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Aggiornamento di applicazioni
{: #updatingapps}

*Ultimo aggiornamento: 9 maggio 2016*


Per aggiornare le applicazioni in {{site.data.keyword.Bluemix_notm}}, puoi utilizzare il comando cf push o {{site.data.keyword.Bluemix}} DevOps Services. In molti casi, anche per i pacchetti di build integrati quali Node.js, devi inoltre fornire un parametro -c per specificare il comando utilizzato per avviare la tua applicazione.
{:shortdesc}

##Creazione e utilizzo di un dominio personalizzato
{: #domain}

Puoi utilizzare un dominio personalizzato nell'URL della tua applicazione anziché il dominio di sistema {{site.data.keyword.Bluemix_notm}} predefinito che è mybluemix.net.

I domini forniscono la rotta dell'URL assegnata alla tua organizzazione in {{site.data.keyword.Bluemix_notm}}. Per utilizzare un dominio personalizzato, devi registrare il dominio personalizzato su un server DNS pubblico, configurare tale dominio in {{site.data.keyword.Bluemix_notm}} e quindi associarlo al dominio di sistema {{site.data.keyword.Bluemix_notm}} sul server DNS pubblico. Dopo aver
associato il tuo dominio personalizzato al dominio di sistema {{site.data.keyword.Bluemix_notm}},
le richieste per il tuo dominio personalizzato vengono instradate alla tua applicazione in {{site.data.keyword.Bluemix_notm}}.

Puoi creare e utilizzare un dominio personalizzato in {{site.data.keyword.Bluemix_notm}} utilizzando
l'interfaccia utente di {{site.data.keyword.Bluemix_notm}}
oppure l'interfaccia riga di comando cf.

* Utilizza l'interfaccia utente di
{{site.data.keyword.Bluemix_notm}}:

  1. Crea un dominio personalizzato per la tua organizzazione.
    
	1. Nella barra dei menu del **DASHBOARD** {{site.data.keyword.Bluemix_notm}}, fai clic su **GESTISCI ORGANIZZAZIONI**.
	
	2. Nella scheda **DOMINI**, fai clic su **AGGIUNGI DOMINIO**, immetti il nome
del tuo dominio personalizzato e fai clic su **SALVA**.
    	
  2. Aggiungi la rotta con il dominio personalizzato a un'applicazione.
  
    1. Nella barra dei menu del **DASHBOARD** {{site.data.keyword.Bluemix_notm}}, fai clic sul tile dell'applicazione a cui desideri aggiungere la rotta. Viene visualizzata la pagina **Panoramica**.
	
	2. Dal menu dell'applicazione nella pagina **Panoramica**, fai clic su **Modifica rotte e accesso all'applicazione**.
	
	3. Fai clic su **Aggiungi rotta** e specifica la rotta
che desideri utilizzare per l'applicazione.
	
* Utilizza l'interfaccia riga di comando cf:
  
  1. Crea un dominio personalizzato per la tua organizzazione digitando il
seguente comando:
    
    ```
    cf create-domain <your org name> mydomain
```
    
    *organization_name*
  
        Il nome della tua organizzazione.
	  
    *ilmiodominio*
    
        Il nome del dominio personalizzato che desideri utilizzare.
	  
  2. Aggiungi la rotta con il dominio personalizzato a un'applicazione digitando il
seguente comando:
    
    ```
    cf map-route myapp mydomain -n host_name
```
    
    *myapp*
      
    	Il nome della tua applicazione.
  	
    *ilmiodominio*
      
    	Il nome del tuo dominio personalizzato.
	
    *home_host*
    
        Il nome host nella rotta che desideri utilizzare per la tua applicazione.
	
Una volta configurato il dominio personalizzato in {{site.data.keyword.Bluemix_notm}}, devi associarlo al dominio personalizzato del dominio di sistema {{site.data.keyword.Bluemix_notm}} sul tuo server DNS registrato:

  1. Imposta un record 'CNAME' per il nome dominio personalizzato sul tuo server DNS.
  2. Associare il nome dominio personalizzato all'endpoint sicuro della regione {{site.data.keyword.Bluemix_notm}} in cui viene eseguita la tua applicazione. Utilizza i seguenti endpoint della regione per fornire la rotta dell'URL assegnata alla tua organizzazione in {{site.data.keyword.Bluemix_notm}}:
  
    * STATI UNITI SUD: `secure.us-south.bluemix.net`
    * EUROPA REGNO UNITO: `secure.eu-gb.bluemix.net`
    * AU-SYD: `secure.au-syd.bluemix.net`
  
In un browser o nell'interfaccia riga di comando, immetti il seguente URL per accedere all'applicazione myapp:

```
http://host_name.mydomain
```

**Nota:** per rimuovere una rotta orfana, utilizza il seguente comando:

```
cf delete-route domain -n hostname -f
```

*domain* è il nome del tuo dominio e *hostname* è il nome host della rotta per la tua applicazione. Per ulteriori informazioni sul
comando **cf delete-route**, digita `cf
delete-route -h`.

##Distribuzioni blue-green
{: #blue_green}

{{site.data.keyword.Bluemix_notm}} supporta
la tecnica di distribuzione Blue-Green che consente la fornitura continua e la riduzione degli eventi di inattività.

La *distribuzione Blue-Green* è una tecnica di distribuzione
con zero tempo di inattività che consiste in due ambienti di produzione quasi identici,
denominati Blue e Green. La differenza sta nelle risorse utente
che lo sviluppatore ha modificato intenzionalmente, solitamente
nella versione dell'applicazione. In ogni momento, almeno uno degli ambienti
è attivo. L'utilizzo della tecnica di distribuzione Blue-Green ti offre i
seguenti vantaggi:

* Portare il software rapidamente dall'ultima fase di test alla produzione
live.
* Distribuire una nuova versione di un'applicazione senza interrompere il traffico
verso quell'applicazione.
* Eseguire un rapido rollback. Se ci sono problemi in uno dei due ambienti,
puoi passare rapidamente all'altro.

Se hai già distribuito un'applicazione in {{site.data.keyword.Bluemix_notm}} e
desideri aggiornare l'applicazione a una nuova versione, puoi utilizzare uno dei
seguenti due approcci per garantire la distribuzione Blue-Green.

###Esempio: Utilizzo del comando cf rename

In questo esempio, il nome dell'applicazione è Blue. L'esempio dimostra come aggiornare la versione di *Blue* utilizzando
il comando **cf rename** senza interrompere il traffico
verso l'applicazione. In via facoltativa, la versione precedente di *Blue* può
essere eliminata quando è in funzione la nuova.

1. Esegui il push dell'applicazione *Blue* a {{site.data.keyword.Bluemix_notm}}.
  
  ```
  cf push Blue
```
  
  **Risultato:** l'applicazione *Blue* è in esecuzione e sta rispondendo all'URL `Blue.mybluemix.net`.
  
2. Utilizza il comando **cf rename** per ridenominare l'applicazione *Blue* in *Green*:
  
```
  cf rename Blue Green
```
  
  Elenca le applicazioni nello spazio corrente utilizzando il comando **cf apps**:
  
```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  ...
```
  
  **Risultato:** l'applicazione *Green* è in esecuzione e sta rispondendo all'URL `Blue.mybluemix.net`.

3. Apporta le modifiche necessarie e prepara la versione
*Blue*. Esegui il push dell'applicazione *Blue* aggiornata a {{site.data.keyword.Bluemix_notm}}:
  
```
  cf push Blue
```
  
  Elenca le applicazioni nello spazio corrente utilizzando il comando **cf apps**:
  
```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  Blue             started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **Risultati:**
    * Vengono distribuite due istanze dell'applicazione, *Blue* e *Green*.
	* L'applicazione *Green* è in esecuzione e sta rispondendo all'URL `Blue.mybluemix.net`.
	
4. Facoltativo: se vuoi eliminare la versione precedente (*Green*) dell'applicazione, utilizza il comando **cf delete**.
  
```
  cf delete Green -f
```
  
  Elenca le rotte nel tuo spazio utilizzando il comando **cf route**:
  
```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  ...
  ```
  
  **Risultato:** l'applicazione *Blue* sta rispondendo all'URL `Blue.mybluemix.net`.
  
###Esempio: Utilizzo del comando cf map-route

In questo esempio, *Blue* è l'applicazione
distribuita in precedenza e *Green* è la versione aggiornata. Questo esempio dimostra come aggiornare la versione di *Blue* utilizzando
il comando **cf map-route** senza interrompere il traffico
verso l'applicazione. In via facoltativa, la versione precedente di *Blue* può
essere eliminata quando è in funzione la nuova.

1. Esegui il push dell'applicazione *Blue* a {{site.data.keyword.Bluemix_notm}}.
  
```
  cf push Blue
```
  
  **Risultato:** l'applicazione *Blue* è in esecuzione e sta rispondendo all'URL `Blue.mybluemix.net`.
  
2. Apportare le modifiche necessarie e preparare la versione
*Green*. Esegui il push dell'applicazione *Green* a {{site.data.keyword.Bluemix_notm}}:
  
```
  cf push Green
```
  
  Elenca le applicazioni nello spazio corrente utilizzando il comando **cf route**:
  
```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  Green            mybluemix.net    Green
  ...
  ```
  
  **Risultati:**
  
    * Vengono distribuite due istanze dell'applicazione, *Blue* e *Green*.
	* L'applicazione *Blue* sta rispondendo all'URL `Blue.mybluemix.net` e l'applicazione *Green* sta rispondendo all'URL `Green.mybluemix.net`.
	
3. Associa l'applicazione *Blue* all'applicazione *Green* in modo che tutto il traffico a `Blue.mybluemix.net` venga instradato sia all'applicazione *Blue* che all'applicazione *Green*.
  
```
  cf map-route Green mybluemix.net -n Blue
  ```
  
  Elenca le rotte nel tuo spazio utilizzando il comando cf routes:
  
```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue, Green
  Green            mybluemix.net    Green
  ...
```
  
  **Risultato:**

    * Il router CF ora invia il traffico per Blue.mybluemix.net sia all'applicazione Blue che all'applicazione Green.
	* Il router CF continua a inviare il traffico per Green.mybluemix.net all'applicazione Green.
	
4. Quando verifichi che *Green* sia in esecuzione nel modo previsto, rimuovi la rotta `Blue.mybluemix.net` dall'applicazione *Blue*:
  
```
  cf unmap-route Blue mybluemix.net -n Blue
```
  
  Elenca le rotte nel tuo spazio utilizzando il comando cf routes:
  
```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  Green            mybluemix.net    Green
  ...
```
  
  **Risultato:** il router CF smette di inviare traffico all'applicazione *Blue*. L'applicazione *Green* risponde a entrambi gli URL: `Green.mybluemix.net` e `Blue.mybluemix.net`.
  
5. Rimuovi la rotta `Green.mybluemix.net` all'applicazione *Green*.
  
```
  cf unmap-route Green mybluemix.net -n Green
```
  
  **Risultato:** il router CF smette di inviare traffico all'applicazione *Blue*. L'applicazione *Green* sta rispondendo all'URL `Blue.mybluemix.net`.
  
6. Facoltativo: se vuoi eliminare la versione precedente (*Blue*) dell'applicazione, utilizza il comando `cf delete`.
  
```
  cf delete Blue -f
```
  
  Elenca le rotte nel tuo spazio utilizzando il comando cf route:
  
```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  ...
```
  
  **Risultato:** l'applicazione *Green* sta rispondendo all'URL `Blue.mybluemix.net`.


# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [Distribuzioni blue-green](http://martinfowler.com/bliki/BlueGreenDeployment.html){:new_window}
* [IBM{{site.data.keyword.Bluemix_notm}} DevOps
Services](https://hub.jazz.net/){:new_window}
