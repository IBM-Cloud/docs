---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


#Kibana-Dashboards exportieren und gemeinsam nutzen
<!-- for example, Uploading your data -->
{: #exporting_sharing_kibana_dash}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Exportieren Sie Ihr Dashboardschema als JSON-Datei oder geben Sie eine URL-Adresse zu den angepassten Kibana-Dashboards für Ihre Protokolldaten zur gemeinsamen Nutzung frei.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Mit Kibana können Sie mit anderen Beteiligten zusammenarbeiten, indem Sie Ihre Dashboards als JSON-Dateien exportieren oder URLs Ihrer Dashboards zur gemeinsamen Nutzung freigeben.

Führen Sie die folgenden Tasks aus, um ein Kibana-Dashboard als JSON-Datei zu exportieren:

1. Klicken Sie auf das Symbol **Speichern** ![Symbol für Speichern](images/logging_save.jpg) und anschließend auf **Advanced** **>** **Export schema**.

    ![Dashboard als JSON-Datei exportieren](images/logging_export_json.jpg)

2. Wählen Sie einen aussagekräftigen Namen für die JSON-Datei aus und klicken Sie auf **Save**. Alle Benutzer mit dieser JSON-Datei können die Datei in ihrem Kibana-Dashboard öffnen. 

Führen Sie die folgenden Tasks aus, um eine URL zu einem Kibana-Dashboard zu erstellen und für die gemeinsame Nutzung freizugeben:

1. Klicken Sie im Kibana-Dashboard auf das Symbol **Ordner** ![Ordnersymbol](images/logging_folder.jpg), um ein Menü anzuzeigen, in dem alle zuletzt verwendeten Dashboards aufgelistet sind. Neben den Dashboards, die Sie unter einem Namen gespeichert haben, werden in dem Menü unbenannte Dashboards im folgenden Format aufgelistet: *ALCH_TENANT_ID_Anwendungs-ID*. 

    ![Liste der Dashboards](images/logging_list_of_dashboards.jpg)

2. Klicken Sie auf das Symbol **Freigeben** ![Symbol für Freigeben](images/logging_create_url.jpg) für das Dashboard, das Sie zur gemeinsamen Nutzung freigeben möchten. Eine gemeinsam nutzbare URL wird erstellt und angezeigt. 

    ![Teilfenster mit gemeinsam nutzbarer URL](images/logging_shareable_link_popup.jpg)

    Kopieren Sie die URL, um Ihr Dashboard mit anderen Benutzern gemeinsam zu nutzen. Klicken Sie auf **Close**, um zu Ihrem Dashboard zurückzukehren.
