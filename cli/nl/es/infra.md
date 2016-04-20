---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}

#  Capas de la infraestructura de Bluemix

*Última actualización: 15 de marzo de 2016*

{{site.data.keyword.Bluemix_notm}} abstrae y oculta las capas de sistema operativo y de infraestructura para que el usuario no tenga que gestionarlas. Sin embargo, es posible que en alguna ocasión desee obtener más información sobre el sistema operativo y el middleware de la app.
{:shortdesc}

## Visualización de las capas de la infraestructura de Bluemix
{:viewinfra}

Puede ejecutar el mandato cf stacks para mostrar las pilas disponibles o los sistemas de archivo raíz en los que están desplegadas las apps. También puede especificar la pila cuando utilice el mandato cf push con la opción *-s* y el *nombre_pila*, donde el nombre_pila es el sistema de archivos raíz, como `lucid64` o `cflinuxfs2`:
```
cf push nombreApp -s nombre_pila
```
Puede utilizar el mandato `cf buildpacks` para mostrar los componentes de middleware, como Perfil de WebSphere Liberty y SDK para Node.js, disponibles como tiempos de ejecución en los que se puede ejecutar la app. También puede especificar el entorno de tiempo de ejecución de la app con el siguiente mandato:
```
cf push nombreApp -b nombre_paquete_compilación
```
