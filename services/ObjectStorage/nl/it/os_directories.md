---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo delle directory

Swift non ha una vera struttura di directory ma utilizza la denominazione per rappresentare un layout di directory. Se specifichi un nome della directory, viene allegato a tutti i nomi file come parte del relativo percorso.
{: shortdesc}

## Aggiunta di una directory a un contenitore con la CLI Swift

Per aggiungere una directory a un contenitore, devi devi disporre della struttura della directory al posto del tuo dispositivo locale.

1. Localmente, crea una directory e salva il tuo file.
2. Esegui il seguente comando per caricare una directory nel tuo contenitore.

    ```
    swift upload <container_name> <directory_name>
    ```
    {: pre}

## Scaricamento di una directory con la CLI
Per scaricare una struttura di directory, utilizza il parametro `-prefix` per indicare la directory o la struttura di directory che vuoi scaricare.

1. Esegui il seguente comando per scaricare una directory.

    ```
    swift download <container_name> --prefix <directory>
    ```
    {: pre}
