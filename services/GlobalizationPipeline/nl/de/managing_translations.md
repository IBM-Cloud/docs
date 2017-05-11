---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Übersetzungen verwalten
{: #globalizationpipeline_managingtranslations}

Sobald Sie Bundle erstellt haben und die Erstellung der Übersetzungen für Ihre Anwendung gestartet wurde, kann der maschinell erstellte Inhalt unverändert oder modifiziert verwendet werden. Sie können auch auswählen, dass Sie eine andere automatische Übersetzung als den Standard verwenden möchten. In diesem Abschnitt wird beschrieben, wie die Engine für automatische Übersetzung, die die Übersetzungen für Ihre Bundles ausführt, geändert werden kann, wie ein Post-Editing durch menschliche Übersetzer durchgeführt wird und auch wie Sie Benutzerrollen und Zugriffsbeschränkungen den Personen zuordnen können, die auf Ihre Übersetzungen zugreifen müssen.
{:shortdesc}

## Konfiguration zur automatischen Übersetzung
{: #globalizationpipeline_service_to_service}

{{site.data.keyword.GlobalizationPipeline_full}} unterstützt die Fähigkeit zur Integration alternativer Services für automatische Übersetzung, um automatische Übersetzungen für Ihre Bundles auszuführen. Das Hinzufügen eines alternativen Service kann vorteilhaft sein, wenn die von {{site.data.keyword.GlobalizationPipeline_short}} verwendete Standard-Engine eine bestimmte Sprache, die Sie benötigen, nicht anbietet oder wenn Sie automatische Übersetzungen bevorzugen, die von einer anderen Engine generiert wurden. Die Verwendung von und die Gebühren für alternative Services werden unter den Bedingungen des jeweiligen Service aufgeführt.

Um einen alternativen Service für automatische Übersetzung für {{site.data.keyword.GlobalizationPipeline_short}} hinzuzufügen und zu konfigurieren, wählen Sie die Registerkarte **Automatische Übersetzung - Konfiguration** im {{site.data.keyword.GlobalizationPipeline_short}}-Dashboard aus.

* Um einen Service für automatische Übersetzung hinzuzufügen, der sich im {{site.data.keyword.Bluemix_notm}}-Katalog befindet, (**Watson Language Translator**), muss der Service zuerst zu Ihrem {{site.data.keyword.Bluemix_notm}}-Bereich hinzugefügt werden.

* Um einen Service anderer Anbieter hinzuzufügen, wählen Sie die Schaltfläche für diesen Service auf der Registerkarte **Automatische Übersetzung - Konfiguration** aus und stellen die erforderliche Benutzerberechtigung für den Zugriff auf den Service bereit.

Nachdem der Service für automatische Übersetzung zu {{site.data.keyword.GlobalizationPipeline_short}} hinzugefügt wurde, führen Sie die verbleibenden Schritte aus, um die Integration dieses Service abzuschließen.

1. Klicken Sie auf **Aktivieren**, um die Integration dieses Service zu aktivieren.

2. Klicken Sie auf **Sprachen aktualisieren**, um die aktualisierte Liste der unterstützten Zielsprachen anzuzeigen.

3. Wählen Sie in der Liste der Zielsprachen die Engine für automatische Übersetzung aus, die die Übersetzung ausführen soll.

4. Klicken Sie auf **Speichern**, um zur Registerkarte **Automatische Übersetzung - Konfiguration** zurückzukehren.

Sobald ein alternativer Service für {{site.data.keyword.GlobalizationPipeline_short}} konfiguriert wurde, werden alle Zielsprachen, die dieser Engine zugeordnet wurden, mithilfe der Engine generiert. 

Gehen Sie wie folgt vor, um die Verwendung der alternativen Engine für automatische Übersetzung zu stoppen:

1. Klicken Sie auf der Registerkarte **Automatische Übersetzung - Konfiguration** für den Service, dessen Verwendung Sie stoppen möchten, auf die Schaltfläche **Inaktivieren**.

Wenn ein alternativer Service für automatische Übersetzung inaktiviert wurde, verbleiben alle Übersetzungen, die von diesem Service generiert wurden, innerhalb Ihrer Bundles. Die Übersetzung in eine bestimmte Zielsprache ist jedoch für künftige Updates möglicherweise nicht mehr verfügbar, wenn die Zielsprache nicht mehr von der Engine für automatische Übersetzung unterstützt wird, die dann aktiviert ist.

<!-- Review comment: When you disable an engine, do you need to go back and reconfigure the languages?? Does it go back to the default engine? What happens? -->

## Übersetzungen anzeigen und bearbeiten
{: #globalizationpipeline_translations}

Der {{site.data.keyword.GlobalizationPipeline_short}}-Service bietet nach der Übersetzung Bearbeitungsmöglichkeiten durch Humanübersetzer an. Ein professioneller Übersetzer oder jemand mit sehr guten Sprachkenntnissen in einer der Zielsprachen kann die generierten Übersetzungen bearbeiten. Sie können durch die Bearbeitung die Qualität oder Konsistenz der Übersetzung verbessern oder bevorzugte Schreibungen ersetzen. Sie möchten zum Beispiel möglicherweise die Übersetzung eines Produktnamens überschreiben.

Gehen Sie wie folgt vor, um die Übersetzungen für eine Zielsprache anzuzeigen und zu bearbeiten:

1. Wählen Sie in der Spalte 'Aktionen' auf der Seite **Bundle-Details** eine Zielsprache aus oder klicken Sie auf das Symbol **Übersetzungen anzeigen** ![Wählen Sie das Symbol 'Übersetzungen anzeigen' aus, um die Übersetzungen einer Zielsprache anzuzeigen](images/viewProjectDetailIcon.png).
2. Die Übersetzungen werden in einer Tabelle dargestellt, die Schlüssel, Quelle und Übersetzungsinformationen anzeigt.
 * **Schlüssel:** Stellt ein Attribut in der Ressourcendatei mit einem zugeordneten Wert dar.
 * **Quelle: ** Stellt eine übersetzbare Zeichenfolge dar, die in die hochgeladene Ressourcendatei integriert wurde.
 * **Übersetzung:** Stellt die übersetzte Version eines Quellenwerts dar.
3. Klicken Sie in der Spalte 'Aktionen' auf das Symbol **Übersetzung ändern** ![Wählen Sie das Symbol 'Übersetzung ändern' aus, um die Übersetzung eines bestimmte Schlüssel/Wertpaares zu bearbeiten](images/editIcon.png), um einen maschinell übersetzten Wert zu bearbeiten.
4. Bearbeiten Sie die Übersetzung und klicken Sie auf **Aktualisieren**, um den ursprünglich übersetzten Wert durch Ihre Bearbeitung zu aktualisieren.

![Das Dialogfenster zum Ändern von Übersetzungen bietet eine einfache Möglichkeit, Übersetzungen zu bearbeiten. ](images/editTranslation.png) 

***Tipp:*** Wenn Sie mit großen Bundles arbeiten, die viele übersetzbare Schlüssel enthalten, kann das Auffinden eines bestimmten Werts schwierig sein. Auf der Seite mit den Zielsprachenübersetzungen können Sie schnell über alle Schlüssel, Quellen und Übersetzungen hinweg suchen, indem Sie das Feld **Suchen nach....** verwenden.

![Verwenden Sie das Suchfeld, das auf der Seite der Zielsprachenübersetzung bereitgestellt wird, um die Schlüssel, Quellen und Übersetzungen oder alle drei Bereiche innerhalb einer Zielsprache zu durchsuchen.](images/search.png) 


## API-Benutzer hinzufügen
{: #globalizationpipeline_users}

Bei der Verwaltung Ihrer Übersetzungen möchten Sie möglicherweise weiteren API-Benutzern, auf Grundlage der von ihnen auszuführenden Aufgaben, Zugriff gewähren. Sie möchten beispielsweise einem Übersetzer ermöglichen, die Übersetzung zu bearbeiten, dieser soll jedoch nicht die Bundle-Information ändern können.

| Rollentyp | Übersetzungen anzeigen? | Übersetzungen bearbeiten? | Bundle-Information ändern? |
|-----------|--------------------|--------------------|----------------------------|
| Leser | Ja | Nein | Nein |
| Übersetzer | Ja | Ja | Nein |
| Administrator | Ja | Ja | Ja |

Wenn Sie mehr API-Benutzer erstellen, können Sie deren Zugriff auf ein oder mehrere spezifische Bundle einschränken oder ihnen Zugriff auf alle verfügbaren Bundles gewähren.

Gehen Sie wie folgt vor, um einem API-Benutzer Zugriff auf ein Bundle in einer Serviceinstanz von {{site.data.keyword.GlobalizationPipeline_short}} zu gewähren:

1. Klicken Sie im {{site.data.keyword.GlobalizationPipeline_short}}-Dashboard auf die Registerkarte **API-Benutzer**.
2. Klicken Sie auf **Neuer API-Benutzer**.
3. Geben Sie einen **Anzeigenamen** und einen **Kommentar** zur Beschreibung des neuen API-Benutzers ein.
4. Wählen Sie einen **Typ** für den neuen API-Benutzer aus.
5. Wählen Sie aus, dass der API-Benutzer Zugriff auf alle Bundles oder nur auf ausgewählte Bundles haben soll.
6. Klicken Sie auf **Speichern**.

![Beenden Sie das Forum, um einen neuen API-Benutzer zu erstellen.](images/newUser.png)

Eine API-Benutzer-ID und ein Kennwort werden generiert und angezeigt. Kopieren und speichern Sie diese Berechtigungsnachweise. Nachdem Sie das Fenster geschlossen haben, können Sie nicht mehr auf diese Daten zugreifen. Die Berechtigungsnachweise können für den RESTful-Service über [SDKs](https://github.com/IBM-Bluemix/gp-common) verwendet werden. 

Gehen Sie wie folgt vor, um das API-Benutzerkennwort zurückzusetzen:

1. Klicken Sie im {{site.data.keyword.GlobalizationPipeline_short}}-Dashboard auf die Registerkarte **API-Benutzer**.
2. Klicken Sie auf das Symbol **Kennwort zurücksetzen** ![Wählen Sie dieses Symbol aus, um das API-Benutzerkennwort zurückzusetzen](images/resetPW.png), um das Kennwort für eine bestimmte Benutzer-ID zurückzusetzen. 
3. Klicken Sie auf **Ja**. 
