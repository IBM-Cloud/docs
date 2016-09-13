---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Aktionstypen{: #actions}

Außer dem Anzeigen von Alerts im Alerts-Dashboard unterstützt {{site.data.keyword.iotrtinsights_short}} verschiedene Typen von durch Regeln ausgelöste Aktionen, wie zum Beispiel das Senden von E-Mails und Webhooks.
{: shortdesc}

## Aktionen erstellen{: #shared}
Sie können [Aktionen direkt über den Regeleditor erstellen](rules.html "Regeln erstellen") oder die Aktionen in der Anzeige "Aktionen" erstellen und anschließend die Aktionen beim Erstellen der Regeln auswählen. 

Gehen Sie wie folgt vor, um eine Aktion über die Anzeige "Aktionen" zu erstellen: 
1. Gehen Sie in der {{site.data.keyword.iotrtinsights_short}}-Konsole zu **Analytics > Aktionen**.
2. Klicken Sie auf **Neue Aktion hinzufügen**, wählen Sie einen Aktionstyp aus, benennen Sie die Aktion und geben Sie eine Beschreibung ein. 
3. Geben Sie die erforderlichen Parameter für den Typ der Aktion an, die Sie erstellen.
Aktionstypen:   
 - [E-Mail senden](#email "E-Mail senden")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#ifttt "IFTTT")
4. Klicken Sie auf **OK**, um die neue Aktion zu erstellen. 

Die Aktion steht nun im [Regeleditor](rules.html#rules "Regeleditor") zur Verfügung.



## E-Mail senden{: #email}
Verwenden Sie die Aktion zum Senden einer E-Mail, um eine E-Mail an einen oder mehrere Empfänger zu senden, wenn eine Regel ausgelöst wird. 

Beispiel: [E-Mail senden](action_examples.html#emailex).

Die folgenden Parameter werden verwendet, um die Aktion zum Senden einer E-Mail zu konfigurieren: 

Parameter | Beschreibung
---|---
Name | Der Name der Aktion, der im Alerts-Dashboard verwendet wird.
Beschreibung | Eine Kurzbeschreibung der Aktion.
An | Eine oder mehrere, durch Kommas getrennte E-Mail-Adressen.
CC | Eine oder mehrere, durch Kommas getrennte E-Mail-Adressen.
Betreff | Die Betreffzeile der E-Mail. Optional können Sie den Betreff automatisch mit "IoT Real-Time Insight-Alert" beginnen.

Der Hauptteil der E-Mail wird automatisch aus der Nachricht des Geräts erstellt, die empfangen wurde, als die Regel ausgelöst wurde.   
**Wichtig:** Wenn die Gerätedaten sensible Informationen enthalten, können Sie auswählen, dass die Gerätedaten nicht in die E-Mail-Nachricht aufgenommen werden, sondern nur in der Alertanzeige aufgelistet werden. 


## Webhook {: #webhook}
Verwenden Sie die Webhook-Aktion, um eine HTTP-Anforderung an einen webhook-fähigen Web-Service zu senden, wenn ein Alert ausgelöst wird. Ein Webhook könnte beispielsweise verwendet werden, um einen Service Request für ein Asset zu erstellen, wenn ein Sensor in dem Gerät einen ungewöhnlichen Wert misst. 

Beispiel: [Webhook zum Posten in Slack verwenden](action_examples.html#webhookex).

Die folgenden Parameter werden verwendet, um eine Webhook-Aktion zu konfigurieren: 

Parameter | Beschreibung
---|---
Name | Der Name der Aktion, der im Alerts-Dashboard verwendet wird.
Beschreibung | Eine Kurzbeschreibung der Aktion.
URL | Die URL des webhook-fähigen Zielservers. **Tipp:** Sie können [Variablensubstitution](#variable_substitution) verwenden, um zusätzliche Daten dynamisch in die URL einzubeziehen.
Methode | Der Type des Webhook-Aufrufs, der ausgeführt werden soll. Wählen Sie einen der folgenden Typen aus: GET, HEAD, OPTIONS, PATCH, PUT, POST oder DELETE.
Benutzername | Geben Sie diese Information an, falls für den Web-Service erforderlich.
Kennwort | Geben Sie diese Information an, falls für den Web-Service erforderlich.
**Wichtig:** Das Kennwort wird als Klartext gesendet.
Kopfzeile | Kopfzeilen bestehen aus Schlüssel/Wert-Paaren. **Tipp:** Sie können [Variablensubstitution](#variable_substitution) verwenden, um zusätzliche Daten dynamisch in die Kopfzeile einzubeziehen.
Inhaltstyp | Der Inhaltstyp des Hauptteils: JSON, XML, Text im Format www-url-encoded oder unformatierter Text.
Verfügbar für die Methoden OPTIONS, PATCH, PUT, POST und DELETE.
Hauptteil | Der Hauptteil des Webhook-Aufrufs. Verfügbar für die Methoden OPTIONS, PATCH, PUT, POST und DELETE.
Standardmäßig ist das Textfeld vorausgefüllt mit allen Variablen, die in [Variablensubstitution](#variable_substitution) aufgelistet sind. Wählen Sie **Angepassten Nachrichtenhauptteil verwenden** aus, um den Inhalt des Hauptteilfelds zu bearbeiten. **Wichtig:** Für den Webhook-Server müssen möglicherweise bestimmte Felder im Hauptteil enthalten sein. Beispiel: Ein Slack-Webhook muss das Feld "text" enthalten.    



## Node-RED {: #nodered}
Verwenden Sie die Node-RED-Aktion, um eine Verbindung zu einer Node-RED-Anwendung herzustellen, wenn eine Regel ausgelöst wird. Weitere Informationen zur Verwendung von Node-RED finden Sie im Thema [Creating apps with the Internet of Things starter application](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500). 

Beispiel: [Node-RED zum Senden einer Textnachricht verwenden](action_examples.html#noderedex).

Die folgenden Parameter werden verwendet, um eine Node-RED-Aktion zu konfigurieren: 

Parameter | Beschreibung
---|---
Name | Der Name der Aktion, der im Alerts-Dashboard verwendet wird.
Beschreibung | Eine Kurzbeschreibung der Aktion.
URL | Die URL Node-RED-HTTP-Zieleingabeknotens.
Benutzername | Geben Sie diese Information an, falls für den Node-RED-Service erforderlich.
Kennwort | Geben Sie diese Information an, falls für den Node-RED-Service erforderlich.
**Wichtig:** Das Kennwort wird als Klartext gesendet.
Hauptteil | Standardmäßig ist das Textfeld vorausgefüllt mit allen Variablen, die in [Variablensubstitution](#variable_substitution) aufgelistet sind. Wählen Sie **Angepassten Nachrichtenhauptteil verwenden** aus, um den Inhalt des Hauptteilfelds zu bearbeiten.
## IFTTT {: #ifttt}
Verwenden Sie die IFTTTT-Aktion, um ein IFTTT-Rezept auszulösen, wenn eine Regel ausgelöst wird. Weitere Informationen zum Auslösen von Real-Time Insights-Aktionen als IFTTT-Rezepte finden Sie im Thema [Maker Channel](https://ifttt.com/maker) auf der IFTTT-Site.

Beispiel: [IFTTT zum Posten einer Trello-Karte verwenden](action_examples.html#iftttex).

Die folgenden Parameter werden verwendet, um eine IFTTT-Aktion zu konfigurieren: 

Parameter | Beschreibung
---|---
Name | Der Name der Aktion, der im Alerts-Dashboard verwendet wird.
Beschreibung | Eine Kurzbeschreibung der Aktion.
Schlüssel | Der Schlüssel für den Maker-Kanal, der zum Auslösen des Ereignisses verwendet werden soll.
Ereignis | Der Ereignisname, den Sie als Auslöser für das Maker-Ereignis konfiguriert haben. Sie können mehrere Rezepte mit unterschiedlichen Auslösern erstellen, von denen jedes einen anderen Ereignisnamen hat.
Wert 1-3 | Sie können beliebigen Inhalt in diesen Parametern übergeben, die an die Aktion in Ihrem IFTTT-Rezept weitergegeben werden. **Tipp:** Sie können [Variablensubstitution](#variable_substitution) verwenden, um zusätzliche Daten dynamisch with die Kopfzeile einzubeziehen.
## Variablensubstitution{: #variable_substitution}
Verwenden Sie die folgenden Variablensubstitutionen, um dynamisch Gerätedaten einzubeziehen. Die Variable muss zwischen doppelten geschweiften Klammern stehen. 

Variable | Beschreibung
---|---
**URL, Kopfzeile und Hauptteil** |
`{{timestamp}}` | Die Zeitmarke der Nachricht
`{{tenantId}}` | Die ID des Real-Time Insights-Service
`{{deviceId}}` | Die ID des Geräts
`{{ruleName}}` | Der Name der Regel, die die Aktion umfasst
**Nur Hauptteil** |
`{{ruleDescription}}`| Die Beschreibung der Regel, die die Aktion umfasst
`{{ruleCondition}}` | Die Regelbedingung, die die Aktion ausgelöst hat
`{{message}}` | Die unformatierte Gerätenachricht, die den Datenpunktwert enthielt, durch den die Regel ausgelöst wurde
