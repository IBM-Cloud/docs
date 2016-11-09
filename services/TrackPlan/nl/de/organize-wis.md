---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Arbeitselemente organisieren und filtern {: #tp-organize}  

*Letzte Aktualisierung: 29. April 2016*
{: .last-updated}

Der Service '{{site.data.keyword.trackplan}}' umfasst mehrere Optionen für das Sortieren und Organisieren Ihrer Arbeitselemente.
{: shortdesc}

##Arbeitselemente filtern {: #tp-filteringwis}

Sie können Arbeitselemente anhand von Wörtern oder von Werten für bestimmte Attribute filtern. 

Die Filterung wird in den folgenden Ansichten unterstützt:   
- Eigene Arbeit
- Eigene Abonnements
- Eingehende Arbeit
- Rückstand
- Sprintplanung
- Arbeit des Teams
- Gesamte Arbeit

Wenn Sie ein Wort eingeben, werden die Zusammenfassungen für Arbeitselemente angezeigt, die dieses Wort enthalten. Sie können Arbeitselemente auch nach Werten für bestimmte Attribute filtern. Details finden Sie in der folgenden Tabelle.

| Attribut | Beispiel | 
|-------|-------|
|*Type  | `*Defect` |
|#Tag  | `#conference`| 
|@:Owner  | `@:jasmith`|
|$Priority|`$High`|
|!Severity|`!Major`|       
   

Sie können Abfragen erstellen, die ein beliebiges Arbeitselementattribut verwenden, indem Sie den Namen des Attributs eingeben. Falls Sie beispielsweise `Erstellt von` eingeben, werden die Abfrageoptionen und die Syntax angezeigt. In Ihren Filterbedingungen können Sie Operatoren wie 'and', 'or' und 'not' einsetzen. Auch die Verwendung von komplexen Operationen, die mehrere Operatoren mittels Klammern verschachteln, ist möglich. Beispiele können Sie anzeigen, indem Sie auf das Symbol **Hilfe** klicken.
![Hilfesymbol für Filterung](images/filter_helpicon.png)

Wenn Sie auf das Feld **Arbeitselemente nach Schlüsselwort filtern** klicken, werden die Operatoren und Filter angezeigt, die Sie zum Erstellen von Abfragen verwenden können.

![Mit automatisch vervollständigten Auswahlmöglichkeiten filtern](images/filterMenu2.png)

##Angepasste Ansichten speichern {: #tp-customviews}
Durch das Anwenden von Filtern können Sie angepasste Ansichten erstellen. Anschließend können Sie diese Ansichten mit Ihrem Team gemeinsam nutzen.    

1. Geben Sie im Feld **Arbeitselemente filtern** die Kurzform eines Attributtyps und einen Wert für dieses Attribut ein, z. B. `$high`. Einige Auswahlmöglichkeiten für Attribute werden automatisch aufgelistet, sobald Sie die Kurzform eingeben, beispielsweise '*Type', '$Priority' und '!Severity'.
![Filterung durch Attributtypen und Attribute](images/filterAttributes.png)
2. Klicken Sie auf **Speichern**.
3. Vergeben Sie einen Namen für die Ansicht. 
4. Falls die angepasste Ansicht den angezeigten Sprint enthalten soll, wählen Sie das Kontrollkästchen aus, um den Sprint einzuschließen. Im folgenden Beispiel wird der Sprint 'Rückstand' in die Ansicht für den Rückstand mit hoher Priorität einbezogen.
![Dialogfenster zum Speichern einer angepassten Ansicht mit eingeschlossenem Sprint](images/filterIncludeSprints.png)
5. Klicken Sie auf **Speichern**. 
6. Falls Sie Ihre gespeicherten Ansichten mit Ihrem Team gemeinsam nutzen wollen, klicken Sie im Abschnitt 'Angepasste Ansichten' auf das Symbol 'Gemeinsam nutzen' neben der neuen Ansicht. Klicken Sie anschließend auf **OK**.
![Symbol 'Gemeinsam nutzen' für angepasste Ansicht](images/filterShare.png)

Angepasste Ansichten geben Ergebnisse nur für den aktuellen Sprint und Status zurück, den Sie anzeigen. Falls in der Ansicht Ergebnisse für mehrere Sprints oder Status zurückgegeben werden sollen, klicken Sie auf die Ansicht und ändern Sie sie wie benötigt.

##Arbeitselemente anzeigen und organisieren {: #tp-organizingwis}

- Um Arbeitselemente anzuzeigen, deren Eigner Sie sind, verwenden Sie die Ansicht 'Eigene Arbeit'. 
- Falls Sie bestimmte Arbeitselemente häufig verwenden, können Sie sie als Favoriten markieren, indem Sie auf deren Sternsymbole (<img class="inline"  src="./images/star.gif" alt="Sternsymbol">) klicken. Anschließend können Sie alle bevorzugten Arbeitselemente in der Ansicht 'Eigene Stern-Markierungen' anzeigen. Wenn Sie auf das Sternsymbol für ein Arbeitselement klicken, ist nur für Sie selbst erkennbar, dass Sie es als Favoriten markiert haben.  
- Um alle Arbeitselemente anzuzeigen, die Sie abonniert haben, verwenden Sie die Ansicht 'Eigene Abonnements'.
- Um die Arbeitselemente nach Änderungsdatum sortiert anzuzeigen, verwenden Sie die Ansicht 'Eigene aktuelle Arbeit'.
- Um Ihre Aktivität für Arbeitselemente anzuzeigen, verwenden Sie die Ansicht 'Meine Aktivitäten'. Im Abschnitt 'Meine Ereignisse' sind dort die Arbeitselemente aufgelistet, in denen Sie genannt sind. Der Abschnitt 'Meine Abonnements' enthält eine Liste aller Änderungen, die an den von Ihnen abonnierten Arbeitselementen vorgenommen wurden.

##Arbeitselemente sichten {: #tp-triaging}

Wenn ein Arbeitselement erstellt, jedoch keinem Sprint zugewiesen wurde, wird es in der Ansicht 'Eingehende Arbeit' angezeigt.
Sobald ein Arbeitselement einem Sprint zugewiesen wurde, wird es aus der Ansicht 'Eingehende Arbeit' entfernt.

In der Ansicht 'Eingehende Arbeit' können Sie Arbeitselemente mit mehreren Verfahren sichten: 
- Um das Arbeitselement abzulehnen, klicken Sie auf das Symbol **Dieses Element in den Papierkorb verschieben** <img class="inline"  src="./images/trash.gif" alt="Symbol 'Dieses Element in den Papierkorb verschieben'">. Das Arbeitselement wird aufgelöst und sein Status in 'Ungültig' geändert.
- Um das Arbeitselement zu akzeptieren und es dem Rückstand zuzuweisen, klicken Sie auf das Symbol **In Rückstand verschieben** <img  class="inline" src="./images/triage.gif" alt="Symbol 'In Rückstand verschieben'">. Anschließend können Sie das Arbeitselement anhand anderer Arbeitselemente in der Ansicht 'Sprintplanung' auswerten und das Arbeitselement einem Sprint zuweisen.
- Um das Arbeitselement einem Sprint zuzuweisen, öffnen Sie das Arbeitselement und wählen Sie einen Wert in der Liste **Geplant für** aus.

![Arbeitselemente in der Ansicht 'Eingehende Arbeit' sichten](images/incoming_work_attributes.png)  

Weitere Informationen zum Verwalten von Arbeitselementen finden Sie unter [Projekt mit dem Quick Planner verwalten](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.1/com.ibm.team.concert.tutorial.doc/topics/tut_quick_planner_lesson.html).
