---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Mandato de inicio
{: #startup_commmand}

Para especificar un mandato de inicio para la aplicación Node.js de Bluemix, se recomienda utilizar un archivo **Procfile** o **package.json**.
{: shortdesc}

Especifique un mandato de inicio en el **Procfile** en el formulario que se indica a continuación. Aquí, app.js es el script js de inicio de la aplicación.
```
web: node app.js
```
{: codeblock}

Guarde **Procfile** en el directorio raíz de la aplicación.

Si un **Procfile** no está presente, el paquete de compilación IBM Bluemix Node.js comprobará si existe una entrada scripts.start en el archivo **package.json**. De nuevo, en el siguiente ejemplo, app.js es el script js de inicio de la aplicación.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Si existe una entrada de script en el archivo **package.json**, se genera un
**Procfile** automáticamente. El contenido del **Procfile** generado automáticamente es:
```
    web: npm start
```
{: codeblock}

Para obtener más información sobre el archivo **Procfile** y **package.json**, consulte [Consejos para aplicaciones Node.js![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
