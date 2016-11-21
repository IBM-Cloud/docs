---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Declaración de soporte de paquete de compilación
{: #buildpack_support_statement}

Última actualización: 8 de septiembre de 2016
{: .last-updated}

## Paquetes de compilación de IBM incorporados
{: #built-in_ibm_buildpacks}

* [Liberty for Java](../runtimes/liberty/index.html)
* [SDK for Node.js](../runtimes/nodejs/index.html)
* [ASP.NET Core](../runtimes/dotnet/index.html)

IBM dará soporte a dos versiones (n & n - 1) de cada paquete de compilación de tiempo de ejecución que se proporcionan en Bluemix (p. ej., IBM Liberty Buildpack v1.22 & IBM Liberty Buildpack v1.21). Cada paquete de compilación proporcionará y dará soporte a una o más versiones principales de su tiempo de ejecución correspondiente según convenga (p. ej., IBM SDK, Java Technology Edition Version 7 Release 1 y Version 8). Por lo general, los paquetes de compilación se actualizan cada dos semanas con la última versión menor del tiempo de ejecución que esté disponible. La política anterior garantiza que se dé soporte a cualquier versión de tiempo de ejecución desplegada durante 1 mes como mínimo a partir del momento del despliegue.

Se pueden notificar problemas contra cualquier versión del paquete de compilación de IBM integrado soportado actualmente en Bluemix, pero se deben verificar contra la versión más reciente. Si se detecta un defecto, IBM proporcionará un arreglo en un futuro nivel del tiempo de ejecución y el paquete de compilación correspondiente. IBM no proporcionará arreglos para versiones principales y menores anteriores (N-1, n-1). IBM no proporcionará soporte para tiempos de ejecución de comunidad incluso cuando se utilicen paquetes de compilación de IBM, por ejemplo, Open JDK con el paquete de compilación Liberty. Estos tiempos de ejecución de comunidad siguen la misma política de soporte que los anteriores "Paquetes de compilación de comunidad integrados".

## Paquetes de compilación de la comunidad incorporados
{: #built-in_community_buildpacks}

Cloud Foundry Community proporciona los siguientes paquetes de compilación de comunidad integrados:

* [Java](../runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](../runtimes/php/index.html)
* [Ruby](../runtimes/ruby/index.html)
* [Python](../runtimes/python/index.html)
* [Go](../runtimes/go/index.html)

Las actualizaciones de estos paquetes de compilación se realizarán cuando se actualice a una versión nueva de Cloud Foundry. Se pueden notificar problemas con estos tiempos de ejecución en Bluemix a IBM para obtener ayuda a la hora de determinar si Bluemix es el origen del problema. Para problemas relacionados con Bluemix, IBM proporcionará un arreglo; sin embargo, para los defectos del propio paquete de compilación o tiempo de ejecución, IBM le ayudará a notificarlos a la comunidad pertinente. IBM no proporcionará arreglos para estos paquetes de compilación y tiempos de ejecución.

## Paquetes de compilación externos
{: #external_buildpacks}


IBM no ofrece soporte para paquetes de compilación externos. Es posible que se deba poner en contacto con la comunidad de Cloud Foundry para obtener ayuda. 


