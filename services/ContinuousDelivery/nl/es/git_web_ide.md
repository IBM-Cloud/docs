---

copyright:
  years: 2017
lastupdated: "2017-5-8"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Cómo trabajar con Git en Eclipse Orion Web IDE
{: #git_web_ide}

Si utiliza Eclipse Orion {{site.data.keyword.webide}}, no necesita el terminal Git; puede ejecutar muchos mandatos GIT comunes en Web IDE.

Independientemente de dónde escriba el código, puede utilizar esta consulta rápida para realizar tareas comunes. 

## Crear una rama local
{: #create_branch}

### Eclipse Orion Web IDE
1. Pulse la lista **Referencia**. 

1. Pulse **Nueva rama**.

2. Escriba el nombre de la rama y luego pulse **Enviar**.

### Terminal Git
1. Escriba `git branch <nombre_rama>` y pulse Intro. 

## Trabajar en una rama local
{: #start_working_on_branch}

### Eclipse Orion Web IDE
1. Pulse la lista **Referencia** y amplíe **local**.

2. Junto a la rama que desea modificar, pulse el icono de extracción <img  class="inline" src="./images/checkout.png" alt="Icono de extracción">.

1. Asegúrese de que la rama seleccionada se muestra en la lista **Referencia**. 

### Terminal Git
1. Para ver las ramas locales, escriba `git branch -l` y pulse Intro.

2. Escriba `git checkout <nombre_rama>` y pulse Intro. 


## Actualizar una rama local a fin de incluir los cambios de la rama remota
{: #update_branch}

### Eclipse Orion Web IDE
1. Pulse **Sincronizar**.

1. Si detecta conflictos, [resuélvalos](#resolve_a_rebase_conflict).

### Terminal Git
1. Escriba `git pull` y pulse Intro.

## Suprimir una rama local
{: #delete_branch}

### Eclipse Orion Web IDE
1. Asegúrese de que la rama que desea suprimir no se ha extraído. Si dicha rama se ha extraído, [extraiga otra rama](#start_working_on_branch).

1. Pulse la lista **Referencia** y amplíe **local**.

2. Junto a la rama local que desea eliminar, pulse **Suprimir** <img class="inline"  src="./images/delete.png" alt="Icono Suprimir">.

### Terminal Git
1. Escriba `git branch -d <nombre_rama>` y pulse Intro. 

##Forzar la transmisión de cambios locales a una rama remota
{: #force_push}

Sustituya el contenido de una rama remota referenciada por el contenido de la rama local activa. 

**Importante:** cuando fuerza la transmisión de una rama local a una remota, es posible que pierda confirmaciones en la rama remota. 

### Eclipse Orion Web IDE

1. En la sección Cambios del directorio de trabajo, en la sección Saliente, pulse la flecha que hay junto a **Enviar**.
2. Pulse **Forzar transmisión de rama**.
3. Confirme el aviso. 

### Terminal Git

1. Escriba `git push <origen> <rama remota> -f` y pulse Intro. 

## Descarte los cambios no transferidos desde la rama local activa
{: #discard_changes}

### Eclipse Orion Web IDE
1. En la sección Cambios del directorio de trabajo, seleccione el recuadro de selección correspondiente a cada archivo modificado que tenga cambios que desea descartar. 
2. Pulse el icono de extracción <img class="inline"  src="./images/discard.png" alt="Extraer los archivos seleccionados, descartando todos los cambios">.

### Terminal Git
1. Escriba `git checkout -- path/to/file/filename` para descartar los cambios en un archivo. 

## Confirmar archivos y enviarlos a la rama remota
{: #commit}

### Eclipse Orion Web IDE
1. En la sección Cambios del directorio de trabajo, seleccione el recuadro de selección correspondiente a cada archivo que desee confirmar. 

3. En el campo **Especificar el mensaje de confirmación**, escriba un mensaje que describa los cambios.


  **Consejo**: especifique un mensaje de confirmación detallado. El mensaje debe proporcionar suficientes detalles como para que se entienda por qué era necesario realizar el cambio sin más información. Puede incluir un enlace con un elemento del rastreador de elementos de su equipo como ayuda. La primera línea del mensaje de confirmación no debe contener más de 50 caracteres. Añada una línea en blanco antes de añadir más texto.

4. Pulse **Confirmar**.

5. Pulse **Enviar**.

### Terminal Git
1. Escriba `git status` y pulse Intro.

2. Revise los cambios que va a confirmar.
Si todos los archivos que desea confirmar están en la lista, continúe.
Para confirmar archivos no transferidos, transfiéralos primero. 

3. Escriba `git commit` y pulse Intro.

4. Especifique el resumen de confirmación, añada una línea en blanco y añada la descripción de la confirmación. 

  **Consejo**: el resumen de confirmación debe tener menos de 50 caracteres. La descripción de la confirmación debe proporcionar suficientes detalles como para que se entienda por qué era necesario realizar el cambio sin más información. Puede incluir un enlace con un elemento del rastreador de elementos de su equipo como ayuda. 

5. Guarde el mensaje de confirmación. 

  **Nota:** para guardar el mensaje de confirmación y cerrar Vim, que puede ser su editor de texto predeterminado, pulse Esc, escriba `:wq` y pulse Intro. 

4. Escriba `git push` y pulse Intro.

## Ver el historial de confirmaciones
{: #view_commit_history}

### Eclipse Orion Web IDE
1. En la sección Rama activa, amplíe **Historial** para ver historial de la rama. 

  El historial de confirmaciones también se puede ver como un gráfico visual conectado. 

1. Pulse el icono de **conmutación de representación gráfica** <img  class="inline" src="./images/graphicalhistoryicon.png" alt="Icono de historial gráfico">.

  Una vez conmutado, el historial de confirmaciones y cualquier cambio entrante o saliente correspondiente a la rama activa se dibuja como un gráfico conectado. La representación visual muestra todas las confirmaciones y las ramas en las que se han realizado. 

  <img class="screen-shot" src="./images/visualhistoryexample.png" alt="Historial de confirmaciones visual">

### Terminal Git
1. Escriba `git log` y pulse Intro.

2. Navegue por las confirmaciones del confirmador. 
 * Para ver más entradas, pulse AvPág.
 * Para ver entradas anteriores, pulse RePág.

3. Para detener la visualización de entradas, pulse Q.

## Comparar cambios incorporados por una confirmación
{: #compare_changes}

### Eclipse Orion Web IDE
1. Consulte el historial de confirmaciones y localice la confirmación. Para obtener más información, consulte [Ver el historial de confirmaciones](#view_commit_history).

2. Vea los detalles de la confirmación pulsando sobre la misma.

3. Junto a un archivo, pulse **>** para revisar los cambios en el archivo.


  **Nota:** si una confirmación ha incorporado un cambio en una línea, la línea original aparece sombreada en rosa y la nueva línea sombreada en verde.
Paralelamente, las líneas que ha añadido una confirmación aparecen sombreadas en verde y las que ha eliminado una confirmación, sombreadas en rosa.

### Terminal Git
1. Escriba `git log -p` y pulse Intro.


  **Nota:** para ver sólo un determinado número de confirmaciones, escriba `git log -p -<número_de_confirmaciones_que_desea_ver>`. 

2. Navegue por las confirmaciones. 
 * Para ver más entradas, pulse AvPág.
 * Para ver entradas anteriores, pulse RePág.

3. Revise los cambios.

  **Nota:** si una confirmación ha incorporado un cambio en una línea, el texto de la línea original se muestra en rojo y comienza por un signo menos (-).
El texto de la línea nueva se muestra en verde y comienza por un signo más (+).
Paralelamente, el texto de las líneas que ha añadido una confirmación aparece en verde y comienza por un signo más.
El texto de las líneas que ha eliminado una confirmación aparece en rojo y comienza por un signo menos.

1. Para detener la visualización de entradas, pulse Q.

## Modificar la última confirmación
{: #modify_last_commit}

  **Nota:** si modifica la última confirmación después de enviarla a un repositorio remoto, vuelve a escribir en el historial de confirmaciones. Esto puede ocasionar errores de confirmación y otros problemas para otros colaboradores en el proyecto. Asegúrese de saber lo que hace antes de modificar una confirmación que ha enviado a un repositorio remoto. 

### Eclipse Orion Web IDE
1. Marque los recuadros de selección correspondientes a los elementos que desea añadir a la confirmación.

1. Marque el recuadro de selección **Modificar confirmación anterior**. 

2. Si es necesario, escriba un nuevo mensaje de confirmación.

3. Pulse **Confirmar**.

### Terminal Git
1. Compruebe el estado.
Transfiera o anule la transferencia de archivos según sea necesario.

2. Escriba `git commit --amend` y pulse Intro. 

3. En el editor de texto, acepte o modifique el mensaje de confirmación.


  **Nota:** para guardar el mensaje de confirmación y cerrar Vim, que puede ser su editor de texto predeterminado, pulse Esc, escriba `:wq` y pulse Intro. 

## Etiquetar una confirmación
{: #tag_commit}

### Eclipse Orion Web IDE
1. Consulte el historial de confirmaciones y localice la confirmación. Para obtener más información, consulte [Ver el historial de confirmaciones](#view_commit_history).

2. Vea los detalles de la confirmación pulsando sobre la misma.

2. En el panel de confirmación, pulse **Cree una etiqueta para la confirmación** <img class="inline" src="./images/tag.png" alt="Crear una etiqueta para la confirmación">.

3. En el campo de nombre, escriba el texto de la etiqueta. Pulse **Enviar**.

### Terminal Git
1. Vea el historial de confirmaciones y obtenga el ID de la confirmación que desea etiquetar. Para obtener más información, consulte [Ver el historial de confirmaciones](#view_commit_history).

2. Escriba `git tag -a <texto_etiqueta> <id_confirmación>` y pulse Intro. 

## Cambiar el nombre y la dirección de correo electrónico del confirmador
{: #change_the_committer_name_and_email_address}

### Eclipse Orion Web IDE
1. Pulse el icono de configuración <img class="inline" src="./images/configurations.png" alt="Icono de configuración">.

3. Cambie la dirección de correo electrónico y el nombre del usuario actualizando los valores user.email y user.name. Pulse **Enviar** para guardar el cambio.

### Terminal Git
Para actualizar su nombre y dirección de correo electrónico para un solo repositorio:

1. Escriba `git config user.email "<su@correoelectrónico.com>"` y pulse Intro. 

2. Escriba `git config user.name "<su nombre>"` y pulse Intro.

Para actualizar su nombre y dirección de correo electrónico para todos los repositorios: 

1. Escriba `git config --global user.email "<su@correoelectrónico.com>"` y pulse Intro. 

2. Escriba `git config --global user.name "<su nombre>"` y pulse Intro.

##Revertir una confirmación
{: #revert}

Revierta los cambios que ha incorporado una confirmación en la rama activa.

### Eclipse Orion Web IDE

1. En Historial, seleccione una confirmación.

2. En la parte derecha de la página, sobre el resumen de confirmaciones, pulse el icono revertir <img class="inline" src="./images/revert.png" alt="Icono Revertir">.

### Terminal Git

1. Escriba `git revert <ID confirmación>` y pulse Intro. 

## Fusionar cambios
{: #merge_changes}

Cuando tenga que distribuir cambios de una rama de origen a una de destino, primero debe fusionar. Normalmente, la rama de origen es la rama en la que ha realizado los cambios y la de destino rama es la rama maestra. 

### Eclipse Orion Web IDE
1. Decida las ramas que desea fusionar.


2. Extraiga la rama de destino. Para obtener más información, consulte [Cómo trabajar en una rama local](#start_working_on_branch).

 <img class="screen-shot" src="./images/destinationbranch.png" alt="Extraer rama de destino">

1. Pulse la lista **Referencia**, amplíe **local** y pulse el nombre de la rama de origen. Los cambios de la rama de origen se muestran en la sección Entrantes.

  <img class="screen-shot" src="./images/sourcebranch.png" alt="Cambios de la rama de origen mostrados en la sección Entrantes">

1. En la sección Entrantes, pulse el icono **Fusionar** <img class="inline" src="./images/mergeicon.png" alt="Icono Fusionar de la sección Entrantes">

1. En la lista **Referencia**, pulse el icono extraer que hay junto a la rama en la que acaba de fusionar los cambios. 

1. Si desea distribuir los cambios, pulse **Enviar**. De lo contrario, en este punto puede crear un despliegue de prueba para asegurarse de que todo está funcionando según lo previsto.

### Terminal Git
1. Decida las ramas que desea fusionar.


2. Extraiga la rama de destino. Para obtener más información, consulte [Cómo trabajar en una rama local](#start_working_on_branch).

3. Escriba `git merge <nombre_origen>` y pulse Intro.


## Resolver un conflicto de fusión
{: #resolve_a_merge_conflict}

### Eclipse Orion Web IDE
1. En el panel Archivos modificados, revise la lista de archivos que contienen conflictos.

2. En Web IDE, abra cada archivo que contenga conflictos.

3. Resuelva cada cambio conflictivo.


  **Nota:** suprima todo el texto que no desee conservar.
Cada conflicto tiene este formato: 

		<<<<<<< HEAD
		Texto de la rama extraída.
		=======
		Testo de la rama fusionada.
		>>>>>>> commit_ID_from_merged_branch
4. Para cada archivo conflictivo, marque el recuadro de selección.
Escriba un mensaje de confirmación de fusión y pulse **Confirmar**.

### Terminal Git
1. Para los archivos que contienen conflictos, revise el mensaje de Git correspondiente a los nombres.

2. En el editor de texto, abra un archivo que contenga conflictos.

3. Resuelva cada cambio conflictivo y guarde el archivo.


  **Nota:** suprima todo el texto que no desee conservar.
Cada conflicto tiene este formato: 

		<<<<<<< HEAD
		Texto de la rama extraída.
		=======
		Testo de la rama fusionada.
		>>>>>>> merged_branch
4. Transfiera cada archivo que haya modificado y confirme la fusión.

## Cambio de base de las ramas
{: #rebase_branches}

### Eclipse Orion Web IDE
1. Decida las ramas cuya base desea cambiar.
Cambiará la base del contenido de la rama de origen y la colocará en la rama de destino.

2. Extraiga la rama de destino. Para obtener más información, consulte [Cómo trabajar en una rama local](#start_working_on_branch).

1. Pulse la lista **Referencia**. 

1. Pulse el nombre de la rama de origen.

1. En la sección Entrantes, pulse el icono de cambio de base <img class="inline" src="./images/rebase.png" alt="Icono de cambio de base">.

5. Si detecta conflictos, [resuélvalos](#resolve_a_rebase_conflict).

6. Repita el paso anterior tantas veces como sea necesario para completar la operación de cambio de base.

1. Pulse la lista **Referencia**, amplíe **origen** y pulse el nombre de la rama de origen. 

1. Pulse **Enviar**.

### Terminal Git
1. Extraiga la rama para actualizarla escribiendo `git checkout <nombre_rama_destino>` y pulsando Intro.

2. Escriba `git rebase <nombre_rama_origen>` y pulse Intro. 

3. Si detecta conflictos, [resuélvalos](#resolve_a_rebase_conflict).

5. Repita el paso anterior tantas veces como sea necesario para completar la operación de cambio de base.

  **Nota:** para detener la operación de cambio de base, escriba `git rebase --abort` y pulse Intro.

## Resolver un conflicto de cambio de base
{: #resolve_a_rebase_conflict}

### Eclipse Orion Web IDE
1. En la sección Cambios del directorio de trabajo, revise la lista de archivos conflictivos. 

2. En Web IDE, abra cada archivo que contenga conflictos.

3. Resuelva cada cambio conflictivo.


  **Nota:**: suprima todo el texto que no desee conservar.
Cada conflicto tiene este formato: 

		<<<<<<< HEAD
		Texto de la rama extraída.
		=======
		Testo de la rama fusionada.
		>>>>>>> commit_ID_from_merged_branch
4. En el panel de cambio de base, marque el recuadro de selección correspondiente a cada archivo corregido y pulse **Continuar**.

### Terminal Git
1. Para los archivos que contienen conflictos, revise el mensaje de Git correspondiente a los nombres.

2. En el editor de texto, abra un archivo que contenga conflictos.

3. Resuelva cada cambio conflictivo y guarde el archivo.


  **Nota:**: suprima todo el texto que no desee conservar.
Cada conflicto tiene este formato: 

		<<<<<<< HEAD
		Texto de la rama extraída.
		=======
		Testo de la rama fusionada.
		>>>>>>> merged_branch
4. Transfiera cada archivo que haya modificado.

5. Reanude la operación de cambio de base escribiendo `git rebase --continue` y pulsando Intro.
