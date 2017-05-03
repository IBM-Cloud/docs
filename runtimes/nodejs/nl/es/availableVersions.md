---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versiones disponibles
{: #available_versions}

{{site.data.keyword.Bluemix}} proporciona todos los [modos de ejecución de Node.js
disponibles actualmente](http://nodejs.org/dist/). De esos, IBM proporciona versiones que contienen las mejoras y los arreglos de errores. Consulte [Últimas actualizaciones del paquete de compilación Node.js](/docs/runtimes/nodejs/updates.html) para obtener más información.
{: shortdesc}

El paquete de compilación Node.js de IBM almacena en caché las versiones de tiempo de ejecución de IBM. Por este motivo, si utiliza IBM SDK para el tiempo de ejecución Node.js en la aplicación, obtiene el rendimiento de la aplicación más rápido si la aplicación se envía por push a Bluemix.

Utilice el parámetro **nodo** en la sección **motores** del archivo **package.json** para especificar la versión de tiempo de ejecución de Node.js que desee ejecutar.

Utilice el parámetro **npm** en la sección **motores** del archivo **package.json** si necesita especificar una versión de npm que no sea la versión empaquetada con Node.js.  

Consulte el siguiente ejemplo:

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

Debería especificarse siempre una versión de nodo en el archivo **package.json**. Si no, se utilizará la versión del nodo más reciente.
