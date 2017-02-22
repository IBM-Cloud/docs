---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Mit Verzeichnissen arbeiten

Swift hat keine eigentliche Verzeichnisstruktur, verwendet jedoch eine bestimmte Benennung, um eine Verzeichnisstruktur darzustellen. Wenn Sie einen Verzeichnisnamen angeben, wird dieser als Teil des relativen Pfads an alle Dateinamen angehängt.
{: shortdesc}

## Mithilfe der Swift-CLI einem Container ein Verzeichnis hinzufügen

Zum Hinzufügen eines Verzeichnisses zu einem Container muss die Verzeichnisstruktur auf Ihrem lokalen Gerät vorhanden sein.

1. Erstellen Sie ein lokales Verzeichnis und speichern Sie Ihre Datei.
2. Führen Sie den folgenden Befehl aus, um ein Verzeichnis in Ihren Container hochzuladen.

    ```
    swift upload <Containername> <Verzeichnisname>
    ```
    {: pre}

## Verzeichnis über die CLI herunterladen
Zum Herunterladen einer Verzeichnisstruktur verwenden Sie den Parameter `-prefix`, um das Verzeichnis bzw. die Verzeichnisstruktur anzugeben, das/die heruntergeladen werden soll.

1. Führen Sie den folgenden Befehl aus, um ein Verzeichnis herunterzuladen.

    ```
    swift download <Containername> --prefix <Verzeichnis>
    ```
    {: pre}
