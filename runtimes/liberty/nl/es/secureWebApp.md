---

copyright:
  years: 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Cómo escribir aplicaciones web Java seguras
{: #secure_java_web_app}

Todas las aplicaciones web se deben designar y codificar pensando en la seguridad para evitar la incorporación de vulnerabilidades de seguridad graves.
{: shortdesc}

{{site.data.keyword.Bluemix}} proporciona una aplicación de iniciación segura para ayudarle a escribir código Java Liberty más segura y evitar la mayoría de los problemas de Cross-Site Scripting (XSS). Puede descargar esta [aplicación de iniciación segura](https://github.com/IBM-Bluemix/java-secure-app), compilarla y desplegarla localmente y en {{site.data.keyword.Bluemix_notm}}.

## Por qué escribir apps web seguras
{: #why}

Diversos ataques de seguridad pueden aprovechar una vulnerabilidad de seguridad. Un ataque puede robar credenciales, provocar la pérdida de datos y funciones, interrumpir servicios y dañar la reputación y los ingresos de una empresa. Cross-Site-Scripting, XSS, es una de las vulnerabilidades de seguridad más comunes que se encuentran en la mayoría de las aplicaciones web que deben evitarse.

En lugar de aprender la teoría de los ataques XSS y las técnicas para ponerles remedio, antes de comenzar el desarrollo de la aplicación web puede utilizar esta [aplicación de iniciación segura](https://github.com/IBM-Bluemix/java-secure-app). La aplicación de iniciación segura incluye ejemplos de codificación de prácticas de codificación segura de claves que evita XSS para que pueda empezar a desarrollar mientras aprende y aplica técnicas de prevención de XSS.

## Cómo utilizar la app de ejemplo segura
{: #how}

Puede utilizar la [aplicación de iniciación segura](https://github.com/IBM-Bluemix/java-secure-app) como un punto de partida para el desarrollo de una nueva aplicación Liberty. Empiece por aprender el código de medidas de prevención de XSS de la app y luego aplíquelo a las operaciones de la API de la aplicación. Las medidas de prevención de la aplicación de iniciación segura ayudan a evitar que una entrada maliciosa de un usuario ocasione daños en la aplicación y en el servidor y el navegador mediante la mitigación o prevención de ataques XSS.

En primer lugar, descargue esta aplicación de iniciación segura y compílela y despliéguela en Bluemix o localmente del mismo modo que lo haría con la aplicación de ejemplo [getting-started-java](https://github.com/IBM-Bluemix/get-started-java).  Vaya a [Iniciación a Liberty en Bluemix](getting-started.html) para obtener más información sobre cómo compilar y desplegar aplicaciones en Bluemix.  Para empezar, puede seguir estos pasos para clonar, compilar y ejecutar la app.

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
Visualice la app en http://localhost:9080/GetStartedSecureJava/

## Más información
{: more}
La aplicación de iniciación segura contiene **BadServlet.java**. Esta aplicación muestra un ejemplo de código no seguro que pueden escribir los desarrolladores si no prestan la atención necesaria.

La aplicación de iniciación segura también contiene **GoodServlet.java**, que incluye varias buenas prácticas de codificación segura, como validación de entrada, codificación de salida, valores seguros de cabeceras HTTP y política de seguridad de contenido. Estas prácticas constituyen medidas de prevención claves contra XSS. Su aplicación también puede mitigar otras vulnerabilidades de inyección y de cruce de directorios.

Consulte la [Hoja de apuntes de prevención de XSS ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.owasp.org/index.php/XSS){: new_window} para obtener más información sobre XSS y sus medidas de prevención.
