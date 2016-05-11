---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}

# Servizi VCAP

*Ultimo aggiornamento: 15 marzo 2016*


La variabile di ambiente VCAP_SERVICES è un oggetto JSON che contiene le informazioni che puoi utilizzare per interagire con un'istanza del servizio in {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Richiamo del valore della variabile di ambiente VCAP_SERVICES
{:retrieving}

La variabile di ambiente VCAP_SERVICES è un oggetto JSON che contiene le informazioni che puoi utilizzare per interagire con un'istanza del servizio in {{site.data.keyword.Bluemix_notm}}. Le informazioni includono il nome dell'istanza del servizio, le credenziali e l'URL di connessione all'istanza del servizio. Questi valori vengono inseriti nella variabile di ambiente VCAP_SERVICES quando la tua applicazione viene associata a un'istanza del servizio in {{site.data.keyword.Bluemix_notm}}.

Il valore della variabile di ambiente VCAP_SERVICES è disponibile solo quando esegui il bind di un'istanza del servizio alla tua applicazione. Puoi visualizzare le variabili di ambiente dell'applicazione utilizzando seguente comando:
```
cf env APP_NAME
```
