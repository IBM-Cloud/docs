---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Einführung in {{site.data.keyword.openwhisk_short}}
*Letzte Aktualisierung: 17. Februar 2016*

{{site.data.keyword.openwhisk}} ist ein verteilter, ereignisgesteuerter Berechnungsservice. {{site.data.keyword.openwhisk_short}} führt Anwendungslogik in Reaktion auf Ereignisse oder direkte Aufrufe durch Web-Apps oder mobile Apps über HTTP aus. Ereignisse können von Bluemix-Services wie Cloudant und von externen Quellen bereitgestellt werden. Entwickler können sich auf das Schreiben von Anwendungslogik sowie auf das Erstellen von Aktionen, die auf Anforderung ausgeführt werden, konzentrieren. Die Rate der Ausführung von Aktionen entspricht immer der Ereignisrate, sodass sich eine inhärente Skalierung und Ausfallsicherheit sowie eine optimale Auslastung ergeben. Sie bezahlen nur für das, was Sie nutzen, und Sie brauchen keinen Server zu verwalten. Sie können darüber hinaus den [Quellcode](https://github.com/openwhisk/openwhisk) erhalten und das System selbst ausführen.
{: shortdesc}

Weitere Einzelheiten zur Funktionsweise von {{site.data.keyword.openwhisk_short}} finden Sie unter [Informationen zu {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

## {{site.data.keyword.openwhisk_short}} einrichten
Sie können Ihren Namensbereich und Ihren Berechtigungsschlüssel über die {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle (CLI) einrichten. Navigieren Sie zu [CLI konfigurieren](https://console.{DomainName}/openwhisk/cli){: new_window} und befolgen Sie die geführten Schritte für die Installation. Beachten Sie, dass Python 2.7 auf Ihrem System installiert sein muss, damit Sie die Befehlszeilenschnittstelle verwenden können.

Nach der Einrichtung von {{site.data.keyword.openwhisk_short}} mithilfe der Befehlszeilenschnittstelle können Sie mit der Verwendung über die Befehlszeile oder durch REST-APIs beginnen.

## {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle (CLI) verwenden
Wenn Sie Ihre Umgebung konfiguriert haben, können Sie mit der Verwendung der {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle zu folgenden Zwecken beginnen:

* Sie können Code-Snippets oder Aktionen in {{site.data.keyword.openwhisk_short}} ausführen. Siehe [Aktionen erstellen und aufrufen](./openwhisk_actions.html).
* Sie können Ihre Aktionen durch Auslöser und Regeln so einrichten, dass sie auf Ereignisse reagieren. Siehe [Auslöser und Regeln erstellen](./openwhisk_triggers_rules.html).
* Sie können sich informieren, wie Aktionen in Paketen gebündelt und externe Ereignisquellen konfiguriert werden. Siehe [Pakete verwenden und erstellen](./openwhisk_packages.html).
* Sie können den Katalog der Pakete durchsuchen und Ihre Anwendungen durch externe Services wie zum Beispiel eine [Cloudant-Ereignisquelle](./openwhisk_catalog.html#openwhisk_catalog_cloudant) erweitern. Siehe [Für {{site.data.keyword.openwhisk_short}} eingerichtete Services verwenden](./openwhisk_catalog.html).


## {{site.data.keyword.openwhisk_short}} über eine iOS-App verwenden
Sie können {{site.data.keyword.openwhisk_short}} mithilfe des {{site.data.keyword.openwhisk_short}}-iOS-SDK über Ihre mobile iOS-App oder Apple Watch verwenden. Weitere Details finden Sie in der [iOS-Dokumentation](./openwhisk_mobile_sdk.html).

## REST-APIs mit {{site.data.keyword.openwhisk_short}} verwenden
Nach der Einrichtung Ihrer {{site.data.keyword.openwhisk_short}}-Umgebung können Sie {{site.data.keyword.openwhisk_short}} mit Ihren Web-Apps oder mobilen Apps mithilfe von REST-API-Aufrufen verwenden. Weitere Details zu den APIs für Aktionen, Aktivierungen, Pakete, Regeln und Auslöser finden Sie in der [API-Dokumentation für {{site.data.keyword.openwhisk_short}}](https://new-console.{DomainName}/apidocs/98).

## {{site.data.keyword.openwhisk_short}}-Beispiel Hello World
Für den Einstieg in {{site.data.keyword.openwhisk_short}} können Sie das folgende Beispiel für JavaScript-Code ausprobieren.

```
/**
 * Hello World als OpenWhisk-Aktion.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

Führen Sie die folgenden Schritte aus, um dieses Beispiel zu verwenden:

1. Speichern Sie den Code in einer Datei. Beispiel: *hello.js*.

2. Erstellen Sie die Aktion, indem Sie über die Befehlszeile der {{site.data.keyword.openwhisk_short}}-CLI den folgenden Befehl eingeben:

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. Rufen Sie anschließend die Aktion auf, indem Sie die folgenden Befehle eingeben.

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    Dieser Befehl liefert die folgende Ausgabe:

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Dieser Befehl liefert die folgende Ausgabe:

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

Sie können darüber hinaus die ereignisgesteuerten Funktionen in {{site.data.keyword.openwhisk_short}} verwenden, um diese Aktion als Reaktion auf Ereignisse aufzurufen. Gehen Sie wie im [Beispiel für den Service Alarm](./openwhisk_packages.html#openwhisk_packages_trigger) beschrieben vor, um eine Ereignisquelle zu konfigurieren, sodass die Aktion `hello` jedes Mal aufgerufen wird, wenn ein regelmäßiges Ereignis generiert wird.


## Systemdetails

Weitere Informationen zu {{site.data.keyword.openwhisk_short}} finden Sie in den folgenden Abschnitten:

* [Entitätsnamen](./openwhisk_reference.html#openwhisk_entities)
* [Aktionssemantik](./openwhisk_reference.html#openwhisk_semantics)
* [Begrenzungen](./openwhisk_reference.html#openwhisk_syslimits)
* [REST-API](https://new-console.{DomainName}/apidocs/98)

# Zugehörige Links
## API
* [REST-API-Dokumentation](https://new-console.{DomainName}/apidocs/98){:new_window}

## Allgemein
* [Entdecken Sie: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} auf IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
