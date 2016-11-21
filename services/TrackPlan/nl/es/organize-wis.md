---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Organización y filtrado de elementos de trabajo{: #tp-organize}  

*Última actualización: 29 de abril de 2016*
{: .last-updated}

El servicio de {{site.data.keyword.trackplan}} incluye varias opciones para clasificar y organizar los elementos de trabajo.
{: shortdesc}

##Filtrado de elementos de trabajo{: #tp-filteringwis}

Puede filtrar elementos de trabajo basados en palabras o en valores para atributos específicos. 

El filtrado está soportado en estas vistas:   
- Mi trabajo
- Elementos donde estoy suscrito
- Trabajo entrante
- Proceso
- Planificación del sprint
- Trabajo del equipo
- Todo el trabajo

Si escribe una palabra, se mostrarán los resúmenes de elementos de trabajo que contienen dicha palabra. También puede filtrar elementos de trabajo basados en valores para atributos específicos. Para obtener detalles, consulte la tabla siguiente.

| Atributo |Ejemplo | 
|-------|-------|
|*Tipo  | `*Defecto` |
|#Etiqueta  | `#conferencia`| 
|@:Propietario  | `@:jasmith`|
|$Prioridad|`$Alta`|
|!Gravedad|`!Mayor`|       
   

Puede crear consultas que utilicen cualquier atributo de elemento de trabajo escribiendo el nombre del atributo. Por ejemplo, si escribe `Creado por`, se mostrarán las opciones de consulta y la sintaxis. Puede utilizar operadores, como por ejemplo "and" "or" y "not" en los criterios de filtros. También puede incluir operaciones complejas que aniden varios operadores utilizando paréntesis. Para ver ejemplos, pulse el icono **Ayuda**.
![Filtrar icono de ayuda](images/filter_helpicon.png)

Al pulsar el campo **Filtrar elementos de trabajo por palabra clave**, se mostrarán los operadores y los filtros que puede utilizar para crear consultas.

![Filtrar con opciones de rellenado automático](images/filterMenu2.png)

##Guardar vistas personalizadas{: #tp-customviews}
Puede crear vistas personalizadas aplicando filtros. A continuación, puede compartir las vistas con el equipo.    

1. En el campo **Filtrar elementos de trabajo**, escriba la forma abreviada de un tipo de atributo y de un valor para dicho atributo, como por ejemplo `$high`. Algunas opciones de atributos se listarán automáticamente al escribir la forma abreviada, por ejemplo, *Tipo, $Prioridad y !Gravedad.
![Filtrar con atributos y tipos de atributos](images/filterAttributes.png)
2. Pulse **GUARDAR**.
3. Dé un nombre a la vista. 
4. Si desea que la vista personalizada incluya el sprint que está visualizando, seleccione el recuadro de selección para que incluya el sprint. En el ejemplo siguiente, el sprint Proceso se incluirá en la vista "High priority backlog".
![Guarde el diálogo de la vista personalizada con el sprint incluido](images/filterIncludeSprints.png)
5. Pulse **GUARDAR**. 
6. Si desea compartir las vistas guardadas con el equipo, en la sección Vistas personalizadas, pulse el icono Compartir junto a la vista nueva. A continuación, pulse **Aceptar**.
![Comparta la flecha de la vista personalizada](images/filterShare.png)

Las vistas personalizadas devuelven resultados para sólo el sprint y el estado actuales que está visualizando. Si desea que la vista devuelva resultados para más sprints o estados, pulse la vista y cámbiela según sea necesario.

##Visualización y organización de elementos de trabajo{: #tp-organizingwis}

- Para ver elementos de trabajo de su propiedad, consulte la vista My Work. 
- Si utiliza con frecuencia elementos de trabajo específicos, puede marcarlos como favoritos pulsando sus iconos de Estrella <img class="inline"  src="./images/star.gif" alt="icono de Estrella">. A continuación, podrá ver todos los elementos de trabajo favoritos en la vista My Starred. Al pulsar el icono de Estrella para un elemento de trabajo, sólo podrá ver que lo ha marcado como favorito.  
- Para ver todos los elementos de trabajo a los que está suscrito, consulte la vista My Subscribed.
- Para ver los elementos de trabajo ordenados por sus fechas de modificación, consulte la vista My Recent Work.
- Para ver la actividad del elemento de trabajo, consulte la vista My Activities. La sección My Events enumera los elementos de trabajo en los que está mencionado. La sección My Subscriptions enumera todos los cambios producidos en los elementos de trabajo a los que está suscrito.

##Clasificación de elementos de trabajo{: #tp-triaging}

Cuando se crea un elemento de trabajo pero no se asigna a un sprint, el elemento de trabajo se mostrará en la vista Incoming Work.
Tan pronto como se asigne un elemento de trabajo a un sprint, se eliminará de la vista Incoming Work.

En la vista Incoming Work, puede seleccionar elementos de trabajo de varias maneras: 
- Para rechazar el elemento de trabajo, pulse el icono **Trash this item** <img class="inline"  src="./images/trash.gif" alt="icono Trash this item">. El elemento de trabajo se resolverá y su estado se modificará a No válido.
- Para aceptar el elemento de trabajo y asignarlo al Proceso, pulse el icono **Triage to backlog** <img  class="inline" src="./images/triage.gif" alt="icono Triage to backlog">. A continuación, puede evaluar el elemento de trabajo frente a otros elementos de trabajo en la vista Sprint Planning y asignar el elemento de trabajo a un sprint.
- Para asignar el elemento de trabajo a un sprint, abra el elemento de trabajo y seleccione un valor desde la lista **Planificado para**.

![Selección de elementos de trabajo en la vista Incoming Work](images/incoming_work_attributes.png)  

Para obtener más información sobre la gestión de elementos de trabajo, [consulte Gestión de un proyecto con Quick Planner](http://www.ibm.com/support/knowledgecenter/SSYMRC_6.0.1/com.ibm.team.concert.tutorial.doc/topics/tut_quick_planner_lesson.html).
