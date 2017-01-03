---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Pipelines verwalten
{: #deliverypipeline_managing}
Letzte Aktualisierung: 17. November 2016
{: .last-updated}

Sie können Integrationen von IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} verwalten, konfigurieren und erweitern.
{:shortdesc}

Führen Sie die folgenden Aufgaben aus, um eine Pipeline zu verwalten, zu konfigurieren und zu erweitern.

## Umgebungseigenschaften und Ressourcen
{: #deliverypipeline_envprop}

Sie können Umgebungseigenschaften und vorinstallierte Ressourcen verwenden, um mit den {{site.data.keyword.deliverypipeline}}-Services zu interagieren. Möglicherweise integrieren Sie diese in ein Job-Script oder einen Testbefehl. Weitere Informationen finden Sie unter [Umgebungseigenschaften und Ressourcen für den {{site.data.keyword.deliverypipeline}}-Service](./deploy_var.html).

Sie können auf der Registerkarte **Umgebungseigenschaften** Ihre eigenen Umgebungseigenschaften zu einer Phase hinzufügen. Umgebungseigenschaften stehen für jeden Job in einer Phase zur Verfügung.

Sie können vier Typen von Eigenschaften von der Registerkarte 'Umgebungseigenschaften' hinzufügen:
* **Text** (Text): Ein Eigenschaftsschlüssel mit einem einzeiligen Wert.
* **Text Area** (Textbereich): Ein Eigenschaftsschlüssel mit einem mehrzeiligen Wert.
* **Secure** (Sicher): Ein Eigenschaftsschlüssel mit einem einzeiligen Wert. Der Wert wird in Form von Sternen angezeigt.
* **Properties** (Eigenschaften): Eine Datei im Projektrepository. Diese Datei kann mehrere Eigenschaften enthalten. Jede Eigenschaft muss in einer eigenen Zeile stehen. Verwenden Sie Gleichheitszeichen (=), um Schlüssel und Werte der Paare zu trennen.

## Die Funktionalität Ihrer Pipeline erweitern
{: #deliverypipeline_extend}

Sie können die Funktionalität Ihrer Pipeline erweitern, indem Sie Ihre Jobs für die Verwendung unterstützter Services konfigurieren. Testjobs können zum Beispiel statische Codescans ausführen und Buildjobs können Zeichenfolgen globalisieren.

Weitere Informationen zum Erweitern von Pipelinefunktionen finden Sie unter [Funktionalität des {{site.data.keyword.deliverypipeline}}-Services erweitern](./deliverypipeline_extension.html).

