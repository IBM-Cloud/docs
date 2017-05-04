---

copyright:
  years: 2017
lastupdated: "2017-02-06"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Resolución de problemas de SDK for Nodejs
{: #ts}


Aquí encontrará las respuestas a preguntas frecuentes sobre la resolución de problemas sobre el uso de SDK for Nodejs en {{site.data.keyword.Bluemix}}.
{:shortdesc}

## La aplicación no se inicia con el error “No queda espacio en el dispositivo”
{: #no_space_left_on_device}


Una aplicación Nodejs no se inicia con el error “No queda espacio en el dispositivo”. Por ejemplo, el error puede parecerse al siguiente en los registros:
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: No se puede grabar: No queda espacio en el dispositivo

```
{: #codeblock}

Las aplicaciones Nodejs que utilizan versiones de NPM anteriores a la versión 3 consumen más espacio al descargar dependencias.
{: tsCauses}

Modifique el archivo package.json de la aplicación de modo que utilice NPM versión 3 o posterior.
{: tsResolve}

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}
