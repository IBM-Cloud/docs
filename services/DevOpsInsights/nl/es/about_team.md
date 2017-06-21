---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acerca de Team Dynamics

{{site.data.keyword.DRA_full}} Team Dynamics utiliza un análisis de codificación social para identificar el nivel de interacción entre los miembros del equipo para corregir prácticas improductivas en el equipo. 
{:shortdesc}

Después de abrir {{site.data.keyword.DRA_short}} desde la cadena de herramientas, pulse **Team Dynamics**. Desde allí, puede seleccionar una categoría analítica para profundizar en las prácticas y en los hábitos de colaboración de su equipo. Lo que indica cada conjunto de datos puede variar de equipo a equipo. Podrá profundizar en cada visualización para obtener ayuda e información.  

## Categorías de datos

Los datos que utiliza {{site.data.keyword.DRA_short}} para llenar sus paneles de control se extraen automáticamente desde el repositorio de control de código fuente del equipo. Podrá obtener más información sobre lo que significan los datos y cómo se aplican a su proyecto pulsando **Información** o **Instrucciones** en cualquier gráfico.

### Codificación social

El gráfico de Codificación social muestra las conexiones entre los contribuidores del proyecto de una forma altamente interactiva y visual. Cada nodo en el gráfico representa un desarrollador. El tamaño de un nodo aumenta de forma logarítmica de acuerdo a las contribuciones del desarrollador a un proyecto. Las líneas entre nodos indican una colaboración. Cuanto más gruesa es una línea, más han colaborado los desarrolladores durante el periodo seleccionado. 

Cada nodo se colorea azul y rojo de forma variable. El color azul indica cuántas líneas de código ha añadido un contribuidor como una parte del total del número de líneas que ha modificado el contribuidor. El color rojo indica cuántas líneas de código ha eliminado un contribuidor. Un contribuidor que únicamente hubiese añadido código sería totalmente azul, mientras que un contribuidor que hubiese añadido y eliminado un mismo número de líneas estaría con una mitad azul y con la otra mitad en rojo. 

### Autores

La categoría de Autores proporciona el número de confirmaciones, cambios de línea y cambios de archivo por contribuidor de repositorio. A pesar de que el número total de líneas codificadas no se debería utilizar para determinar la contribución neta de un miembro del equipo al proyecto, esta información puede ser valiosa para los gestores y responsables del equipo. Un miembro del equipo que aporta un número excesivo de cambios de línea podría estar desbordado de trabajo y originar un cuello de botella en sus procesos, o estar codificando en un estilo distinto y más sobrecargado en comparación a otros miembros del equipo. 
