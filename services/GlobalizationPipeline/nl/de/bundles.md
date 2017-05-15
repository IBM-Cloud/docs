---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Mit Bundles arbeiten
{: #globalizationpipeline_workingwithbundles}

*Letzte Aktualisierung: 30. August 2016*
{: .last-updated}

Jedes von Ihnen erstellte Bundle enthält die Schlüssel/Wert-Paare aus Ihrer Ressourcendatei und die vollständige Gruppe von generierten Übersetzungen.
{:shortdesc}

Die Ressourcendateien, die Sie hochladen, können eines der folgenden Formate aufweisen und müssen Inhalt in Form von Schlüssel/Wertpaaren enthalten, die die Zeichenfolgen der Benutzerschnittstelle Ihrer App darstellen.


* Dateityp: *Java™-Eigenschaftendateien (.properties)*<br>
Beispiel:
```js
logout=Logout 
back=Back 
examples=Menu 
home=Home 
web=Web 
enterprise=Enterprise 
extra=Resources 
about=About 
settings=Settings 
help=Help 
support=Support 
topics=Topics 
appExitMsg=Are you sure you want to quit the application?
```
* Dateityp: *AMD I18N (.js)*<br>
Beispiel:
```js
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
``` 
* Dateityp: *JSON (.json)*<br>
Beispiel:
```js
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
``` 

Zusätzlich muss eine Ressourcendatei die folgenden Richtlinien einhalten:
* Jeder Schlüssel kann maximal 255 Zeichen enthalten.
* Jeder Wert kann maximal 8191 Zeichen enthalten.
* Jedes Bundle kann maximal 500 Schlüssel/Wertpaare enthalten.


## Bundle übersetzen
{: #globalizationpipeline_translatingabundle}

Nur hochgeladene Ressourcendateien werden übersetzt. Sie können eine Ressourcendatei hochladen, wenn Sie ein [Bundle erstellen](index.html#globalizationpipeline_creatingbundles) oder [Details zum Bundle ändern](bundles.html#globalizationpipeline_modifyingbundles).

Nachdem Sie eine Ressourcendatei hochgeladen haben, können Sie ihren Inhalt in eine der Sprachen übersetzen, die von der Standardengine für automatische Übersetzung angeboten wird. Optional können Sie eine alternative Engine für automatische Übersetzung verwenden. Dies wird im Abschnitt über die [Konfiguration der automatischen Übersetzung](managing_translations.html#globalizationpipeline_service_to_service) beschrieben. Die Standardengine unterstützt die folgenden Zielsprachen:

<table>
<thead>
<tr>
<th>Zielsprachen</th>
</tr>
</thead>
<tbody>
<tr>
<td>Chinesisch (Simplified)</td>
</tr>
<tr>
<td>Chinesisch (Traditional)</td>
</tr>
<tr>
<td>Französisch</td>
</tr>
<tr>
<td>Deutsch</td>
</tr>
<tr>
<td>Italienisch</td>
</tr>
<tr>
<td>Japanisch</td>
</tr>
<tr>
<td>Koreanisch</td>
</tr>
<tr>
<td>Portugiesisch (Brasilianisch)</td>
</tr>
<tr>
<td>Spanisch</td>
</tr>
</tbody>
</table>

**Anmerkung:** Die Standardengine für die automatische Übersetzung von {{site.data.keyword.GlobalizationPipeline_short}} bietet nur Unterstützung für Englisch als Ausgangssprache. Allerdings sind alternative Engines für die automatische Übersetzung zur Konfiguration innerhalb der {{site.data.keyword.GlobalizationPipeline_short}} verfügbar und unterstützen die Übersetzung weiterer Sprachenpaare außer Englisch.

Wenn Sie Bundle erstellen, werden diese zur Registerkarte **Bundles** hinzugefügt, damit leichter auf sie zugegriffen werden kann. Von der Registerkarte aus können weitere Tasks mit den Übersetzungen ausgeführt werden.


## Ein Bundle für die Arbeit auswählen
{: #globalizationpipeline_selectingabundle}

1. Klicken Sie auf die Registerkarte **Bundles**, um alle Bundles anzuzeigen, die Sie erstellt haben.
2. Klicken Sie auf eine **Bundle-ID** in der Liste, um weitere Details zu diesem Bundle anzuzeigen, oder klicken Sie auf das Symbol **Bundle-Details anzeigen** ![Wählen Sie das Symbol 'Bundle-Details anzeigen', um ein Bundle zu öffnen und mit seiner Übersetzung zu arbeiten](images/viewProjectDetailIcon.png)	in der Spalte 'Aktionen'.

![Alle verfügbaren Bundles auf der Registerkarte 'Bundles' anzeigen.](images/translationBundles.png)

Nachdem Sie ein Bundle für die Arbeit ausgewählt haben, können Sie den Status der zugehörigen Übersetzungen anzeigen, Sprachen hinzufügen oder entfernen, die Übersetzungen bearbeiten oder Updates für die Ressourcendatei zur Verfügung stellen.

Wenn Sie ein Bundle nicht mehr benötigen, können Sie es von der Registerkarte **Bundles** löschen. Alle Übersetzungen, die dem Bundle zugeordnet sind, werden ebenfalls gelöscht.

## Details zu Bundle ändern
{: #globalizationpipeline_modifyingbundles}

Wenn Sie ein Bundle öffnen, können Sie alle Details zum Bundle anzeigen. Alle Zielsprachen im Bundle werden zusammen mit dem jeweils aktuellen Übersetzungsstatus aufgelistet.

![Die Seite mit den Bundle-Details zeigt Informationen zum Bundle und den zugehörigen Übersetzungen an. ](images/bundleDetails.png)

Der Status für jede Sprache im Bundle kann 'In Bearbeitung', 'Fehlgeschlagen' oder 'Übersetzt' lauten:

| Status | Beschreibung |
|--------|-------------|
| In Bearbeitung | Die automatische Übersetzung ist noch in Bearbeitung. |
| Fehlgeschlagen | Es ist ein Fehler aufgetreten, als die Ressourcendatei in die Zielsprache übersetzt wurde. |
| Übersetzt | Die Übersetzung in die Zielsprache ist abgeschlossen. |

Sie können die Ressourcendatei aktualisieren, die das Bundle verwendet, eine Zielsprache zum Bundle hinzufügen, eine Zielsprache aus dem Bundle löschen und die generierten Übersetzungen für eine Zielsprache herunterladen.

### Ressourcendatei aktualisieren, die vom Bundle verwendet wird

1. Klicken Sie in der Spalte 'Aktionen' neben der Ausgangssprache auf das Symbol **Ressourcen hochladen** ![Wählen Sie dieses Symbol aus, um eine neue Ressourcendatei hochzuladen](images/uploadIcon.png).
2. Klicken Sie auf **Durchsuchen** und wählen Sie eine neue Ressourcendatei zum Hochladen aus.
3. Wählen Sie den Typ der Ressourcendatei aus, den Sie hochladen.
 * Java-Eigenschaftendatei
 * AMD I18N
 * JSON
4. Klicken Sie auf **Aktualisieren**, um die neue Ressourcendatei hochzuladen.

Die Schlüssel/Wertpaare, die sich in der neuen oder aktualisierten Ressourcendatei befinden, werden mit den Werten synchronisiert, die bereits hochgeladen wurden. Nur neuer oder geänderter Inhalt wird übersetzt.

### Eine Zielsprache zu einem Bundle hinzufügen

1. Klicken Sie auf die Schaltfläche **Sprache hinzufügen**.
2. Alle verfügbaren Zielsprachen werden angezeigt. Wählen Sie die Sprachen aus, die zum Bundle hinzugefügt werden sollen.

Die Übersetzung für die ausgewählten Sprachen beginnt sofort.

### Eine Zielsprache aus dem Bundle löschen

Wenn Sie eine Zielsprache aus dem Bundle löschen, entfernen Sie die Zielsprache und alle zugehörigen Übersetzungen aus dem Projekt. Klicken Sie in der Spalte 'Aktionen' der Zielsprache auf das Symbol **Diese Zielsprache entfernen** ![Wählen Sie das Papierkorbsymbol zum Entfernen dieser Zielsprache aus](images/trashIcon.png).

### Generierte Übersetzungen für eine Zielsprache herunterladen.

{{site.data.keyword.GlobalizationPipeline_short}} bietet mehrere Möglichkeiten, um die Übersetzung in eine Zielsprache in Ihre Anwendung zu integrieren. Sie können die Übersetzung als Ressourcendatei herunterladen und in Ihren Anwendungsbuild einbeziehen. Sie können auf die Übersetzung auch dynamisch von {{site.data.keyword.GlobalizationPipeline_short}} mithilfe eines der Open-Source-[SDKs](https://github.com/IBM-Bluemix/gp-common) verweisen. 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

Gehen Sie folgt vor, um die Übersetzung als Ressourcendatei herunterzuladen: 

1. Klicken Sie in der Spalte **Aktionen** der Ziel- und Ausgangssprache auf das Symbol **Übersetzungen herunterladen** ![Wählen Sie das Symbol zum Herunterladen der Ausgangsschlüssel oder der Übersetzungen für eine Zielsprache aus](images/downloadIcon.png).
2. Wählen Sie ein Dateiformat aus.
3. Klicken Sie auf **Herunterladen**.
