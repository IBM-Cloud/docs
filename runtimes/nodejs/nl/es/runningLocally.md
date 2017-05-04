---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Consejos para ejecutar la aplicación Node.js de forma local
{: #hints}

Utilice esta información para facilitar la ejecución de la aplicación Node.js localmente y en Bluemix.
{: shortdesc}

El ejemplo siguiente muestra parte de la fuente para un archivo **js**:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Con este código, cuando la aplicación se esté ejecutando en Bluemix, la variable de entorno PORT contiene el valor de puerto que es interno de Bluemix y en el que la app escucha conexiones entrantes. Cuando la aplicación se ejecuta localmente, PORT no está definido, de modo que se utiliza **3000** como número de puerto. Grabados de esta forma, puede ejecutar la aplicación localmente a efectos de prueba y en Bluemix sin realizar más cambios.
