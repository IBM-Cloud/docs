---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Comando di avvio
{: #startup_commmand}

Per specificare un comando di avvio per la tua applicazione Node.js Bluemix si consiglia di utilizzare un file **Procfile** o **package.json**.
{: shortdesc}

Specifica un comando di avvio nel tuo **Procfile** nel seguente formato. Qui, app.js è lo script js di avvio per la tua applicazione.
```
web: node app.js
```
{: codeblock}

Salva il **Procfile** nella directory root della tua applicazione.

Se non è presente un **Procfile**, il pacchetto di build Node.js IBM Bluemix verifica se è presente una voce scripts.start nel file **package.json**. Anche nell'esempio sottostante, app.js è lo script js di avvio per la tua applicazione.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Se nel file **package.json** è presente una voce di script di avvio, un **Procfile** viene generato automaticamente. Il contenuto del **Procfile** generato automaticamente è il seguente:
```
    web: npm start
```
{: codeblock}

Per ulteriori informazioni sui file **Procfile** e **package.json** consulta [Tips for Node.js Applications ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
