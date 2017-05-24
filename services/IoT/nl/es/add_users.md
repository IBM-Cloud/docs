---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestión de acceso de usuario
{: #managing-user-access}

Desde el panel de control de miembros, puede controlar y gestionar el acceso a la organización de {{site.data.keyword.iot_full}}. Puede añadir usuarios añadiéndolos, invitándolos<!--, registering--> o importándolos. También puede dar distintos niveles de acceso a los usuarios asignando roles.
{:shortdesc}

## Adición de usuarios
{: #adding-new-users}

Desde el separador **Miembros** del panel de control, puede añadir miembros individuales utilizando las funciones <!--Add, Invite, or Register--> Añadir o Invitar. También puede <!--add, invite, or register-->añadir, invitar o registrar varios miembros simultáneamente utilizando la función Importar.

De forma predeterminada, las cuentas de los miembros no caducan. Al añadir usuarios a la organización de {{site.data.keyword.iot_short_notm}}, puede, si lo desea, establecer una fecha de caducidad para su cuenta.

### Adición de miembros a la organización de {{site.data.keyword.iot_short_notm}}

Para añadir un miembro a su organización, necesitará el ID de IBM del miembro. Para añadir un miembro, no necesita que este se lo confirme.

Para añadir un solo miembro a la organización de {{site.data.keyword.iot_short_notm}}:
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Miembros**.
2. Pulse **Añadir miembros** y seleccione el separador **Añadir**.
3. Especifique el ID de IBM del miembro.
4. Seleccione un rol para el miembro.
5. Opcional: Establezca una fecha de caducidad para el miembro.
6. Pulse **Añadir**.

Para añadir varios miembros simultáneamente, debe cargar un archivo `.csv` que contiene el ID de IBM, el rol y la fecha de caducidad opcional de cada miembro. Para obtener información, consulte [Construir el archivo CSV](#constructing-your-csv).
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Miembros**.
2. Pulse **Añadir miembros** y seleccione el separador **Importar**.
3. Examine los archivos o arrastre el archivo `.csv` a la ventana **Cargar CSV**.
4. Seleccione un rol predeterminado para utilizar si no se reconoce un rol especificado en el archivo CSV.
5. Correlacione los números de la columna de su archivo CSV con el ID de IBM correspondiente, rol y (opcional) entradas de fecha de caducidad.
6. Seleccione el separador de columna de coma o punto y coma adecuado para que coincida con el separador utilizado en el archivo `.csv`.
7. Pulse **Importar** para importar los ID de IBM y crear los miembros.


### Invitación de miembros a la organización de {{site.data.keyword.iot_short_notm}}

Al invitar a un usuario para que sea miembro de la organización de {{site.data.keyword.iot_short_notm}}, el usuario recibirá un correo electrónico que contiene un enlace de invitación. Los enlaces de invitación caducan 48 horas después de ser enviados. Si un enlace de invitación no se utiliza en 48 horas, el usuario tiene que ser invitado de nuevo para que reciba un nuevo enlace de invitación.

**Importante:** la característica de invitar requiere un servicio de correo configurado. Para obtener más información, consulte la sección de correo electrónico del tema [Integraciones de servicios externos](reference/extensions/index.html#email).

Para invitar a un miembro a la organización de {{site.data.keyword.iot_short_notm}}:
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Miembros**.
2. Seleccione el separador **Invitaciones**.
2. Pulse **Invitar a miembros** y seleccione el separador **Invitar**.
3. Especifique la dirección de correo electrónico del miembro.
4. Seleccione un rol para este miembro.
5. Opcional: Establezca una fecha de caducidad para el miembro.
6. Pulse **Invitar miembro**.

Para invitar a varios miembros simultáneamente, debe cargar un archivo `.csv` que contiene la dirección de correo electrónico, el rol y la fecha de caducidad opcional de cada miembro. Para obtener información, consulte [Construir el archivo CSV](#constructing-your-csv).
1. En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Miembros**.
2. Seleccione el separador **Invitaciones**.
2. Pulse **Invitar a miembros** y seleccione el separador **Importar**.
3. Examine los archivos o arrastre el archivo `.csv` a la ventana **Cargar CSV**.
4. Seleccione un rol predeterminado para utilizar si no se reconoce un rol especificado en el archivo CSV.
5. Correlacione los números de la columna de su archivo CSV con la dirección de correo electrónico correspondiente, rol y (opcional) entradas de fecha de caducidad.
6. Seleccione el separador de columna de coma o punto y coma adecuado para que coincida con el separador utilizado en el archivo `.csv`.
7. Pulse **Importar** para enviar las invitaciones.

<!-- ### Registering a member with your {{site.data.keyword.iot_short_notm}} organization

If your organization is using {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, you can add individual members to your organization by registering them, which does not require an IBMid.

To register a member with your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Select the **Invitations** tab.
2. Click **Invite Members** and select **Invite**.
3. Enter the email address of the member.
4. Select a role for this member.
5. Enter the subject, realm name, and issuer.
   **Important:** Ensure that the `Subject`, `Realm Name`, and `Issuer` fields comply with the OpenID Connect recommendations and standards. For more information, see the [OpenID Connect ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://openid.net/connect/){: new_window} website.
6. Optional: Set an expiry date for the member.
7. Click **Register Member**.

To register multiple members simultaneously, you must upload a CSV (`.csv`) file that contains the email address, role, subject, realm name, issuer, and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Register**.
4. Select a default role and ensure that the column numbers on your CSV file match the column numbers in the CSV settings.
5. Ensure the column separator in your CSV file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the CSV file into the **Upload CSV** window. -->

### Construir el archivo CSV
{: #constructing-your-csv}

Cuando se construye un archivo CSV para importar miembros a su organización, asegúrese de incluir la información necesaria para el método que está utilizando. Utilice comas o puntos y comas para separar columnas.  
**Importante:** al cargar el archivo CSV, en **Valores CSV**, asegúrese de que selecciona el separador de columna correcto.

Archivo CSV de ejemplo con delimitación por comas:  
```
user1@sample.com,PD_DEVELOPER_USER,1489505652152
user2@sample.com,PD_OPERATOR_USER,1489505652152
user3@sample.com,PD_ADMIN_USER,1489505652152
```

Donde se utilizan las siguientes entradas de columna:  
- Columna 1: la dirección de correo electrónico del usuario.  
Si está añadiendo miembros, asegúrese de utilizar la dirección de correo electrónico correspondiente a un ID de IBM válido. Si está invitando a miembros, puede utilizar cualquier dirección de correo electrónico válida.
- Columna 2: el rol que se asignará al usuario.  
Especifique uno de los roles siguientes:
 - PD_ADMIN_USER
 - PD_OPERATOR_USER
 - PD_DEVELOPER_USER
 - PD_ANALYST_USER
 - PD_READER_USER  
 Para obtener más información sobre los roles de usuario, consulte [Roles de usuario, aplicación y pasarela](roles_index.html#user_roles).
- Columna 3: la indicación de fecha y hora de Unix (en milisegundos, a partir del 1 de enero de 1970, 00:00 UTC) que corresponda a la fecha de caducidad del usuario.

## Edición de usuarios
{: #editing-users}

Los usuarios se pueden editar para modificar su rol, añadir, eliminar o cambiar una fecha de caducidad de acceso o añadir o eliminar el acceso a la organización.

1. Desde el panel de control de {{site.data.keyword.iot_short_notm}}, pulse **Miembros** en la barra de navegación en la izquierda.
2. Pulse el icono **Editar**, situado junto al usuario que desea editar.
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
2. Pulse el icono **Suprimir**, situado junto al usuario que se va a eliminar.
3. Pulse **Suprimir** en el diálogo de confirmación.
