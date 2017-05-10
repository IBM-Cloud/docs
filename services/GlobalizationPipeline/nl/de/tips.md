---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Tipps zur automatischen Übersetzung
{: #globalizationpipeline_tips}

Automatische Übersetzung kann dazu dienen, eine Näherung der Bedeutung des Ausgangstextes zur Verfügung zu stellen. Die Qualität und Zweckmäßigkeit von automatische Übersetzung variiert stark und hängt von der Zielsprache und der verwendeten Engine für automatische Übersetzung ab. Einer der Schlüsselfaktoren für die Qualität einer automatischen Übersetzung ist die Qualität des Ausgangstexts selbst. Ein Ausgangstext, der viele umgangssprachliche Ausdrücke, unvollständige Sätze, falsche Interpunktion und mehrdeutige Wörter und Ausdrücke enthält, wird möglicherweise nicht angemessen übersetzt.
{:shortdesc}

Wenn Sie Ihre Benutzerschnittstelle der {{site.data.keyword.Bluemix_notm}}-App erstellen, befolgen Sie bitte einige Grundregeln beim Schreiben, um nicht nur Ihren Ausgangstext sondern auch die Qualität der automatischen Übersetzung zu verbessern.

Bitten Sie zusätzlich Muttersprachler darum, die automatische Übersetzung zu überprüfen und zu bearbeiten. Sammeln Sie ferner Rückmeldungen von Ihren App-Benutzern. Sie können möglicherweise am besten über die Zweckmäßigkeit und Richtigkeit der Übersetzung urteilen.

## Tipps zum Schreibstil
{: #writingstyletips}

* **Verwenden Sie kurze bis mittellange einfache Sätze (5-20 Wörter): ** Engines für automatische Übersetzung haben häufig Schwierigkeiten bei der Übersetzung verschachtelter und komplexer Sätze sowie bei der Übersetzung von Sätzen mit Semikolon. Pro Satz sollte ein Gedanke enthalten sein. Falls ein Satz zwei aktive Verben enthält, um zwei Gedanken auszudrücken, teilen Sie den Satz in zwei Sätze auf. Engines für automatische Übersetzung haben ferner Probleme damit, zu kurze Sätze zu analysieren, die nur wenig Kontext bieten.
* **Vermeiden Sie Wortfolgen:** Verwenden Sie nach Möglichkeit vollständige Sätze. Wortfolgen sind für Überschriften und Unterüberschriften annehmbar. Vermeiden Sie jedoch einen Telegrammstil beim Schreiben. Verwenden Sie vollständige Sätze, um Listen einzuführen.
* **Vermeiden Sie ideomatische Ausdrücke, Slang und Jargon: ** Ersetzen Sie Wortfolgen, für die eine Übersetzung keinen Sinn ergibt. Ersetzen Sie beispielsweise "on the fly" durch "dynamic," "on the other hand" durch "alternatively" und "keep in mind" durch "remember."
* **Vermeiden Sie Humor, Sarkasmus, Umgangssprache, Emoticons und Metaphern. **
* **Seien Sie prägnant:** Entfernen Sie unnötigen Text und Redundanzen. Ersetzen Sie beispielsweise "It is useful to remember that large values increase the response time" durch "Large values increase the response time."
* **Vermeiden Sie Sätze, die vollständig in Großbuchstaben geschrieben werden.** Die Großschreibung bietet Hinweise auf die Bedeutung des Wortes. Wenn Sie zum Beispiel "BILL" schreiben, kann die Engine für automatische Übersetzung nicht feststellen, ob Sie den Namen Bill oder das englische Wort 'bill' (zu Deutsch: Rechnung) meinen.
* **Vermeiden Sie mehrdeutige Wörter:** Verwenden Sie beispielsweise nicht "once" anstelle von "after" oder "when." Verwenden Sie nicht "while" anstelle von "although" oder "whereas." Verwenden Sie nicht "may", wenn Sie "might" oder "can" meinen.
* **Vermeiden Sie Pronomen:** Wiederholen Sie nach Möglichkeit Nomen und Nominalphrasen. Das Pronomen "it" ist besonders problematisch.
* **Verwenden Sie nach Möglichkeit die Verben im Aktiv:** Sätze im Aktiv sind in der Regel klarer als Sätze im Passiv. Schreiben Sie beispielsweise "The utility determines which path is most efficient" anstelle von "The most efficient path is determined."
* **Vermeiden Sie kulturspezifische Informationen.**
* **Denken Sie daran, dass die Engines für automatische Übersetzung möglicherweise auch Produktnamen übersetzen:** Viele Ländern behalten die ursprünglichen Englischen Produktnamen bei. Die Engines für automatische Übersetzung versuchen möglicherweise Produktnamen zu übersetzen, insbesondere wenn die Namen reale Wörter enthalten. Testen Sie die Übersetzung des Produktnamens, bevor Sie diesen verwenden. Wenn Sie Probleme feststellen, ändern Sie den Text oder die Übersetzung entsprechend.
* **Stellen Sie sicher, dass alle Informationen in einer Sprache geschrieben wurden:** Engines für automatische Übersetzung gehen in der Regel davon aus, dass alle Informationen in einer Sprache vorliegen, auch wenn der Text ein oder zwei Wörter einer anderen Sprache enthält. Wenn der Text beispielsweise "en route" (Französisch) enthält, versucht die Engine für automatische Übersetzung auch diese Wörter zu übersetzen, als seien sie Englisch.
* **Vermeiden Sie die Verwendung von Slogans:** Marketing-Slogan basieren häufig darauf, dass die Zielgruppe ein bestimmtes kulturelles Wissen hat. Vermeiden Sie diese Art von Slogans, da die Engines für automatische Übersetzung voraussichtlich Schwierigkeiten damit haben werden, diese korrekt zu übersetzen.
* **Stellen Sie sicher, dass Listenelemente vollständig sind und eine parallele Struktur aufweisen:** Wenn ein Element mit einem Verb beginnst, stellen Sie sicher, dass alle Elemente mit einem Verb beginnen.
* **Vermeiden Sie die Verwendung von 'please' und 'thank you':** Diese Wörter können in einigen Kulturen unpassend oder gar herablassend wirken.
* **Schreiben Sie Daten nicht im numerischen Format:** Das numerische Datumsformat ist von Land zu Land unterschiedlich. Schreiben Sie den Monatsnamen, den Tag und das Jahr. Schreiben Sie beispielsweise '1 September 2003' anstelle von '9/01/03', was möglicherweise als 1. September 2003 oder als 9. Januar 2003 interpretiert wird.

## Tipps zur Grammatik
{: #grammartips}

* **Verwenden Sie eine korrekte Interpunktion:** Das Auslassen von Punkt und Komma kann dazu führen, dass eine Engine für Interpunktion die Informationen falsch interpretiert.
* **Stellen Sie sicher, dass die Subjekte mit den Verben übereinstimmen: ** Stellen Sie sicher, dass Subjekte im Plural auch Verben im Plural haben und dass Subjekte im Singular Verben im Singular haben.
* **Verwenden Sie einfache Verben im Präsens:** Viele andere Sprachen weisen keine Verbkategorien wie im Englischen auf. Zum Beispiel Passiv- und Zeitformen. Vermeiden Sie nach Möglichkeit Futur und Vergangenheitsformen. Sie können zum Beispiel folgenden Satz: "If you run this program, DB2® will return an error message" wie folgt umschreiben: "If you run this program, DB2 returns an error message."
* **Stellen Sie sicher, dass Pronomen mit Ihrem Bezugswort übereinstimmen:** So sollten zum Beispiel "A user should first determine their tasks" wie folgt korrigiert werden: "Users should first determine their tasks.".
* **Vermeiden Sie nicht korrekt verbundene Nebensätze:** Verwenden Sie Nebensätze korrekt, so dass sie das richtige Nomen modifizieren. So kann zum Beispiel "While typing in commands, the program does not send any messages to you" wie folgt umgeschrieben werden: "While typing in commands, you do not receive any messages from the program."
* **Vermeiden Sie doppelte Negationen:** So kann der Satz "Do not omit the date" ersetzt werden durch: "Include the date."
* **Vermeiden Sie am Anfang von Sätzen die Verbformen Infinitiv (to write), Verlaufsform (writing) und Vergangenheitsform (wrote):** Diese Verbformen sind häufig zweideutige und schwierig zu übersetzen.
* **Vermeiden Sie Folgen von Nomen:** Begrenzen Sie zusammengesetzte Nominalphrasen wie "special filter factor estimate considerations" auf maximal drei Wörter.
* **Vermeiden Sie die Verwendung von Wörtern, die in mehreren grammatikalischen Kategorien vorkommen:** Im Englischen können viele Wörter ein Nomen oder ein Verb sein. Zum Beispiel "default". Diese Struktur ist für viele andere Sprachen nicht zutreffend. Seien Sie konsistent bei der Verwendung jedes einzelnen Wortes. Verwenden Sie "default" beispielsweise immer als Nomen.
* **Stellen Sie sicher, dass die Elemente eines Satzes eine parallele Struktur aufweisen:** Verwenden Sie bei Aufzählungen in einem Satz beispielsweise nur Nomen oder nur Verben. Mischen Sie Nomen und Verben nicht.
* **Lassen Sie notwendige Wörter nicht aus:** Schreiben Sie beispielsweise anstelle von "The file names are displayed in uppercase characters and the file extensions in lowercase." den Satz "The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters." Verwenden Sie das Wort "that", um gegebenenfalls eine Erläuterung anzugeben. Ersetzen Sie beispielsweise "If you determine the problem is a missing file" durch "If you determine that the problem is a missing file."
* **Verwenden Sie den Gedankenstrich nicht für zusätzliche Erläuterungen: ** Schreiben Sie beispielsweise nicht "When you get to this point - the point when all data has been loaded - you need to test the system." Ersetzen Sie die Gedankenstriche durch Kommas oder schreiben Sie den Satz neu.
 
## Tipps zur Terminologie
{: #terminologytips}

* **Verwenden Sie die Terminologie konsistent: ** Vermeiden Sie es, mehrere Benennungen für ein und denselben Gegenstand zu verwenden. Vermeiden Sie es auch, eine Benennung für mehrere Dinge zu verwenden.
* **Schließen Sie Erläuterungen für alle Fachbegriffe ein. **
* **Vermeiden Sie Benennungen, mit unterschiedlichen Bedeutungen in anderen Umgebungen und Kontexten:** Diese Benennungen sind unter anderem "billion," "domestic" und "foreign."
* **Verwenden Sie eine konsistente und standardisierte Großschreibung, Silbentrennung und Wortbildung:** Schreiben Sie beispielsweise in einem Text stets "fix pack" und nicht sowohl "fixpack" als auch "fix pack".
* **Verwenden Sie Kleinschreibung wenn es sich nicht um einen Eigennamen handelt.**
* **Vermeiden Sie besondere Symbole:** Wenn Sie das Symbol # verwenden müssen, bezeichnen Sie es nicht als 'pound sign'. Nennen Sie es stattdessen 'number symbol (#)'.
* **Vermeiden Sie Abkürzungen:** Engines für automatische Übersetzung erkennen möglicherweise allgemein bekannte Abkürzungen wie IBM und DB2. Sie erkennen jedoch nicht alle Abkürzungen. Vermeiden Sie nach Möglichkeit Abkürzungen. Verwenden Sie keine Lateinischen Abkürzungen wie "i.e." und "etc."

## Tipps zur Interpunktion
{: #punctuationtips}

* **Vermeiden Sie die Verwendung des Schrägstrichs mit der Bedeutung von 'und' und 'oder': ** Schreiben Sie den Satz neu, um die exakte Bedeutung auszudrücken. Sie können beispielsweise "You can view the draft copy and/or the review copy" wie folgt neu schreiben: "You can view the draft copy, the review copy, or both."
* **Geben Sie den Plural nicht durch das Hinzufügen von (s) an:** Verwenden Sie entweder den Ausdruck "one or more" oder nur die Pluralform.
* **Verwenden Sie nicht das Et-Zeichen (&) mit der Bedeutung von 'und'.**
* **Verwenden Sie Kommas, um Elemente in einer Aufzählung im Satz zu trennen. Stellen Sie das Komma vor die Konjunktion in der Liste:** Beispiel: "Select your company, location, and profession."

## Tipps zur Rechtschreibung
{: #spellingtips}

* **Überprüfen Sie die Rechtschreibung:** Rechtschreibfehler können zu Übersetzungsfehlern führen. Suchen Sie immer nach Schreibfehlern!
* **Verwenden Sie eine konsistente Schreibweise:** Stellen Sie sicher, dass Begriffe, Akronyme und Eigennamen immer auf dieselbe Weise geschrieben werden. Dies betrifft auch die Schreibweise mit Groß- und Kleinbuchstaben.

## Tipps zur grafischen Darstellung
{: #visualtips}

* **Vermeiden Sie Text in Grafiken.**
* **Vermeiden Sie Formatierungen und Hervorhebungen. **

