---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-24"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestión de acceso de usuario

Desde el panel de control de acceso, puede controlar y gestionar el acceso a la organización de {{site.data.keyword.iot_full}}. Puede añadir usuarios añadiéndolos, invitándolos, registrándolos o importándolos. También puede dar distintos niveles de acceso a los usuarios asignando roles.
{:shortdesc}

- [Adición de nuevos usuarios](#adding-new-users)
- [Edición de usuarios](#editing-users)
- [Bloqueo del acceso de usuarios](#blocking-users)
- [Eliminación de usuarios](#removing-users)

## Adición de nuevos usuarios
{: #adding-new-users}

Desde el separador **Acceso** del panel de control, puede añadir miembros individuales utilizando las funciones Añadir, Invitar o Registrar. También puede añadir, invitar o registrar varios miembros simultáneamente utilizando la función Importar.

De forma predeterminada, las cuentas de los miembros no caducan. Al añadir usuarios a la organización de {{site.data.keyword.iot_short_notm}}, puede, si lo desea, establecer una fecha de caducidad para su cuenta.

### Adición de miembros a la organización de {{site.data.keyword.iot_short_notm}}

Para añadir un miembro a su organización, necesitará el ID de IBM del miembro. Para añadir un miembro, no necesita que este se lo confirme.

Para añadir un solo miembro a la organización de {{site.data.keyword.iot_short_notm}}:
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Acceso**.
2. Pulse **Añadir miembro** y seleccione **Añadir**.
3. Especifique el ID de IBM del miembro.
4. Seleccione un rol para el miembro.
5. Opcional: Establezca una fecha de caducidad para el miembro.
6. Pulse **Añadir miembro**.

Para añadir varios miembros simultáneamente, debe cargar un archivo `.csv` que contiene el ID de IBM, el rol y la fecha de caducidad opcional de cada miembro.
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Acceso**.
2. Pulse **Añadir miembro** y seleccione **Importar**.
3. Pulse **Adición masiva**.
4. Seleccione un rol predeterminado y asegúrese de que los números de columna del `archivo .csv` coinciden con los números de columna de los valores CSV.
5. Asegúrese de que el separador de la columna del archivo `.csv` coincide con el separador de columna de los valores CSV.
6. Pulse **Examinar los archivos** o arrastre el archivo `.csv` a la ventana **Cargar CSV**.

### Invitación de miembros a la organización de {{site.data.keyword.iot_short_notm}}

Al invitar a un usuario para que sea miembro de la organización de {{site.data.keyword.iot_short_notm}}, el usuario recibirá un correo electrónico que contiene un enlace de invitación. Los enlaces de invitación caducan 48 horas después de ser enviados. Si un enlace de invitación no se utiliza en 48 horas, el usuario tiene que ser invitado de nuevo para que reciba un nuevo enlace de invitación.

Para invitar a un miembro a la organización de {{site.data.keyword.iot_short_notm}}:
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Acceso**.
2. Pulse **Añadir miembro** y seleccione **Invitar**.
3. Especifique la dirección de correo electrónico del miembro.
4. Seleccione un rol para este miembro.
5. Opcional: Establezca una fecha de caducidad para el miembro.
6. Pulse **Invitar miembro**.

Para invitar a varios miembros simultáneamente, debe cargar un archivo `.csv` que contiene la dirección de correo electrónico, el rol y la fecha de caducidad opcional de cada miembro.
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Acceso**.
2. Pulse **Añadir miembro** y seleccione **Importar**.
3. Pulse **Invitación masiva**.
4. Seleccione un rol predeterminado y asegúrese de que los números de columna del archivo `.csv` coinciden con los números de columna de los valores CSV.
5. Asegúrese de que el separador de la columna del archivo `.csv` coincide con el separador de columna de los valores CSV.
6. Pulse **Examinar los archivos** o arrastre el archivo `.csv` a la ventana **Cargar CSV**.

### Registro de un miembro con la organización de {{site.data.keyword.iot_short_notm}}

Si la organización no utiliza {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, puede añadir miembros individuales a su organización registrándolos, lo que no requiere un ID de IBM.

Para registrar un miembro con la organización de {{site.data.keyword.iot_short_notm}}:
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Acceso**.
2. Pulse **Añadir miembro** y seleccione **Invitar**.
3. Especifique la dirección de correo electrónico del miembro.
4. Seleccione un rol para este miembro.
5. Especifique el asunto, el nombre de reino y el emisor.
   **Importante:** Asegúrese de que los campos `Asunto`, `Nombre de reino` y `Emisor` cumplen con las recomendaciones y los estándares de OpenID Connect. Para obtener más información, consulte el sitio web de [OpenID Connect](http://openid.net/connect/).
6. Opcional: Establezca una fecha de caducidad para el miembro.
7. Pulse **Registrar miembro**.

Para registrar varios miembros simultáneamente, deberá cargar un archivo CSV (`.csv`) que contiene la dirección de correo electrónico, el rol, el asunto, el nombre de reino, el emisor y la fecha de caducidad opcional de cada miembro.
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Acceso**.
2. Pulse **Añadir miembro** y seleccione **Importar**.
3. Pulse **Registro masivo**.
4. Seleccione un rol predeterminado y asegúrese de que los números de columna del archivo CSV coinciden con los números de columna de los valores CSV.
5. Asegúrese de que el separador de columna del archivo CSV coincide con el separador de columna de los valores CSV.
6. Pulse **Examinar los archivos** o arrastre el archivo CSV a la ventana **Cargar CSV**.

### Construir el archivo CSV

Cuando se construye un archivo CSV para importar miembros a su organización, asegúrese de incluir la información necesaria para el método que está utilizando. Utilice comas o puntos y comas para separar columnas. Al cargar el archivo CSV, en **Valores CSV**, asegúrese de que selecciona el separador de columna correcto.

## Edición de usuarios
{: #editing-users}

Los usuarios se pueden editar para modificar su rol, añadir, eliminar o cambiar una fecha de caducidad de acceso o añadir o eliminar el acceso a la organización.

1. Desde el panel de control de {{site.data.keyword.iot_short_notm}}, pulse **Miembros** en la barra de navegación en la izquierda.
2. Pulse el icono **Editar** ![Editar](/docs/images/edit_32.svg) junto al usuario que desea editar.
3. Realice los cambios que desee en el usuario.
4. Pulse **Guardar**.

## Bloqueo del de acceso de usuarios
{: #blocking-users}

Se puede bloquear el acceso de los usuarios a la organización {{site.data.keyword.iot_short_notm}} mientras siguen manteniendo la pertenencia a la organización.

1. Desde el panel de control de {{site.data.keyword.iot_short_notm}}, pulse **Miembros** en la barra de navegación en la izquierda.
2. Pulse el conmutar situado junto al usuario cuyo acceso a la organización {{site.data.keyword.iot_short_notm}} desea bloquear.


## Eliminación de usuarios
{: #removing-users}

Los usuarios se pueden eliminar por completo de la organización {{site.data.keyword.iot_short_notm}}. La eliminación de usuarios no se puede deshacer y los usuarios se deben [añadir a la plataforma](#adding-new-users) para restaurar el acceso.

1. Desde el panel de control de {{site.data.keyword.iot_short_notm}}, pulse **Miembros** en la barra de navegación en la izquierda.
2. Pulse el icono **Suprimir** ![Suprimir](/docs/images/trash_32.svg) situado junto al usuario que se va a eliminar.
3. Pulse **Suprimir** en el diálogo de confirmación.
