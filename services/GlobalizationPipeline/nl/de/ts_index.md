---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.GlobalizationPipeline_short}} - Fehlerbehebung
{: #globalizationpipelinets}

Hier finden Sie einige Antworten auf häufig gestellte Fragen zur Verwendung von {{site.data.keyword.GlobalizationPipeline_short}}. 
{:shortdesc}


## Der Name meiner App wurde nicht korrekt übersetzt
{: #problem1}

Die generierten Übersetzungen bestimmter Zeichenfolgen war nicht das, was erwartet wurde.
{:shortdesc}

Bei der Übersetzung einer Ressourcendatei werden Zeichenfolgen mit bestimmten Produktnamen oder anderen Eigennamen möglicherweise nicht richtig übersetzt.
{: tsSymptoms}

Häufig werden Produktnamen und andere Eigennamen nicht korrekt in andere Sprachen übersetzt. Dies passiert insbesondere dann, wenn diese Namen normale Wörter enthalten. Bei der Übersetzung dieser Wörter oder Ausdrücke hat der übersetzte Text, abhängig von der Bedeutung dieser Wörter in einer bestimmten Sprache, möglicherweise eine andere Bedeutung als der englische Name.
{: tsCauses}

Testen Sie die Übersetzung von Produktnamen, bevor Sie diese verwenden. Falls Probleme auftreten, ändern Sie den Text oder die Übersetzung entsprechend. Hinweise zum Schreiben von Texten, die für die automatische Übersetzung vorgesehen sind, finden Sie unter [Tipps zur automatischen Übersetzung](./tips.html#globalizationpipeline_tips).
{: tsResolve}



## Ich kann keine Ressourcendatei hochladen
{: #problem2}

Die Ressourcendatei, die ich hochladen möchte, wird nicht akzeptiert.
{:shortdesc}

Beim Hinzufügen einer Ressourcendatei zu einem neuen Übersetzungsbundle oder beim Aktualisieren einer vorhandenen Ressourcendatei, die übersetzt werden soll, erhalte ich einen Fehler.
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} akzeptiert nur Ressourcendateien der folgenden Typen: Java™ .properties, JSON und AMD I18N.
{: tsCauses}

Stellen Sie sicher, dass die hochgeladene Ressourcendatei einen dieser Typen aufweist.
{: tsResolve}
* Java .properties
* JSON
* AMD I18N



## Ich kann meine Ressourcendatei hochladen, da sie zu groß ist
{: #problem3}

Die Ressourcendatei, die ich hochladen möchte, wird nicht akzeptiert.
{:shortdesc}

Beim Hinzufügen oder Aktualisieren einer Ressourcendatei zu einem Übersetzungsprojekt tritt ein Fehler auf, weil ein Teil der Datei zu groß ist.
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} kann nur die Ressourcendateien akzeptieren, die bestimmte Größenanforderungen erfüllen.
{: tsCauses}

Stellen Sie sicher, dass die Ressourcendatei mit den folgenden Richtlinien übereinstimmt:
{: tsResolve}
* Jeder Schlüssel kann maximal 256 Zeichen lang sein.
* Jeder Wert kann maximal 2048 Zeichen enthalten.
* Jedes Übersetzungsprojekt kann maximal 500 Schlüssel-/Wertepaare enthalten.
* Eine Ressourcendatei kann nicht größer als 2 MB sein.




## Die Zwischenräume um Variablen in Zeichenfolgen ist nicht konsistent
{: #problem5}

Der Abstand, der um Variablen herum verwendet wird, ist nach der Übersetzung nicht immer identisch.
{:shortdesc}

Der Abstand, der um Variablen herum verwendet wird, die in Zeichenfolgen enthalten sind, ist nach der Übersetzung von einer Sprache in eine andere nicht immer konsistent.
{: tsSymptoms}

Automatische Übersetzungssysteme sind für natürliche Sprache konzipiert und erkennen nicht immer bzw. wissen nicht immer, wie eine bestimmte Syntax, die von Programmiersprachen verwendet wird, zu handhaben ist. Die Übersetzung von Syntax, die mit einfachem Text gemischt ist, ist daher möglicherweise vom Original verschieden.
{: tsCauses}

{{site.data.keyword.GlobalizationPipeline_short}} erkennt aktuell das Muster "{}", das häufig für die Darstellung von Variablen verwendet wird, und behält das Originalformat des darin enthaltenen Inhalts bei.
{: tsResolve}
