---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Nicht gebundenen {{site.data.keyword.mobilepushshort}}-Service für Android erstellen
{: #create_android_unbound}
Letzte Aktualisierung: 11. Januar 2017
{: .last-updated}

Erstellen Sie eine Instanz des {{site.data.keyword.mobilepushshort}}-Service. Sie können die Instanz des {{site.data.keyword.mobilepushshort}}-Service ohne Bindung an jegliche Back-End-Anwendung verwenden.

1. Binden Sie die Instanz des {{site.data.keyword.mobilepushshort}}-Service an eine Bluemix-Anwendung. Durch das Binden werden alle Details im Zusammenhang mit dem Service, die in JSON-Format in der Umgebungsvariablen 'VCAP_SERVICES' gespeichert sind, sichtbar. 

![Binden eines Service für Push-Benachrichtigungen](images/unbound_1.jpg)
 2. Klicken Sie auf **Binden** und wählen Sie die Instanz des {{site.data.keyword.mobilepushshort}}-Service aus, die gebunden werden soll. Nachdem Ihre Anwendung an den {{site.data.keyword.mobilepushshort}}-Service gebunden worden ist, werden Informationen zum Service im JSON-Format in der Umgebungsvariablen 'VCAP_SERVICES' für Ihre App gespeichert. Beispiel: 
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
