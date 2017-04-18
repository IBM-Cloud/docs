---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Creazione di un servizio {{site.data.keyword.mobilepushshort}} senza binding per Android
{: #create_android_unbound}
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}

Crea un'istanza del servizio
{{site.data.keyword.mobilepushshort}}. Puoi utilizzare l'istanza del servizio {{site.data.keyword.mobilepushshort}} senza binding per ogni applicazione di backend.

1. Esegui il bind dell'istanza del servizio {{site.data.keyword.mobilepushshort}} a un'applicazione Bluemix. Durante il bind, vedrai che tutti i dettagli correlati al servizio vengono archiviati nel formato JSON nella variabile di ambiente VCAP_SERVICES. 

![Bind a un servizio Push Notification](images/unbound_1.jpg)
 2. Fai clic su **Bind** e scegli l'istanza del servizio {{site.data.keyword.mobilepushshort}} di cui eseguire il bind. Quando è stato eseguito il bind della tua applicazione al servizio {{site.data.keyword.mobilepushshort}}, le informazioni sul servizio vengono archiviate in formato JSON nella variabile di ambiente VCAP_SERVICES per la tua applicazione. Ad esempio: 
```
 	{
    "imfpush_Dev": [
   {
         "name": "myname_sampleUnbound",
         "label": "imfpush_Dev",
         "plan": "Basic",
         "credentials": null
      }
    ]
    }
```
	{: codeblock}
