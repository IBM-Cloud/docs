---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-20"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} - Fehlerbehebung
{: #ts}

Hier finden Sie Antworten auf allgemeine Fragen zur Fehlerbehebung bei der Verwendung von {{site.data.keyword.iot_full}} in {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Fehler beim Zugriff auf Ihre {{site.data.keyword.iot_short_notm}}-Organisation
{: #access-expiry-problem}

Sie können sich bei einer {{site.data.keyword.iot_short_notm}}-Organisation nicht anmelden, deren Eigner Sie sind.
{:shortdesc}

Sie können sich bei Ihrer {{site.data.keyword.iot_short_notm}}-Organisation weder mit der URL der Organisation noch über die Webadresse `https://internetofthings.ibmcloud.com` direkt anmelden.
{: tsSymptoms}

Die Zugriffsberechtigung für Ihre {{site.data.keyword.iot_short_notm}}-Organisation ist möglicherweise abgelaufen. Für {{site.data.keyword.iot_short_notm}}-Organisationen, die unter Verwendung von {{site.data.keyword.Bluemix}} erstellt wurden, werden standardmäßig temporäre Benutzerprofile verwendet.
{: tsCauses}

Zur Behebung dieses Problem können Sie über {{site.data.keyword.Bluemix_notm}} auf Ihre {{site.data.keyword.iot_short_notm}} zugreifen und die Ablaufeinstellungen für Ihr Benutzerprofil ändern. Gehen Sie wie folgt vor, um die Ablaufeinstellungen für Ihr Benutzerprofil zu ändern:

1. Öffnen Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard Ihren {{site.data.keyword.iot_short_notm}}-Service.
2. Klicken Sie in der Navigationsleiste auf **Mitglieder**.
3. Klicken Sie auf das Bearbeitungssymbol****.
4. Löschen Sie den Inhalt des Felds **Zugriff läuft ab** und klicken Sie auf **Speichern**.
{: tsResolve}

## Problem beim Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}}
{: #connection_problem}

Ihre Verbindung zu {{site.data.keyword.iot_short_notm}} wird unerwartet gelöscht oder unterbrochen.
{:shortdesc}

Wenn Sie versuchen, eine Verbindung zu {{site.data.keyword.iot_short_notm}} herzustellen, empfängt Ihr Gerät oder Ihre Anwendung einen Fehler.
{: tsSymptoms}

Möglicherweise haben Sie zwei Geräte, die versuchen, mithilfe derselben Client-ID und Berechtigungsnachweise eine Verbindung herzustellen. Pro Client-ID ist nur eine eindeutige Verbindung zulässig. Sie können unter Verwendung derselben ID nicht zwei gleichzeitig bestehende Verbindungen haben. Anwendungen können denselben API-Schlüssel gemeinsam nutzen; MQTT erfordert jedoch, dass die Client-ID jeweils eindeutig ist.
{: tsCauses}

Sie können dieses Problem beheben, indem Sie bestätigen, dass Sie nicht zwei Geräte haben, die versuchen, mithilfe derselben Berechtigungsnachweise eine Verbindung aufzubauen.
{: tsResolve}

## Sporadisches Auftreten einer Unterbrechung der Verbindung des Geräts zu {{site.data.keyword.iot_short_notm}}
{: #disconnection_problem}

Sporadisches Auftreten einer Löschung der Geräteverbindung zu {{site.data.keyword.iot_short_notm}}
{:shortdesc}

Es tritt sporadisch auf, dass die Verbindung für ein mit dem {{site.data.keyword.iot_short_notm}}-Service verbundenes Gerät unterbrochen wird. Das Gerät stellt die Verbindung wieder her, aber die Verbindung wird nach einem kurzen Zeitraum wieder unterbrochen.
{: tsSymptoms}

Möglicherweise verwenden Sie beim Herstellen einer Verbindung einen zu niedrigen Wert für eine MQTT-Ping-Option, wodurch es so aussieht, als habe die Verbindung das Zeitlimit überschritten. Wenn das Client-MQTT falsch festgelegt wurde, werden Pingsignale nicht zeitnah empfangen und die Verbindung wird geschlossen.
{: tsCauses}

Sie können dieses Problem beheben, indem Sie bestätigen, dass Sie die Parameter für Ping und Keepalive für Ihre Verbindung richtig festgelegt haben.   
{: tsResolve}


## Hilfe und Unterstützung für {{site.data.keyword.iot_short_notm}} abrufen
{: #gettinghelp}

Bei Problemen und Fragen zur Verwendung von {{site.data.keyword.iot_short_notm}} können Sie Hilfe anfordern, indem Sie nach Informationen suchen oder über ein Forum Fragen stellen. Sie können auch ein Support-Ticket öffnen.

Wenn Sie zum Stellen von Fragen die Foren verwenden, müssen Sie Ihre Frage mit einem Tag versehen, damit die {{site.data.keyword.Bluemix_notm}}-Entwicklungsteams auf sie aufmerksam werden.

* Wenn Sie technische Fragen dazu haben, wie eine App mithilfe von {{site.data.keyword.iot_short_notm}} entwickelt oder implementiert wird, posten Sie Ihre Fragen an [Stack Overflow ![Symbol für externen Link](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=watson-iot+ibm-bluemix){:new_window} und verwenden Sie die Tags 'ibm-bluemix' und 'watson-iot'.
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* Verwenden Sie für Fragen zu den Anweisungen für Services und die Einführung das Forum [IBM developerWorks dW Answers ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/watson-iot/?smartspace=bluemix){:new_window}. Schließen Sie die Tags 'watson-iot' und 'bluemix' ein.

Weitere Details zur Verwendung der Foren finden Sie in [Hilfe anfordern](https://www.{DomainName}/docs/support/index.html#getting-help).

Informationen zum Öffnen eines IBM Support-Tickets oder zu Supportebenen und zur Priorität von Tickets finden Sie unter [Support kontaktieren ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://www.{DomainName}/docs/support/index.html#contacting-support).
