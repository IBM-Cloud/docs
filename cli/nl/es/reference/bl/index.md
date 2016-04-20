---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Mandatos de {{site.data.keyword.Bluemix_notm}} Live Sync (bl)

*Última actualización: 29 de enero de 2016*

Si está creando una app Node.js, puede utilizar Bluemix™ Live Sync para actualizar rápidamente la instancia de la app que se ejecuta en Bluemix y desarrollarla como lo haría en el escritorio sin tener que volver a desplegarla. Cuando realice un cambio, puede verlo de inmediato en la app Bluemix en ejecución. La interfaz de línea de mandatos de Bluemix Live Sync se llama *bl*.

Puede utilizar la interfaz de línea de mandatos **bl** para realizar las tareas siguientes:

* Iniciar y detener una app que se esté ejecutando en Bluemix.
* Crear un proyecto nuevo basado en nube desde su escritorio.
* Sincronizar los cambios entre el escritorio y el espacio de trabajo del proyecto basado en la nube y con la app que se ejecuta en Bluemix.
* Ver la lista de los proyectos que se pueden sincronizar.
* Ver el estado de las apps en ejecución.

Para obtener más información sobre cómo descargar y utilizar el mandato bl, consulte [Bluemix Live Sync](../develop/bluemixlive.html).

## Mandatos bl

La línea de mandatos de Bluemix Live Sync, **bl**, tiene la siguiente sintaxis:

``mandato` bl [argumentos][options] [--help]```

### Mandatos
<dl>
<dt>login, l</dt>
<dd>Inicia la sesión en Bluemix.</dd>
<dt>logout, lo</dt>
<dd>Cierra la sesión del usuario.</dd>
<dt>sync, s</dt>
<dd>Inicia el proceso de sincronización entre el escritorio y el servidor.</dd>
<dt>create, c</dt>
<dd>Crea un proyecto privado; enlácelo al repositorio de Git en este directorio y despliegue el contenido en Bluemix.</dd>
<dt>projects, p</dt>
<dd>Lista todos los proyectos que están disponibles para sincronización.</dd>
<dt>start, st</dt>
<dd>Inicia la instancia de la app en Bluemix.</dd>
<dt>stop, sp</dt>
<dd>Detiene la instancia de la app en Bluemix.</dd>
<dt>status, ss</dt>
<dd>Lista el estado de la instancia de app en ejecución en Bluemix.</dd>
</dl>

### Argumentos
Argumentos para el mandato.

### Opciones
Opciones para el mandato.

### Opciones globales
<dl>
<dt>--help</dt>
<dd>Muestra la página de ayuda para el mandato especificado</dd>
<dt>--verbose</dt>
<dd>Habilita el registro detallado.</dd>
</dl>

**Nota:** Si alguno de los argumentos u opciones contiene un espacio, escriba el valor entre comillas dobles.
